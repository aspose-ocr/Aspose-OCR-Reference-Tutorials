---
category: general
date: 2026-05-25
description: كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور. تعلم التعرف على
  الأحرف الصينية من ملف JPG باستخدام Aspose.OCR في بضع خطوات بسيطة.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور. يوضح لك هذا
  الدليل كيفية التعرف على الأحرف الصينية من ملف JPG باستخدام Aspose.OCR.
og_title: كيفية استخدام OCR في C# – التعرف على النص الصيني من JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: كيفية استخدام OCR في C# – التعرف على النص الصيني من ملف JPG
url: /ar/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – التعرف على النص الصيني من JPG

هل تساءلت يومًا **كيفية استخدام OCR** لاستخراج الكلمات من صورة التقطتها بهاتفك؟ لست وحدك. في العديد من المشاريع الواقعية—مثل ماسحات الفواتير، تطبيقات الترجمة، أو إدخال البيانات الآلي—ستحتاج إلى **استخراج النص من الصورة** بسرعة وبشكل موثوق.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ **يتعرف على النص من ملفات JPG** ويتعامل أيضًا مع الحالة الصعبة **التعرف على الأحرف الصينية** باستخدام حزمة اللغة **OCR Chinese Simplified**. في النهاية ستحصل على تطبيق console مستقل يطبع السلسلة المكتشفة في نافذة الأوامر، دون الحاجة إلى تنزيلات يدوية إضافية.

> **ملاحظة سريعة:** يعمل الكود مع Aspose.OCR ≥ 23.7، الذي يجلب موارد اللغة تلقائيًا عند الاستخدام الأول. إذا كنت تستخدم نسخة أقدم، سيتعين عليك إضافة اللغة يدويًا.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (المثال يستهدف .NET 6، لكن .NET 5 يعمل أيضًا)
- نسخة حديثة من Visual Studio 2022 أو VS Code مع امتداد C#
- اتصال إنترنت لتنزيل اللغة لأول مرة
- صورة JPG تحتوي على نص صيني مبسط (سنسميها `chinese_sign.jpg`)

هذا كل شيء—بدون محركات OCR ثقيلة، بدون التعامل مع DLLs الأصلية. فقط بضع أوامر NuGet وقليل من أسطر الكود.

## الخطوة 1: تثبيت Aspose.OCR عبر NuGet

أولًا: نحتاج إلى مكتبة OCR. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو إذا كنت تفضّل واجهة Visual Studio، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages**، ابحث عن “Aspose.OCR”، ثم اضغط **Install**.

> **نصيحة احترافية:** حافظ على تحديث الحزم. حزم اللغات الجديدة وتحسينات الأداء تُضاف في كل إصدار فرعي.

## الخطوة 2: إنشاء مشروع Console جديد (إذا لم تقم بذلك بعد)

إذا كنت تبدأ من الصفر، أنشئ تطبيق console جديد:

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

الآن لديك ملف `Program.cs` جاهز لكود OCR.

## الخطوة 3: كتابة كود OCR – التعرف على الصيني المبسط من JPG

افتح `Program.cs` واستبدل محتوياته بما يلي. كل سطر مشروح حتى ترى *لماذا* نقوم بهذه الخطوة، وليس فقط *ماذا* نفعل.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### ما الذي يحدث خلف الكواليس؟

- **`OcrEngine.Language`** يخبر Aspose أي قاموس يستخدم. باختيار `ChineseSimplified`، نوجه المحرك للبحث عن حزمة اللغة الصينية المبسطة.
- **التنزيل لأول مرة**: عندما يتم تشغيل `Recognize`، يتواصل SDK مع CDN الخاص بـ Aspose، ينزل ملف اللغة ≈6 MB، يخزنه محليًا، ثم يواصل عملية OCR. الاستدعاءات اللاحقة تكون فورية.
- **`Image.FromFile`** يعمل مع أي تنسيق نقطي يمكن لـ .NET فك تشفيره—JPG، PNG، BMP—وبالتالي يمكنك **استخراج النص من الصورة** لملفات بأنواع متعددة، وليس JPG فقط.

## الخطوة 4: تشغيل التطبيق والتحقق من المخرجات

Build and run:

```bash
dotnet run
```

You should see something like:

```
=== Recognized Text ===
欢迎光临
```

إذا طبع الـ console نصًا غير مفهوم أو سلسلة فارغة، تحقق مرة أخرى من:

1. الصورة تحتوي فعليًا على أحرف صينية واضحة وعالية التباين.
2. مسار الملف صحيح (بدون مسافات زائدة أو امتدادات مفقودة).
3. جهازك يستطيع الوصول إلى `https://download.aspose.com` للحصول على حزمة اللغة.

## الخطوة 5: التعامل مع الحالات الحدية والمشكلات الشائعة

### 5.1 التعامل مع الصور منخفضة الجودة

تنخفض دقة OCR عندما تكون الصورة المصدرية غير واضحة، مشوشة، أو ذات إضاءة ضعيفة. حل سريع هو معالجة الصورة مسبقًا:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 التشغيل في بيئة بدون واجهة رسومية

إذا كنت تنشر إلى حاوية Linux بدون واجهة رسومية، تأكد من تثبيت مكتبة `libgdiplus` (المطلوبة لـ `System.Drawing`):

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 تخزين حزمة اللغة مؤقتًا يدويًا

يمكنك تنزيل ملف اللغة مرة واحدة وتوجيه Aspose إليه عبر واجهة برمجة التطبيقات `License`، مما يلغي الحاجة إلى الاتصال الشبكي مرة واحدة. هذا مفيد للسيناريوهات غير المتصلة.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## مثال كامل يعمل (الكل في واحد)

فيما يلي البرنامج *الكامل* الذي يمكنك نسخه ولصقه في `Program.cs`. لا توجد أجزاء مخفية، ولا سكريبتات خارجية.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### المخرجات المتوقعة

إذا كان JPG يحتوي على العبارة “欢迎光临”، سيطبع الـ console:

```
=== Recognized Text ===
欢迎光临
```

لا تتردد في استبدال الصورة بأي علامة صينية مبسطة أخرى، اسم شارع، أو ملصق منتج—المحرك سيبذل قصارى جهده.

## الخلاصة

لقد غطينا للتو **كيفية استخدام OCR** في C# **لاستخراج النص من الصورة**، مع التركيز على تحدي **التعرف على الأحرف الصينية** في **JPG**. من خلال الاستفادة من تنزيل اللغة الفوري في Aspose.OCR، يمكنك الحفاظ على خفة نشر تطبيقك مع دعم **OCR Chinese Simplified** مباشرةً.

ما التالي؟ جرّب هذه الأفكار:

- **Batch processing**: تكرار عبر مجلد من الصور وكتابة كل نتيجة إلى ملف CSV.
- **Combine with translation APIs**: تمرير السلسلة المعترف بها إلى Azure Translator لتطبيقات متعددة اللغات في الوقت الفعلي.
- **Explore other languages**: استبدال `OcrLanguage.ChineseSimplified` بـ `Japanese` أو `Arabic` وملاحظة كيف يتكيف الكود نفسه.

هل لديك أسئلة حول تحسين الأداء، الترخيص، أو دمج OCR في خدمة ويب؟ اترك تعليقًا أدناه—برمجة سعيدة!

---

![لقطة شاشة لمخرجات الـ console تُظهر كيفية استخدام OCR في C# للتعرف على النص الصيني من صورة JPG](ocr-chinese-demo.png "كيفية عرض مخرجات OCR في الـ console")

## دروس ذات صلة

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}