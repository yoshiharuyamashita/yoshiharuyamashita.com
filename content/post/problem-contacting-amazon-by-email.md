+++
date = "2016-04-23T21:31:52+01:00"
description = "WE'RE SORRY. THERE WAS AN ERROR TRYING TO SEND YOUR E-MAIL. PLEASE TRY AGAIN IN A FEW MINUTES OR CONTACT US BY PHONE. Says Amazon"
draft = false
tags = ["input validation"]
title = "Problem Contacting Amazon by Email"
topics = ["Rant"]

+++

Over the last few days, I spent some time trying to find out how to read Japanese Kindle books on my UK iPad.

<!--more-->

In the end, I could not find the information I was looking for so I contacted Amazon.co.uk from the following URL:

- [amazon.co.uk](https://www.amazon.co.uk/gp/help/contact-us/general-questions.html?skip=true#a)

I filled in the form provided and hit "Send E-mail", to which it responded:

> **WE'RE SORRY. THERE WAS AN ERROR TRYING TO SEND YOUR E-MAIL. PLEASE TRY AGAIN IN A FEW MINUTES OR CONTACT US BY PHONE.**

You can see the message in the following screenshot:

{{% fluid_img class="pure-u-1-1" src="/img/post/contacting-amazon-by-email.png" alt="Contacting Amazon by Email" %}}

It did not take long until I realised that I **also had to fill in the "From" field**, which is not marked as required. The message does not help the user (well, apart from the "OR CONTACT US BY PHONE" bit perhaps).

If I submit without providing "Your e-mail address", the page displays:

> **Please enter your e-mail address.**

Without "Enter additional information", it complains:

> **Please enter comments.**

Both messages tell the user what to do.

### How About Amazon.com and Amazon.co.jp?

Being a software engineer, I could not help but digging this issue a bit deeper.

So I tried the same steps on these Amazon sites:

- [amazon.com](https://www.amazon.com/gp/help/contact-us/general-questions.html?skip=true#a)

> **WE'RE SORRY. THERE WAS AN ERROR TRYING TO SEND YOUR E-MAIL. PLEASE TRY AGAIN IN A FEW MINUTES OR CONTACT US BY PHONE.** (same as amazon.co.uk)

- [amazon.co.jp](https://www.amazon.co.jp/gp/help/customer/contact-us?skip=true#a)

> **申し訳ありません。Eメールの送信中にエラーが発生しました。数分後にもう一度送信していただくか、電話でお問い合わせください。**, which is a Japanese translation of the above.

These results are not so interesting but at least consistent among the three sites.

### End of Rant

It is a minor issue but I was not expecting this kind of validation error from the e-commerce giant.