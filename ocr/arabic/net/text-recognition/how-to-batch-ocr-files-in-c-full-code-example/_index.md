---
category: general
date: 2026-02-17
description: كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) لعدة ملفات PDF وصور دفعة واحدة
  في C# باستخدام Aspose OCR. تعلم استخراج النص من PDF، تحويل PDF إلى نص، والتعرف على
  النص من الصور.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: ar
og_description: كيفية تنفيذ OCR دفعي لعدة مستندات في C# باستخدام Aspose OCR. احصل
  على كود خطوة بخطوة لاستخراج النص من PDF، تحويل PDF إلى نص، والتعرف على النص من الصور.
og_title: كيفية معالجة ملفات OCR دفعيًا في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: كيفية معالجة ملفات OCR دفعيًا في C# – مثال كامل للكود
url: /ar/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

عي". Keep.

Now produce final.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعي للملفات في C# – دليل كامل

هل تساءلت يومًا **كيفية تنفيذ OCR دفعي** لمجموعة من ملفات PDF والمسحات الضوئية دون كتابة حلقة منفصلة لكل ملف؟ لست وحدك. يواجه معظم المطورين هذه المشكلة عندما يحتاجون إلى استخراج النص من عشرات الصفحات دفعة واحدة. الخبر السار؟ مع Aspose OCR يمكنك تمرير مجموعة من الملفات إلى محرك واحد ودعه يتولى العمل الشاق.  

في هذا الدرس سنستعرض حلًا عمليًا يتيح لك **استخراج النص من pdf**، **تحويل pdf إلى نص**، و**التعرف على النص من الصور** جميعًا في تشغيل دفعي واحد. في النهاية ستحصل على تطبيق console جاهز للتنفيذ يطبع نتيجة OCR لكل صفحة، وستفهم السبب وراء كل خطوة لتتمكن من تعديلها وفقًا لمشاريعك الخاصة.

## المتطلبات المسبقة – ما تحتاجه قبل أن نبدأ

- **.NET 6.0 أو أحدث** (الكود يعمل أيضًا على .NET Framework، لكن يُنصح بـ .NET 6+)
- **حزمة Aspose.OCR عبر NuGet** – ثبّتها باستخدام `dotnet add package Aspose.OCR`
- بعض الملفات التجريبية: PDF متعدد الصفحات (`doc1.pdf`) وTIFF ممسوح ضوئيًا (`doc2.tif`). ضعها في مجلد يمكنك الإشارة إليه، مثل `C:\OCRSamples`.
- معرفة أساسية بلغة C# – يجب أن تكون مرتاحًا مع عبارات `using` والمجموعات.

> نصيحة محترف: إذا لم يكن لديك ترخيص، تقدم Aspose مفتاحًا مؤقتًا مجانيًا يزيل حد الـ 100 صفحة أثناء التطوير.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولًا، أنشئ مشروع console جديد (أو أضف إلى مشروع موجود) واستورد المساحات الاسمية المطلوبة.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **لماذا هذا مهم:** استيراد `Aspose.OCR.Image` يمنحك طريقة `ImageStream.FromFile` المريحة، التي تقسم صفحات PDF تلقائيًا إلى تدفقات صور منفصلة. هذه هي الصلصة السحرية التي تجعل المعالجة الدفعية سهلة بلا عناء.

## الخطوة 2: تهيئة محرك OCR

المحرك هو العنصر الأساسي الذي يتواصل مع محرك OCR الداخلي. تحتاج إلى نسخة واحدة فقط لكامل الدفعة.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **شرح:** إعادة استخدام نفس `OcrEngine` يقلل من استهلاك الذاكرة ويسرّع المعالجة لأن المكتبات الأصلية تبقى محملة بين الصفحات.

## الخطوة 3: بناء قائمة من تدفقات الصور

هنا نجمع كل المستندات التي نريد معالجتها. `ImageStream.FromFile` ذكي بما يكفي لتقسيم PDF إلى صفحات فردية، لذا يتحول PDF من ثلاث صفحات إلى ثلاث تدفقات منفصلة خلف الكواليس.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **حالة حافة:** إذا كان لديك مزيج من ملفات PDF، TIFF، JPEG أو PNG، فقط أضفها إلى نفس القائمة – Aspose يتعامل مع اكتشاف الصيغة تلقائيًا.

## الخطوة 4: تشغيل عملية OCR الدفعية

