---
title: প্রোগ্রামিং কনসেপ্ট ১০১ - কন্ডিশন
template: templates/post.pug
date: 2017-10-02
author: Lenin Hasda
keywords: programming, basics, concept, programming concepts, conditions, if, if else, প্রোগ্রামিং, প্রোগ্রামিং বেসিক, প্রোগ্রামিং কনসেপ্ট, প্রোগ্রামিং ধারনা, কন্ডিশন
excerpt:
    অপারেটর (Operator), অপারেশন (Operation), অপারেন্ড (Operand) এই কঠিন কঠিন শব্দ গুলো প্রোগ্রামিং এ কিভাবে যায় সেটাই সহজ করে তুলে ধরার চেষ্টা করেছি এই পোস্টে
---

`কন্ডিশন` বা শর্ত প্রোগ্রামের খুবই গুরুত্ব পূর্ণ একটা অংশ, কোন একটা decision নিতে গেলে এটার দরকার পড়ে। ব্রাউজারের কথায় ধরা যাক, যেটাতে এই লেখাটা পড়তেসেন, সেটাতে অনেক গুলা বাটন আছে মেনু আছে, কোনটাতে ক্লিক করলে কি হবে, কিংবা কোন একটা ওয়েব সাইট দেখতে চাইলে আসলে ইন্টারনেট আছে কি না... এইযে ছোট ছোট চেক গুলো করা লাগে, এটাতে কোন না কোন ভাবে কন্ডিশন ব্যাবহার হচ্ছে। 

আর এর মদ্ধেই দেখে আসছি যে আমরা [বার্গার খাবো না, বন্ধুর বাসায় পোলাও খাবো না নিজের বাসায় ডাল ভাত খাবো](/post/programming-concepts-101-data-and-data-types-bn) সেটা নির্ভর করছে আমার পকেটে টাকা আছে কি না, কিংবা বন্ধুর সাথে দেখা হচ্ছে কিনা সেটার উপর। তেমনি আমাদের প্রোগ্রামে হয়তো অনেক গুলো অংশ থাকবে, এবং কোন অংশটা কাজ করবে সেটা নির্ভর করবে ব্যাবহারকারি বা User কি চাচ্ছে তার উপর। কোন একটা বাটনে ক্লিক করে বা লিখে হয়তো User বলবে যে সে কি চাচ্ছে, সেটা চেক করে প্রোগ্রামের এক বা একাধিক অংশ রান করাবো। অথবা এমনও হতে পারে যে প্রোগ্রামের কোন একটা অংশ রান হচ্ছে কি হচ্ছে না সেটার উপর নির্ভর করে আর একটা অংশ রান করবে। 

এই চেক অংশটাকে কন্ডিশন বলতেসি এবং প্রোগ্রামে `if ... else` আর `switch ... case` এই দুটি জিনিস দিয়ে চেকিং এর কাজটা করা হয়। আমরা বার্গার খাওয়ার প্রোগ্রামটা যদি `if ... else` দিয়ে তাহলে জিনিসটা এরকম হবে: 

```
if পকেটে টাকা থাকে
        তাহলে হোটেলে বার্গার খাবো
else if যদি বন্ধুর সাথে দেখা হয়
        তার বাসায় পোলাও খাবো
else
        নিজের বাসায় ডাল ভাত খাবো
```

খুব একটা কঠিন কিছু না, শুধু বাংলাটাকে ইংলিশ করে দিয়েছি :D আমরা বিরিয়ানী নিয়ে আর একটা কন্ডিশন প্রোগ্রাম দেখেছিলাম সেটার ইংলিশ টা হলঃ  

```
if (পকেটের টাকা >= ১০০) && (আজকের দিন == শনিবার)
        তাহলে দোকানে বিরিয়ানী খাবো
```

উপরের দুটি প্রোগ্রাম খেয়াল করলে দেখবো যে `if ... else` আসলে বেশ কয়েক ভাবে লেখা যায়। প্রথম প্রোগ্রামে দুটি কন্ডিশন একটি `if` দিয়ে, পরেরটি `else if` দিয়ে লেখা এবং আমাদের প্রোগ্রামে আরও কন্ডিশন থাকলে সেটা `else if` দিয়ে লিখতে পারবো। সব শেষে কোন কন্ডিশনই যদি না মিলে তাহলে কি হবে সেটা `else` দিয়ে লেখা হয়েছে। দ্বিতীয় প্রোগ্রামে দেখবো যে শুধু একটি `if` দিয়ে দুটি কন্ডিশন চেক করেছি এবং কি কন্ডিশন মিললে কি হবে সেটা বলেছি। `else` এবং `else if` সব সময় দরকার তা কিন্তু না, আমাদের প্রয়োজন হলে দিবো না হলে না। 

আচ্ছা আমদের প্রোগ্রাম যদি এমন হয় যে সপ্তাহের সাতটা দিনে এক এক দিন এক এক বন্ধুর বাসায় হামলা করবো (পোলাও খাইতে আরকি ;) ) তাহলে আমরা সেটা এভাবে লিখতেই পারি: 

