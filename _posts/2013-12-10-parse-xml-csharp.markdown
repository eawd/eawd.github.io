---
layout: post
title:  "[ar] Parsing an XML file using C#"
language: arabic
date: 2013-12-10 21:06:26 +0800
categories: arabic csharp xml
url: "http://awdallah.tumblr.com/post/69610334093/parsing-an-xml-file-in-c"
---

*ممكن تشوف البوست على [تمبلر](http://awdallah.tumblr.com/post/69610334093/parsing-an-xml-file-in-c) أو [هنا]({{ site.baseurl }}{% post_url 2013-12-10-parse-xml-csharp %})*


أول مرّة أكتب على تيمبلر , هكتب عن البرمجة .. عجب :D

كُنت عملت أبليكيشن[ للقُرآن على ويندوز فون](https://www.microsoft.com/en-eg/store/p/%d8%a7%d9%84%d9%82%d8%b1%d8%a2%d9%86-%d8%a7%d9%84%d9%83%d8%b1%d9%8a%d9%85/9nblggh08sh5?rtc=1) وفي أكتر من حد سألني إزّاي عملته , فأنا هكتب عن الحاجات اللي إتسأل عنها , مش هدخُل في تفاصيل كتير عشان صعب بسبب ظروف الإمتحانات..

الأوّل ملف القُرآن كان عبارة عن فايل إكس إم إل جايبه من موقع إسمه تنزيل [[لينك]](http://tanzil.net/download/) لأنّي حسّيت إنّه موثوق لعدد البرامج اللي مستخدماه ..
<!--description-->
تاني حاجة إستخدمتها كانت لايبراري إسمها [System.Xml.Linq](https://msdn.microsoft.com/en-us/library/system.xml.linq(v=vs.110).aspx) موجودة مع الدوت نت , فلو بتستخدم سي شارب مع دوت نت يبقى هي أكيد موجودة سواء ويندوز فون , 8 أو ديسك توب .. 

طريقة إستخدامها :

- الأوّل بنعمل لود للدوكيومنت بتاعت الإكس إم إل ..

```csharp
Document.Load(@“X:\Path\to\file.xml”)
```

- وبنحطّها في فاريابُل من نوع XDocument ..
مثلًأ:

```csharp
XDocument doc = XDocument.Load(@“C:\quran.xml”);
```

- بعد كدة بنعرّف فاريابل من نوع IEnumerable<XElement> بنحُط فيه كُل النودز اللي هنستخدمها , فمثلًا أنا محتاج السور والنود اللي بيكون فيها السور إسمها sura هكتب:

```csharp
IEnumerable<XElement> sowar = doc.Elements().Elements(“sura”);
```

- مُمكن تكمّل بعد النود دي وتكويري نود تاني بإنّك تكول الميثود `.Elements("nodeName”)` تاني
أو تجيب أتريبيوت مُعينة عن طريق الميثود `”.Attribute(“attributeText”);`
وطبعًا تقدر تـ iterate على كُل النودز زي أي حاجة تانية ..

الكود في النهاية المفروض يبقى حاجة زي كدة :

```csharp
    XDocument doc = XDocument.Load(@“C:\quran.xml”);
    IEnumerable<XElement> sowar = doc.Elements().Elements(“sura”);
    String s = “السور الموجودة في القُرآن هي :\n”;
    foreach (var sura in sowar)
    {
        s += (String)sura.Attribute(“name”) + “\n”;
    }
```

وكأي مُهاجر غير شرعي لتمبلر معتقدش إنّي هتابع أو هكمّل كتير .. فلو مردّتش على حد محدّش يزعل ..