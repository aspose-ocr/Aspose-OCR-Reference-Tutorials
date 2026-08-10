---
category: general
date: 2026-07-18
description: استخراج النص من PNG باستخدام Aspose OCR في C#. تعلم كيفية تحويل الصورة
  إلى نص، وإجراء التعرف الضوئي على الأحرف على الصورة، والتعرف بسرعة على النص السيريلي.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from png
- convert image to text
- perform ocr on image
- recognize cyrillic text
- ocr cyrillic image
language: ar
lastmod: 2026-07-18
og_description: استخراج النص من ملف PNG باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  تحويل الصورة إلى نص، وإجراء OCR على الصورة، والتعرف على النص السيريلي في بضع أسطر
  فقط من C#.
og_image_alt: Screenshot showing C# console output after extracting text from a PNG
  image
og_title: استخراج النص من PNG باستخدام Aspose OCR – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Extract text from PNG using Aspose OCR in C#. Learn how to convert
    image to text, perform OCR on image and recognize Cyrillic text quickly.
  headline: Extract Text from PNG with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from PNG using Aspose OCR in C#. Learn how to convert
    image to text, perform OCR on image and recognize Cyrillic text quickly.
  name: Extract Text from PNG with Aspose OCR – Complete C# Guide
  steps:
  - name: Why Each Piece Matters
    text: '* **`var ocrEngine = new OcrEngine();`** – This creates the engine object
      that holds all OCR settings. Think of it as the “brain” that will analyze the
      pixels. * **`ocrEngine.Language = OcrLanguage.Cyrillic;`** – By explicitly setting
      the language, you tell the engine which character set to expect. '
  - name: 4.1 Dealing with Low‑Resolution PNGs
    text: 'OCR accuracy drops when the source image is under 300 dpi. You can pre‑process
      the image using `System.Drawing` or `ImageSharp` to upscale it:'
  - name: 4.2 Recognizing Multiple Languages
    text: 'If you need to **perform OCR on image** files that contain both Latin and
      Cyrillic characters, set a composite language:'
  - name: 4.3 Saving the Result to a File
    text: 'Instead of printing to the console, you might want a persistent text file:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: استخراج النص من PNG باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-text-from-png-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG باستخدام Aspose OCR – دليل C# الكامل

هل احتجت يومًا إلى **استخراج النص من PNG** لكنك لم تكن متأكدًا أي مكتبة يمكنها التعامل مع الأحرف السيريلية مباشرةً؟ لست وحدك. في العديد من المشاريع—مثل معالجة الإيصالات الآلية أو أرشفة المستندات متعددة اللغات—إمكانية **تحويل الصورة إلى نص** هي مشكلة يومية.  

الأخبار السارة؟ باستخدام Aspose.OCR يمكنك **إجراء OCR على الصورة** في بضع أسطر فقط، وتقوم المكتبة حتى بتحميل وحدات اللغة اللازمة تلقائيًا. أدناه ستشاهد كيف **تتعرف على النص السيريليني** في PNG وتحصل على سلسلة نصية نظيفة جاهزة للمعالجة الإضافية.

## ما يغطيه هذا الدرس

* تثبيت حزمة Aspose.OCR عبر NuGet  
* تهيئة محرك OCR في C#  
* اختيار نموذج اللغة **Cyrillic** (حتى تتمكن من **التعرف على النص السيريليني**)  
* تمرير ملف PNG إلى المحرك والسماح له **بإجراء OCR على الصورة** تلقائيًا  
* إخراج النتيجة إلى وحدة التحكم أو إلى ملف  

لا أدوات خارجية، ولا تحميل يدوي لملفات اللغة—فقط كود C# نقي يمكنك وضعه في أي مشروع .NET.

---

![مخطط سير عمل OCR – استخراج النص من PNG](/images/ocr-workflow.png "مخطط يوضح كيفية معالجة صورة PNG وتحويلها إلى نص باستخدام Aspose OCR")

*نص بديل للصورة: “مخطط يوضح عملية استخراج النص من PNG باستخدام Aspose OCR في C#.”*

