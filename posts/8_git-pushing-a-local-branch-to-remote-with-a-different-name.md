---
title: Git pushing a local branch to remote with a different name
template: templates/post.pug
date: 2016-10-19
author: Lenin Hasda
keywords: git, git branch, push branch, new remote branch name
---

Most of the time when I push local git changes to remote I do something like `git push origin master` or `git push origin branch-name`. But there are times when you might need to push local branch to remote but with a different name. Well you can do that with following line:

```
git push origin local-branch-name:remote-branch-name
```

