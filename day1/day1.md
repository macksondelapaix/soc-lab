# Case 001: Suspected password spray on lab-web-02

>Training lab exercise. All data is synthetic


**Date investigated:** 2026-10-19 
**Data source:** `auth.log`
**Status:** Suspected compromise

## Summary 

An unidentified IP address *198.51.100.77* tried to guess the passwords to accounts 
belonging to this organisition (alice,backup,bob,deploy,intern,jsmith,mchirwa)
After some tries the IP logged into *intern* account. From that account
they created a new account *sysupd* and gave it sudo privileges which allow it to
do alot of things. Now from a separate Ip address
*203.0.113.88*, sysupd logged in. 

## Timeline(UTC)
> October 9 2026
|Time|What the log show|
|---|---|
|02:30:00 - 02:33:40 | Passwords guessed for multiple accounts(failed passwords) |
|02:33:40 | Password correctly guessed for *intern* |
|02:33:41 | intern logged in |
|02:34:20 | intern checked their permissions |
|02:35:15 | intern searched for programs that run as root |
|02:37:45 | intern created account sysupd |
|02:38:10 | intern added sysupd to privileged users group |
|02:42:40 | intern logged out |
|21:12:00 | *sysupd* logged in(from IP address 203.0.113.88) |

## Logs show
+ 20 failed password logins from 198.51.100.77 against 7 accounts between 02:30:00 and 02:33:29 about 11 seconds between each guess
+ successful password login from same IP at 02:33:40 
+ Unidentified user found password for *intern*
+ With the password they logged in and created sysupd with root access(persistence)

## Suggests

+ Password attack (spraying)
+ recon for root access
+ persistence through sysupd

## We can't tell
+ what they want to do
+ who was behind the IP
+ what sysupd did after 21.12 
+ whether the real intern created sysupd

## Recommended Actions
1. disable sysupd and lock intern
2. Check what sysupd account did in system
3. remove intern sudo and turn off ssh password logins
4. Make sure people have secure passwords
## Commands used 
```bash

grep -i "Failed password" auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr

grep "198.51.100.77" auth.log | grep "Accepted"

grep "intern" auth.log

grep "sysupd" auth.log

grep "alice" auth.log

```

## What I learned

+ How to use awk,grep, uniq and sort
+ how auth.log looks linux logs
