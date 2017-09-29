---
title: Currency Conversion – The Simple Way
template: templates/post.pug
date: 2016-05-04
author: Lenin Hasda
keywords: algorithm, currency conversion
---

Currency conversion is must if you are making any e-commerce project or any other project that deals with money and requires you to process multiple currencies. I found this simple and very handy technique to convert one currency to another in stackexchange that I thought I should keep as reference as well as for those in needs.

The first thing you need is select a base currency and the conversion rate of all the currencies based on that base currency. For our example lets have USD as our base currency and followings as the conversion rate:

```
	:USD
USD	:1.0
Euro	:0.78391
GBP	:0.621484
Yen	:107.174
```

Followings are things we need as user input or input for this technique

```
double sourceAmount = ....; // source amount that we want to convert
String sourceCurrency = ...; // currency of the source amount
String targetCurrency = ....; // currency that we want to convert to
```

Now from above input we need to figure out following two things:

```
double sourceToBaseRate = ....; // conversion rate of source to base currency
double targetToBaseRate = ....; // conversion rate of target to base currency
```

We can find these two value from the conversion rate table using user input currencies. And finally the calculation part which is as following

```
double targetAmount = (sourceAmount / sourceToBaseRate) * targetToBaseRate;
```

Full pesudo is:

```
double currencyConversion( double sourceAmount, String sourceCurrency, String targetCurrency )
{
    double sourceToBaseRate = getConversionRate( sourceCurrency )
    double targetToBaseRate = getConversionRate( targetCurrency )
    double targetAmount = (sourceAmount / sourceToBaseRate) * targetToBaseRate;
     
    return targetAmount
}
```

That’s it! Now you can convert one currency to another use this simple algorithm.

**Note:** that you do need to have a way to getConversionRate which could be as simple as using an array or some database table


------


**Ref:**
* http://codereview.stackexchange.com/questions/67272/introductory-currency-converter
