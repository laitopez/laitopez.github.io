---
slug: browse-github-repos-with-fzf
title: Browse Github repos with FZF
description: "wtf"
pubDate: "Dec 03 2025"
tags: [automation, shell, git]
---

The goal is to open a repo on Github from the terminal. You can do that using the `gh` cli if your current working directory is the same as the repo. But I want to be able to browse all repos from any terminal window.

This is a similar automation to my [bookmarks manager cli](https://laitopez.github.io/blog/fzf-terminal-bookmark-manager/)

We just need to change the input for the shell function to the following using the `gh` cli

```sh
gh repo list ORG \
-- no-archived \
-- limit 250 \
-- json name,url \
-- template '{{tablerow "NAME" "URL"}}{{range .}}{{tablerow .name .url}}{{end}}{{tablerender}}'
```

I did notice the latency is quite slow when fetching all the repos

This still relies on the Github ui (which is what I'm trying to replace) but at least this remove the need to use the Github search or navigation tree ui for repos and can just go straight to the repo

The full function

```sh
function ORG {
 gh repo list ORG \
    -- no-archived \
    -- limit 250 \
    -- json name,url \
    -- template '{{tablerow "NAME" "URL"}}{{range .}}{{tablerow .name .url}}{{end}}{{tablerender}}'
  | fzf \
  | awk -F ' ' '{print $2}' \
  | xargs open
}
```
