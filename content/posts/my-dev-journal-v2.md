---
title: "My Dev Journal V2"
date: 2024-07-11T01:35:41+05:30
tags: [productivity]
---

Since the first blog on a dev journal [here](https://www.thejazeto.com/posts/my-dev-journal/), I've made some changes.

With the onset of LLMs I've gotten help from chatGPT to upgrade my dev journal workflow.

Some things that have not changed are the log markdown file(daily_log.md) where your logs go into and the alias names.

Things that have changed:

### 1) Shell script

Instead of having a cron job update the daily dates and month headers on a set time, which can and will fail to run if your machine is not ON at the time of cron schedule. So instead this script below will be used to do regex checks on the log file and update dates and months as required.

```bash
#!/bin/bash
# AI generated and modified for personal use

# Path to your notes file
NOTES_FILE="<bunch_of_directories>/daily_log.md"

# Get the current date and time
CURRENT_DATE=$(date +"%d %A")
CURRENT_MONTH=$(date +"%B %Y")

# Check if the current month title is present in the file
if ! grep -q "^# $CURRENT_MONTH" "$NOTES_FILE"; then
    echo -e "\n# $CURRENT_MONTH" >> "$NOTES_FILE"
    echo "Updated month"
fi

# Check if the current day title is present in the file
if ! grep -q "^## $CURRENT_DATE" "$NOTES_FILE"; then
    echo -e "\n## $CURRENT_DATE" >> "$NOTES_FILE"
    echo "Updated day"
fi
```

### 2) Bash alias
```bash
alias slog='bat ~/notes/worklog.md'
alias clog='<path_to_script_above>/check_update_notes.sh && echo "- [$(date +%I:%M%p)]$1" >> <bunch_of_directories>/daily_log.md'
```

`slog` remains the same and I forgot to mention what [bat](https://github.com/sharkdp/bat) was in the last blog but it's an upgraded `cat` command with syntax coloring and other fancy stuff.

`clog` has undergone an major makeover. It now uses the script shared in previous section to check for lines in the log file to see if required dates and months are present then add or not update based on the conditionals. No dependency on cronjobs anymore. OTG FTW!

### Usage

Usage is the same

### Closing

I may improve on this again. But for now this works great!