الآن نسلم القائمة إلى المحرك. `RecognizeBatch` تُعيد مجموعة من كائنات `OcrResult`، واحدة لكل صفحة.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **لماذا الدفعة؟** تشغيل OCR صفحةً بصفحة في حلقة يدوية يجبر المحرك على إعادة التهيئة في كل مرة، مما قد يضاعف زمن المعالجة. `RecognizeBatch` يبقي المحرك "دافئًا" ويُعيد النتائج فور توفرها.

## الخطوة 5: إخراج النص المُعترف به

أخيرًا، نمر على النتائج ونكتب نص كل صفحة إلى الـ console. هنا يمكنك استبدال `Console.WriteLine` بكتابة إلى ملف، إدخال إلى قاعدة بيانات، أو أي إجراء لاحق آخر.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### النتيجة المتوقعة في الـ Console

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

إذا شغّلت البرنامج مع الملفات التجريبية، سترى كتلة نص لكل صفحة، مما يثبت أنك نجحت في **استخراج نص من pdf ممسوح** في تمريرة واحدة.

## التعامل مع المشكلات الشائعة

| المشكلة | لماذا يحدث | الحل السريع |
|---------|------------|-------------|
| **أخطاء نفاد الذاكرة** | ملفات PDF الكبيرة تُنتج العديد من الصور عالية الدقة. | حدِّد DPI عند تحميل PDFs: `ocrEngine.Settings.ImageDpi = 200;` |
| **حروف غير مفهومة** | المسح الضوئي منخفض الجودة أو يستخدم لغة غير مدعومة. | عيّن اللغة صراحةً: `ocrEngine.Language = Language.English;` |
| **نتائج جزئية** | القائمة الدفعية تحتوي على ملف تالف. | غلف `RecognizeBatch` بكتلة `try/catch` وسجِّل `e.Message` للملف المسبب. |
| **عنق زجاجة في الأداء** | التشغيل على خيط واحد في جهاز متعدد الأنوية. | استخدم `Parallel.ForEach` مع نسخ منفصلة من `OcrEngine` لكل خيط (متقدم). |

## إضافي: حفظ نتائج OCR إلى ملفات نصية

إذا رغبت في حفظ ملف `.txt` منفصل لكل صفحة، أضف كتلة كتابة صغيرة داخل الحلقة:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

الآن حولت **تحويل pdf إلى نص** إلى مجلد من ملفات نصية عادية—مثالي للفهرسة أو البحث لاحقًا.

## مثال كامل جاهز للتنفيذ

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. لا توجد تبعيات مخفية، ولا سكريبتات خارجية.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

شغّل `dotnet run` من مجلد المشروع وشاهد الـ console يملأ بالنص المستخرج. هذا هو **كيفية تنفيذ OCR دفعي** لمجموعة من المستندات في بضع أسطر من C# فقط.

## ما تم تغطيته – ملخص سريع

- إعداد تطبيق console بـ .NET وتثبيت Aspose.OCR.  
- إنشاء نسخة واحدة من `OcrEngine` لجعل العملية فعّالة.  
- بناء قائمة من كائنات `ImageStream` التي تقسم PDFs إلى صفحات تلقائيًا.  
- تنفيذ `RecognizeBatch` لـ **استخراج النص من pdf** وصيغ الصور الأخرى دفعة واحدة.  
- طباعة النتائج وحفظها اختياريًا كملفات `.txt` منفصلة، مكملًا سير عمل **تحويل pdf إلى نص**.  

## الخطوات التالية والمواضيع ذات الصلة

- **التوسيع**: استخدم `Parallel.ForEach` مع مجموعة من كائنات `OcrEngine` لمعالجة مئات الملفات بشكل متزامن.  
- **حزم اللغات**: استبدل `Language.English` بـ `Language.French` أو حمّل قاموسًا مخصصًا عندما تحتاج إلى **التعرف على النص من الصور** بلغات أخرى.  
- **ما بعد المعالجة**: مرّر مخرجات OCR عبر مدقق إملائي أو محلل لغة طبيعية لتحسين الدقة في المستندات الممسوحة.  
- **مكتبات بديلة**: قارن بين Aspose OCR و Tesseract.NET إذا كنت تبحث عن خيار مفتوح المصدر—كلاهما يستطيع **استخراج نص من pdf ممسوح** لكن يختلفان في الترخيص والدقة الجاهزة.

---

![how to batch OCR example](alt="مثال على تنفيذ OCR دفعي")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}