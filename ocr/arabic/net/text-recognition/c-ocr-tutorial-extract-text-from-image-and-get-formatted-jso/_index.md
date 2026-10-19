---
category: general
date: 2026-01-13
description: دروس C# OCR التي توضح كيفية استخراج النص من الصورة، تحميل الصورة للـ
  OCR، وتنسيق مخرجات JSON باستخدام Aspose OCR. تعلم كيفية تسلسل الكائن إلى JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: ar
og_description: دليل c# OCR يشرح لك كيفية استخراج النص من الصورة، تحميل الصورة للـ
  OCR، وتنسيق مخرجات JSON باستخدام Aspose OCR.
og_title: c# دليل OCR – استخراج النص وتنسيق JSON
tags:
- OCR
- C#
- JSON
title: دليل OCR بلغة C# – استخراج النص من الصورة والحصول على JSON منسق
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – استخراج النص من الصورة وتنسيق مخرجات JSON

هل تساءلت يومًا كيف **استخراج النص من الصورة** في مشروع C# دون التعامل مع معالجة البكسل منخفضة المستوى؟ هذه هي المشكلة التي يحلها *c# ocr tutorial*. خلال بضع دقائق فقط سترى كيف **تحميل الصورة للـ OCR**، تشغيل Aspose OCR، و **تنسيق مخرجات JSON** حتى تتمكن من إرسال البيانات مباشرة إلى API أو قاعدة البيانات الخاصة بك.

سنستعرض كل سطر من الشيفرة، نشرح لماذا كل جزء مهم، وحتى نعرض لك الـ JSON الدقيق الذي يجب أن تتوقعه. في النهاية ستحصل على تطبيق console جاهز للتنفيذ يحول صورة فاتورة PNG إلى JSON نظيف ومُنسق. لا إطالة، مجرد حل عملي يمكنك إدراجه في أي مشروع .NET 6+.

## ما يغطيه هذا c# ocr tutorial

- تثبيت حزمة NuGet الخاصة بـ Aspose.OCR  
- تحميل ملف صورة لمعالجة OCR  
- التعرف على النص الإنجليزي (أو أي لغة مدعومة)  
- **تحويل نتيجة OCR إلى JSON** مع تنسيق جميل  
- عرض الـ JSON في الـ console وحفظه إذا رغبت  

كل ما تحتاجه هو فهم أساسي للغة C# و .NET SDK حديث. لا شيء آخر. إذا كنت مهتمًا بـ **استخراج النص من الصورة** للفواتير أو الإيصالات أو النماذج الممسوحة، استمر في القراءة.

---

## الخطوة 1: إعداد بيئة c# ocr tutorial

قبل كتابة أي شيفرة، تأكد من أن لديك الأدوات الصحيحة:

1. **.NET 6 SDK أو أحدث** – يمكنك تنزيله من موقع Microsoft.  
2. **Visual Studio 2022** (الإصدار Community يكفي) أو أي محرر تفضله.  
3. **حزمة NuGet الخاصة بـ Aspose.OCR** – نفّذ الأمر `dotnet add package Aspose.OCR` في مجلد المشروع.

> **نصيحة احترافية:** إذا كنت تستخدم خط أنابيب CI، أضف إشارة الحزمة إلى ملف `.csproj` حتى يقوم البناء باستعادتها تلقائيًا.

---

## الخطوة 2: تحميل الصورة للـ OCR

الخطوة الأولى الفعلية في دليلنا هي جلب الصورة التي تريد معالجتها. Aspose OCR يدعم الصيغ الشائعة مثل PNG و JPEG و TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **لماذا هذا مهم:** تحميل الصورة كـ `OcrImage` يمنح المحرك إمكانية الوصول إلى بيانات البت ماب وأي معلومات DPI، مما يحسن دقة التعرف. تخطي هذه الخطوة أو تمرير ملف تالف سيتسبب في استثناء وقت التشغيل.

---

## الخطوة 3: استخراج النص من الصورة

