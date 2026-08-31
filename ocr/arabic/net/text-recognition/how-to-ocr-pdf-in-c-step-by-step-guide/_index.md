---
category: general
date: 2025-12-29
description: تعلم كيفية التعرف الضوئي على الأحرف (OCR) لملفات PDF باستخدام C# واستخراج
  النص من صفحات PDF. يغطي هذا الدرس أيضًا تحويل PDF إلى نص وقراءة صفحات PDF باستخدام
  تقنيات C#.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: ar
og_description: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام C# موضح في دليل
  مختصر. احصل على الكود الكامل لاستخراج النص من PDF، تحويل PDF إلى نص، وقراءة صفحة
  PDF باستخدام C#.
og_title: كيفية إجراء OCR لملف PDF في C# – دليل برمجة شامل
tags:
- OCR
- C#
- PDF processing
title: كيفية تحويل PDF إلى نص باستخدام OCR في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص (OCR) لملف PDF في C# – دليل خطوة بخطوة

هل تساءلت يومًا **كيف تقوم بعمل OCR لملفات PDF** مباشرةً من تطبيق C# الخاص بك؟ ربما لديك مجموعة من الفواتير الممسوحة ضوئيًا وتحتاج إلى استخراج النص دون النسخ واللصق يدويًا. هذه مشكلة شائعة، خاصةً عندما تكون ملفات PDF مبنية على صور وتفشل طرق استخراج النص التقليدية.  

في هذا الدرس سنستعرض حلًا كاملًا وجاهزًا للتنفيذ لا يوضح لك فقط **كيفية عمل OCR لملف PDF** بل يوضح أيضًا كيفية *استخراج النص من PDF*، *تحويل PDF إلى نص*، و*قراءة صفحة PDF باستخدام C#* باستخدام مكتبة Aspose.OCR. لا مراجع غامضة—فقط الكود الذي يمكنك وضعه في Visual Studio والبدء في التجربة.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)  
- حزمة **Aspose.OCR** عبر NuGet – تثبيت باستخدام `dotnet add package Aspose.OCR`  
- ملف PDF ممسوح ضوئيًا (مثال: `invoice.pdf`) موجود في مجلد يمكنك الإشارة إليه  
- إلمام أساسي بتطبيقات C# console  

هذا كل شيء. إذا كان لديك مشروع بالفعل، فقط أضف الحزمة وستكون جاهزًا للبدء.

## الخطوة 1: إعداد المشروع وإضافة Aspose.OCR

أولاً، أنشئ مشروع console جديد (أو استخدم مشروعًا موجودًا) وأضف مكتبة OCR.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

لماذا هذه الخطوة مهمة: تقوم Aspose.OCR بالمعالجة الثقيلة لتحليل الصور، واكتشاف التخطيط، والتعرف على الأحرف. بدونها سيتعين عليك تجميع rasterizer، ومحرك Tesseract، والكثير من الكود الوسيط.

## الخطوة 2: استيراد المساحات الاسمية (Namespaces) وتحضير محرك OCR

الآن افتح `Program.cs` (أو أي ملف .cs تفضله) وأضف توجيهات `using` المطلوبة.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

إنشاء المحرك سهل، لكننا سنقوم أيضًا بتكوين بعض الخيارات التي تحسن الدقة في مسحات الفواتير النموذجية.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**نصيحة احترافية:** إذا كنت تعرف اللغة مسبقًا، قم بتعيين `Language` صراحةً؛ فهذا يسرّع العملية.

## الخطوة 3: الإشارة إلى ملف PDF الخاص بك

حدد المسار المطلق أو النسبي إلى ملف PDF الذي تريد معالجته. من أجل هذا المثال سنفترض أن الملف موجود في مجلد اسمه `Samples`.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

التحقق من وجود الملف خطوة صغيرة، لكنها تحميك من استثناءات غامضة لاحقًا.

## الخطوة 4: اختيار الصفحة (الصفحات) للقراءة

يمكن أن يحتوي PDF على عشرات الصفحات، لكن غالبًا ما تحتاج إلى صفحة معينة—مثلاً، الصفحة الثانية من الفاتورة حيث يظهر المبلغ الإجمالي. تسمح لك طريقة `RecognizePdf` باستهداف صفحة واحدة أو المستند بالكامل.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

إذا كنت تريد *تحويل PDF إلى نص* للمستند بأكمله، ما عليك سوى حذف معامل `pageNumber`:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## الخطوة 5: عرض أو حفظ النص المستخرج

