---
title: "My Dev Journal V3"
date: 2024-10-26T03:40:55+05:30
tags: [productivity]
---

> Refer blogs for [v1](https://www.thejazeto.com/posts/my-dev-journal/) and [v2](https://www.thejazeto.com/posts/my-dev-journal-v2/) for more history about this

> And here's a reminder on how important it is to document: https://jvns.ca/blog/brag-documents/

Dev journal v2 has done a pretty good job for me. I recently also added a functionality on my windows laptop to sync it up to a cloud storage (onedrive) via a windows automation scheduler called "Task Scheduler" at regular intervals of the day. I gotta say it's pretty neat feature which I didn't know about.

After a while of using onedrive I moved to using icloud after installing the icloud client on my windows laptop. I came to learn that icloud has been getting a lot of hate due to it's inconsistency. Files getting deleted at random and wiping out complete directories for no reason. It was a risk I took. Now I had the journals accessible on my mac. The only issue here was that the sync happens at fixed schedules (3hrs apart) and if the laptop goes offline before the next schedule then the changes which I added never reaches icloud and what I see on my mac or iphone is outdated data.

On top of all that the sync was one way. I make changes on windows and view on mac or iphone. Given the unreliability of these file storage providers I could not risk trying to make it two-way without knowing which write takes priority over the other. I guess windows and apple chose availability at the price of consistency, very weak consistency.

Anyway it was at this time when I slowly started to move back to my mac as primary laptop. But because of the dev journal workflow right now I wasn't logging in as regularly. I started exploring other ideas. Using git stood out so I sat down and revamped my workflow to integrate with git one evening.

The new worklow would now use a remote private git repo to write into every time I submitted a "clog". And of course to make sure to avoid conflicts I added a pull before every push action.

## Using git to store and sync journal logs

### What hasn't changed

The day and month header update script hasn't changed except some minor tweaks in getting paths.

Recap of what it does: This script checks your dev journal file to see if todays day header has been added already. If not then add new day. If it's a new month it also add the month header.

```bash
#!/bin/bash

# Path to your notes file
NOTES_PATH="$(dirname $0)"
NOTES_FILE="$NOTES_PATH/daily_log.md"

# Get the current date and time
CURRENT_DATE=$(date +"%d %A (%Y%m%d)")
CURRENT_MONTH=$(date +"%B %Y")

# Check if the current month title is present in the file
if ! grep -q "^# $CURRENT_MONTH" "$NOTES_FILE"; then
    echo -e "\n---\n\n# $CURRENT_MONTH" >> "$NOTES_FILE"
    echo "Updated month heading"
fi

# Check if the current day title is present in the file
if ! grep -q "^## $CURRENT_DATE" "$NOTES_FILE"; then
    echo -e "\n## $CURRENT_DATE" >> "$NOTES_FILE"
    echo "Updated day heading"
fi
```

### change-1: `clog` alias logic extracted out to a shell script

```bash
#!/bin/bash

# Define paths
REPO_PATH="$(dirname $0)"
NOTES_FILE="$REPO_PATH/daily_log.md"

echo "Daily log repo path: $REPO_PATH"

# Define functions for each step
pull_notes() {
    git -C "$REPO_PATH" pull --quiet origin main
}

# Updates the headers (month or day)
update_headers() {
    $REPO_PATH/update_headers.sh
}

add_log_entry() {
    echo "- **$(date +"%I:%M%p")** $1" >> "$NOTES_FILE"
}

commit_notes() {
    git -C "$REPO_PATH" add "$NOTES_FILE"
    git -C "$REPO_PATH" commit -m "Log entry update on $(date +"%Y-%m-%d %H:%M:%S")"
}

push_notes() {
    git -C "$REPO_PATH" push --quiet origin main
}

# Run each step in sequence
pull_notes
update_headers
add_log_entry "$1"
commit_notes
push_notes
```

This is where the bulk of the work is done. Pretty straight forward. Bunch of git operations but I think it's safe to assume that interruptions between these will be super rare. Assuming this is a personal dev log and you are the sole author, you'll only ever be on one computer at a single instance of time. So no git related conflicts should happen. If it does happen even the manual interventions should be simple to fix.

### change-2: Bash aliases

The bash aliases are now way simpler with the weight now carried by the shell scripts. Love this change.

```bash
DEVLOG_REPO='<path to devlog.git repo>'
alias slog='bat -p --theme=ansi $DEVLOG_REPO/dev_log.md'
alias clog='$DEVLOG_REPO/clog.sh $1'
```

### Wrapping up

This version is probably going to stay for a while I think. IMO a massive jump from previous versions. Now I can pull the repo from anywhere. All I need to do is set up the aliases and that's it. The repo is self contained comes bundled with the scripts and the dev journal file.

## Conclusion

* Ability to add logs from any system
* Simpler setup. Moving to a new computer and logging is super simple.
* Very reliable consistent storage
* Versioning and history of changes (if you need) via git commits

### Open issues
* How to keep record of logs when laptop is offline (no access to git)
* How to reduce number of git push and pull (maybe batch somehow?)
