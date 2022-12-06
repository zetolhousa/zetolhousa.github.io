---
title: "My Dev Journal"
date: 2022-12-06T20:23:12+05:30
---

If you read tech blogs you’ll come across articles stating how important how important it is to maintain a dev journal or bragging doc or what have you. Basically it’s just a doc where you track all that you have done, read, watched, etc.

Your brain being a finite resource can only hold so much information. Over time you lose track of the code change you made, the valuable life advice you gave to that junior, some quote someone said over a meeting. Okay that’s going overboard but you get the gist.

I’ve tried all sorts of things. Tried one too many note apps, todo apps, methods, processes and tricks. Non seem to work. Having tried all those, now I think I have come up with my own thing. Which seems to be working pretty well.

## What you’ll need

- Terminal
- Shell scripts for cronjobs to execute
    - Daily script
    - Monthly script
- Cron jobs
    - Daily job
    - Monthly job
- Bash alias
    - To add a log line
    - To view (optional)

The list looks long but it’s pretty simple. Just verbose for the sake of this blog.

## The setup

### 1) Single markdown file to log

Create and save it in a path of your choosing. Eg: `/<bunch_of_directories>/daily_log.md`

### 2) Markdown file structure

```
# January 2022

## 16 Monday
- did this
- did that

## 17 Tuesday
- did this again

# February 2022
...so on
```

### 3) Shell scripts

Daily header:

```
now=$(date +"%d %A")
echo "\n## $now" >> /<bunch_of_directories>/daily_log.md
```

Monthly header:

```
month=$(date +"%B %Y")
echo "\n# $month" >> /<bunch_of_directories>/daily_log.md
```

### 4) Cron jobs

```
0 10 * * 1-5 ~/code/cronjobs/new_log_day.sh
0 0 1 * * ~/code/cronjobs/new_log_month.sh
```

Line 1 adds a new day header. At 10AM from Mon-Fri.

Line 2 adds a new month header. On 1st of every month.


### 5) Bash aliases

```
alias slog='bat ~/notes/worklog.md'
alias clog='echo "- $1" >> ~/notes/worklog.md'
```

Line 1 shows current daily log state.

Line 2 adds a log line for the day.

## Usage

So if I did thing X. Switch to the open terminal and quickly type in:

> `$ clog “I did thing X”`
