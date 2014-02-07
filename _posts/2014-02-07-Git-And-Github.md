---
layout: post
title: An Introduction to Git and Github
author: jimmy
---

This is some accompanying material I've written for people who attended the Git workshop we held, kindly hosted by the guys at [StudentHack](//studenthack.com), or just those of you who are interested in getting an introduction to Git and Github. I'll keep updating it as we get closer to the event, in-case you need to reference it.

<iframe src="http://prezi.com/embed/tuad5y0fedri/?bgcolor=ffffff&amp;lock_to_path=0&amp;autoplay=0&amp;autohide_ctrls=0&amp;features=undefined&amp;disabled_features=undefined" width="550" height="400" frameBorder="0"></iframe>

Git is a distributed version control system which empowers developers with the ability to switch between, roll back and compare iterations of their work in real-time. If you've done any serious development, you will have encountered a situation where having a tool like Git is extremely useful, for example:

1. You find yourself copying versions of your code to a blank text file, incase what you're doing ends up in an irreparable mess.

2. You don't have the foresight to create a copy of your code somewhere, and you make a mess of your code. You've saved the file multiple times since in order to compile/interpret your code and now Google Drive has synchronised your broken/messy code across all your devices.

3. You've got a shared folder on Dropbox for your group work, you and another student both edit the same file, one of your work is overwritten or written away to some conflicted copy file.

These aren't the only examples, but probably the most common encountered by students and people working on their own projects. Using a Git workflow can solve these problems instantly and with incredible ease; you just have to learn how to use it and stick to it. Admittedly, it's quite a difficult concept to get your head around, but once you know it, you won't soon forget it.

Bare Basics
===

Git is a complicated beast to tackle all at once. A *commit* is an individual piece of work. A good analogy for this is that commiting to Git is like saving your progress in a video game. You could load your game and be back where you saved (committed), even changing direction and going somewhere else. A *repository* is, in layman's terms, a bunch of commits in sequence. Your current position in this repository (because you can move around on a whim) is called your `HEAD`.

Your First Repository
===

 Creating your first repository begins and ends, quite simply, with `git init`; which will turn your **current directory** into a Git repository. This can be applied to both an existing project or to an empty folder. After that, it becomes a matter of committing any work you've done using `git commit -am "A brief description"`, where `A brief description` is a summary of the changes made to a commit.

**Converting existing projects to a Git repository**

{% highlight sh %}
$ git init
$ git add -A
$ git commit -m "Initial commit"
{% endhighlight %}

Branches
===

In Git, a branch is simply a reference to a commit, not dissimilar from a bookmark in a book. The parallels between books and a git repository are numerous, a book can have any number of bookmarks, they could all be on the same page or on different pages, and they let you switch between different locations in the book at any time.

Branches allow you to keep track of and switch between different developments, for whatever reason. If you're working on a feature and decide you need to go work on something else, if you've been committing on a branch, you can just switch back to master and create a new branch. This allows you to keep master in a state of always working, which is useful at a hackathon as you near the final hours and need to sort out your presentations.

**Create a branch and switch to it**

{% highlight sh %}
$ git checkout -b <BranchName>
{% endhighlight %}

**Switch to an existing branch**

{% highlight sh %}
$ git checkout <BranchName>
{% endhighlight %}

**Merge another branch into the one you're on**

{% highlight sh %}
$ git merge <BranchName>
{% endhighlight %}

Needing to Start Again
===

![We've all been there.][kill_it]

Picture this. You've started work on a fantastic new feature, but there's 30 minutes left and your team needs you to finish one of the key features of your product. You are now stuck: if you leave your code in place it will break the system; you don't know if you can finish both features. This is when you shout out "Why did we do something this ambitious?!"

The solution isn't to be less ambitious but to be smarter about how you work. With Git (and maybe investing time looking at some frameworks) this scenario could be avoided. If you're working on your own, you can roll back commits to a working state with no problem.

**Rollback all work to the last commit**

{% highlight sh %}
$ git reset --hard HEAD
{% endhighlight %}

**Rollback a single file the last commit**

{% highlight sh %}
$ git checkout HEAD <FileName>
{% endhighlight %}

*Note: You can change HEAD to any commit in your tree, which are identified by an MD5 hash. Even easier, you can go back **n** commits by changing the location to HEAD~**n**.*

If you're working as a team, you can do the same, although a smarter thing to do would be to do your features on branches. In the above scenario, if your feature was on a branch, you'd have been able to switch to the branch with the feature and then merge it into `master`. When you're done, if you have time, you can finish your feature on its own branch.

Handling Conflicts
===

As those who attended the workshop know, conflicts can still happen despite Git's incredible merge management. You'll know you hit a conflict when you've gone to merge a branch or pull from a remote repository (like on Github) see a message like this:

{% highlight sh %}
Automatic merge failed; fix conflicts and then commit the result.
{% endhighlight %}

Then, in one or more of your files, you get something which looks like this:

{% highlight java %}
public static void main(String[] args)
{
<<<<<<< HEAD
System.out.println("Hello, World!");
=======
System.out.println("I'm afraid I can't let you do that, Dave.");
>>>>>>> ab25hd
}
{% endhighlight %}

The first thing to mention is that this isn't as bad as it looks. Git is not infalliable, and can sometimes get confused. Rather than toy around trying to guess what you want it is merely *asking* what you want. If we remove the context, this is what it looks like:

{% highlight diff %}
<<<<<<< 
What your repository looks like.
=======
What the branch/remote looks like.
>>>>>>> 
{% endhighlight %}

To solve this problem, simply edit the file. Remove the `<<<<<<<`, `=======`, `>>>>>>>` and get the code within those symbols looking how you expect. Whether this be by replacing one section with another, merging them together or writing something else entirely. Once you've done this, your team will not receive this conflict unless they continue to edit the affected area whilst you were fixing it. Once you've fixed up the code, push it.

To avoid conflicts, try to commit, pull and push often.

Using Github
===

*Coming soon...*

[kill_it]: /images/killitwithfire.jpg