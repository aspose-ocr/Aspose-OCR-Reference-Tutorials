---
category: general
date: 2026-03-05
description: كيفية استخدام OCR في C# لاستخراج النص من الصورة. تعلم تحويل الصورة إلى
  نص، قراءة الأحرف الكورية، وتحميل الصورة لـ OCR بسرعة.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: ar
og_description: كيفية استخدام OCR في C# واستخراج النص من الصورة فورًا. يوضح هذا الدليل
  كيفية تحويل الصورة إلى نص، قراءة الأحرف الكورية وتحميل الصورة لاستخدام OCR.
og_title: كيفية استخدام OCR في C# – استخراج النص من الصورة
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص من الصورة
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصورة

هل تساءلت يومًا **كيفية استخدام OCR** عندما تكون لديك لقطة شاشة مليئة بالنص الكوري وتحتاج إلى استرجاع السلسلة النصية البسيطة؟ لست الوحيد الذي يحاول حل هذه المشكلة. في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ **يستخرج النص من الصورة**، **يحوّل الصورة إلى نص**، وحتى يوضح لك كيفية **قراءة الأحرف الكورية** باستخدام Aspose.OCR.

سنغطي أيضًا الخطوة التي غالبًا ما تُهمل وهي **تحميل الصورة لـ OCR** حتى لا تواجه مفاجأة “الملف غير موجود” لاحقًا. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET.

## ما الذي ستحتاجه

- .NET 6+ (أو .NET Framework 4.7.2 وما بعده) – الكود يعمل على كلاهما.  
- Aspose.OCR for .NET – يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose.  
- صورة نموذجية (`korean_doc.png`) تحتوي على نص كوري.  
- بيئة التطوير المفضلة لديك (Visual Studio، Rider، VS Code – أيًا كان).

لا توجد مكتبات طرف ثالث أخرى مطلوبة.

## الخطوة 1: إعداد المشروع وإضافة Aspose.OCR

أولاً، أنشئ تطبيق console جديد:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

ثم أضف حزمة NuGet الخاصة بـ Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كان لديك ملف ترخيص، ضعّه في جذر المشروع؛ وإلا فإن النسخة التجريبية المجانية ستعمل ولكنها ستضيف علامة مائية إلى الناتج.

## الخطوة 2: كيفية استخدام OCR – تهيئة المحرك

الآن سنكتب كود C#. أول شيء يجب القيام به عندما **تسأل عن كيفية استخدام OCR** هو إنشاء كائن `OcrEngine`. هذا الكائن هو قلب المكتبة؛ فهو يحمل جميع الإعدادات التي ستحتاجها لاحقًا.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**لماذا هذا مهم:** بدون وجود مثال صالح من المحرك لا يمكنك تعيين اللغة، تحميل الصور، أو استرجاع النتائج. كما أن المحرك يدير الموارد الداخلية، لذا إن إنشاءه مرة واحدة وإعادة استخدامه أكثر كفاءة من إنشاء كائنات جديدة في كل مرة.

## الخطوة 3: اختيار اللغة – قراءة الأحرف الكورية

السطر التالي يخبر المحرك أي لغة يبحث عنها. بما أن هدفنا هو **قراءة الأحرف الكورية**، نضبط `OcrLanguage.Korean`. يمكنك استبداله بالعربية أو التايلاندية أو الغوجاراتية، حسب حالتك.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**لماذا هذا مهم:** اختيار اللغة يحسن الدقة بشكل كبير. يستخدم محرك OCR قواميس ونماذج حروف مخصصة لكل لغة؛ وإعطاؤه لغة غير صحيحة قد ينتج مخرجات مشوشة.

## الخطوة 4: تحميل الصورة لـ OCR – تحويل الصورة إلى نص

قبل أن يتمكن المحرك من القيام بأي عمل، عليك **تحميل الصورة لـ OCR**. طريقة `ImageStream.FromFile` تقرأ الملف إلى صيغة يفهمها المحرك.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

إذا كانت الصورة موجودة في مجلد مختلف، ما عليك سوى تعديل المسار. تذكر ضبط *إجراء البناء* للملف إلى “Copy if newer” حتى يتمكن الملف التنفيذي من العثور عليه أثناء التشغيل.

