---
title: "TIL 2"
date: 2021-09-25T12:17:43+05:30
tags: [til]
---

## `jq` command
A command to manipulate json files. At work we usually have a bunch json serialized ouputs in S3 or some other datastore, which are absurdly many lines long and deeply nested. Often, if I need to grep something out of it, I'll just copy and paste it to a company internal json prettifier to make it human readable and get what I need. There must be some out on the web too. Something like [this](https://codebeautify.org/jsonviewer).

It's a hassle when you need to switch multiple windows, download files, copy paste content, etc. Now come 'jq', a command line utility to, hopefully, end all that.

Download(on mac): `brew install jq`

Print full json:
```shell
>> jq '.' your_file.json
```

Print a level-1 keys value:
```shell
>> jq '.your_key' your_file.json
```

Print a level-2 keys value:
```shell
>> jq '.your_key.your_sub_key' your_file.json   # and so on
```

Print an array element (0 indexed):
```shell
>> jq '.[4]' your_file.json     # index 4 is the 5th element in a 0 indexed array
```

Print a range of array elements:
```shell
>> jq '.[2:6]' your_file.json   # prints index 2 up until 5
```

Print range without bound:
```shell
>> jq '.[2:'] your_file.json    # prints index 2 till the last
```

Print range from the right end:
```shell
>> jq '.[-3:]' your_file.json   # prints the last 3 elements
```

Print key of an array element:
```shell
>> jq '.[4].key' your_file.json # prints the index 4's key
```

Print for all array elements key:
```shell
>> jq '.[].key' your_file.json  # for all elements in array having 'key', all its values will get printed
```

There so much more power in `jq`, feel free to explore.

### References:
* https://earthly.dev/blog/jq-select/
* https://www.baeldung.com/linux/jq-command-json