```
if আজকে শনিবার 
        তাহলে আজকে ফাহিমের বাসা 
else if আজকে রবিবার 
        তাহলে সাইমনের বাসা 
else if আজকে সোমবার 
        তাহলে রাজুর বাসা 
.
.
.
```

এভাবে সাত দিনের জন্য সাতটা কন্ডিশন হবে। কিন্তু ধরা যাক আমরা পুরো এক মাসের হিসাব রাখতে প্রোগ্রাম করছি আমাদেরকে ৩০টা `else if` দিয়ে প্রোগ্রাম লিখতে হবে!!! আমরা চাইলে এগুলোকে `switch ... case` দিয়ে লিখতে পারি। `switch ... case` হল `if ... else` এর মতই কন্ডিশন লেখার আর একটা উপায় কিন্তু একটু কম লিখতে হয় আরকি। আমরা সাত দিনের জন্য `switch ... case` টা লিখে দেখি তাহলে বুঝতে শুবিধা হবে। 

```
switch আজকের দিন 
        case শনিবার :
                তাহলে আজকে ফাহিমের বাসা 
        case রবিবার :
                তাহলে সাইমনের বাসা 
        case সোমবার:
                তাহলে রাজুর বাসা 
        case মঙ্গলবার:
                তাহলে জুনানের বাসা 
        case বুধবার:
                তাহলে প্রনয়েব বাসা 
        case বৃহস্পতিবার:
                তাহলে তামিমের বাসা 
        case শুক্রবার:
                তাহলে কামরুলের বাসা 
```

`switch ... case` এ যেটাকে চেক করবো সেটা `switch` এর পরে লিখবো, আর যেটার সাথে মিলাবো সেটা হল এক একটা `case`। আমরা চাইলে `if ... else` বা `switch ... case` যেকোনো টা যেকোনো সময় লিখতে পারি, এটার উপর আসলে কোন নিয়ম নেই।

আশা করি কন্ডিশনের ব্যাপারটা এবং কিভাবে প্রোগ্রামে ব্যাবহার করতে পারি সেটা কিছুটা হলেও বুঝতে পারছি। তবে বলে রাখি যে প্রোগ্রামিং ল্যাঙ্গুয়েজে হয়তো একটু অন্য ভাবে লিখতে হতে পারে যেটা ল্যাঙ্গুয়েজটা শেখার সময় অবশ্যই ভাল মত দেখে নিতে হবে। 

#### এবং বোনাস

উপরে অনেক বক বক করসি এখন আমাদের ক্যালকুলেটরে ফেরত আসি। ক্যালকুলেটর প্রোগ্রাম তো আগেই করলাম কিন্তু সমস্যা হল User ২টা সংখ্যা দেয়ার পর তাকে যোগ, বিয়োগ, গুন, ভাগ সব গুলো উত্তর দেখায়!!! এমন হলে কি ভালো হতোনা যে আমরা User কে জিজ্ঞেস করলাম, ভাই তুমি কোনটা করবা যোগ না বিয়োগ না কি ??? তারপর User যেটা চাইবে শুধু সেটা করে দেখাবো। 

আমরা এই মাত্র যে কন্ডিশন দেখলাম সেটা ব্যাবহার করে দেখি কেমন হয়। আমরা শুরুতে User কে লেখা print করে দেখাবো যে আমাদের কাছে কি কি option আছে, তারপর তার কাছে থেকে তার choise টি input হিসেবে নিবো। এই input চেক করে আমরা ঠিক করবো যে user আসলে কি চাচ্ছে। 

```
[1] যোগ
[2] বিয়োগ
[3] গুন
[4] ভাগ
[5] ভাগশেষ

অই ভাই, কোনটা করবেন? 

choise = user choise input

x = users first input data
y = users second input data

if choise = 1 // যোগ
	z = x + y
	print z

else if choise = 2 // বিয়োগ
	z = x - y
	print z

else if  choise = 3 // গুন
	z = x * y
	print z

else if choise = 4 // ভাগ
	z = x / y
	print z

else if choise = 5 // ভাগশেষ
	z = x % y
	print z
```
শেষ! এখনে user কে যোগ, বিয়োগ ... এর পাশে যে 1, 2, 3 ... সংখ্যা গুলো আছে সেটার যে কোন একটি choise হিসেবে দিতে হবে। এখন যদি আমরা এটা রান করি তাহলে user যা চাচ্ছে শুধু সেটাই করে দেখান হবে। 

------

**আগের লেখা:** [প্রোগ্রামিং কনসেপ্ট ১০১ - অপারেটর এবং অপারেশন](/post/programming-concepts-101-operators-and-operatiorns-bn)    
**পরবর্তী লেখা:** [প্রোগ্রামিং কনসেপ্ট ১০১ - লুপ](/post/programming-concepts-101-loop-bn)


