---
title: FZF terminal bookmark manager
description: FZF terminal bookmark manager
date: 2024-10-30
tags: [automation, shell]
---

At work there are a lot of (sub)domains for all the different platforms. Internal tenant platform, internal email platform, internal azure group management platform, internal ci/cd platform, internal docs, this specialized tool, that specialized tool, etc.

Some I have ready at the end of finger tips but many require me to bother someone for the link again or go searching in the blazingly fast Confluence site for the domain.

Why don't we load all those domains in to a csv file and then create a shell function for searching and opening that site in the browser?

### Example
I won't use the links.csv I use at work but here is a simple example using some company domains. Place this file in your root directory

links.csv
```text
description, domain
airbnb, https://www.airbnb.com/
apple, https://www.apple.com/
apple music, https://music.apple.com/us/browse,
aws, https://aws.amazon.com
aws docs, https://docs.aws.amazon.com/index.html
```

shell function
```sh
function li {
    column -t -s="," ~/links.csv | sort | fzf | awk -F ' ' '{print $2}' | xargs open
}
```
