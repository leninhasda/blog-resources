---
title: প্রোগ্রামিং কনসেপ্ট ১০১ - অপারেটর এবং অপারেশন
template: templates/post.pug
date: 2017-09-29
author: Lenin Hasda
keywords: programming, basics, concept, programming concepts, operators, operations, operand, প্রোগ্রামিং, প্রোগ্রামিং বেসিক, প্রোগ্রামিং কনসেপ্ট, প্রোগ্রামিং ধারনা, অপারেটর, অপারেশন, অপারেন্ড
excerpt:
    অপারেটর (Operator), অপারেশন (Operation), অপারেন্ড (Operand) এই কঠিন কঠিন শব্দ গুলো প্রোগ্রামিং এ কিভাবে যায় সেটাই সহজ করে তুলে ধরার চেষ্টা করেছি এই পোস্টে
---

Variable লেখাতে আমরা ছোট্ট একটা অপারেশন (Operation) দেখেছিলাম সেটা হচ্ছে যোগ অপারেশন। ঐ x যে আর y এর মান যে যোগ করতেসিলাম, সেখানে যোগ করাটা ছিল অপারেশন আর `+` ছিল অপারেটর (Operator)। আমরা x আর y কে অপারেন্ড (Operand) বলে থাকি, অর্থাৎ যাদের মদ্ধে Operation টা করা হয়।

প্রোগ্রামে আমাদের সব সময় কোন না কোন Operation করতে হবে, সেটা যোগ বিয়োগ হতে পারে, একটা ফাইল ওপেন করে লেখা এডিট করা হতে পারে, কিংবা ডেটাবেসের সাথে কানেক্ট করে সেটার উপর কাজ করার হতে পারে। পরের গুলো আসলে একটা অপারেশন না, বেশ কয়েকটা অপারেশনের সমষ্টি। আমরা আজকে বেসিক গুলো একটু দেখবো। বেসিক অপারেটরের মদ্ধে আছে:

- আরিথম্যাটিক অপারেটর
- অ্যাসাইনমেন্ট অপারেটর
- কম্পারিজন অপারেটর
- লজিক্যাল  অপারেটর

**আরিথম্যাটিক অপারেটর** মোটামুটি আমরা জানি, `+` বা যোগ, `-` বা বিয়োগ, `*` বা গুন, `/` বা ভাগ। আর একটা আছে সেটা হচ্ছে ভাগ শেষ বের করা, সেটাকে বলা হয় মডুলাস অপারেটর এবং বুঝানো হয় `%` সাইন দিয়ে। আরিথম্যাটিক অপারেটর Number ডেটা টাইপের উপর কাজ করে থাকে।

**অ্যাসাইনমেন্ট অপারেটর** আমরা ইতিমদ্ধে দেখেছি। সেটা হচ্ছে `=`, এটার কাজও মোটামুটি আন্দাজ করা যায়, ডান পাশের মান বা Value কে বাম পাশের Variable এ রাখা। যেমন: `x = 10`, মানে `x` এর মান হিসেবে `10` রাখি। এই সমান `=` ছাড়াও আরও কিছু অ্যাাসাইমেন্ট অপারেটর হতে পারে, যেমন: `+=` উদাহরণ হতে পারে: `x += 10`। এটা আসলে `x = x + 10` কে ছোট করে লেখা, যার অর্থ x এর মানের সাথে 10 যোগ করে ফলাফল x এর মদ্ধে রাখো। একি ভাবে আছে `-=` , `*=` , `/=` , `%=` ।

**কম্পারিজন অপারেটর** ২ট Value বা Variable এর মদ্ধে তুলনা করে, যেমন: `10 > 11`। তুলনা টা আসলে একটা ছোট প্রশ্ন যেটার উত্তর হয় True বা False হবে এবং আমরা চাইলে এই উত্তরটাকে Boolean টাইপ Variable এ রাখতে পারবো। `10 > 11` এর জন্য উত্তরটা False হবে কারণ 10, 11 থেকে বড় না। কম্পারিজন অপারেটর গুলো হল:

- **`==`** :  দুই পাশের Operand দুইটি সমান হলে উত্তর True হয়
- **`!=`** : দুই পাশের Operand দুইটি সমান না হলে উত্তর True হয়
- **`<`** : বাম পাশের Operand টি ডান পাশের থেকে ছোট হলে উত্তর True হয়
- **`>`** : বাম পাশের Operand টি ডান পাশের থেকে বড় হলে উত্তর True হয়
- **`<=`** : বাম পাশের Operand টি ডান পাশের থেকে ছোট বা সমান হলে উত্তর True হয়
- **`>=`** : বাম পাশের Operand টি ডান পাশের থেকে বড় বা সমান হলে উত্তর True হয়

**লজিক্যাল অপারেটর** সাধারণত কম্পারিজন অপারেটরের সাথে মিলিয়ে ব্যাবহার হয়ে থাকে, তবে অন্য ভাবেও ব্যাবহার হতে পারে। লজিক্যাল অপারেটর গুলো হল:

- **`&&`** বা and
- **`||`** বা or
- **`!`** বা not

অনেক ল্যাঙ্গুয়েজ যেমন পাইথনে সরাসরি and, or, not লেখাকেই ব্যাবহার করা হয়। কিভাবে ব্যাবহার হতে পারে?

```
যদি (পকেটের টাকা >= ১০০) && (আজকের দিন == শনিবার)
    তাহলে দোকানে বিরিয়ানী খাবো
```
উপরে যেটা বলা হয়সে সেটা হল, যদি পকেটে ১০০ টাকার সমান বা বেশি থাকে এবং আজকে শনিবার হয় তাহলে বিরিয়ানী খাওয়া হবে মামা!!! ছুটির দিন বলে কথা :D

#### বোনাস

Variable লেখাতে আমরা ক্যালকুলেটরের যোগ Operation টি করসিলাম আর এখন বাকি অপারেটর গুলোও শিখে ফেলসি। আমারদের ক্যালকুলেটরের বাকি Operation গুলোও লিখে ফেলি:

```
x = users first input data
y = users second input data

// যোগ
z = x + y
print z

// বিয়োগ
z = x - y
print z

// গুন
z = x * y
print z

// ভাগ
z = x / y
print z

// ভাগশেষ
z = x % y
print z
```
জোস!!! আমাদের ক্যালকুলেটর এখন যোগ, বিয়োগ, গুন, ভাগ এমনকি ভাগশেষও বের করতে পারে :D

------

**আগের লেখা:** [প্রোগ্রামিং কনসেপ্ট ১০১ - ভ্যারিয়েবল](/post/programming-concepts-101-variable-bn)    
**পরবর্তী লেখা:** [প্রোগ্রামিং কনসেপ্ট ১০১ - কন্ডিশন](/post/programming-concepts-101-condition-bn)


