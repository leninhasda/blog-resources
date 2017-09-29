---
title: কিভাবে গিটহাব প্রজেক্টে কন্ট্রিবিউট করবেন
template: templates/post.pug
date: 2016-11-07
author: Lenin Hasda
keywords: git, contribution, how to, গিট, কন্ট্রিবিউশন, গিটহাব 
---

> লেখাটি আমার নিজের [একটি গিটহাব প্রোজেক্টের](https://github.com/leninhasda/bitbook-raw-php) জন্য লেখা হলেও অন্যান্য সব ওপেনসোর্স প্রজেক্ট গুলোতেও প্রায় একই ধরনের নিয়ম ব্যাবহার হয়ে থাকে।
[যেসব কমন গিট কমান্ড এখানে ব্যাবহার করা হয়েছে সেগুলোর লিস্ট এখান থেকে পাওয়া যাবে।](http://blog.leninhasda.me/post/common-git-commands)

> [গিট ওয়ার্ক-ফ্লো নিয়ে হাসিন ভাইয়ের চমৎকার একটি লেখা পাবেন এখানে।](https://hasin.me/2014/05/13/git-workflow-in-bangla/)


##### Setp #1 : Fork the repo to your account.

কোন ওপেনসোর্স প্রোজেক্টে কন্ট্রিবিউট করতে হলে প্রথমে প্রোজেক্টি ফোর্ক করে নিজের অ্যাকাউন্ট এ নিতে হবে। এজন্য প্রোজেক্টের লিঙ্কে গিয়ে `Fork` বাটনে ক্লিক করতে হবে।

##### Setp #2 : git clone from your fork

এরপর ফোর্ক করা প্রজেক্টি ক্লোন করে লোকাল মেশিনে নামিয়ে নিতে `Clone or download` বাটনে ক্লিক করে লিঙ্কটি কপি করে নিতে হবে এবং টারমিনালে নিচের কমান্ডটি দিতে হবে :

```bash
cd /to/your/www/
git clone https://github.com/leninhasda/bitbook-raw-php.git
```

##### Step #3 : Add the original repo as upstream

ফোর্ক থেকে লোকাল মেশিনে প্রোজেক্টি ক্লোন হলো কিন্তু একই সাথে অরিজিনাল প্রোজেক্টকেও `upstream` হিসেবে যোগ করে নিতে হবে যাতে করে লেটেস্ট কোড আমরা নামিয়ে নিতে পারি। এজন্য অরিজিনাল রিপোতে গিয়ে `Clone or download` বাটনে ক্লিক করে লিঙ্কটি কপি করে নিতে হবে এবং টারমিনালে নিচের কমান্ডটি দিতে হবে :

```bash
git remote add upstream https://github.com/leninhasda/bitbook-raw-php.git
# if you use ssh, git@github.com:leninhasda/bitbook-raw-php.git
```

##### Step #4 : Recommended: Create a local dev branch (ex: dev-lenin) and work in that branch

ডেভ ব্রাঞ্চে কাজ করার সুবিধা হল কোন সমস্যা হলে ব্রাঞ্চটাকে ডিলিট করে আমরা সহজেই আগের অবস্থায় ফেরত যেতে পারি । (ডেভ ব্রাঞ্চের নাম যা খুশি হতে পারে, আমার বুঝার সুবিদার্থে আমি সামনে `dev-` ব্যাবহার করি )

```bash
git checkout -b dev-lenin
```

##### Step #5 : Before pushing your changes, checkout master branch and pull the latest changes from upstream

আমাদের করা পরিবর্তন গুলো রিপোতে দেয়ার আগে সবসময় অরিজিনাল রিপো `(upstream)` থেকে একবার পুল করে নিতে হবে। এতে করে নতুন কোন কোড পরিবর্তন হলে আমাদের ব্রাঞ্চেও সেটা থাকবে।

```bash
git checkout master
git pull upstream master
```

###### Step #6 : Go back to your local dev branch (ex: dev-lenin) and rebase from master. Resolve any conflicts that may happen in this step.

অরিজিনাল রিপো থেকে যে পরিবর্তন গুলো নামালাম সেগুলো আমাদের ডেভ ব্রাঞ্চে নিতে হবে। এ অবস্থায় কোন কোড কনফ্লিক্ট হলে সেগুলো ফিক্স করতে হবে এবং কমিট করতে হবে।

```bash
git checkout dev-lenin
git rebase master
# resolve conflicts, if any, and commit before pushing it to github
```

###### Step #7 : Push your changes on a new branch into your fork

কাজ শেষ হলে কোড গুলোকে আমাদের ফোর্ক করা রিপোতে পুশ করতে হবে। আমরা চাইলে পুশ করার সময় ব্রাঞ্চের নাম বদল করে দিতে যেন বুঝতে সুবিধা হয় যে এই ব্রাঞ্চে কি নিয়ে কাজ করা হয়েছে।

```bash
git push origin dev-lenin:new-branch-name
# OR 
# git push origin dev-lenin
```

##### Step #8 : Finally go to your or original repo and make a pull request if everything is ok.

এখন সবকিছু ঠিক থাকলে আমরা অরিজিনাল রিপোতে পুল রিকুয়েস্ট পাঠিয়ে দিবো।