## المتطلبات المسبقة

قبل أن نغوص في التفاصيل، تأكد من توفر ما يلي:

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7.2+) | بيئة تشغيل حديثة توفر أحدث ميزات اللغة. |
| Visual Studio 2022 (أو أي محرر تفضله) | يسهل إضافة حزم NuGet وتشغيل تطبيق وحدة التحكم. |
| صورة PNG تحتوي على أحرف سيريلية (مثال: `sample_cyrillic.png`) | هذا هو الملف الذي سنمرره إلى محرك OCR. |
| اتصال بالإنترنت (التشغيل الأول سيحمّل وحدة اللغة السيريلية) | Aspose.OCR يجلب حزم اللغة عند الحاجة. |

هذا كل شيء—لا ملفات DLL إضافية، ولا خدمات خارجية. جاهز؟ لنبدأ.

## الخطوة 1: تثبيت Aspose.OCR عبر NuGet

للحفاظ على النظافة، سننشئ مشروع وحدة تحكم جديد تمامًا ونضيف مكتبة OCR.

```bash
dotnet new console -n OcrCyrillicDemo
cd OcrCyrillicDemo
dotnet add package Aspose.OCR
```

تشغيل أمر `dotnet add package` يجلب أحدث نسخة مستقرة من Aspose.OCR من NuGet، والتي تشمل محرك OCR الأساسي لكن **ليس** حزم اللغة—فهي تُحمَّل تلقائيًا عند تحديد لغة.

> **نصيحة احترافية:** إذا كنت تستهدف .NET Framework، افتح مدير حزم NuGet في Visual Studio وابحث عن “Aspose.OCR”. الحزمة نفسها تعمل عبر جميع بيئات التشغيل.

## الخطوة 2: إنشاء برنامج C# بسيط

افتح `Program.cs` واستبدل محتوياته بالمثال الكامل أدناه. هذا المقتطف يقوم بكل شيء: يهيئ المحرك، يختار نموذج السيريلية، يقرأ PNG، ويطبع النص المتعرف عليه.

```csharp
using System;
using Aspose.OCR;

namespace OcrCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // ---------------------------------------------------------
            // Step 2.1: Instantiate the OCR engine – the heart of the process
            // ---------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------
            // Step 2.2: Choose the Cyrillic language model.
            // Aspose will download the necessary module on first use.
            // ---------------------------------------------------------
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // ---------------------------------------------------------
            // Step 2.3: Define the path to the PNG you want to convert.
            // You can also accept this as a command‑line argument.
            // ---------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\sample_cyrillic.png";

            // ---------------------------------------------------------
            // Step 2.4: Perform OCR on the image.
            // RecognizeImage returns a string with the extracted text.
            // ---------------------------------------------------------
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // ---------------------------------------------------------
            // Step 2.5: Output the result – you could write to a file instead.
            // ---------------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### لماذا كل جزء مهم

* **`var ocrEngine = new OcrEngine();`** – ينشئ كائن المحرك الذي يحمل جميع إعدادات OCR. فكر فيه كـ “العقل” الذي سيحلل البكسلات.  
* **`ocrEngine.Language = OcrLanguage.Cyrillic;`** – بتحديد اللغة صراحةً، تخبر المحرك ما مجموعة الأحرف التي يتوقعها. هذا يحسّن الدقة بشكل كبير للنصوص السيريلية ويُطلق تحميلًا تلقائيًا لحزمة اللغة (بدون خطوات يدوية).  
* **`RecognizeImage(imagePath)`** – الطريقة تقرأ ملف PNG، تشغّل خوارزميات OCR، وتعيد سلسلة نصية عادية. هذه هي عملية **تحويل الصورة إلى نص** الأساسية.  
* **`Console.WriteLine`** – طريقة مباشرة للتحقق من نجاح الاستخراج. في التطبيقات الواقعية قد تخزن السلسلة في قاعدة بيانات أو تمرّرها إلى خدمة ترجمة.

## الخطوة 3: تشغيل التطبيق

من الطرفية، نفّذ:

```bash
dotnet run
```

التشغيل الأول سيظهر شريط تقدم قصير بينما يقوم Aspose بتحميل وحدة اللغة السيريلية (عادةً بضع ميغابايت). بعد ذلك، سترى شيئًا مثل:

```
=== Extracted Text ===
Пример текста на кириллице.
```

إذا كان الإخراج مشوشًا، تحقق مرة أخرى من أن الصورة تحتوي فعلاً على أحرف سيريلية واضحة وأن مسار الملف صحيح.

## الخطوة 4: معالجة الحالات الشائعة

### 4.1 التعامل مع PNG منخفض الدقة

تنخفض دقة OCR عندما تكون الصورة الأصلية أقل من 300 dpi. يمكنك معالجة الصورة مسبقًا باستخدام `System.Drawing` أو `ImageSharp` لتكبيرها:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;
using System.Drawing.Imaging;

// Load, upscale, and save a temporary higher‑resolution copy.
using (var original = new Bitmap(imagePath))
{
    var upscale = new Bitmap(original.Width * 2, original.Height * 2);
    using (var g = Graphics.FromImage(upscale))
    {
        g.InterpolationMode = InterpolationMode.HighQualityBicubic;
        g.DrawImage(original, 0, 0, upscale.Width, upscale.Height);
    }
    upscale.Save("temp_upscaled.png", ImageFormat.Png);
    recognizedText = ocrEngine.RecognizeImage("temp_upscaled.png");
}
```

