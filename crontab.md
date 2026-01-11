# Cron Cheatsheet 📅

A comprehensive visual guide to understanding and using cron jobs for task scheduling in Linux/Unix systems.

## Overview

This repository contains detailed cheatsheets and visual references for working with cron, the time-based job scheduler in Unix-like operating systems. Whether you're a beginner or need a quick reference, these resources will help you master cron syntax and scheduling.

## What is Cron?

Cron is a powerful utility that allows you to schedule commands or scripts to run automatically at specified times and dates. It's commonly used for:

- System maintenance and administration tasks
- Automated backups
- Log rotation
- Database maintenance
- Periodic data synchronization
- Sending scheduled reports or notifications

## Cheatsheets

### Basic Cron Syntax

![Cron Cheatsheet](image1.png)

The basic structure of a cron job consists of five time fields followed by the command to execute:

```
* * * * * command to be executed
│ │ │ │ │
│ │ │ │ └─── Weekday (0=Sun .. 6=Sat)
│ │ │ └───── Month (1..12)
│ │ └─────── Day (1..31)
│ └───────── Hour (0..23)
└─────────── Minute (0..59)
```

### Detailed Linux Cron Guide

![Linux Cron Cheatsheet](image2.png)

This comprehensive guide includes:
- Field ranges and explanations
- Special strings (`@reboot`, `@hourly`, `@daily`, `@weekly`, `@monthly`, `@yearly`)
- Practical examples with explanations
- Special characters and operators
- Crontab management commands

### How to Schedule Cron Jobs

![How to Schedule Cron Jobs](image3.png)

Step-by-step examples for common scheduling patterns:

**Daily**: Run a job every day at a specific time
```bash
0 3 * * *  # Runs at 3:00 AM every day
```

**Weekly**: Run a job on a specific day of the week
```bash
0 4 * * 1  # Runs at 4:00 AM every Monday
```

**Monthly**: Run a job on a specific day of the month
```bash
0 5 1 * *  # Runs at 5:00 AM on the 1st day of every month
```

**Hourly**: Run a job every hour
```bash
0 * * * *  # Runs at the beginning of every hour
```

### Advanced Cron Job Reference

![Cron Job Advanced](image4.png)

Includes:
- Common scheduling patterns with shortcuts
- Special operators (asterisk, comma, hyphen, slash, L, W, #, ?)
- Crontab management commands
- User-specific crontab operations

## Common Cron Patterns

| Pattern | Cron Expression | Description |
|---------|----------------|-------------|
| Every minute | `* * * * *` | Runs every minute |
| Every 5 minutes | `*/5 * * * *` | Runs every 5 minutes |
| Every hour | `0 * * * *` | Runs at the start of every hour |
| Every day at midnight | `0 0 * * *` | Runs at 12:00 AM daily |
| Every Sunday at midnight | `0 0 * * 0` | Runs weekly on Sunday |
| Every weekday at 6 AM | `0 6 * * 1-5` | Runs Monday through Friday |
| First day of month | `0 0 1 * *` | Runs on the 1st of each month |
| Every 6 hours | `0 */6 * * *` | Runs at 0:00, 6:00, 12:00, 18:00 |

## Special Strings

Instead of the five time fields, you can use these special strings:

- `@reboot` - Run once at startup
- `@yearly` or `@annually` - Run once a year (0 0 1 1 *)
- `@monthly` - Run once a month (0 0 1 * *)
- `@weekly` - Run once a week (0 0 * * 0)
- `@daily` or `@midnight` - Run once a day (0 0 * * *)
- `@hourly` - Run once an hour (0 * * * *)

## Special Characters

- `*` (Asterisk) - Matches all possible values for a field
- `,` (Comma) - Specifies a list of values (e.g., `1,3,5`)
- `-` (Hyphen) - Specifies a range of values (e.g., `1-5`)
- `/` (Slash) - Specifies step values (e.g., `*/5` for every 5 units)
- `L` - Last value (only in day-of-month and day-of-week fields)
- `W` - Closest weekday to a given day
- `#` - Nth occurrence of a weekday in a month

## Managing Crontab

### Basic Commands

```bash
# Edit your crontab
crontab -e

# List your cron jobs
crontab -l

# Remove your crontab
crontab -r

# Edit another user's crontab (requires privileges)
crontab -u username -e
```

### System-wide Cron Directories

- `/etc/cron.hourly/` - Scripts that run hourly
- `/etc/cron.daily/` - Scripts that run daily
- `/etc/cron.weekly/` - Scripts that run weekly
- `/etc/cron.monthly/` - Scripts that run monthly

## Examples

### Backup Database Daily
```bash
0 2 * * * /usr/local/bin/backup-database.sh
```

### Clear Cache Every Hour
```bash
0 * * * * rm -rf /tmp/cache/*
```

### System Update Every Sunday
```bash
0 3 * * 0 apt-get update && apt-get upgrade -y
```

### Monitor Disk Space Every 15 Minutes
```bash
*/15 * * * * /usr/local/bin/check-disk-space.sh
```

### Send Monthly Report
```bash
0 9 1 * * /usr/local/bin/generate-monthly-report.sh
```

## Tips and Best Practices

1. **Use absolute paths** - Always use full paths for commands and scripts
2. **Redirect output** - Capture output and errors: `command >> /var/log/cron.log 2>&1`
3. **Test your scripts** - Run scripts manually before scheduling them
4. **Set environment variables** - Cron runs with a minimal environment
5. **Use comments** - Add comments to document your cron jobs
6. **Check logs** - Monitor `/var/log/syslog` or `/var/log/cron` for execution details
7. **Mind the timezone** - Cron uses the system's timezone

## Troubleshooting

### Common Issues

**Cron job not running?**
- Check cron service: `systemctl status cron` or `service cron status`
- Verify syntax with `crontab -l`
- Check logs: `grep CRON /var/log/syslog`
- Ensure script has execute permissions: `chmod +x script.sh`

**Environment variables missing?**
- Define variables in crontab: `PATH=/usr/bin:/bin`
- Source environment in script: `source ~/.bashrc`

**Email notifications?**
- Set MAILTO variable: `MAILTO=user@example.com`
- Disable emails: `MAILTO=""`

## Resources

- [Crontab Guru](https://crontab.guru/) - Interactive cron expression editor
- [Cron Documentation](https://man7.org/linux/man-pages/man5/crontab.5.html) - Official manual page

## Contributing

Feel free to submit issues, suggestions, or improvements to make these cheatsheets even better!

## License

This project is available for free use and distribution.

---

**Note**: Replace `path/to/imageX.png` with the actual paths to your cheatsheet images in the repository.

Made with ❤️ for the sysadmin community
