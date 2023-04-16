---
title: The Ultimate Godot Setup Guide™
description: how to get setup with Godot, Visual Studio Code, and GitHub with automatic deploys to itch.io
author: ikestrel
date: git Last Modified
tags:
  - tutorial
  - godot
  - github
  - itch
draft: true
---

hi! what follows is a straightforward guide to help you get past all the annoying parts of setting up a new project with Godot. there may be parts of this that are still helpful even if you have a Godot project in development (e.g. getting your code backed up to GitHub or automatically generating builds for itch.io) so feel free to jump around if need be - i will try to keep things compartmentalized so it's equally useful that way as it would be if you were reading start to finish.

(btw - if you haven't read [my thoughts on tutorial writing](docs-manifesto.md), i might recommend that first just so you know what you're getting into. or not. i'm not your boss 😉)

# Step 1: Downloading Godot Engine

Godot Engine is a free, cross-platform, and open-source game engine that allows you to create 2D and 3D games with relative ease. i like it a lot! if you have any familiarity with Unity or Unreal you should feel somewhat at home here (after a bit of reorientation), but even if you're coming in with no prior gamedev experience, i think the learning curve is pretty managable.

anyway, the purpose of this guide is not to teach you how to use the engine, but just get past the boring part of getting it on your machine and Ready To Create. so let's get into it.

{% image "./godotsetup-download.png", "this is a screenshot and not real buttons, please do not click" %}

you can find download links for Godot on the main website at [https://godotengine.org/](https://godotengine.org/). it should autodetect which platform you're on (Windows/Mac/Linux) so no need to worry about that.

there is one somewhat complex decision you'll have to make at this stage, however: at time of writing, there are two versions readily available that are meaningfully different enough that you might want to take a minute to be sure you're downloading the correct one. again, i wanna keep this guide light and airy so i'll try not to go super deep:

### Download Latest (4.x)
the latest and "greatest" Godot version makes a lot of great improvements to the already great version 3!

it also makes changes to the scripting language that are incompatible with projects made with Godot 3 (and similarly could make it more challenging to learn as a beginner - there are dramatically more educational resources geared toward Godot 3). that hurdle can probably be overcome with some effort, but the greatest sin that v4 commits (imho) is that exporting to web is Totally Busted.

as someone who's almost exclusively made browser-based games for her whole career, i think this majorly sucks and especially hurts newer devs who already have enough barriers to getting their work in front of ppl. i can't speak for The Entire Internet but at least personally i'm dramatically less likely to try out a new thing if i have to download it. i'm just too spoiled on web builds, sorry.

### Download LTS (3.x)
an oldie but a goodie - LTS stands for "Long Term Service", which means the developer intends to provide some level of support and updates for this version into the forseeable future. so while it may be tempting to use the shiny new Godot 4, you also can't really go wrong with Godot 3.

considering this along with my aforementioned points about there being a wealth of tutorials and Actually Working web exports, i would strongly encourage sticking with this version until the new hotness gets more mature.

**NOTE:** it _mostly_ shouldn't change things much either way for the purposes of this guide, but just fyi i will assume you're working with Godot 3 for the duration.

go ahead and extract the downloaded zip file wherever you like - it's worth noting that Godot does not get "installed" like most programs, so the exe/app/whatev that you get is the thing that you'll make your game with.

i keep it at the root of my `C:\` drive bc i'm an idiot and will forget where it is otherwise (on Mac you can just drag and drop it into your `Applications` folder, which is the norm anyway)

# Step 2: Backup, Versioning, & Collaboration with GitHub

now that you have Godot downloaded, you can start making a game! but oh no! your hard drive exploded and you lost all your progress. what are we going to do-

what's that? you had your project backed up in Dropbox? okay cool, let's open that up and- OH NO there's an incredibly game-breaking bug that you introduced last week and didn't even realize, how are you ever going to-

oh. you...

...duplicate your project folder once an hour to keep backups of individual versions...

...i'd say that's serial killer behavior but i also used to do that soooo

ANYWAY i'm glad you came up with a system to deal with these catastrophes, but surely there's a better way, right? the ppl who make Fortnite aren't burning their codebase to a DVD at the end of every work day (probably), so what _are_ they doing?

## Version Control with Git

now, i am not an expert on this subject by any means, so don't expect a killer crash course or anything. i do, however, know Just Enough to be Dangerous (but like, in a cool and alluring way, not in the serial killer way, i promise) so i will give you just a bit of context and then link to resources if you want to learn more.

Git is a "version control system" that smart ppl use to maintain a _local_ running history on individual files inside a project. after "initializing" Git inside your Godot project folder, you can "commit" changes that you make to your files to the Git "repository" (or "repo"). each commit acts as a snapshot of the project's state that you can (somewhat) easily review at any time.

this is obviously great for when you make changes that introduce bugs since you can "diff" two versions of a file against each other and research what went wrong, but you may be wondering where the "backup" part of this comes in since i very intentionally emphasized _local_ in that last bit. let's get into it!

## Backup and Collaboration with GitHub

while _Git_ is a program that runs on your local computer and maintains a version history, _GitHub_ is a website that allows you to "push" (or upload) your local Git repo to The Internet for ALL THE WORLD TO SEE...or just you and ppl you specifically invite, if you make the repo private.

it's pretty much always a good idea to go through the process of initializing a new project as a Git repo and pushing it up to GitHub! it may be just a little daunting at first, but after you've done the workflow a couple times it'll be just like riding a bike

if you had to type `bike init` to get the bike out of the garage

and then `bike add *` to mount it

and uhhh `bike commit -m 'first bike ride of the summer hope i don't die :)'` to commit this memory to your brain and `bike push` to start moving (or send the memory to the cloud? sorry the metaphor is starting to break down)

# Step 2.5: ~~Bike~~ Project Management with Visual Studio Code

okay i'd like to formally apologize if things got a little scary back there. you can open your eyes now and stop imagining that you're tumbling down Springfield Gorge on that bike you definitely forgot how to ride.

while Git is tradionally one of those things you have to open a Command Prompt/Terminal and remember a bunch of super specific syntax to work with, we thankfully live in The Future with lots of nice graphical interfaces layered on top of all the boring nerd shit so us normies can benefit too. so forget everything you know about riding a bike, we're gonna make the computer do most of the remembering work for us!

## Setting up Visual Studio Code for GitHub

head on over to [https://code.visualstudio.com/](https://code.visualstudio.com/) and click the big download button. do all the installation stuff and come back when you have the program open. it's okay, i'll wait.

alright, welcome back. so you're probably wondering what the fuck this thing is - or maybe not bc you already read the "Code editing" bit on the homepage. sorry. i didn't mean to insult your intelligence. thank you for sticking with me this far, i promise i will try to be nicer.

while VS Code is primarily an IDE (Inegrated Development Environment) that gives you a nice interface for coding, the important bit for this guide is that it has Git stuff built-in! while you'll still ultimately be doing the same workflow of "init" a project repo, "commit" changes locally, and "push" changes to GitHub, VS Code mercifully abstracts all of this to a degree that you only need to develop muscle memory for some buttons rather dedicate precious Brain Memory to a bunch of typed commands.

i _could_ go into specifics about this workflow, but honestly it's pretty straightforward (assuming you did allocate Brain Memory to the basic Git workflow of init/commit/push after i mentioned it mulitple times). if you need a little more support (or just need some visual aid on where to find the buttons), check out this [Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview) page.

the one new concept i might want to highlight here is "cloning" a repository, which is when you want to work locally with an existing Git repo that's stored in GitHub. you can provide a URL to the online GitHub repository and "pull" it down that way, but even better, you can link your GitHub account with VS Code and use the "Clone from GitHub" option to pick something right out of a list. easy!

## *OPTIONAL*: Setting up VS Code for Godot

while everything discussed in Step 2 so far has been largely not specific to Godot (you can manage lots of different projects with Git!), i do want to give a little insight into my personal workflow using Visual Studio Code with Godot.

Godot is very slick in the way that it includes a built-in code editor for editing scripts, so you don't _really_ need VS Code or any other editor to work with it. however! it can be nicer to use a dedicated tool that you can have open on a second monitor, especially if you have it open for dealing with Git stuff anyway.

if that sounds compelling to you, i'd recommend installing the [godot-tools](https://marketplace.visualstudio.com/items?itemName=geequlim.godot-tools) extension from the VS Code Marketplace, which brings VS Code largely up to speed with the functionality of the built-in editor (with syntax highlighting and autocompletion and all that)

once the extension is installed, you'll want to do a little extra config inside Godot to make VS Code your default editor:

1. Open the Editor Settings
2. Select Text Editor > External
3. Make sure the Use External Editor box is checked
4. Fill Exec Path with the path to your VS Code executable
   - On macOS, this executable is typically located at: `/Applications/Visual Studio Code.app/Contents/MacOS/Electron`
5. Fill Exec Flags with `{project} --goto {file}:{line}:{col}`

i copied that directly from the marketplace page, which has more details about usage and config if you scroll down. there's a lot of cool stuff it can do with debugging and breakpoints that i probably don't use nearly as much as i should, so i'd encourage you to do a little reading and become a better developer than i am with this newfound power

with this setup, my workflow is typically that i open my Godot project in VS Code _first_ and run the command to open Godot from VS Code so it automatically attaches. if Godot isn't attached to VS Code, it won't be able to communicate all the syntax/autocomplete/etc stuff and at that point you may as well just be using the built-in editor.

i've had my fair share of weird config issues having set this up multiple times on both Mac and Windows machines with Godot 3 and 4, so if you have any trouble feel free to [email me](mailto:contact@iznaut.com) and i can _try_ to help get you sorted. no promises tho (i am not an expert)

# Step 3: Automatic itch.io Builds with GitHub Actions

{% image "./godotsetup-githubaction.png", "dedicate just a little work up front and you'll get to see this nice green checkmark every time you change your code. unless something breaks. which it probably won't. probably" %}

alright! here's the cool part! at least, i think it's pretty cool.

you may well be familiar with the lovely indie game marketplace [itch.io](https://itch.io/) already. you may even have an account already! woah, you have a game uploaded too?? sick, i can skip over all explaining all that stuff then.

if you've already shipped a game on itch, you've likely had to update said game as well, which is a bit less exciting than that initial upload. imo gamedev should be _nonstop_ fun and excitement so let's continue our journey toward streamlining the everloving shit out of your development workflow so you can spend more time doing That Good Shit like spending two hours troubleshooting an error that was caused by you typing `palyer` somewhere instead of `player` (it's okay we've all been there)

with pushing changes up to GitHub already an important part of our workflow, we can take advantage of another neat tool that comes along with it: GitHub Actions!

[GitHub Actions](https://github.com/features/actions) are workflows triggered _automatically_ when certain events occur on a GitHub repository, such as pushing code changes. thanks to this framework and the hard work of individual contributors, we can rig up a workflow that will rebuild our Godot project and submit it to itch.io _every time_ a change is made. see?? it's cool, right???

## Github Action Template

this is another section that you could easily do your own research and find better resources on, so i'm just going to make this as painless as possible by giving you a nice template to start off with. don't be intimidated! it's not that bad!

<script src="https://gist.github.com/iznaut/a7bea257911284f8f4b2a740c36d42cf.js"></script>

go ahead and download (by right clicking "view raw" and "Save link as...") this file - it should be named `build-and-publish.yml`. create two new folders in your project: `.github` at the root and `workflows` within that.

{% image "./godotsetup-githubdir.png", "you should end up with something like this in VS Code, maybe with different colors if you haven't spent 20 hours finding the perfect theme yet" %}

before we push it up to GitHub, we just need to make a few tweaks:

- replace `[YOUR USERNAME HERE]` with your itch.io username (e.g. `iznaut`)
- replace `[YOUR GAME ID HERE]` with your itch.io project ID (e.g. `gexfeld`)

you can grab these easily out of the url for your game, even if it's not live yet (e.g. [https://iznaut.itch.io/gexfeld](https://iznaut.itch.io/gexfeld))

