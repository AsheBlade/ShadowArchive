---
layout: post
title: gitignore cheatSheet
date: 2020-10-09
author: Shadow Walker
tags: [Tech, Git]
toc: true
comments: true
---

I have always been borthered with how to use Git. As a SDE, it's very important to get to know how to use Git. Based on this, I would like to keep recording of some knowledge I have about .gitignore in here. 


## How to create

To create is simple, you can basically create one with vim or whatever IDE you prefer. However, after creating with vim, the .gitignore file might be hidden. If you are using mac, you can set everything in Finder visible by using such commands: 

```
defaults write com.apple.finder AppleShowAllFiles -bool true
killall Finder
```

## .gitignore Syntax

The syntax is very ituitive and I don't feel like spending time to talk about it. 

For more resource, you can google. It's not a hard syntax anyway. 

```
.jekyll-cache/*
.DS_Store
_posts/.DS_Store
node_modules/*
_site/*
```

## Most Common Question

.gitignore is supposed to be simple, but it is not as simple as it seems. People may thought they can just put file names or directory in gitignore and they will be gone forever. That's not true and not how Github works. 

If you work on a repo with file already commited, you have to untrack a file first, and then commit. 

To untrack a single file that has already been added/initialized to your repository, i.e., stop tracking the file but not delete it from your system use: `git rm --cached filename`

To untrack every file that is now in your `.gitignore`:

First commit any outstanding code changes, and then, run this command:

```
git rm -r --cached .
```

This removes any changed files from the index(staging area), then just run:

```
git add .
```

Commit it:

```
git commit -m ".gitignore is now working"
```


