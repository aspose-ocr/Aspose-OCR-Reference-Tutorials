---
category: general
date: 2026-05-31
description: تعلم كيفية الحصول على درجات الثقة في OCR باستخدام C# أثناء استخراج النص
  من الصورة وقراءة صورة الإيصال باستخدام Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: ar
og_description: تتيح لك درجات ثقة OCR قياس الدقة؛ يوضح هذا الدليل كيفية استخراج النص
  من الصورة، والحصول على الصناديق المحيطة، وقراءة صورة الإيصال باستخدام Aspose OCR.
og_title: درجات ثقة OCR في C# – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: درجات الثقة في OCR باستخدام C# – دليل شامل
url: /ar/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# درجات ثقة OCR في C# – دليل شامل

هل تساءلت يومًا كيف تحصل على **درجات ثقة OCR** عندما تحتاج إلى *استخراج النص من صورة*؟ ربما تحاول **قراءة صورة إيصال** لتتبع النفقات وتريد معرفة الأحرف التي لا يكون المحرك متأكدًا منها. الخبر السار؟ مع Aspose.OCR يمكنك سحب نسب الثقة، ومربعات الإحاطة، والنص العادي من ملف JPG في بضع أسطر من C#.

في هذا الدرس سنستعرض كل ما تحتاج إلى معرفته: تثبيت المكتبة، تكوين المحرك لـ **أداء OCR على JPG**، استخراج درجات الثقة، وتفسير **مربعات إطارات OCR** التي تخبرك بمكان وجود كل حرف على الصفحة. في النهاية ستحصل على تطبيق وحدة تحكم جاهز للتشغيل يطبع كل حرف، وثقته، وموقعه — مثالي للتحقق من الإيصالات أو أي مستند ممسوح.

## ما ستتعلمه

- تثبيت Aspose.OCR عبر NuGet وإعداد محرك OCR أساسي.  
- تكوين `OcrOptions` لطلب إخراج نص عادي **مع درجات الثقة** و **مربعات الإحاطة**.  
- التكرار عبر `OcrResult` لـ **استخراج النص من صورة** سطرًا بسطر ورمزًا برمز.  
- معالجة المشكلات الشائعة مثل الملفات المفقودة، الأحرف ذات الثقة المنخفضة، والصيغ غير JPG.  
- توسيع المثال لمعالجة صور إيصالات متعددة في مجلد.

لا يلزم أي خبرة سابقة مع Aspose؛ فقط بيئة .NET تعمل وصورة إيصال (JPG) ترغب في اختبارها.

---

## الخطوة 1 – تثبيت Aspose.OCR وتحضير مشروعك

أولًا وقبل كل شيء: تحتاج إلى حزمة Aspose.OCR عبر NuGet. افتح طرفية في مجلد مشروعك وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** النسخة التجريبية المجانية تعمل حتى 200 صفحة، وهو أكثر من كافٍ لاختبار مسح الإيصالات.

بعد تثبيت الحزمة، أنشئ مشروع وحدة تحكم جديد (إذا لم يكن لديك واحد بالفعل):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

الآن يمكنك فتح الملف `Program.cs` المُنشأ والبدء بإضافة توجيهات using:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

هذه المساحات الاسمية تمنحك الوصول إلى `OcrEngine` و `OcrOptions` وأنواع النتائج التي سنحتاجها لاحقًا.

## الخطوة 2 – الحصول على درجات ثقة OCR ومربعات إطارات OCR

هذا هو جوهر الدرس. سنقوم بتكوين المحرك بحيث يأتي كل حرف مُعترف به مع **درجة ثقة** و **مربع إطارة** (المستطيل الذي يحيط بالحرف). عنوان H2 نفسه يحتوي على الكلمة المفتاحية الأساسية، مما يحقق قاعدة تحسين محركات البحث.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**لماذا تضمين درجات الثقة؟**  
درجة الثقة (0‑100٪) تخبرك بمدى تأكد المحرك من كل حرف. إذا كنت تُدخل النتيجة في منطق لاحق — مثل سير عمل موافقة النفقات — يمكنك رفض أو وضع علامة على الرموز ذات الثقة المنخفضة تلقائيًا.

