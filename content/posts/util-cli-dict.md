---
title: "Util: CLI Dictionary"
date: 2023-07-11T22:05:07+05:30
tags: [productivity, utility]
---

I end up having to lookup certain words which I'm not familiar with often and even though spotlight(macOS) provides quick lookup sometimes it mixes up with other files or OS related applications.

So if you are someone who finds yourself in the terminal most of your days this will be helpful.

## What you'll need

- Terminal
- `curl` CLI tool (which is inbuilt in most cases)
- `jq` CLI command (google "how to install jq in *your_os*)`

That's it!

## The setup

1. Open your shell rc file (.bashrc, .zshrc etc)
2. Add the following lines

```sh
meaning() {
    echo "The meaning of: $1"
    curl https://api.dictionaryapi.dev/api/v2/entries/en/$1 -s \
        | jq '.[].meanings[] | {(.partOfSpeech): [.definitions[].definition]}'
}
```

Curl calls the api endpoint given, which then sends a json reponse. This json response is piped to the `jq` command to trim the json down to only the required bits.

## Usage

Source your shell rc file eg: `source .bashrc`

Start using it by calling `meaning`:

```
$ meaning supercalifragilisticexpialidocious 
```