الآن بعد أن أنجز محرك OCR مهمته، يمكنك إما طباعة النص إلى وحدة التحكم، أو كتابته إلى ملف `.txt`، أو إرساله إلى نظام آخر (مثل قاعدة بيانات).

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**لماذا هذا مهم:** من خلال حفظ المخرجات تنشئ قطعة قابلة لإعادة الاستخدام—مثالية للتحليلات اللاحقة أو فهرسة البحث.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك برنامج مستقل يمكنك نسخه ولصقه في `Program.cs` وتشغيله فورًا.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

إذا كان PDF يحتوي على مسحات واضحة وعالية الدقة، ستكون النتيجة شبه مثالية. قد تحتاج الصور ذات الجودة المنخفضة إلى معالجة مسبقة إضافية (مثل زيادة DPI أو تطبيق فلاتر)؛ يمكن تعديل `ImagePreprocessingOptions` في Aspose.OCR لتناسب هذه الحالات.

## أسئلة شائعة وحالات خاصة

### 1️⃣ ماذا لو كان PDF محميًا بكلمة مرور؟

طريقة التحميل الزائدة `RecognizePdf` في Aspose.OCR تقبل كائن `PdfLoadOptions` حيث يمكنك تعيين كلمة المرور:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ هل يمكنني عمل OCR للمستند بالكامل مرة واحدة؟

نعم—فقط استدعِ `RecognizePdf(pdfFilePath)` دون تحديد رقم الصفحة. تُعيد الطريقة كائن `OcrResult` واحد يحتوي على النص المدمج من جميع الصفحات.

### 3️⃣ كيف يختلف هذا عن “استخراج النص من PDF” باستخدام مكتبة تعتمد على النص؟

استخراج النص النقي (مثلاً باستخدام iTextSharp) يعمل فقط على ملفات PDF التي تحتوي بالفعل على نص قابل للتحديد. **كيفية عمل OCR لملف PDF** ضروري عندما يكون PDF عبارة عن مجموعة من الصور، مثل الفواتير الممسوحة ضوئيًا. في هذه الحالات، يقوم محرك OCR بالتعرف البصري على الأحرف لتحويل الصور إلى نص قابل للبحث.

### 4️⃣ ماذا عن الأداء مع ملفات PDF الكبيرة؟

وقت المعالجة يزداد تقريبًا بشكل خطي مع عدد الصفحات ودقة الصورة. للمهام الضخمة، ضع في الاعتبار:
- تشغيل OCR بالتوازي (`Parallel.ForEach`)  
- تقليل DPI للصورة قبل OCR (`Resolution = 150`)  
- تخزين كائن `OcrEngine` في الذاكرة بدلاً من إعادة إنشائه لكل ملف

### 5️⃣ هل هناك طريقة للحصول على إطارات الحدود (bounding boxes) لكل كلمة؟

`OcrResult` يوفّر مجموعة من كائنات `OcrRegion`، كل منها يحتوي على إحداثيات. يمكنك التجول عبرها لبناء ملفات PDF قابلة للبحث أو لتسليط الضوء على النتائج في واجهة المستخدم.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## نصائح لتطبيقات جاهزة للإنتاج

- **معالجة الأخطاء:** ضع استدعاءات OCR داخل كتل try/catch لتظهر الاستثناءات الخاصة بالمكتبة.  
- **التسجيل (Logging):** سجّل أرقام الصفحات وأوقات المعالجة؛ فهي تساعد في اكتشاف المسحات المشكلة.  
- **إدارة الذاكرة:** حرّر كائنات `Bitmap` الكبيرة إذا قمت بتحويل صفحات PDF إلى صور يدويًا قبل OCR.  
- **الأمان:** لا تخزّن ملفات PDF الأصلية على أقراص غير آمنة؛ فكر في بثها مباشرةً إلى محرك OCR.  

## الخاتمة

الآن لديك إجابة كاملة وشاملة على **كيفية عمل OCR لملف PDF** باستخدام C#. غطى الدرس كل شيء من تثبيت Aspose.OCR، اختيار صفحة محددة، استخراج النص، ومعالجة الحالات الخاصة الشائعة. مع هذه الأساسيات يمكنك *استخراج النص من PDF*، *تحويل PDF إلى نص*، و*قراءة صفحة PDF باستخدام C#* لأي خط أنابيب معالجة مستندات تبنيه.

هل أنت مستعد للخطوة التالية؟ جرّب إمداد مخرجات OCR إلى محرك بحث نص كامل مثل Lucene.NET، أو أنشئ ملفات PDF قابلة للبحث عن طريق وضع النص المعترف به فوق الصور الأصلية. السماء هي الحد، وقد حصلت الآن على الأدوات للوصول إلى هناك.

![مثال على كيفية عمل OCR لملف PDF](image-placeholder.png "توضيح عملية OCR على صفحة PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}