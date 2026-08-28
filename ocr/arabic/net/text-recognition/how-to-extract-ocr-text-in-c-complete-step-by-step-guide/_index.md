---
category: general
date: 2025-12-30
description: تعلم كيفية استخراج نص OCR من الصور باستخدام C#. يغطي هذا الدرس استخراج
  النص من ملفات الصور، قراءة النص من PNG، ويتضمن دليلًا كاملاً لتقنية OCR باستخدام
  C#.
draft: false
keywords:
- how to extract ocr
- extract text from image
- read text from png
- c# ocr tutorial
language: ar
og_description: كيفية استخراج نص OCR من الصور باستخدام C#. اتبع هذا الدرس التعليمي
  لـ C# OCR لقراءة النص من ملفات PNG واستخراج النص من الصورة بسهولة.
og_title: كيفية استخراج نص OCR في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
title: كيفية استخراج نص OCR في C# – دليل خطوة بخطوة كامل
url: /ar/net/text-recognition/how-to-extract-ocr-text-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج نص OCR في C# – دليل خطوة بخطوة كامل

هل تساءلت يومًا **كيفية استخراج OCR** من نموذج ممسوح ضوئيًا دون قضاء ساعات في كتابة محللات مخصصة؟ لست الوحيد. في العديد من المشاريع الواقعية—مثل معالجة الفواتير، مسح جوازات السفر، أو رقمنة الأرشيفات القديمة—تحتاج إلى طريقة موثوقة لاستخراج النص من ملف صورة. الخبر السار؟ مع Aspose.OCR يمكنك القيام بذلك ببضع أسطر فقط من C#.

في هذا الدرس سنستعرض **c# ocr tutorial** يوضح لك كيفية **استخراج النص من صورة**، وبشكل محدد من ملف PNG، وكيفية **قراءة النص من png** مع الحفاظ على البيانات الوصفية لكل حرف. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع سلسلة JSON منسقة بشكل جميل تحتوي على كل ما التقطته Aspose.

> **المتطلبات المسبقة**  
> • .NET 6.0 أو أحدث مثبت  
> • Visual Studio 2022 (أو أي بيئة تطوير تفضلها)  
> • حزمة NuGet Aspose.OCR for .NET (`Aspose.OCR`)  

إذا كنت قد غطيت هذه الأساسيات، فلنبدأ.

---

## كيفية استخراج نص OCR من صورة في C# – إعداد المشروع

قبل أن نبدأ بالبرمجة، نحتاج إلى مشروع نظيف والاعتماد المناسب.

```bash
# Create a new console app
dotnet new console -n OcrDemo
cd OcrDemo

# Add Aspose.OCR package
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك إضافة الحزمة عبر واجهة مدير الحزم NuGet—فقط ابحث عن “Aspose.OCR”.

بعد تثبيت الحزمة، افتح `Program.cs`. سترى طريقة `Main` الافتراضية جاهزة لتملأها.

---

## الخطوة 1 – تهيئة محرك OCR (لماذا هو مهم)

محرك OCR هو قلب العملية. تهيئته تخبر Aspose أي نماذج اللغة التي تنوي استخدامها لاحقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance
            var ocrEngine = new OcrEngine();

            // The rest of the steps will follow here...
        }
    }
}
```

*لماذا هذه الخطوة؟*  
إنشاء كائن `OcrEngine` يخصص الموارد اللازمة لتحليل الصورة. بدون ذلك، لا شيء يمكنك إمداد الصورة إليه، ولا يمكن للمكتبة تطبيق خوارزميات التعرف على الأنماط المتقدمة.

---

## الخطوة 2 – تحميل نموذج اللغة الإنجليزية (استخراج النص من صورة)

تأتي Aspose مع عدة حزم لغوية. تحميل الحزمة الصحيحة يحسن الدقة بشكل كبير.

```csharp
// Step 2: Load the English language model
ocrEngine.LoadLanguage(LanguageModel.English);
```

