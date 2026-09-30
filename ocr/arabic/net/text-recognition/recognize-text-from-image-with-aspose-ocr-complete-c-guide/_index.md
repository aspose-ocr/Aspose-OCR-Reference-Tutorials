---
category: general
date: 2026-02-09
description: تعلم كيفية التعرف على النص من الصورة واستخراج النص العادي باستخدام قاموس
  مخصص في C#. يتضمن كودًا خطوة بخطوة ونصائح.
draft: false
keywords:
- recognize text from image
- extract plain text
- read dictionary file
- how to extract text
- how to add custom dictionary
language: ar
og_description: التعرف على النص من الصورة في C# باستخدام Aspose OCR. اتبع هذا الدليل
  لاستخراج النص العادي وإضافة قاموس مخصص لتحسين الدقة.
og_title: التعرف على النص من الصورة – دليل C# الكامل
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل C# الكامل

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكن النتائج كانت تفتقد الكلمات الخاصة بمجالك؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، قراءة البطاقات، أو مجرد استخراج العناوين من لقطات الشاشة—محرك OCR الافتراضي لا يكون ذكياً بما يكفي حول مفرداتك.  

الخبر السار؟ بتحميل **custom dictionary** يمكنك تحسين الدقة بشكل كبير، وبالطبع **extract plain text** في خطوة واحدة نظيفة. في هذا الدرس سنستعرض العملية بالكامل، من قراءة ملف القاموس إلى طباعة نتيجة OCR، باستخدام Aspose.OCR في C#.  

سنجيب أيضاً على سؤال “**how to add custom dictionary**” المتكرر، ونظهر لك **how to extract text** بكفاءة، ونشير إلى الأخطاء الشائعة حتى لا تضيع ساعة أخرى في تعديل الإعدادات.

## ما ستحتاجه

- **.NET 6+** (أي بيئة تشغيل حديثة تعمل)
- حزمة NuGet **Aspose.OCR for .NET**  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **ملف نصي** (`custom_dictionary.txt`) يحتوي على كلمة واحدة في كل سطر – هذه هي المصطلحات التي تتوقع رؤيتها.
- **صورة** (`input_image.png`) تحتوي على النص الذي تريد التعرف عليه.

لا توجد مكتبات إضافية، ولا خدمات خارجية. مجرد C# صافية وAspose.

## الخطوة 1: تهيئة محرك OCR – التعرف على النص من الصورة

