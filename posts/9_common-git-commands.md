---
title: কমন কিছু গিট কমান্ড
template: templates/post.pug
date: 2016-10-31
author: Lenin Hasda
keywords: git, basic git, git commands, গিট, গিট কমান্ড, বেসিক কমান্ড
---

> প্রথমেই বলে নেই নিচের প্রায় সব কমান্ডেরই বেশ কয়েক রকমের ভেরিয়েশন আছে। আমি নিজে যেগুলার ব্যাবহার বেশি করি সেগুলোই শুধু এখানে দিচ্ছি। যেকোনো কমান্ড কপি করে গুগল এ খুঁজলেই আরও অনেক ডিটেইল পাওয়া যাবে।

**git status**    
কমান্ডটির মাধামে গিট প্রোজেক্টের স্ট্যাটাস চেক করা হয়। কমান্ডটি নতুন, পরিবর্তিত বা ডিলিট করা ফাইলের লিস্ট দেখায়।


------


**git add .**     
নতুন পরিবর্তন গুলো কমিটের জন্য রেডি করে এই কমান্ড। এখানে . মানে হল পরিবর্তিত সব ফাইলকে কমিটের জন্য রেডি করবে। সব ফাইলকে একসাথে অ্যাড না করে আলাদা করেও অ্যাড করা যায় নিচের কমান্ড দিয়ে:

```
git add file.php
```


------


**git commit -m <commit_message>**      
কমিটের জন্য রেডি করা পরিবর্তন গুলোকে কমিট বা রেকর্ড করে। <commit_message> টি অবশ্যই একটি স্ট্রিং হতে হবে এবং তা সিঙ্গেল বা মাল্টি লাইনে হতে পারে।


------


**git pull <remote> <branch_name>**    
এই কমান্ডটি দিয়ে রিমোট সার্ভারের পরিবর্তন গুলোকে পুল করে বর্তমান ব্রাঞ্চের সাথে মার্জ করা হয়। এখানে origin  বা upstream হল রিমোট সার্ভার এবং master হল ব্রাঞ্চের নাম।

```
# example
git pull origin master
git pull upstream master
```


------


**git push <remote> <branch_name>**    
কমান্ডটির মাধামে লোকাল মেশিনের কোন ব্রাঞ্চকে রিমোট সার্ভারে আপ করা হয়। এখানে origin হল রিমোট সার্ভার এবং fix-bug-x হল লোকাল ব্রাঞ্চের নাম। উল্লেখ্য যে সার্ভারেও fix-bug-x তৈরি হবে এবং পরিবর্তন গুলো সেখানে আপ হবে।

```
#example
git push origin fix-bug-x
```


------


**git branch**      
লোকাল মেশিনের সবগুলো ব্রাঞ্চকে লিস্ট করবে।


------


**git checkout <branch_name>**    
এই কমান্ড দিয়ে বর্তমান একটিভ ব্রাঞ্চ বদলানো হয়।

```
        F (fix-A) <- current head
       /
A--B--C--D (master)
    \
     X--Y (ft-B)
```

*git checkout fix-A কমান্ডটি fix-A ব্রাঞ্চকে একটিভ করবে*


------


**git checkout -b <branch_name>**    
এই কমান্ডটি বর্তমান ব্রাঞ্চ থেকে branch_name নামে নতুন একটি ব্রাঞ্চ বানাবে এবং সেটিকে একটিভ করবে।

```
           N (fix-C) <- current head
          /
A--B--C--D (master)
```

*git checkout -b fix-C কমান্ডটি fix-C নামে নতুন ব্রাঞ্চ বানাবে এবং ব্রাঞ্চকে একটিভ করবে*


------


**git rebase <branch_name>**      
কমান্ডটি দিয়ে বর্তমান ব্রাঞ্চের শুরুর হেডকে branch_name এ বসানো হয় ।

```
        F (fix-A)
       /
A--B--C--D (master)
         \
          X--Y (ft-B) <- current head
```

*git rebase master কমান্ডটি ft-B ব্রাঞ্চের হেডকে master ব্রাঞ্চের পুরাতন কমিট B থেকে বর্তমান কমিট D তে বসাবে।*


------


**git merge <branch_name>**    
বর্তমান ব্রাঞ্চের সাথে branch_name কে মার্জ করে।

```
        F (fix-A) 
       /
A--B--C--D--M (master) <- current head
   \       /
    X--Y--Z (ft-B)
```

*git merge ft-B কমান্ডটি ft-B ব্রাঞ্চকে বর্তমান ব্রাঞ্চের শেষ কমিটের (master এর D) সাথে মার্জ করবে এবং নতুন একটি মার্জ কমিট M বানাবে।*


------


**git diff**    
কমান্ডটি দিয়ে পরিবর্তিত ফাইলের পরিবর্তন গুলো দেখায়।


------


**git log**      
কমিটের লগ মেসেগ গুলো লিস্ট করে।


------


**git stash**      
কমান্ডটি বর্তমান পরিবর্তন গুলোকে টেম্পোরারি সেভ করে ইমিডিয়েট আগার কমিটে রিসেট করে।


------


**git stash apply**      
টেম্পোরারি সেভ করা পরিবর্তন গুলোকে আবার প্রয়োগ করবে।


------


**git reset –hard**      
বর্তমান পরিবর্তন গুলোকে ইগনোর করে ইমিডিয়েট আগার কমিটে রিসেট করে।

