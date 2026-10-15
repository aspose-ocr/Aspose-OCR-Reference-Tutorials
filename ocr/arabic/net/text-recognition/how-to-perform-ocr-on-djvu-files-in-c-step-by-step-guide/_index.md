---
category: general
date: 2026-02-20
description: كيفية تنفيذ OCR على ملفات DjVu باستخدام C#. تعلم كيفية التعرف على النص
  من الصورة وتحويل DjVu إلى نص بسرعة باستخدام Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: ar
og_description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) لملفات DjVu باستخدام C#.
  يوضح لك هذا الدرس كيفية التعرف على النص من الصورة، قراءة DjVu، وتحويل DjVu إلى نص
  باستخدام Aspose OCR.
og_title: كيفية تنفيذ OCR على ملفات DjVu في C# – دليل كامل
tags:
- OCR
- C#
- DjVu
- Aspose
title: كيفية تنفيذ OCR على ملفات DjVu في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على ملفات DjVu في C# – دليل كامل

هل تساءلت يومًا **كيف تقوم بإجراء OCR** على مستند DjVu دون أن تشد شعرك؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى **التعرف على النص من صورة** الموجودة داخل حاويات DjVu. الخبر السار؟ ببضع أسطر من C# ومكتبة Aspose OCR، يمكنك استخراج ذلك النص المخفي في لحظة.

في هذا الدرس سنستعرض كل ما تحتاجه لتحويل صفحة DjVu إلى نص عادي. في النهاية ستعرف **كيفية قراءة DjVu**، وكيفية **استخراج النص من صورة**، وحتى **كيفية تحويل DjVu إلى نص** للمعالجة اللاحقة. لا خدمات خارجية، ولا مراجع غامضة—فقط مثال مكتمل يمكن تشغيله مباشرة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من توفر ما يلي:

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.8).
- Visual Studio 2022 أو أي محرر يدعم C#.
- ترخيص Aspose OCR for .NET (الإصدار التجريبي المجاني يكفي للاختبار).
- ملف DjVu تجريبي (`sample.djvu`) موجود في مجلد يمكنك الإشارة إليه.

وجود هذه المتطلبات سيجعل العملية سلسة—دون مفاجآت “مرجع مفقود” لاحقًا.

## كيفية إجراء OCR على صفحة DjVu

الفكرة الأساسية بسيطة: تحميل صفحة DjVu كصورة، تمريرها إلى محرك OCR، ثم قراءة السلسلة الناتجة. لنفصل ذلك خطوة بخطوة.

### الخطوة 1: تثبيت Aspose OCR

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

هذا سيجلب أحدث ملفات Aspose OCR الثنائية واعتمادياتها. إذا كنت تفضّل واجهة مدير الحزم NuGet، ابحث عن **Aspose.OCR** وانقر **Install**.

### الخطوة 2: تهيئة محرك OCR

إنشاء كائن `OcrEngine` هو أول ما تقوم به عندما تريد **إجراء OCR**. فكر فيه كتشغيل دماغ الماسح الضوئي.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **نصيحة احترافية:** إعادة استخدام كائن `OcrEngine` واحد لعدة صفحات يوفر الذاكرة ويسرّع المعالجة.

### الخطوة 3: تحميل صفحة DjVu كصورة

ملفات DjVu لا تُدعم مباشرةً من معظم واجهات برمجة الصور، لكن Aspose يمكنه التعامل مع كل صفحة كصورة bitmap. هنا نستخدم `System.Drawing.Image` لقراءة الملف.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **لماذا يعمل هذا:** `Image.FromFile` يقوم تلقائيًا بفك ترميز تدفق DjVu إلى تنسيق نقطي يفهمه محرك OCR. إذا احتجت معالجة صفحة معينة من DjVu متعدد الصفحات، استخدم Aspose PDF أو Aspose Imaging لاستخراج الصفحة أولًا.

### الخطوة 4: التعرف على النص من الصورة

الآن يحدث السحر. طريقة `Recognize` تفحص الـ bitmap وتعيد سلسلة تحتوي على الأحرف المكتشفة.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

في هذه المرحلة تكون قد **قمت بالتعرف على النص من صورة** كانت في الأصل داخل حاوية DjVu. قد تحتوي السلسلة على فواصل أسطر، علامات ترقيم، وحتى أحرف Unicode إذا كانت اللغة المصدر تدعمها.

### الخطوة 5: عرض أو حفظ النتيجة

لإجراء فحص سريع، يمكنك طباعة النص إلى وحدة التحكم. في تطبيق حقيقي ربما تفضّل حفظه في ملف أو قاعدة بيانات.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

بجمع كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**الناتج المتوقع** (مقتطع للتوضيح):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

إذا رأيت أحرفًا غير مفهومة، تأكد من أن ملف DjVu غير مشفر وأنك ضبطت اللغة الصحيحة في `ocrEngine.Language`. بشكل افتراضي يُفترض اللغة الإنجليزية؛ يمكنك التبديل إلى الفرنسية أو الألمانية إلخ عبر تعيين `ocrEngine.Language = Language.French;`.

## التعرف على النص من صورة – المشكلات الشائعة

حتى مع مثال ثابت، يواجه المطورون بعض الحالات الخاصة:

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **ناتج فارغ** | دقة الصورة منخفضة (<300 dpi). | استخدم `ocrEngine.ImageResolution = 300;` قبل استدعاء `Recognize`. |
| **لغة غير صحيحة** | OCR يفترض اللغة الإنجليزية افتراضيًا. | عيّن `ocrEngine.Language = Language.Spanish;` (أو أي لغة مدعومة). |
| **تسرب الذاكرة** | صفحات DjVu الكبيرة تبقى في الذاكرة بعد المعالجة. | استدعِ `djvuPage.Dispose();` بعد الانتهاء. |
| **DjVu متعدد الصفحات** | يتم تحميل الصفحة الأولى فقط. | استخدم حلقة لتكرار الصفحات عبر فئة `DjvuImage` في Aspose Imaging. |

معالجة هذه القضايا مبكرًا توفر عليك ساعات طويلة من التصحيح.

## كيفية قراءة ملفات DjVu في C# – ما بعد OCR البسيط

إذا كان مشروعك يحتاج إلى أكثر من صفحة واحدة، سيتوجب عليك استخراج كل صفحة كصورة أولًا. Aspose Imaging يجعل ذلك سهلًا:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

بهذا النمط يمكنك **تحويل DjVu إلى نص** صفحة بصفحة، وهو مثالي لمعالجة دفعات كبيرة من الأرشيفات.

## استخراج النص من صورة – تحسين الدقة

الإعدادات الافتراضية لـ OCR تعمل جيدًا مع المسحات النظيفة، لكن يمكنك رفع الدقة:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

هذه التعديلات مفيدة خاصةً عندما يحتوي مصدر DjVu على ملاحظات مكتوبة يدويًا أو رسومات منخفضة التباين.

## تحويل DjVu إلى نص – مثال كامل من البداية إلى النهاية

فيما يلي نسخة مختصرة تجمع كل شيء: تحميل DjVu متعدد الصفحات، معالجة كل صفحة مسبقًا، إجراء OCR، وحفظ النتيجة في ملف `.txt`.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

تشغيل هذا السكريبت ينشئ `sample_extracted.txt` مع محتوى كل صفحة مفصول بوضوح. إنه أسرع طريقة لـ **تحويل DjVu إلى نص** للفهرسة أو البحث أو الأرشفة.

## الخلاصة

لقد غطينا **كيفية إجراء OCR** على ملفات DjVu من البداية إلى النهاية، واستعرضنا طرقًا لـ **التعرف على النص من 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}