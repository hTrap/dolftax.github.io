---
layout: post
category : General
title : "Merging git histories"
tagline: ""
tags : [Git]
---

Consider a case like you started a project with a git repository and after sometime you moved it to another repository. And now, you want to merge them into one. Because, history is important! Assume, x-repo is the base repo and y-repo is the one you want to merge.

- First , add the y-repo as a remote:

{% highlight css c%}
cd x-repo/
git remote add y-repo uname@servname:dannyboy
{% endhighlight %}

- Download all the y-repo's commits:

{% highlight css %}
git fetch y-repo
{% endhighlight %}

- Create a new local branch from the y-repo's branch:

{% highlight css %}
git branch y-repo-branch y-repo/master
{% endhighlight %}

- Move all of its files into a subdirectory:

{% highlight css %}
git checkout y-repo-branch
mkdir sub-dir/
git ls-tree -z --name-only HEAD | xargs -0 -I {} git mv {} sub-dir/
git commit -m "Files moved to directory sub-dir"
{% endhighlight %}

- Merge the y-repo-branch into the x-repo's master branch:

{% highlight css %}
git checkout master
git merge y-repo-branch
{% endhighlight %}

Done!