الآن نقوم فعليًا بتشغيل محرك OCR. طريقة `Recognize` تُعيد كائن `OcrResult` غني يحتوي على النص الخام، درجات الثقة، وتفاصيل التخطيط.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **حالة خاصة:** إذا كنت بحاجة لمعالجة مستند متعدد اللغات، استدعِ `Recognize` مرتين بقيم `OcrLanguage` مختلفة وادمج النتائج. المحرك آمن للاستخدام المتعدد الخيوط، لذا يمكنك حتى تنفيذ عمليات متوازية على دفعات كبيرة.

---

## الخطوة 4: تحويل الكائن إلى JSON – تنسيق مخرجات JSON

كائن `OcrResult` هو فئة C# عادية، مما يعني أنه يمكن تمريره إلى `System.Text.Json`. بتمكين `WriteIndented` يصبح الإخراج قابلاً للقراءة البشرية.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **ما ستحصل عليه:** سلسلة JSON مُنسقة بشكل جميل تشمل النص المعترف به، الثقة، وتخطيط الصفحة. هذا مثالي للتسجيل، الإرسال إلى خدمة ويب، أو التخزين في قاعدة NoSQL.

---

## الخطوة 5: عرض (واختياريًا) حفظ الـ JSON المُنسق

أخيرًا، نطبع الـ JSON إلى الـ console. يمكنك أيضًا كتابته إلى ملف باستخدام `File.WriteAllText` إذا رغبت.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**الناتج المتوقع في الـ console (مقتطع للت brevity):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

إذا لم يتمكن محرك OCR من العثور على أي نص، سيكون حقل `Text` سلسلة فارغة و`Confidence` سيكون `0`. هذا إشارة جيدة للتحقق من جودة الصورة.

---

## الخطوة 6: مثال كامل يعمل

بجمع كل شيء معًا، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق console جديد:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

شغّل البرنامج (`dotnet run` من مجلد المشروع) وسترى الـ console يطبع تمثيل JSON مُنسق بشكل جميل لفاتورتك الممسوحة.

---

## المشكلات الشائعة & نصائح (إضافات c# ocr tutorial)

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **حقل `Text` فارغ** | الصورة منخفضة التباين أو مائلة. | عالج الصورة مسبقًا (زيادة التباين، تصحيح الميل) أو استخدم `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | ملفات Aspose OCR الأصلية مفقودة. | تأكد من أن حزمة NuGet استُعيدت بشكل صحيح وأن بنية وقت التشغيل (x64/x86) تتطابق مع نظامك. |
| **بطء الأداء على ملفات PDF الكبيرة** | OCR يعالج كل صفحة بالتتابع. | نفّذ عمليات متوازية بإنشاء مثيلات منفصلة من `OcrEngine` لكل صفحة (المحرك آمن للـ thread). |
| **JSON كبير جدًا** | تقوم بتسلسل كل التفاصيل، بما في ذلك الصناديق المحيطة. | استخدم DTO يحتوي فقط على `Text` و `Confidence` قبل التسلسل. |

> **تذكر:** هدف هذا الدليل هو إظهار تدفق نظيف من البداية للنهاية. يمكنك دائمًا تقليل حجم الـ JSON أو إضافة المزيد من البيانات الوصفية لاحقًا.

---

## الخلاصة

لقد أكملت الآن **c# ocr tutorial** الذي يحمل صورة، **يستخرج النص من الصورة**، وينتج **تنسيق مخرجات JSON** عبر **تحويل الكائن إلى JSON**. الخطوات بسيطة، الشيفرة جاهزة للتنفيذ، والـ JSON منسق بشكل مثالي للاستخدام اللاحق.

ما الخطوة التالية؟ جرّب استبدال `OcrLanguage.English` بـ `OcrLanguage.French` أو عالج مجلدًا من الإيصالات داخل حلقة. يمكنك أيضًا استكشاف حفظ الـ JSON مباشرةً إلى Azure Blob Storage أو إرساله إلى نموذج تعلم آلي.

إذا واجهت أي مشاكل، تحقق من صحة مسار الصورة وأن رخصة Aspose OCR (إن وجدت) تم تحميلها قبل استدعاء `Recognize`. برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة! 

*صورة توضح تدفق OCR (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}