أول ما تفعله هو إنشاء كائن `OcrEngine`. هذا الكائن يحمل جميع خيارات التكوين، بما في ذلك القاموس المخصص الذي سنضيفه لاحقاً.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class CustomDictionaryDemo
{
    static void Main()
    {
        // Initialise the OCR engine – this is where recognition starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:**  
> بدون وجود مثال للمحرك لا يوجد سياق للإعدادات مثل اللغة، DPI، أو قوائم الكلمات المخصصة. فكر في `OcrEngine` كالعقل الذي سيتعرف لاحقاً على **التعرف على النص من الصورة**.

## الخطوة 2: قراءة ملف القاموس – How to Add Custom Dictionary

بعد ذلك، نحتاج إلى **read dictionary file** محتويات إلى `HashSet<string>`. مجموعة التجزئة توفر بحث O(1)، وهو مثالي لفحوصات المحرك الداخلية.

```csharp
        // Load a custom dictionary from a plain‑text file
        // Each line in the file should contain a single word
        HashSet<string> customDictionary = new HashSet<string>(
            File.ReadAllLines(@"YOUR_DIRECTORY/custom_dictionary.txt"));
        
        // Attach the dictionary to the OCR configuration
        ocrEngine.Configuration.CustomDictionary = customDictionary;
```

> **نصيحة محترف:**  
> احرص على أن يكون ملف القاموس مشفرًا بـ UTF‑8 وتجنب السطور الفارغة؛ سيتم التعامل معها كسلاسل فارغة وقد تربك المحرك.

## الخطوة 3: تحميل الصورة – How to Extract Text

الآن نقوم بتمرير الصورة التي نريد معالجتها. تستخدم Aspose `ImageStream` لتجريد التعامل مع الملفات.

```csharp
        // Load the image that contains the text you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/input_image.png");
```

> **حالة حافة:**  
> إذا كانت صورتك أكبر من 2000 × 2000 بكسل، فكر في تصغيرها أولاً. الصور الضخمة قد تبطئ عملية التعرف دون تحسين الدقة.

## الخطوة 4: تشغيل عملية OCR – Extract Plain Text

بعد تجهيز كل شيء، استدعِ `Recognize`. تُعيد الطريقة كائن `OcrResult` يحتوي على النص الأصلي والنص المنقح.

```csharp
        // Run OCR – this is where the engine actually recognises text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Display the extracted plain text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

> **ما ستراه:**  
> يطبع الطرفية نسخة نظيفة من النص مع الحفاظ على فواصل الأسطر. إذا كان القاموس المخصص يحتوي على “Aspose” و“OCR”، فستظهر تلك الكلمات بالضبط كما عرّفتها، حتى وإن كانت الصورة مشوشة قليلاً.

## مثال كامل يعمل

فيما يلي البرنامج **complete, copy‑and‑paste ready**. استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد الذي حفظت فيه القاموس والصورة.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class CustomDictionaryDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load a custom dictionary and assign it to the engine configuration
        HashSet<string> customDictionary = new HashSet<string>(
            File.ReadAllLines(@"YOUR_DIRECTORY/custom_dictionary.txt"));
        ocrEngine.Configuration.CustomDictionary = customDictionary;

        // Step 3: Load the image that contains the text to be recognized
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/input_image.png");

        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Display the extracted plain text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**الناتج المتوقع** (بافتراض أن الصورة تحتوي على “Welcome to Aspose OCR Demo”)  

```
=== Extracted Text ===
Welcome to Aspose OCR Demo
```

إذا كان “Aspose” موجوداً في القاموس المخصص، فستكون الإملائية مثالية حتى وإن كانت الصورة تحتوي على ضبابية خفيفة.

## الأسئلة المتكررة

### كيف يمكنني **read dictionary file** بترميزات مختلفة؟
استخدم `File.ReadAllLines(path, Encoding.UTF8)` (أو `Encoding.Unicode`) لتطابق ترميز الملف. هذا يمنع الأحرف المخفية من التسلل إلى `HashSet`.

### ماذا لو لا يزال نتيجة OCR تفتقد كلمة من القاموس؟
تأكد من أن حالة الأحرف للكلمة تتطابق مع إدخال القاموس، أو اضبط `ocrEngine.Configuration.IgnoreCase = true`. كما يجب التحقق من أن دقة الصورة لا تقل عن 300 dpi للحصول على أفضل النتائج.

### هل يمكنني **extract plain text** من PDF بدلاً من صورة؟
نعم—يمكن لـ Aspose.PDF تحويل كل صفحة إلى صورة، ثم تمرير تلك الصور إلى نفس خط أنابيب OCR. سير العمل هو نفسه؛ فقط أضف خطوة تحويل PDF إلى صورة.

### هل هناك طريقة لـ **how to add custom dictionary** في وقت التشغيل لعدة لغات؟
بالتأكيد. أنشئ `HashSet<string>` منفصل لكل لغة وبدّل `ocrEngine.Configuration.CustomDictionary` قبل كل استدعاء `Recognize`.

## نصائح وحيل لتحسين الدقة

- **Pre‑process the image**: حوّلها إلى تدرج الرمادي، زد التباين، أو طبّق تمويه غاوسي خفيف لإزالة البقع.
- **Batch processing**: إذا كان لديك عشرات الصور، أعد استخدام نفس مثال `OcrEngine`؛ إعادة التهيئة في كل مرة تضيف عبئًا غير ضروري.
- **Log the raw OCR data**: `ocrResult.TextLines` يمنحك درجات الثقة سطرًا بسطر، مفيدة للمعالجة اللاحقة أو لتحديد النتائج ذات الثقة المنخفضة.

## الخطوات التالية

الآن بعد أن عرفت **how to extract text** و**how to add custom dictionary**، فكر في المواضيع التالية:

1. **Integrate with ASP.NET Core** – إتاحة نقطة API تستقبل صورة وتعيد نتائج OCR بصيغة JSON.  
2. **Combine with Entity Framework** – خزن النص المستخرج مباشرةً في قاعدة بيانات لتصبح سجلات قابلة للبحث.  
3. **Explore language detection** – تبديل القواميس تلقائيًا بناءً على رموز اللغة المكتشفة.

كل من هذه المواضيع يبني على الأساس الذي وضعناه في هذا الدليل، مما يتيح لك تحويل مقتطف بسيط لـ **recognize text from image** إلى خدمة جاهزة للإنتاج.

---

*برمجة سعيدة! إذا واجهت أي مشكلة، اترك تعليقًا أدناه أو راجع وثائق Aspose.OCR للحصول على خيارات تكوين أعمق. تذكر، القاموس المخصص المصمم جيدًا هو غالبًا المكوّن السري الذي يحول OCR المتوسط إلى استخراج نص حاد كالشفرة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}