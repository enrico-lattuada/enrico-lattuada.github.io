---
title: How to create an academic group website with Hugo Academic in 2024
subtitle: ""

# Summary for listings and search engines
summary: A note to my future self (and anyone who might be interested) on how to build and customize a Hugo Academic group static webpage.

# Link this post with a project
projects: []

# Date published
date: '2024-03-22T00:00:00Z'

# Date updated
lastmod: '2024-03-22T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
# image:
#   caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
#   focal_point: ''
#   placement: 2
#   preview_only: false

authors:
  - admin

tags:
  - Website

categories:
  - Tutorial

commentable: true
---

{{% callout warning %}}
This post is under construction.
{{% /callout %}}

In this post, I will go through the steps to set your Windows computer up to run a [Hugo Blox](https://hugoblox.com/) academic group static website and host it on GitHub Pages.
This post serves as a personal guide for my future self, detailing the steps to create a page using the Hugo Research Group template.
However, it’s not just for me -- if you’re interested in embarking on this journey of creating your own Hugo Research Group or Academic CV page, I hope you’ll find this guide useful too!

If you have doubts whether or not to choose this tool for your website, the post of [Jianing Yang](https://jedyang.com/post/how-to-build-academic-research-group-website-in-2021/) states some pros and cons and I found it very clear in this regard.

# Setup git and GitHub

## Create a GitHub account

If you are familiar with Git and GitHub, you probably have a GitHub account already.
If this is not the case, don't worry: you will not need super technical expertise to navigate your way through the next steps!
Just head to [GitHub](https://github.com/) and create an account.

## Install GitHub Desktop

If you are on Windows, [GitHub Desktop](https://desktop.github.com/) provides a more user-friendly way to manage your GitHub repositories (including the one that will contain the source of your website).
Just download and run the installer.
During the installation, you will be asked if you prefer to use the email, which is assigned to you by GitHub, or your personal email.
I suggest to select the latter from the dropdown menu.

## Install VSCode

Also, having an IDE like [VSCode](https://code.visualstudio.com/) is not mandatory, but it surely will help.
Again, just download and run the installer.

## Install git

Finally, download and install [git](https://git-scm.com/download/win).
During the installation, you will be asked to select from several options.
Among them:

* Select Visual Studio Code as the default editor.
* Override the default branch name and use `main`.

# Install Hugo

{{% callout note %}}
You will not need your terminal to update your website.
However, you might want to check how it looks **locally** before you publish it.
{{% /callout %}}

## Install Go

Download and install [Go](https://go.dev/doc/install).
After installation, test it from the PowerShell by running the command:

```powershell
go version
```

and confirm that the command prints the installed version of Go.

## Install Dart Sass

Download the [dart-sass](https://github.com/sass/dart-sass/releases/tag/1.72.0) prebuilt binary from GitHub (current version, v1.72.0).
Unzip it and save it wherever you prefer.
Finally, add it to the `Path` variable.

{{% callout note %}}
To add a path to the `Path` environment variable, search for `Edit system environment variables` in the Windows' search bar.
From the window, select `Environment variables...`.
Select the `Path` variable in the user variables' list and edit it.
Add the path of the directory containig the `.exe` (**!!**) file to the list.
{{% /callout %}}

## Install Hugo

It's now time to install [Hugo](https://gohugo.io/installation/).
Download the [hugo extended](https://github.com/gohugoio/hugo/releases/tag/v0.124.1) prebuilt binary from Github (current version, v0.124.1).

{{% callout warning %}}
Installing the extended version is **highly** recommended.
Download the appropriate installer, for example hugo_**extended**_0.124.1_windows-amd64.zip.
{{% /callout %}}

Unzip it and save it wherever you prefer.
Finally, add it to the `Path` variable (see section above for instructions).

Confirm the installation by running this command from the PowerShell:

```powershell
hugo version
```

# Clone the template repository

{{% callout warning %}}
Hugo Blox, formerly Wowchemy, seems to keep changing name.
The links provided below could change in the future.
However, the steps we see should not change much and could be used as a starting point in any case.
{{% /callout %}}

Go to the [Hugo Blox](https://github.com/HugoBlox/) GitHub page and find the theme-research-group repository.
Click on the `Use this template` green button on the top-right corner and select `Create a new repository`.
Select a name (usually, `<yourname>.github.io`) and leave the repository public.

Finally, you can clone the repository locally on you computer.
Use GitHub Desktop to clone the repository containing the website source.

You will now be able to build and run the website locally on your computer, without deploying it to the web.
Use your PowerShell terminal and run the following command:

```powershell
cd path\to\your\repository
```

where `path\to\your\repository` is the path to your repository.
If you cloned the repository using GitHub Desktop, this will probably be in

```powershell
cd Documents\GitHub\<your-repository-name>
```
where `<your-repository-name>` is the name you chose for your repository.

You will be able to build and run your website locally by running the following command:

```powershell
hugo server -D
```

You will be able to access the webpage (usually) from the address `http://localhost:1313/`.
