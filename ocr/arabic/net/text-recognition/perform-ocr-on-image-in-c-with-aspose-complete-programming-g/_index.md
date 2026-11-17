---
category: general
date: 2026-06-16
description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose OCR
  في C#. تعلم خطوة بخطوة كيفية الحصول على نتائج JSON، ومعالجة الملفات، وحل المشكلات
  الشائعة.
draft: false
keywords:
- perform OCR on image
- Aspose OCR C#
- JSON result handling
- C# image recognition
- OCR engine configuration
language: ar
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام Aspose
  OCR في C#. يشرح هذا الدليل مخرجات JSON وإعداد المحرك والنصائح العملية.
og_title: إجراء OCR على صورة في C# – دليل Aspose OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Perform OCR on image using Aspose OCR in C#. Learn step‑by‑step how
    to get JSON results, handle files, and troubleshoot common issues.
  headline: Perform OCR on Image in C# with Aspose – Complete Programming Guide
  type: TechArticle
- questions:
  - answer: Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF. If you need to work
      with PDFs, convert each page to an image first (Aspose.PDF can help).
    question: What image formats are supported?
  - answer: Yes – set `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON
      is preferred when you need more metadata.
    question: Can I get plain text instead of JSON?
  - answer: Feed each page image to `RecognizeImage` in a loop and concatenate the
      results, or use `RecognizePdf` which returns a combined JSON structure.
    question: How do I handle multi‑page documents?
  - answer: For batch processing, reuse a single `OcrEngine` instance rather than
      creating a new one per image. Also, enable `RecognitionMode.Fast` if accuracy
      can be traded for speed.
    question: Performance concerns?
  - answer: Without a license, the output JSON will include a watermark field. Apply
      your license early in `Main` with `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.
    question: License warnings?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: تنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في C# باستخدام Aspose – دليل
  برمجة شامل
url: /ar/net/text-recognition/perform-ocr-on-image-in-c-with-aspose-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على صورة في C# – دليل برمجة شامل

هل احتجت يومًا إلى **تنفيذ OCR على صورة** لكن لم تكن متأكدًا من كيفية تحويل البكسلات الخام إلى نص قابل للاستخدام؟ لست وحدك. سواءً كنت تقوم بمسح الفواتير، استخراج البيانات من جوازات السفر، أو رقمنة المستندات القديمة، فإن القدرة على **تنفيذ OCR على صورة** برمجيًا تُغيّر قواعد اللعبة لأي مطور .NET.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح بالضبط كيفية **تنفيذ OCR على صورة** باستخدام مكتبة Aspose.OCR، التقاط النتائج بصيغة JSON، وحفظها للمعالجة اللاحقة. في النهاية ستحصل على تطبيق Console جاهز للتنفيذ، شرح واضح لكل خطوة إعداد، وبعض النصائح الاحترافية لتجنب المشكلات الشائعة.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث مثبت (يمكنك تحميله من موقع مايكروسوفت).  
- ترخيص صالح لـ Aspose.OCR أو نسخة تجريبية مجانية – المكتبة تعمل بدون ترخيص لكنها تضيف علامة مائية.  
- ملف صورة (PNG، JPEG، أو TIFF) تريد **تنفيذ OCR على صورة** له – في هذا الدليل سنستخدم `receipt.png`.  
- Visual Studio 2022، VS Code، أو أي محرر تفضله.

لا تحتاج إلى أي حزم NuGet إضافية بخلاف `Aspose.OCR`.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

أولًا، أنشئ مشروع Console جديد وأضف مكتبة OCR.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك إضافة الحزمة عبر واجهة NuGet Package Manager. سيقوم تلقائيًا باستعادة الاعتمادات، مما يوفر عليك تنفيذ `dotnet restore` يدويًا لاحقًا.

الآن افتح `Program.cs` – سنستبدل محتوياته بالكود الذي يَـ **ينفّذ OCR على صورة** فعليًا.

## الخطوة 2: إنشاء وتكوين محرك OCR

الجوهر الأساسي لأي سير عمل Aspose OCR هو الفئة `OcrEngine`. أدناه نقوم بإنشائه ونخبر المحرك بإخراج النتائج بصيغة JSON – تنسيق سهل التحليل لاحقًا.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine we want JSON output.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: tweak language or recognition speed.
        // ocrEngine.Settings.Language = Language.English; // default is English
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Fast; // or Accurate
```

**لماذا نضبط `ResultFormat` إلى JSON؟**  
JSON لغة مستقلة عن أي منصة ويمكن تحويلها إلى كائنات قوية النوع في C#، JavaScript، Python، أو أي بيئة قد تتكامل معها. كما أنها تحتفظ بدرجات الثقة وإحداثيات المربعات المحيطة، وهو ما يكون مفيدًا للتحقق اللاحق.

## الخطوة 3: تنفيذ OCR على صورة والتقاط JSON

الآن بعد أن أصبح المحرك جاهزًا، نقوم فعليًا **بتنفيذ OCR على صورة** عبر استدعاء `RecognizeImage`. تُعيد الطريقة سلسلة نصية تحتوي على حمولة JSON.

```csharp
        // Step 3: Perform OCR on the image and capture the JSON output.
        // Replace the path with the location of your own image file.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);
```

> **حالة حدية:** إذا كانت الصورة تالفة أو كان المسار غير صحيح، فإن `RecognizeImage` ترمي استثناء `FileNotFoundException`. احwrap الاستدعاء داخل كتلة `try/catch` إذا كنت تحتاج إلى معالجة أخطاء سلسة.

## الخطوة 4: حفظ نتيجة JSON للمعالجة اللاحقة

تخزين مخرجات OCR يتيح لك تمريرها إلى قواعد البيانات، الـ APIs، أو مكونات الواجهة لاحقًا. إليك طريقة بسيطة لكتابة JSON إلى القرص.

```csharp
        // Step 4: Save the JSON result for later use.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);