إذا احتجت يومًا إلى **قراءة النص من png** يحتوي على لغة أخرى، ما عليك سوى استبدال `LanguageModel.English` بالقيمة المناسبة من الـ enum (مثال: `LanguageModel.French`). هذه المرونة هي السبب في أن Aspose خيار شائع للتطبيقات العالمية.

---

## الخطوة 3 – التعرف على النص من ملف PNG الخاص بك (قراءة النص من PNG)

الآن نوجه المحرك إلى الصورة الفعلية. لهذا العرض التجريبي، ضع ملف PNG اسمه `form_image.png` داخل مجلد يسمى `YOUR_DIRECTORY` بالنسبة إلى الملف التنفيذي.

```csharp
// Step 3: Perform OCR on the image
var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");
```

> **ماذا لو لم يتم العثور على الملف؟**  
> طريقة `Recognize` ترمي استثناء `FileNotFoundException`. غلف الاستدعاء بكتلة try‑catch إذا كنت تريد معالجة أخطاء سلسة في بيئة الإنتاج.

---

## الخطوة 4 – تحويل النتيجة إلى JSON منسق (لماذا JSON؟)

تُعيد Aspose كائن `RecognitionResult` غني يحتوي ليس فقط على النص العادي بل أيضًا على صناديق الإحاطة، درجات الثقة، ومعلومات السطر. تحويله إلى JSON يجعل من السهل تسجيله، تخزينه، أو إرساله عبر API.

```csharp
// Step 4: Serialize the result to a nicely indented JSON string
string json = JsonResult.FromRecognitionResult(recognitionResult)
                        .ToString(prettyPrint: true);

// Optional: Write the JSON to a file for later inspection
System.IO.File.WriteAllText("ocr_output.json", json);
```

علامة `prettyPrint: true` تضيف فواصل أسطر وتنسيق، وهو مثالي للتصحيح. إذا كنت تحتاج فقط النص الخام، يمكنك ببساطة استخدام `recognitionResult.Text`.

---

## الخطوة 5 – عرض مخرجات JSON (رؤية النتيجة)

أخيرًا، لنطبع JSON إلى الكونسول حتى تتمكن من التحقق من أن كل شيء عمل.

```csharp
// Step 5: Output the JSON to the console
Console.WriteLine(json);
```

تشغيل البرنامج الآن يجب أن ينتج مخرجات مشابهة للمقتطف أدناه (مقتطع للاختصار):

```json
{
  "Text": "John Doe\n123 Main St\nAnytown, USA",
  "Characters": [
    {
      "Value": "J",
      "Confidence": 0.99,
      "Bounds": { "X": 12, "Y": 8, "Width": 10, "Height": 14 }
    },
    // ... more character objects ...
  ],
  "Lines": [
    { "Text": "John Doe", "Confidence": 0.98 },
    { "Text": "123 Main St", "Confidence": 0.97 },
    { "Text": "Anytown, USA", "Confidence": 0.96 }
  ]
}
```

لاحظ البيانات الوصفية لكل حرف—هذه هي القيمة الإضافية التي تقدمها Aspose مقارنة بالعديد من مكتبات OCR المجانية. الآن يمكنك تصفية الأحرف ذات الثقة المنخفضة أو ربط النص مرة أخرى بالصورة الأصلية للتظليل.

---

## مثال كامل يعمل (جميع الخطوات في مكان واحد)