### 4.2 التعرف على لغات متعددة

إذا كنت بحاجة إلى **إجراء OCR على الصورة** التي تحتوي على أحرف لاتينية وسيريلية معًا، عيّن لغة مركبة:

```csharp
ocrEngine.Language = OcrLanguage.Cyrillic | OcrLanguage.English;
```

سيحاول المحرك اكتشاف كل نص تلقائيًا.

### 4.3 حفظ النتيجة إلى ملف

بدلاً من الطباعة إلى وحدة التحكم، قد ترغب في ملف نصي دائم:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognizedText);
Console.WriteLine("Text saved to extracted_text.txt");
```

## الخطوة 5: نصائح لـ OCR جاهز للإنتاج

* **تخزين وحدات اللغة مؤقتًا** – بعد التحميل الأول، تُحفظ الملفات في مجلد مؤقت للمستخدم. في بيئة الخادم، انسخها إلى موقع دائم وعيّن `OcrEngine.LanguageFolder` إلى هناك.  
* **ضبط `ocrEngine.Config`** – يمكنك تعديل تقليل الضوضاء، التحويل إلى ثنائي، واكتشاف الدوران للحصول على نتائج أفضل في المستندات الممسوحة.  
* **المعالجة الدفعية** – غلف استدعاء التعرف داخل حلقة `foreach` لمعالجة العشرات من PNGs. تذكّر إعادة استخدام نفس كائن `OcrEngine` لتجنب تحميل الوحدات المتكرر.

---

## الخلاصة

أصبح لديك الآن مثال عملي من البداية إلى النهاية **يستخرج النص من ملفات PNG** باستخدام Aspose OCR في C#. باتباع الخطوات أعلاه يمكنك **تحويل الصورة إلى نص**، **إجراء OCR على الصورة**، و**التعرف على النص السيريليني** بثقة، مع ترك المكتبة تدير وحدات اللغة لك.  

من هنا، يمكنك توسيع الحل: إضافة إخراج PDF، دمجه مع Azure Functions للمعالجة بدون خادم، أو تجميع الكود في مكتبة فئات قابلة لإعادة الاستخدام. الاحتمالات بقدر ما تواجهه من أنظمة كتابة.

هل لديك أسئلة حول التعامل مع أبجديات أخرى، تحسين الأداء، أو التكامل مع واجهة مستخدم؟ اترك تعليقًا، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية استخراج النص من الصورة عبر إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [تحويل الصورة إلى نص – إجراء OCR على الصورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}