**لماذا طلب مربعات الإطارات؟**  
مربعات الإطارات ضرورية عندما تحتاج إلى تمييز النص على الصورة الأصلية، استخراج مناطق فرعية، أو محاذاة نتائج OCR مع طبقة واجهة المستخدم. كل `character.Bounds` يعطيك إحداثيات X, Y, العرض، والارتفاع بالبكسل.

## الخطوة 3 – تنفيذ OCR على JPG واستخراج النص من الصورة

الآن نقوم فعليًا بتشغيل المحرك. استدعاء `Recognize()` يقوم بكل المعالجة الثقيلة ويعيد كائن `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

إذا كان مسار الصورة غير صحيح أو الملف ليس بتنسيق مدعوم، تقوم Aspose بإلقاء استثناء `FileNotFoundException` أو `UnsupportedImageFormatException`. غلف الاستدعاء في كتلة try/catch في الكود الإنتاجي للتعامل مع هذه الحالات بشكل سلس.

### استخراج النص العادي

إذا كنت تحتاج فقط إلى النص المتسلسل، يمكنك قراءة `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

ولكن لأننا طلبنا أيضًا درجات الثقة ومربعات الإطارات، سنقوم بالتكرار عبر البنية لرؤية تفاصيل كل حرف.

## الخطوة 4 – التكرار عبر السطور، الرموز، وعرض درجات ثقة OCR

إليك الحلقة التي تطبع كل حرف، وثقته، ومربع إطاره. هذا هو المكان الذي يبرز فيه مثال **قراءة صورة إيصال** حقًا.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

قد يبدو الناتج النموذجي كالتالي:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**تفسير الأرقام:**  
- **الثقة ≥ 90٪** – عادةً ما تكون مقبولة.  
- **الثقة 70‑89٪** – قد ترغب في التحقق مرة أخرى، خاصةً للأرقام في المبالغ.  
- **الثقة < 70٪** – فكر في وضع علامة للمراجعة اليدوية.

## الخطوة 5 – مثال كامل قابل للتنفيذ (مع معالجة الأخطاء)

بجمع كل شيء معًا، إليك برنامج كامل يمكنك نسخه ولصقه في `Program.cs`. يتضمن فحصًا بسيطًا للملفات المفقودة ويطبع رسالة ودية إذا فشل OCR.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### الناتج المتوقع

عند تشغيل `dotnet run` سيعرض الطرفية أولًا النص المتسلسل للإيصال، ثم قائمة بكل حرف مع درجة ثقته ومربع إطاره. إذا كانت ثقة حرف ما منخفضة، سترى نسبة أقل من 80، وهذا إشارة للتحقق من ذلك الجزء من الإيصال يدويًا.

## إضافي: معالجة إِيصالات متعددة في مجلد

إذا كان لديك مجموعة من ملفات JPG للإيصالات، غلف المنطق السابق داخل حلقة `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. تذكر إعادة ضبط `OcrEngine` لكل ملف، أو إنشاء نسخة جديدة داخل الحلقة لتجنب تسرب الحالة.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

المعالجة بالجملة مفيدة لاستيراد النفقات الليلي.

## الخاتمة

أصبح لديك الآن حل شامل من البداية إلى النهاية للحصول على **درجات ثقة OCR** في C#، **استخراج النص من صورة**، واسترجاع **مربعات إطارات OCR** أثناء **أداء OCR على JPG** مثل **قراءة صورة إيصال**. الكود مستقل تمامًا، يعمل مع أحدث نسخة من Aspose.OCR (اعتبارًا من 2026‑05‑31)، ويزودك بالبيانات الدقيقة التي تحتاجها لبناء خطوط معالجة مستندات موثوقة.

ما التالي؟ جرّب تصور مربعات الإطارات على الإيصال الأصلي باستخدام `System.Drawing` أو مكتبة واجهة مستخدم، أو مرّر الأحرف ذات الثقة المنخفضة إلى خدمة تحقق ثانوية. يمكنك أيضًا تجربة لغات مختلفة بتعيين `ocrEngine.Options.Language = OcrLanguage.French;` — الـ API يدعم العديد من اللغات.

برمجة سعيدة، ولتظل درجات الثقة لديك دائمًا مرتفعة! 

![مخرجات وحدة التحكم تظهر درجات ثقة OCR ومربعات الإطارات لإيصال

## ماذا يجب أن تتعلم بعد ذلك؟

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [كيفية الحصول على خيارات أحرف OCR للأحرف المعترف بها في التعرف على الصور](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}