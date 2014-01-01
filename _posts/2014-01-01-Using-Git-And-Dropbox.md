---
layout: post
title: Using Git and Dropbox
author: jimmy
---

This guide is for people who want to use [Git](//git-scm.com) with their existing [Dropbox](//dropbox.com) account. People who use Dropbox for software development encounter problems with things like synchronising binaries and conflicted copies, exacerbated by falling into the habit of working directly on files in the Dropbox folder, something which many have come to regret time and time again.

Git is a very useful tool, but for a student starting out trying to learn it, it can prove very difficult to understand. Whether you want to use Git via your IDE, or using a program like [SourceTree](//sourcetreeapp.com), or even via the command line, you'll probably find yourself asking how to share your repositories between machines. This usually ends up with a setup like the one shown below:

![How people conventionally work with Git and an external server][git_1]

1. You do some work on your home desktop, `git add` it, then `git commit` it. You now want to share your commit, `509645`, to your laptop. So you `git push` it to an intermediary such as [Github](//github.com) or [BitBucket](//bitbucket.org), which you made online and then did `git clone`.

2. You then go onto your laptop and `git pull` those changes from your intermediary, and all is well.

With Dropbox, we're simply going to replace that intermediate location (i.e. Github, BitBucket) with your Dropbox folder.

![How we're going to use Git with Dropbox][git_2]

Obviously, Github and BitBucket have advantages, however it's perfectly understandable to not want to share their assignments or final year projects online (especially open source!) Dropbox is secure, stable and doesn't require an internet connection all of the time, you can push your commits to your Dropbox folder and it will synchronise across all of your devices the moment you regain a connection.

Create Somewhere to Store your Git Repositories in your Dropbox
=====
Firstly you need to create somewhere to put your repositories on Dropbox, for this example we'll be using `Repositories`. You can call it whatever you wish.

**Mac/Linux**
{% highlight sh %}
$ mkdir ~/Dropbox/Repositories
{% endhighlight %}

**Windows**
{% highlight bat %}
cd %HOMEPATH%\Dropbox
mkdir Repositories
{% endhighlight %}

Create a New Repository in your Dropbox
=====
Once you've created somewhere to put them, you can now begin creating git repositories for your projects. How you choose to divide up your projects is up to you, they could be by subject, by assignment or even by year, the only thing to note is [how Git handles your commits](//www.youtube.com/watch?v=ZDR433b0HJY); the more projects your repository contains the less you'll have to do in order to sync your work between machines, but the messier your repository will be. For clarity's sake, the below example creates a project called `MyExampleProject`.

**Mac/Linux**
{% highlight sh %}
$ cd ~/Dropbox/Repositories
$ git --bare init MyExampleProject.git
{% endhighlight %}

**Windows**
{% highlight bat %}
cd %HOMEPATH%\Dropbox\Repositories
git --bare init MyExampleProject.git
{% endhighlight %}

The thing to note here is the `--bare` flag. The bare flag means that none of your actual files are stored in Dropbox, only the repository. The repository can then be used to create all of those files, from any point in the repository's history. When you do `git clone` the contents of `/MyExampleProject.git` are copied to `/MyExampleProject/.git` in your destination folder; the files associated with the branch you're working on will be placed in the `/MyExampleProject` folder.

As you commit and push changes from your desktop, Dropbox will synchronise the repository across all devices, meaning you can then pull those commits into your local repositories.

Clone your Dropbox Repository into your Local Development Folder
=====
*For those used to working directly in Dropbox, this is where you should start to move your development out of Dropbox. Working in the Dropbox folder defies the idea of only sharing what you want between devices. Furthermore, as you begin to work on more complex projects which depend on external libraries, sharing these between devices may not be appropriate. A good alternative is to create a folder on your machine called `Development` and store your projects plus any extras in there.*

You need to now clone your newly created repository. You should receive a warning `You appear to have cloned an empty repository`, this can be ignored.

**Mac/Linux**
{% highlight sh %}
$ cd ~/Development
$ git clone ~/Dropbox/Repositories/MyExampleProject.git
{% endhighlight %}

**Windows**
{% highlight bat %}
cd %HOMEPATH%\Development
git clone %HOMEPATH%\Dropbox\Repositories\MyExampleProject.git
{% endhighlight %}

Once you have cloned the repository you need to get it ready for working. Because we created the repository using `--bare`, it has no branches. By convention, the main branch is `master`, so we will create it and check it out as our main branch.

**All**
{% highlight sh %}
$ cd MyExampleProject
$ git checkout master
{% endhighlight %}

Commit and Push your Work to your Dropbox Repository
=====

Once you've done some work, you need to `git add` it, then `git commit` it. When you're ready to push, you just need to do the following command:

**All**
{% highlight sh %}
$ git push origin master
{% endhighlight %}

In this command `origin` refers to the repository you made in `Dropbox/Repositories`.

*Now you have pushed a branch to your Dropbox repository, you can simply use the command `git push origin` to push all commits. The only time you need to specify the branch name is when you want to push to a single branch, or if that branch doesn't exist on the repository you're pushing to.*

That's about it, any questions/comments feel free to get in touch. If I've made a mistake please point it out for the benefit of fellow readers.

Extras
=====

**I want to Share my Repository on Github**

Create your repository on [Github](https://github.com/repositories/new) and then do as follows:

{% highlight sh %}
cd MyExampleProject
git remote add github git@github.com:YourUsername/YourRepositoryName.git
git push -u github master
{% endhighlight %}

The same branch rules apply as before, if the branch does not yet exist, you must pass the name via `git push`, after that you may drop the branch names to push all branches which exist on all repositories.

[git_1]: /images/git_1.png
[git_2]: /images/git_2.png