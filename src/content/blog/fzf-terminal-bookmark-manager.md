---
slug: fzf-terminal-bookmark-manager
title: FZF terminal bookmark manager
description: "wtf"
pubDate: "Oct 15 2024"
updatedDate: "Oct 16 2024"
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
airbnb, https://medium.com/airbnb-engineering
aws, https://aws.amazon.com/blogs/aws/
cloudflare, https://blog.cloudflare.com/
discord, https://discord.com/blog/
dropbox, https://dropbox.tech/
facebook, https://engineering.fb.com/
github, https://github.blog/engineering/
heroku, https://www.heroku.com/blog/category/engineering/
instagram, https://instagram-engineering.com/
linkedin, https://www.linkedin.com/blog/engineering
netflix, https://netflixtechblog.com/
stackoverflow, https://stackoverflow.blog/engineering/
stripe, https://stripe.com/blog
twilio, https://www.twilio.com/en-us/blog
yahoo, https://yahooeng.tumblr.com/
```

shell function

```sh
function li {
    column -t -s="," ~/links.csv | sort | fzf | awk -F ' ' '{print $2}' | xargs open
}
```
