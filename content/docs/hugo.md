---
title: "Hugo"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

Hugo

Command Line
help : hugo --help
generate folder public : hugo
new content : hugo new posts/newpost.md , hugo new docs/newdocs.md

Installation

Windows

1. install scoop

Scoop installs the tools you know and love
command: scoop install curl
Make sure PowerShell 5 (or later, include PowerShell Core) and .NET Framework 4.5 (or later) are installed. Then run:
command: Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')

# or shorter

    command: iwr -useb get.scoop.sh | iex

Note: if you get an error you might need to change the execution policy (i.e. enable Powershell) with
command: Set-ExecutionPolicy RemoteSigned -scope CurrentUser

2. install hugo dengan scoop
   command: scoop install hugo
   Or install the extended version with:
   command: scoop install hugo-extended
   install theme (cari di web hugo)
   command: git submodule add https://github.com/alex-shpak/hugo-book themes/book
   Then run hugo (or set theme = "book"/theme: book in configuration file)
   command: hugo server --minify --theme book

3. jalankan web dengan perintah
   command: hugo server
   copy link server ke browser.
   Untuk generate folder public
   command: hugo
   folder public akan muncul, website statis siap di upload.