فيما يلي البرنامج الكامل، جاهز للنسخ واللصق. لا توجد أجزاء مفقودة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Step 2: Load the English language model
            ocrEngine.LoadLanguage(LanguageModel.English);

            // Step 3: Recognize text from the PNG image
            var recognitionResult = ocrEngine.Recognize("YOUR_DIRECTORY/form_image.png");

            // Step 4: Convert the result to pretty‑printed JSON
            string json = JsonResult.FromRecognitionResult(recognitionResult)
                                    .ToString(prettyPrint: true);

            // Optional: Save JSON to a file
            System.IO.File.WriteAllText("ocr_output.json", json);

            // Step 5: Display the JSON output
            Console.WriteLine(json);
        }
    }
}
```

احفظه كـ `Program.cs`، ضع ملف PNG الخاص بك، شغّل `dotnet run`، وسترى JSON مطبوعًا.

---

## أسئلة شائعة وحالات خاصة (الإجابة على “ماذا لو؟”)

### ماذا لو كانت الصورة JPEG بدلاً من PNG؟

طريقة `Recognize` تقبل أي تنسيق تدعمه Aspose (JPEG، BMP، TIFF، إلخ). فقط غيّر امتداد الملف في المسار.

### كيف أحسن الدقة للماسحات منخفضة الدقة؟

1. **معالجة مسبقة للصورة** – زيادة التباين، تحويل إلى تدرج رمادي، أو تطبيق مرشح تحسين الحدة.  
2. **استخدام مصدر بدقة أعلى** – عادةً تحتاج محركات OCR إلى ما لا يقل عن 300 dpi للحصول على نتائج موثوقة.  
3. **تمكين التدوير التلقائي** – استدعِ `ocrEngine.AutoRotate = true;` قبل التعرف.

### هل يمكن استخراج النص العادي فقط دون JSON؟

نعم. بعد `Recognize`، ببساطة اقرأ `recognitionResult.Text`:

```csharp
Console.WriteLine(recognitionResult.Text);
```

### هل هناك طريقة لاستخراج النص من PDF متعدد الصفحات؟

Aspose.OCR يعمل على الصور، لكن يمكنك دمجه مع Aspose.PDF لتحويل كل صفحة PDF إلى صورة، ثم تمرير تلك الصور إلى محرك OCR داخل حلقة.

---

## نصائح احترافية لدرس c# OCR قوي

- **تحرير المحرك**: ضع `OcrEngine` داخل كتلة `using` إذا كنت تعالج العديد من الصور لتحرير الموارد الأصلية بسرعة.  
- **معالجة دفعات**: للمجلدات الكبيرة، استعرض الملفات باستخدام `Directory.GetFiles` وعالج كل ملف داخل كتلة try‑catch لتجنب توقف العملية بسبب ملف واحد سيء.  
- **التسجيل**: احفظ درجات الثقة؛ فهي لا تقدر بثمن عندما تحتاج إلى وضع علامة على النتائج منخفضة الجودة للمراجعة اليدوية.  
- **سلامة الخيوط**: كائنات `OcrEngine` **ليست** آمنة للاستخدام المتعدد الخيوط. أنشئ نسخة منفصلة لكل خيط إذا قمت بالتوازي.

---

## الخلاصة

لقد تعلمت الآن **كيفية استخراج نص OCR** من صورة باستخدام C#. من خلال تهيئة محرك OCR، تحميل نموذج اللغة المناسب، التعرف على PNG، وتحويل النتيجة إلى JSON منسق، لديك الآن أساس قوي لأي مشروع رقمنة مستندات. هذا **c# ocr tutorial** غطى أيضًا كيفية **استخراج النص من صورة**، **قراءة النص من png**، والتعامل مع المشكلات الشائعة.

هل أنت مستعد للخطوة التالية؟ جرّب تغذية دفعة من الفواتير الممسوحة إلى نفس خط الأنابيب، جرب حزم لغات مختلفة، أو دمج مخرجات JSON في قاعدة بيانات قابلة للبحث. السماء هي الحد، والكود الذي كتبته هو منصة الإطلاق.

إذا وجدت هذا الدليل مفيدًا، لا تتردد في مشاركته مع زملائك، وضع نجمة على المستودع، أو ترك تعليق بقصص نجاح OCR الخاصة بك. برمجة سعيدة! 

![how to extract ocr example](https://example.com/ocr-demo.png "how to extract ocr example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}