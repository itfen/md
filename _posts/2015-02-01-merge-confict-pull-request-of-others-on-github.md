---
layout: post
title:  "合并 GitHub 上他人提交的冲突代码"
categories:
comments: true
share: true
---

GitHub 上他人的 Repository 里有人创建了一个 Pull Request，但是后来又有人更改了这个 Pull Request 里的文件，造成此
Pull Request 无法自动 Merge，这时候就可以先用编辑器把 Conflict 先修复，然后使用 git 命令行手动创建一个新的
Pull Request，就可以把文件的更改同步到最新的版本。

未完，等待填坑

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
