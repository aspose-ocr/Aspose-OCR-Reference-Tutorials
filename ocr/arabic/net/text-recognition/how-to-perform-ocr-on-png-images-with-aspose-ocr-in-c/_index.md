---
category: general
date: 2026-11-26
description: تعرّف على كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) لملفات PNG، وتحويل
  PNG إلى نص، واستخراج النص السيريلي باستخدام Aspose.OCR – دليل خطوة بخطوة للمطورين.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: ar
lastmod: 2026-11-26
og_description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) لملفات PNG واستخراج النص
  السيريلي باستخدام Aspose.OCR في C#. اتبع هذا الدليل الكامل لتحويل PNG إلى نص.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: كيفية تنفيذ OCR على صور PNG باستخدام Aspose.OCR – دليل C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: كيفية تنفيذ OCR على صور PNG باستخدام Aspose.OCR في C#
url: /ar/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على صور PNG باستخدام Aspose.OCR في C#

إذا كنت بحاجة إلى **كيفية إجراء OCR** على ملف PNG، يوضح لك هذا الدليل الخطوات الدقيقة لتحويل PNG إلى نص باستخدام Aspose.OCR. سواء كنت تستخرج نصًا سيريليًا من مستندات ممسوحة ضوئيًا أو ببساطة تتعرف على النص من لقطات شاشة PNG، فإن الحل يعمل مباشرةً ويتطلب فقط بضع أسطر من شفرة C#.

في هذا الدرس ستتعلم كيف تقوم بـ:

* **تحميل الصورة لـ OCR** من مجلد محلي،
* تكوين المحرك لـ **استخراج النص السيريلي**،
* **التعرف على النص من PNG** والحصول على سلسلة نظيفة،
* معالجة المشكلات الشائعة مثل فقدان وحدات اللغة والصور الكبيرة.

لا يلزم أي خبرة سابقة مع Aspose.OCR — فقط بيئة تطوير .NET وصورة PNG تريد معالجتها.

## المتطلبات المسبقة

* .NET 6.0 (أو أحدث) مثبت.
* نسخة مرخصة أو تجريبية من **Aspose.OCR for .NET**. يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose.
* Visual Studio 2022 (أو أي بيئة تطوير تدعم .NET).
* ملف PNG يحتوي على النص الذي تريد استخراجَه (المثال يستخدم `sample_image.png`).

## الخطوة 1: تثبيت حزمة Aspose.OCR NuGet

افتح نافذة طرفية في مجلد المشروع الخاص بك وشغّل:

```bash
dotnet add package Aspose.OCR
```

تتضمن الحزمة محرك OCR الأساسي وجميع وحدات اللغة. عندما تطلب لغة غير موجودة محليًا، يقوم Aspose.OCR بتنزيل الوحدة المطلوبة تلقائيًا.

## الخطوة 2: إنشاء مثيل محرك OCR (كيفية إجراء OCR)

الخطوة العملية الأولى في أي سير عمل OCR هي إنشاء مثيل للمحرك. هذا الكائن يدير جميع العمليات اللاحقة مثل تحميل الصورة وإجراء التعرف.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**لماذا هذا مهم:** فئة `OcrEngine` تغلف خط أنابيب OCR. إنشاء مثيل واحد وإعادة استخدامه عبر صور متعددة يقلل من استهلاك الذاكرة ويحسن الأداء.

## الخطوة 3: تحميل الصورة لـ OCR – تحديد ملف PNG المصدر

