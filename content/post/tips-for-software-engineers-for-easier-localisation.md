+++
date = "2016-02-27T15:49:25Z"
description = ""
draft = false
tags = ["l18n", "software localisation tips"]
title = "Tips for Software Engineers for Easier Localisation"
topics = ["Software Localisation"]

+++

Here is a list of tips I recently came up with while carrying out an English to Japanese software localisation task. To put it simply the tips are things I wished the software engineers had considered in order to make the translator's job easier.

<!--more-->

## 1. Agree a message format, including tenses and punctuations

```cpp
"X found: %1%. X required: %2%."
"Actual X: %1%. Required X: %2%."
"X should have been %1% but found %2%"
"X is %1% (it must be %2%)"
```

These varying message formats are more or less conveying the same meaning to the user. It would be better to agree on a format within the development team and use it for the same type of messages. This would help to make the software look more consistent to the user. The number of strings to be sent to the translator would also be reduced.  It is not always possible or practical to make these kind of changes at later development stages so this is best done early.

## 2. Provide context information where it would be helpful to the translator

```cpp
"Found %1% references."
```

Without knowing the type of information the format specifier carries, for example, whether it is a number, it is possible to translate the sentence incorrectly. At least this is the case with Japanese localisation.

## 3. Include verbs

```cpp
"No %1%"
"Up to %1% files"
```

What could possibly have happened to that `%1%`? Maybe it has been found or perhaps deleted?

A poor translator with no access to the source code would have no choice but to guess or else come back to you for clarification.

## 4. Make entire sentences translatable using format string

Before you send strings to the translator, you will have to prepare them for localisation. For example using [boost::locale::translate()](http://www.boost.org/doc/libs/1_56_0/libs/locale/doc/html/messages_formatting.html). 

To make this process as efficient as possible, it is best to aim for as little string concatenation as possible when coding. Even if you make each segment of the message translatable, it will be very difficult to translate it correctly due to lack of context. This problem can be addressed by making entire sentences translatable using format strings instead.

## 5. Hide unnecessary details from the translator

```cpp
" This is an example."
"This is another example.\n"
"Yet another example: %1$d%2% %3$.f%4%."
```

In the first and second examples, it is all to easy to delete the space at the beginning or forget to add the last new line character. In the final example, the series of format specifiers does not need translating so why show it making the whole sentence look unnecessary complicated? More importantly if it were modified in error, your software would probably throw a bad format specifier exception. The bit after the colon can be built into a string prior to the message. That way the sentence simply becomes "Yet another example: %s%.", which is much preferable for the translator.  Hiding unnecessary details will make it less likely for translators to accidentally modify them.

## 6. Include the order in format specifiers

```cpp
"page %d of %d" // error-prone
"page %1$d of %2$d" // good
```

There is no guarantee that the order of all format specifiers will be the same in another language. Correct translation becomes impossible if all format specifiers do not carry the order information with them. Even if the string contains only one format specifier it is better to include the order in case someone adds more at a later date.

## Conclusion

Software localisation can be time-consuming and costly. It is also an on-going process. As long as changes are being made to the software, further localisation is required. 

Making it possible for translators to translate strings easily and correctly is beneficial not only for translators but for development teams. The speedy delivery of correctly translated files is vital to the software development process.

