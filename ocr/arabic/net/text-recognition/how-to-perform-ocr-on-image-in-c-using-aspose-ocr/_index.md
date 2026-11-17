---
category: general
date: 2026-10-11
description: تعلم كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على الصور في C# باستخدام
  Aspose.OCR، بما في ذلك تثبيت System.Drawing.Common واستخراج النص من ملفات JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: ar
lastmod: 2026-10-11
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في C# باستخدام Aspose.OCR.
  يوضح هذا الدليل كيفية تثبيت System.Drawing.Common، تحميل صورة للتعرف الضوئي على
  الأحرف، واستخراج النص من ملف JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: إجراء التعرف الضوئي على الأحرف (OCR) على صورة في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: كيفية إجراء OCR على صورة في C# باستخدام Aspose.OCR
url: /ar/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR على صورة في C# باستخدام Aspose.OCR

إذا كنت بحاجة إلى **perform OCR on image** ملفات في تطبيق .NET، يوضح لك هذا الدليل حلاً كاملاً. باستخدام Aspose.OCR يمكنك بسرعة **recognize text from picture** ملفات مثل JPGs وعرض النتيجة في نافذة وحدة التحكم.

ستتعلم كيف:

* **install System.Drawing.Common package** – المكتبة التي توفر الفئة `Image`,
* **load image for OCR** – قراءة ملف JPEG أو PNG إلى الذاكرة,
* تكوين نموذج اللغة,
* **perform OCR on image** وأخيرًا,
* **extract text from JPG** وإخراجها.

تم كتابة الخطوات لـ .NET 6+، لكنها تعمل أيضًا مع .NET Framework 4.6.1 أو أحدث.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | يوفر بيئة التشغيل لتطبيق وحدة التحكم C#. |
| Visual Studio 2022 (or any IDE) | يسهل إضافة حزم NuGet وتشغيل البرنامج. |
| Internet connection (first run only) | Aspose.OCR يقوم بتنزيل وحدة اللغة تلقائيًا. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | تُستخدم لتوضيح **extract text from JPG**. |

---

## الخطوة 1: تثبيت حزمة System.Drawing.Common

حزمة NuGet `System.Drawing.Common` توفر الفئة `Image` التي ستقوم بـ **load image for OCR**. افتح وحدة تحكم مدير الحزم Package Manager Console وشغّل:

```powershell
Install-Package System.Drawing.Common
```

> **نصيحة احترافية:** استهدف `net6.0-windows` أو أضف `<UseWindowsForms>true</UseWindowsForms>` إلى ملف المشروع إذا واجهت تحذيرات خاصة بالمنصة على Linux/macOS.

---

## الخطوة 2: إضافة حزمة Aspose.OCR NuGet

تحتوي Aspose.OCR على محرك OCR ونماذج اللغة. قم بتثبيتها باستخدام:

```powershell
Install-Package Aspose.OCR
```

الحزمة خفيفة الوزن؛ يتم تنزيل بيانات اللغة المطلوبة (مثال: سيريلي) في المرة الأولى التي تقوم فيها بتعيين `OcrEngine.Language`.

---

## الخطوة 3: كيفية تحميل الصورة لـ OCR

تحميل الصورة هو الخطوة العملية الأولى قبل أن تتمكن من **perform OCR on image**. طريقة `Image.FromFile` تقرأ أي تنسيق يدعمه GDI+، بما في ذلك JPG و PNG و BMP و TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*إذا كان الملف غير موجود، يتم إلقاء استثناء `FileNotFoundException` – غلف الاستدعاء بكتلة try/catch للشفرة الإنتاجية.*

---

## الخطوة 4: تكوين المحرك و **perform OCR on image**

أنشئ كائن `OcrEngine`، اختر نموذج اللغة، عيّن الصورة المحمَّلة، واستدعِ `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

طريقة `Recognize()` تُعيد كائن `OcrResult` يحتوي على النص المستخرج، درجات الثقة، ومربعات الإحاطة. يتم تنزيل وحدة اللغة تلقائيًا في الاستخدام الأول، لذا لا تحتاج إلى ملفات إضافية.

---

## الخطوة 5: **Extract text from JPG** وعرضه

الآن يمكنك **recognize text from picture** وإخراج النتيجة. خاصية `Text` في `OcrResult` تحتوي على السلسلة النصية العادية.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### مخرجات وحدة التحكم المتوقعة

```
Recognized text:
Пример текста на кириллице
```

إذا كانت الصورة المصدر تحتوي على نص إنجليزي، ستكون النتيجة الجملة الإنجليزية التي وضعتها في الصورة.

---

## الحالات الخاصة ونصائح الممارسات المثلى

| الحالة | التوصية |
|-----------|----------------|
| **Large images ( > 5 MB )** | قم بإعادة تحجيم الصورة إلى ≤ 2000 px على الجانب الأطول قبل OCR لتقليل استهلاك الذاكرة وتحسين السرعة. |
| **Multiple languages in one picture** | استدعِ `ocrEngine.AddLanguage(OcrLanguage.English)` بالإضافة إلى السيريلي، ثم عيّن `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | زد التباين باستخدام `System.Drawing.Graphics` قبل تمرير الـ bitmap إلى المحرك. |
| **Running on Linux/macOS** | تأكد من تثبيت الاعتماد الأصلي `libgdiplus` (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | أعد استخدام نفس كائن `OcrEngine` واستبدل فقط `ocrEngine.Image` لتجنب تحميل الوحدة المتكرر. |

---

## برنامج كامل قابل للتنفيذ

فيما يلي تطبيق وحدة التحكم الكامل الذي يدمج جميع الخطوات السابقة. انسخ الشيفرة إلى مشروع C# وحدة تحكم جديد، استبدل مسار الصورة، وشغّله.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**تشغيل البرنامج** يطبع السلسلة المعترف بها إلى وحدة التحكم، مؤكدًا أنك نجحت في **performed OCR on image** و **extract text from JPG**.

---

## الخلاصة

أنت الآن تعرف كيف **perform OCR on image** ملفات في C# باستخدام Aspose.OCR، بدءًا من تثبيت **System.Drawing.Common package** المطلوبة إلى **load image for OCR**، اختيار اللغة المناسبة، وأخيرًا **extract text from JPG**. هذا المثال المتكامل يمنحك أساسًا قويًا لبناء خطوط معالجة مستندات أكثر تقدمًا، مثل معالجة دفعات من مجلدات الصور أو دمج OCR في واجهة برمجة تطبيقات ويب.

### ما التالي؟

- استكشف **recognize text from picture** في ملفات PDF عن طريق تحويل كل صفحة إلى صورة أولاً.
- جرّب خصائص `OcrEngine` مثل `Resolution` و `Threshold` و `MaxProcessingTime` لضبط الدقة على المسحات الضوضائية.
- ادمج مخرجات OCR مع مكتبة معالجة اللغة الطبيعية لتصنيف المحتوى المستخرج تلقائيًا.

لا تتردد في تعديل الشيفرة لتدعم صيغ صور أخرى، إضافة معالجة الأخطاء، أو دمجها في تطبيقات أكبر. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة في C# – دليل Aspose OCR الكامل](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [استخراج نص الصورة في C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية استخراج نص الصورة من تدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}