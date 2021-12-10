## Because privacy matters

[

![Rene Schallner](https://miro.medium.com/fit/c/28/28/1*xMb_N43CWRV4I0eF8xi47A.png)



](https://renerocksai.medium.com/?source=post_page-----615d5a7028c1--------------------------------)

![](https://miro.medium.com/max/700/0*QSj4zb8xvMKfeeLA)

Photo by [Yancy Min](https://unsplash.com/@yancymin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

Here I show you how I use an encrypted git repository on GitHub to sync my Zettelkasten (Obsidian vault) to all my devices, including my Android smartphone.

In case you’re wondering: My digital Zettelkasten is a folder in my filesystem, containing plain text files with Markdown formatting (and images) that I manage with [Obsidian](https://obsidian.md/) and sometimes with [Sublimeless\_ZK](https://renerocksai.github.io/projects/sublimeless_zk). This future-proof format lends itself perfectly to being version-controlled and distributed with [git](https://git-scm.org/).

**Update: If you implement this, please make sure you also follow my post about** [**merges and conflicts**](https://renerocksai.medium.com/handling-merges-and-conflicts-in-an-encrypted-github-zettelkasten-a7a16495fe51)**!**

You will get the most out of this article when you know git and the command line does not put you off. Setting up my workflow requires both. While I will walk you through all steps necessary to get to an encrypted, GitHub-hosted Zettelkasten, it can appear intimidating if you’re completely unfamiliar with the command line.

I primarily work on Linux (or ChromeOS + Linux Shell), but all software involved is available for Windows and macOS, too.

## Motivation

I usually use 5 different machines regularly:

-   my Chromebook is my private laptop
-   my Linux desktop at home with the big screen
-   my work laptop under Linux
-   occasionally my same work laptop booted into Windows
-   my mobile phone running Android

I want to be able to work on my notes on all machines.

The solution I came up with involves the following software:

-   git
-   Obsidian Git Plugin for Obsidian
-   [git-crypt](https://github.com/AGWA/git-crypt)
-   [termux](https://termux.com/) for Android
-   [termux:widget](https://wiki.termux.com/wiki/Termux:Widget) for Android

## Why not use BoxCryptor / Cryptomator and DropBox?

I had used DropBox sync in the past, with [Sublimeless\_ZK](https://renerocksai.github.io/projects/sublimeless_zk), and that lead to all sorts of sync conflicts on the DropBox side of things, especially after having been offline for a while — and in general, the sync was rather slow and also intermixed with everything else in my DropBox that wanted syncing. Syncing my Zettelkasten on Windows was never instant, as DropBox had to catch up with too much. Also, at that time, I didn’t use any encryption.

## Boxcryptor

When searching for cloud encryption software, [Boxcryptor](https://boxcryptor.com/) is one of the first search results. From what I read, its Linux support seems to be second-class, only available via its “portable” version that seems to only allow access to files through its GUI, making it inaccessible for other software.

Google also returns that in the past, their “classic” version had supported Linux properly, something they seem to have given up on. These days, they seem to focus more on MS Teams than Linux.

The overall picture I get is:

-   it is paid software
-   there is a clear focus on Windows and Mac
-   it has subpar Linux support: no longer supporting Linux as a first-class citizen

So Boxcryptor disqualified itself.

## Cryptomator

I instantly liked [Cryptomator](https://cryptomator.org/):

-   it is free
-   it is open source
-   it supports Linux, Windows, Mac, Android, iOS
-   independent security audits exist

So if I ever wanted to use cloud encryption software, it would be Cryptomator.

Cloud encryption software like Cryptomator provides you with a virtual drive or virtual folder that acts as the interface to transparently encrypt and decrypt your files residing in another folder, one that is synced with the cloud.

The cloud-sync is left to the cloud provider. To use Dropbox, you have to install their software that creates yet another virtual folder that gets synced to the cloud.

I’m not too fond of the idea of nesting virtual folders, and: I don’t like to have encryption software and cloud-sync software running in the background. Especially on my Chromebook, where I start the virtual Linux machine on-demand by opening the terminal, I want this to be as lightweight as possible. Just for running a terminal, I don’t want to start unnecessary background software.

Instant synchronization, as handy as it might look, can be dangerous: If you delete a file (or large portions of it) by accident, this gets synced with the cloud instantly — your errors get propagated to all other devices instantly as well. By the time you realize you made a mistake, it might be too late. I don’t like that. To protect yourself against such errors, you have to use some backup or version control solution on top of the sync that sits on top of the transparent encryption.

Three layers of magic software is where too many things can go wrong. While I wouldn’t mind syncing my Dropbox and using Cryptomator in general, I don’t want to set them up just — and especially — for my Zettelkasten.

For all my version control needs, I use git anyway — so if I can encrypt my git repository transparently, that’s actually all I need.

I quite like the synchronization workflow I get through git:

-   I work on my local copy.
-   I can refresh the local copy to the state of the cloud repository (`git pull`)
-   I can make changes locally
-   I stage the changes that I want to keep and commit them locally (`git add` and `git commit`)
-   When I’m happy with it, I push the changes to the cloud repository (`git push`)

With an Obsidian plugin, committing and pushing are just one hotkey press away, as is pulling. However, if I feel like it, I can use git’s command-line tools or any other git software for syncing.

Syncing on demand is very useful. It protects me against accidentally propagating mistakes to all synced devices. It gives me a chance to review my changes. And since git is built for distributed version control, detecting and resolving conflicts is very natural.

Reverting to previous versions, etc., is also possible with git. Since I use git extensively in my daily work, I really like the idea of using it to take care of my Zettelkasten, just as I trust it with all my source code.

Before deciding to take my Zettelkasten (back to) the cloud, I had used git to sync between my devices:

-   Chromebook
-   Linux desktop
-   Work laptop
-   Android phone

However, I used my Linux box to keep the central repository that all working copies push to, with my local IP address. Obviously, this only works in my home network, so syncing on the go is not possible.

Using GitHub (or GitLab) or any public, cloud-hosted git repository will provide me with an off-site backup in the cloud and enable syncing at work and on the go.

So let’s dive in and get our vault under git control.

## (Re-) Initialize your Repo

In the following examples, your Obsidian vault will be located in `~/zettelkasten`.

**!!! PLEASE MAKE A COPY OF YOUR VAULT FIRST !!!**

This, `zettelkasten.bak`, will be our backup if anything goes wrong later.

We initialize a git repository, initialize git-crypt and copy the secret key it generates to `~/git-crypt-key`:

## Set up .gitignore and .gitattributes

Here is my `.gitignore` ; you may want to put the entire `.obsidian` directory into there, but I prefer it this way:

Alternatively, copy back the ignore file from your backup if you had used git before:

git-crypt only encrypts files with certain git attributes. In my case, I specify:

-   all `.md` markdown files in all subfolders
-   all files in all subfolders
-   this will exclude dotfiles like `.gitattributes`

You need to store these attributes in a file called `.gitattributes`.

Here is my `.gitattributes`:

Now, if you’re using oh-my-zsh, the following two commands will prevent it from slowing down your command line:

## Add your files

## TEST YOUR .gitattributes

You should only see harmless files like `.gitattributes` be reported as unspecified. If any file pops up here that you want to be encrypted, you need to change your `.gitattributes`.

If unsure, use mine:

## Commit and push

First, we’ll commit all files we have added before:

## Set up a remote repo for testing your config

To test the encryption when pushing, we’ll set up a bare git repository :

We’ll temporarily add it as a remote repo and push our Zettelkasten there:

Now we clone the bare repo to see whether we get back encrypted files:

The file should come back as scrambled. Let’s try to unlock the repository:

The file should be decrypted.

**Note:** From now on, you can add, commit, push from the `testcrypt` repository, and git-crypt will transparently encrypt and decrypt your files.

## Cleaning up local test repos

Create an empty, **private** repository on GitHub and follow the instructions about pushing an existing repository.

I assume you have used GitHub before and have your credentials set up (e.g., for ssh use):

Great! Your encrypted Zettelkasten is now on GitHub 😀!

## Checking it out on a different machine

To work with your vault on a different machine

-   install git-crypt
-   clone the repository
-   unlock the repository

For that to work, copy the `git-crypt-key` to the new machine; I use `scp` for that:

Now clone and unlock:

Don’t forget, if you use oh-my-zsh, to do the following:

**Note:** From now on, you can add, commit, push from this repository, and git-crypt will transparently encrypt and decrypt your files.

Install the plugin Obsidian Git. Configure the plugin: Make sure, _“Disable Push”_ is deactivated.

Do this on all your machines.

Now, every time you want to sync your changes, press `ctrl+p` and search for _"Obsidian Git: commit ..."_.

The plugin will automatically pull all remote changes when you start Obsidian. If you leave it running for days, you might want to pull recent changes manually: `ctrl+p` and search for _"Obsidian Git: Pull"_.

**Update: If you implement this, please make sure you also follow my post about** [**merges and conflicts**](https://renerocksai.medium.com/handling-merges-and-conflicts-in-an-encrypted-github-zettelkasten-a7a16495fe51)**!**

Now on to the hackiest part of them all: syncing your repository on Android!

Once you have your Zettelkasten on your mobile, you can access it, add and edit files with software like [iA / Writer](https://ia.net/writer) or [Epsilon Notes](http://epsilonexpert.com/).

We will install the fantastic [termux](https://termux.com/) to get a Linux shell on Android. Then we will install git and git-crypt and clone the repository like we would on Linux.

We’ll add a handy commit and push and a pull shortcut that we can launch directly from the home screen.

## Installing termux

First, we install termux. The play store version works fine, even though they recommend [F-Droid](https://f-droid.org/). Later, we'll install an add-on that adds scripts for pulling and pushing to our home screen. This add-on is free on F-Droid but costs ca EUR 2.00 on the play store. Since one shouldn't mix play store and F-Droid and I had termux installed already, I just kept continuing using the play store version.

The following commands typed within termux will install git and git-crypt and give termux access to your phone’s files:

Now we’ll prepare for GitHub access.

## GitHub

First, we generate a new ssh key for Android.

In termux, we type:

When prompted for a passphrase, we press enter.

Next, we add the ssh key to GitHub: [like described here](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account):

-   we sign in to Github
-   we click our photo
-   we select settings
-   we click on “SSH and GPG keys.”
-   we click on “New SSH key.”
-   we go to termux and type `cat .ssh/id_ed25519.pub`
-   we copy the key
-   we paste it into the “key” field of the browser
-   we click “Add SSH key.”

## git-crypt

We need to copy the `git-crypt-key` file into termux. I zipped it, uploaded it to a safe space, and used Chrome on Android to download it. So my downloads folder contained `git-crypt-key.zip` which I unpacked in termux:

Next, we clone the repository:

Now we unlock it using git-crypt:

Once it’s finished, we move it to the shared folder:

Great, now you can access your notes from any Android app!

## Shortcuts for committing, pushing, and pulling

We’ll create a few scripts:

`**repo.conf**`**:**

`**pull.sh**`**:**

`**push.sh**`**:**

`**log.sh**`**:**

You can prepare and download them, just like we did with `git-crypt-key` or edit them directly in termux.

Next, we’ll make them executable:

From now on, we can commit and push like this:

`$ ./push.sh`

And we can pull remote changes like this:

`$ ./pull.sh`

We can see what version we’re on with:

`./log.sh`

However, it will be even cooler when we can push and pull directly from our phone's home screen.

## Adding shortcuts to the home screen

First, we need to install _termux:widget_ from the play store or F-Droid, just like we did with termux itself.

Next, we create the shortcuts in termux:

After that, **after exiting termux**, you can open your launcher’s widget menu, select _Termux:Widget,_ and place it on your home screen.

**Note:** The shortcuts will only work when termux is not running. To exit, type `exit` and press `[enter]`!

There are two different variants:

-   one shows a little text menu
-   the other one allows you to place an icon per script

![](https://miro.medium.com/max/14/0*Doo14mw0ShlKTpYX.jpg?q=20)

And here is my output of `log.sh` on Android:

![](https://miro.medium.com/max/14/0*HPUTlyW6wuPX_-VO.jpg?q=20)

Et voila! Now you have an encrypted GitHub repository for your Zettelkasten that you can use to sync all your devices!

**Update: If you implement this, please make sure you also follow my post about** [**merges and conflicts**](https://renerocksai.medium.com/handling-merges-and-conflicts-in-an-encrypted-github-zettelkasten-a7a16495fe51)**!**