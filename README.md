# Links
By using github actions, github pages and jekyll I made myself a public bookmark service
you can see it [here](https://umtksa.github.io/links/)

every link in my "bookmarks" is a jekyll post, posts just directing you to url at the yaml so markdown files are only yaml frontmatter without content.

Pushing a new markdown file to _posts folder fires a github action that build the jekyll blog and update the github page.

here is the yaml
```
---
layout: post
title: Title of the link
link: https://example.com/
summary: a short description
tags: tags seperated with space
---

```

I'm not using this for all my bookmarks but I have some
bookmark generation tools I have like a bash script, a static html form and a siri shortcut for sharing links directly from mobile browser (in this case Firefox but shorcut works with any browser.)

The one I use most is a bash script I come up from some internet searching.
This bash script just ask title, link, summary, and tags then generate a md file with proper format  
date and title seperated with dashes, like this "yyyy-mm-dd-name-of-the-link.md"

Here is the bashscript

```
#!/bin/ksh
echo "title: "
read title
echo "link: "
read link
echo "summary: "
read sum
echo "tags: "
read tags

ptitle=${title// /-}
plc=`echo "$ptitle" | tr '[:upper:]' '[:lower:]'`
pdate=`date +%Y-%m-%d`
filename=/links/_posts/$pdate-$plc.md
touch $filename

echo -e "---
layout: post
title: $title
link: $link
summary: $sum
tags: $tags
---\n" > $filename

echo "link created"

cd /Users/mac/links
git add .
git commit -m "new link"
git push

echo "new link posted"

```

And [here](https://umtksa.github.io/links/post) is the static form I use to generate markdown files with proper name and frontmatter. Its just a static html file with a download button that generate md file for you to save in your _posts folder.
based on [this](https://www.simongriffee.com/notebook/form-to-txt/) page.

For sending links from my mobile phone running iOS I'm using [this siri shortcut](https://www.icloud.com/shortcuts/65a5ef0312ec4b0cae187dfe0f33349c) to generate a markdown file in _posts folder on dropbox. If you want to use it just change the "destination Path" to your own path.

Some useful links:

[github repo](https://github.com/umtksa/links)

My theme is based on [this](https://github.com/P0WEX/Gesko)theme

[Jekyll documentation](https://jekyllrb.com/docs/continuous-integration/github-actions/) about using github actions for jekyll.

peace.

post code sample adapted from [form to text](https://www.simongriffee.com/notebook/form-to-txt/)


Forked from [Asko](https://github.com/manuelmazzuola/asko).
Original theme from [Sidey](https://github.com/ronv/sidey).
