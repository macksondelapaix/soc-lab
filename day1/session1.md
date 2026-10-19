# Week 1, Session 1: Follow the IP

> **TRAINING LAB DATA:** `auth.log` in this folder is synthetic. Host `lab-web-02`, all IPs are documentation ranges.
> Time: about 1 to 1.5 hours.

## The idea in simple English

An investigation is mostly asking "what else did *this* do?". You pick one thing you're sure about, like an IP address, a username or a time, and search for **everything else** linked to it. Analysts call this **pivoting**. When one thread runs out, you pick a new value from what you found and pivot again.

A log line is a *record that something was claimed or happened*. It is not a story, and the story is your interpretation. So keep two columns in your notes: **"The log shows"** and **"I think this means"**.

## Commands you'll need

Run these in the folder containing `auth.log`:

```bash
grep "Accepted" auth.log                      # every successful login
grep -c "Failed password" auth.log            # count of failed-password lines
grep "198.51.100" auth.log                    # every line containing that text
awk '{print $1, $2, $3}' auth.log | head      # print just the date/time fields
sort | uniq -c | sort -rn                     # (after a pipe) count identical lines, biggest first
```

`awk` splits each line on spaces. `$1` is the first word, `$NF` the last, and `$(NF-3)` the 4th from the end.

## Tasks

Do them in order, and write down the **command** you used for each one.

1. **Who's knocking?** Count failed password attempts per source IP. Which IP stands out, and how is its pattern different from the others? *(Look at which usernames each one tries, and how fast.)*
2. **Who got in?** List every successful login: user, IP, and method (password or publickey).
3. **Pivot.** Pick the IP from task 1 and show every line it appears in. What happened right after it stopped failing?
4. **Follow the user.** Pivot on the user who logged in from that IP. List everything that user did, in time order.
5. **Pivot again.** Something in task 4 gives you a *new* name to search for. Search for it. What do you find, and why does it matter?
6. **Malicious or admin?** The user `alice` also has a failed password and some sudo commands. Is her activity suspicious? What evidence supports your answer?
7. **Careful conclusions.** Write 3 to 4 sentences:
   - what the logs **show**,
   - what they **suggest**,
   - two things they **cannot** tell you, and what you'd check next.
8. **On your own laptop:** run `journalctl -u sshd --since "7 days ago"` and `journalctl _COMM=sudo --since today`. Is sshd even running? (`systemctl status sshd`). Just note what you see; there's nothing to find.

**Bonus (optional):** look up the term "password spraying" *after* you finish task 1, and say whether it fits.

Reply in the thread with your answers numbered 1 to 8. I'll review them before showing you my solution.