```

إذا كنت تعمل في بيئة سحابية، يمكنك استبدال `File.WriteAllText` باستدعاء إلى Azure Blob Storage أو AWS S3 – سلسلة JSON تعمل بنفس الطريقة.

## الخطوة 5: إبلاغ المستخدم وتنظيف الموارد

رسالة صغيرة في الـ Console تؤكد أن كل شيء نجح. في تطبيق واقعي قد تسجل هذه الرسالة في ملف أو ترسلها إلى خدمة مراقبة.

```csharp
        // Step 5: Inform the user that the JSON file has been saved.
        Console.WriteLine("JSON result saved to " + outputPath);
    }
}
```

هذه هي العملية بالكامل! شغّل البرنامج باستخدام `dotnet run` وسترى رسالة التأكيد، بالإضافة إلى ملف `receipt.json` يحتوي على شيء مشابه لـ:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $23.45",
          "Confidence": 0.98,
          "Rectangle": { "X": 120, "Y": 340, "Width": 150, "Height": 20 }
        }
      ]
    }
  ]
}
```

## مثال كامل قابل للتنفيذ

للتكامل، إليك الملف *الدقيق* الذي يمكنك نسخه ولصقه في `Program.cs`. لا توجد أجزاء مفقودة.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Configure the engine to return results in JSON format.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: adjust language or recognition mode if needed.
        // ocrEngine.Settings.Language = Language.English;
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Accurate;

        // Step 3: Perform OCR on the image and capture the JSON output.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);

        // Step 4: Save the JSON result for further processing.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);

        // Step 5: Notify that the JSON file has been saved.
        Console.WriteLine($"JSON result saved to {outputPath}");
    }
}
```

> **نصيحة:** استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي بناءً على جذر المشروع. استخدام `Path.Combine(Environment.CurrentDirectory, "receipt.png")` يتجنب كتابة فواصل ثابتة على Windows مقابل Linux.

## أسئلة شائعة ومشكلات محتملة

- **ما صيغ الصور المدعومة؟**  
  Aspose.OCR يدعم PNG، JPEG، BMP، TIFF، و GIF. إذا احتجت للعمل مع ملفات PDF، حوّل كل صفحة إلى صورة أولًا (يمكن أن تساعدك Aspose.PDF).

- **هل يمكن الحصول على نص عادي بدلاً من JSON؟**  
  نعم – اضبط `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. يُفضَّل JSON عندما تحتاج إلى مزيد من البيانات الوصفية.

- **كيف أتعامل مع المستندات متعددة الصفحات؟**  
  مرّر صورة كل صفحة إلى `RecognizeImage` داخل حلقة وادمج النتائج، أو استخدم `RecognizePdf` التي تُعيد بنية JSON موحدة.

- **هل هناك مخاوف تتعلق بالأداء؟**  
  للمعالجة الدفعية، أعد استخدام كائن `OcrEngine` واحد بدلاً من إنشاء جديد لكل صورة. كذلك، فعّل `RecognitionMode.Fast` إذا كان بإمكانك التضحية بالدقة مقابل السرعة.

- **تحذيرات الترخيص؟**  
  بدون ترخيص، سيتضمن JSON حقل علامة مائية. ضع ترخيصك مبكرًا في `Main` باستخدام `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

## نظرة بصرية عامة

فيما يلي مخطط سريع يوضح تدفق البيانات من ملف الصورة → محرك OCR → مخرجات JSON → التخزين. يساعدك على رؤية موضع كل خطوة في خط أنابيب أكبر.

![مخطط سير عمل تنفيذ OCR على صورة](https://example.com/ocr-workflow.png "تنفيذ OCR على صورة")

*نص بديل: مخطط يوضح كيفية تنفيذ OCR على صورة باستخدام Aspose OCR، تحويلها إلى JSON وحفظها في ملف.*

## توسيع المثال

الآن بعد أن عرفت كيفية **تنفيذ OCR على صورة** والحصول على حمولة JSON، قد ترغب في:

- **تحليل JSON** باستخدام `System.Text.Json` أو `Newtonsoft.Json` لاستخراج حقول محددة.  
- **إدخال النص في قاعدة بيانات** لأرشفة قابلة للبحث.  
- **دمج مع API ويب** بحيث يمكن للعملاء رفع صورهم وتلقي نتائج OCR فورًا.  
- **تطبيق معالجة مسبقة للصور** (تصحيح الميل، تعزيز التباين) باستخدام `Aspose.Imaging` لتحسين الدقة.

كل من هذه المواضيع يبني على الأساس الذي غطيناه، ويمكن إعادة استخدام نفس كائن `OcrEngine` عبرها.

## الخلاصة

لقد تعلمت الآن كيفية **تنفيذ OCR على صورة** في C# باستخدام Aspose OCR، ضبط المحرك لإخراج JSON، وحفظ النتائج للاستخدام لاحقًا. شمل الدرس كل سطر من الكود، شرح سبب أهمية كل إعداد، وأبرز الحالات الحدية التي قد تواجهها في بيئة الإنتاج.

من هنا، جرّب لغات مختلفة (`ocrEngine.Settings.Language`)، عدّل `RecognitionMode`، أو اربط الـ JSON بأنابيب تحليل لاحقة. السماء هي الحد عندما تجمع بين OCR موثوق وأدوات .NET الحديثة.

إذا وجدت هذا الدليل مفيدًا، فكر في وضع نجمة على مستودع Aspose.OCR على GitHub، مشاركة المقال مع زملائك، أو ترك تعليق بنصائحك الخاصة. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}