تحميل الصورة هو النقطة التي تقوم فيها **بتحميل الصورة لـ OCR**. يقبل Aspose.OCR عدة أنواع من المدخلات؛ أبسطها هو `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **نصيحة احترافية:** استخدم مسارًا مطلقًا أو `Path.Combine` لتجنب أخطاء وقت التشغيل في بيئات مختلفة.

### التعامل مع الصور الكبيرة

إذا كان حجم PNG أكبر من 2 ميغابايت، فكر في تقليل حجمه قبل التعرف لتسريع المعالجة:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## الخطوة 4: تكوين اللغة – استخراج النص السيريلي

بشكل افتراضي، يفترض Aspose.OCR اللغة الإنجليزية. لاستخراج **النص السيريلي**، اضبط خاصية `Language` إلى `Language.Cyrillic`. سيتم تنزيل الوحدة المطلوبة تلقائيًا في المرة الأولى التي تشغّل فيها الشفرة.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

إذا كنت بحاجة إلى التعرف على عدة لغات (مثل الإنجليزية والسيريلي)، يمكنك دمجها:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### حالة خاصة: وحدة اللغة مفقودة

إذا فشل التنزيل (مثلاً في بيئة غير متصلة)، يرمي المحرك استثناءً `OcrException`. امسك به لتوفير حل احتياطي سلس:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## الخطوة 5: تنفيذ عملية التعرف (التعرف على النص من PNG)

الآن بعد ضبط الصورة واللغة، يمكنك **التعرف على النص من PNG**. طريقة `Recognize` تشغّل خط أنابيب OCR بشكل متزامن.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**لماذا يعمل:** داخليًا، يطبق Aspose.OCR معالجة مسبقة (تحويل إلى ثنائي، إزالة الضوضاء) قبل تمرير الصورة إلى مُعرّف قائم على الشبكة العصبية مُضبط للغة المختارة.

## الخطوة 6: استرجاع وعرض النص المُعترف به (تحويل PNG إلى نص)

بعد التعرف، تكون السلسلة المستخرجة متاحة عبر خاصية `Text`. هذه هي الخطوة الأخيرة في **تحويل PNG إلى نص**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### النتيجة المتوقعة

إذا كان `sample_image.png` يحتوي على العبارة السيريليّة “Привет мир”، سيعرض الطرفية:

```
=== OCR Result ===
Привет мир
```

قد يتضمن الناتج فواصل أسطر وعلامات ترقيم تمامًا كما تظهر في الصورة. يمكنك معالجة السلسلة لاحقًا باستخدام `String.Trim()`, `Regex` أو أدوات تنظيف النص الأخرى إذا لزم الأمر.

## الخطوة 7: اختياري – حفظ النتيجة إلى ملف

تخزين نتيجة OCR يتيح معالجة لاحقة (مثل الفهرسة، الترجمة). إليك طريقة سريعة لكتابة النص إلى ملف UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## المشكلات الشائعة وكيفية تجنّبها

| Issue | Symptom | Fix |
|-------|----------|-----|
| **وحدة اللغة مفقودة** | `OcrException` on `Language = Language.Cyrillic` | تأكد من وجود اتصال بالإنترنت في التشغيل الأول أو قم بتنزيل الوحدات مسبقًا عبر حزمة Aspose غير المتصلة. |
| **صورة غير واضحة أو منخفضة التباين** | Poor accuracy, many “?” characters | قم بمعالجة الصورة مسبقًا: زيادة التباين، تطبيق الشحذ، أو تحويلها إلى تدرج الرمادي قبل تمريرها إلى المحرك. |
| **PNG كبير جدًا** | Long processing time, possible `OutOfMemoryException` | قلل الحجم كما هو موضح في الخطوة 3، أو قسّم صورة متعددة الصفحات إلى قطع منفصلة. |
| **أحرف غير UTF‑8** | Garbled output | تحقق من أن الطرفية أو كاتب الملف يستخدم ترميز UTF‑8 (`Encoding.UTF8`). |

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يدمج جميع الخطوات السابقة. انسخه إلى مشروع وحدة تحكم جديد وشغّله بعد تعديل مسارات الملفات.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### كيف يعمل

1. **إنشاء المحرك** – يجهّز خط أنابيب OCR.  
2. **تحميل الصورة** – يدعم كلًا من PNG الأصلي والإصدارات المصغرة للأداء.  
3. **اختيار اللغة** – يوضح **استخراج النص السيريلي** مع معالجة الوحدات المفقودة.  
4. **التعرف** – الاستدعاء الأساسي **للتعرف على النص من PNG**.  
5. **معالجة النتيجة** – يوضح **تحويل PNG إلى نص** ويكتب الناتج إلى ملف.

شغّل البرنامج باستخدام `dotnet run`. إذا تم إعداد كل شيء بشكل صحيح، سترى النص المُعترف به يُطبع في الطرفية ويتم حفظه في `ocr_output.txt`.

## الخلاصة

في هذا الدليل تعلمت **كيفية إجراء OCR** على ملفات PNG باستخدام Aspose.OCR لـ .NET، مع تغطية كل شيء من **تحميل الصورة لـ OCR** إلى **استخراج النص السيريلي** و**تحويل PNG إلى نص**. يُظهر المثال الكامل القابل للتنفيذ سير العمل القياسي، الحالات الخاصة الشائعة، والنصائح العملية التي تجعل خط أنابيب OCR الخاص بك موثوقًا.

**الخطوات التالية**

* استكشف **التعرف على النص من PNG** مع لغات إضافية (العربية، الصينية) عن طريق دمج علامات `Language`.  
* دمج نتيجة OCR مع Azure Cognitive Search لأرشفة المستندات القابلة للبحث.  
* جرّب إعدادات `OcrEngine` في Aspose.OCR مثل `Resolution

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية تنزيل نموذج Aspose.OCR واستخراج النص من PNG في C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [كيفية إجراء OCR في C# – التعرف على النص السيريلي باستخدام Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [كيفية تنفيذ OCR دفعيًا في C# – طريقة سريعة لاستخراج نص ملفات PNG](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}