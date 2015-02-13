---
layout: post
title:  "合并 GitHub 上他人提交的冲突代码"
categories:
comments: true
share: true
---

{% highlight bash%}
git status
git remote -v
git remote add mine git@github.com:mdluo/rails.git
git rebase master
git rebase --abort
git merge master
atom activerecord/CHANGELOG.md
git status
git add activerecord/CHANGELOG.md
git branch
git commit
git pull
git push
{% endhighlight %}