> **خطأ شائع:** توفير مسار يحتوي على شرطات مائلة عكسية (`\`) داخل سلسلة نصية دون هروبها سيؤدي إلى خطأ تجميعي. استخدم إما شرطات مزدوجة (`\\`) أو سلسلة حرفية (`@"C:\path\file.png"`).

## الخطوة 5: تنفيذ OCR – استخراج النص من الصورة

الآن يحدث الجزء الثقيل. استدعاء `Recognize()` يشغل خوارزمية OCR، وخصيصة `Text` تعطيك السلسلة النصية الخام.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

في هذه المرحلة تكون قد **استخرجت النص من الصورة** وفعليًا **حوّلت الصورة إلى نص**. قد يحتوي الناتج على أحرف سطر جديد إذا كان التخطيط الأصلي يحتوي على فواصل أسطر.

## الخطوة 6: عرض النتيجة – التحقق من المخرجات

أخيرًا، لنطبع النتيجة إلى وحدة التحكم حتى تتمكن من التحقق من نجاح العملية.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

شغّل البرنامج:

```bash
dotnet run
```

### النتيجة المتوقعة

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

إذا رأيت أحرفًا كورية مشابهة لتلك الموجودة في الصورة، تهانينا—لقد أتقنت **كيفية استخدام OCR** مع Aspose.OCR!

![مخطط مثال كيفية استخدام OCR](image.png)

*نص بديل للصورة: مخطط مثال كيفية استخدام OCR يوضح التدفق من تحميل الصورة إلى طباعة النص المعترف به.*

## الحالات الخاصة والبدائل

### 1. معالجة صفحات متعددة

إذا كنت بحاجة إلى **استخراج النص من صورة** تحتوي على عدة صفحات (مثل TIFF متعدد الصفحات)، قم بالتكرار على كل صفحة واستدعِ `Recognize()` لكل كائن `ImageStream`.

### 2. التعامل مع مسحات منخفضة الجودة

الصور منخفضة الدقة قد تضر بالدقة. قبل استدعاء `Recognize()`، يمكنك تحسين الصورة باستخدام أدوات ما قبل المعالجة من Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. تبديل اللغات أثناء التشغيل

إذا كان لديك مستند مختلط اللغات. يمكنك تغيير `ocrEngine.Language` بين عمليات التعرف:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. حفظ النتيجة إلى ملف

إذا كنت تفضّل **تحويل الصورة إلى نص** وتخزينه، ما عليك سوى كتابة السلسلة إلى ملف `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## الأسئلة الشائعة

- **هل أحتاج إلى ترخيص لتشغيل هذا الكود؟**  
  لا. النسخة التجريبية المجانية تعمل جيدًا للتجربة، لكنها تضيف علامة مائية إلى الناتج. الترخيص المدفوع يزيل العلامة المائية ويفتح الأداء الكامل.

- **هل يمكنني استخدامه على Linux؟**  
  بالتأكيد. Aspose.OCR متعدد المنصات؛ فقط تأكد من وجود الاعتماديات الأصلية المطلوبة (libgdiplus لـ .NET Core على Linux).

- **ماذا لو كانت صورتي في تدفق (stream) بدلاً من ملف؟**  
  استخدم `ImageStream.FromStream(yourStream)` – الـ API يقبل أي `System.IO.Stream`.

## الخلاصة

لقد مررنا معًا خطوة بخطوة عبر **كيفية استخدام OCR** في C# لـ **استخراج النص من الصورة**، **تحويل الصورة إلى نص**، و**قراءة الأحرف الكورية** مع تحميل الصورة بشكل صحيح لـ OCR. المثال الكامل القابل للتنفيذ أعلاه يجب أن يعمل مباشرة، والنصائح الإضافية تعطيك خريطة طريق لسيناريوهات أكثر تقدمًا.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال اللغة، معالجة ملفات PDF صفحة بصفحة، أو دمج استدعاء OCR في واجهة ويب API بحيث يمكن للمستخدمين رفع الصور والحصول على النص فورًا. الاحتمالات لا حصر لها، والآن لديك أساس قوي للبناء عليه.

برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}