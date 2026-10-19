[README.md](https://github.com/user-attachments/files/33674330/README.md)
# SOC Analyst Lab

Hands-on security investigations I completed while training for an entry-level SOC analyst role.
Each case starts from raw logs or traffic, works through the evidence, and ends with a short report that separates **what the evidence shows** from **what it suggests**.

> All data in this repository is **synthetic training data** from lab exercises. No real systems, users or incidents are involved.

## Cases

| # | Case | Data | Skills |
|---|------|------|--------|
| 001 | [SSH password spray and persistence account](day1/report.md) | Linux `auth.log` | grep/awk log analysis, pivoting, timeline, careful reporting |

## Tools
`grep`, `awk`, `sort`, `uniq`, `journalctl` · (coming: Wireshark/tshark, Elastic Security, Sigma)

## Structure
```
dayxx/      one folder per investigation (evidence file + writeup) e.g day1
template.md:  the reporting template I use throughout the journey
```
