---
category: general
date: 2026-02-17
description: كيفية تنفيذ OCR في C# وتحويل الصورة إلى JSON بسرعة. اتبع هذا الدرس حول
  OCR في C# لاستخراج النص من الصور وحفظ التخطيط كـ JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: ar
og_description: كيف تقوم بتنفيذ OCR في C#؟ يوضح لك هذا الدليل كيفية تحويل صورة إلى
  JSON، استخراج النص من الصورة في C#، وتحميل ملف الصورة للتعرف الضوئي على الأحرف.
og_title: كيفية تنفيذ OCR في C# – تحويل الصورة إلى JSON
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR في C# – دليل تحويل الصورة إلى JSON
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – دليل تحويل الصورة إلى JSON

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على إيصال، فاتورة، أو أي مستند ممسوح ضوئيًا باستخدام C#؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج النص *مع* الحفاظ على التخطيط دون قضاء ساعات في كتابة محللات مخصصة.  

في هذا الدرس سنستعرض **c# ocr tutorial** كامل يوضح لك بالضبط كيفية تنفيذ OCR، **تحويل الصورة إلى json**، وحفظ النتيجة للتحليل لاحقًا. بنهاية الدرس ستحصل على تطبيق كونسول جاهز للتشغيل يقوم بتحميل ملف صورة في C#، استخراج النص، وكتابة ملف JSON مفصل يحتوي على الإحداثيات، درجات الثقة، والنص الأصلي.

## المتطلبات المسبقة — ما ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل على .NET Core أيضًا)  
- Visual Studio 2022 أو أي محرر تفضله  
- رخصة Aspose OCR (يمكنك البدء بتجربة مجانية)  
- صورة نموذجية، مثل `receipt.png`، موجودة في مجلد يمكنك الإشارة إليه  

هذا كل شيء—لا تحتاج إلى حزم NuGet إضافية بخلاف `Aspose.OCR`. إذا كان لديك هذه المكونات، فأنت جاهز للبدء.

## كيفية تنفيذ OCR والحصول على مخرجات JSON

جوهر **how to perform OCR** باستخدام Aspose بسيط: أنشئ `OcrEngine`، زوده بتدفق صورة، استدعِ `Recognize`، ثم سَلِّس `OcrResult` إلى JSON. دعنا نفصل ذلك خطوة بخطوة.

### الخطوة 1: تثبيت حزمة Aspose OCR عبر NuGet

افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** استخدم العلامة `--version` لتثبيت أحدث نسخة مستقرة (مثال: `23.9.0`). هذا يجعل بناء المشروع قابلًا لإعادة الإنتاج.

### الخطوة 2: إنشاء هيكل مشروع الكونسول

إذا لم يكن لديك مشروع بعد، أنشئ واحدًا:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

الآن لديك ملف `Program.cs` جاهز لإضافة الكود الذي سيقوم **load image file c#** ويبدأ عملية OCR.

### الخطوة 3: كتابة كود OCR‑to‑JSON الكامل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه والصقه في `Program.cs`. كل سطر مشروح لتعرف *لماذا* كل جزء مهم.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### ما يفعله الكود

| الخطوة | لماذا يهم |
|--------|-----------|
| **Initialize OcrEngine** | يضبط اللغة الافتراضية (الإنجليزية) ويجهز النماذج الداخلية. |
| **Load image file** | استخدام `ImageStream.FromFile` يضمن قراءة الصورة بالصيغ التي تتوقعها Aspose. |
| **Recognize** | العملية الأساسية—تحليل البكسل، تجزئة الأحرف، والبحث في القاموس. |
| **ToJson** | ينتج مخرجات منظمة تشمل الصناديق المحيطة، الثقة، والنص الأصلي. |
| **WriteAllText** | يحفظ الـ JSON لتتمكن من مشاركته مع خدمات أخرى. |
| **Console.WriteLine** | يعطي تغذية راجعة فورية—مفيد عند التشغيل من الطرفية. |

> **احذر:** إذا كانت صورتك كبيرة، فكر في تعديل حجمها أولًا لتحسين السرعة واستهلاك الذاكرة. Aspose توفر طرق `Resize` يمكنك استدعاؤها على `ImageStream`.

### الخطوة 4: تشغيل التطبيق والتحقق من المخرجات

من الطرفية:

```bash
dotnet run
```

يجب أن ترى:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

افتح `receipt.json` في أي محرر؛ ستجد محتوى يشبه:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

هذا الـ JSON يلتقط **extract text image c#** بالإضافة إلى بيانات التخطيط، وهو مثالي للمعالجة اللاحقة.

## تحويل الصورة إلى JSON – ما بعد الأساسيات

الآن بعد أن عرفت **how to perform OCR**، دعنا نستكشف بعض الاختلافات التي قد تحتاجها في المشاريع الواقعية.

### معالجة صفحات متعددة

إذا كان المصدر PDF أو TIFF متعدد الصفحات، ببساطة كرّر العملية لكل صفحة:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### تخصيص اللغة والدقة

Aspose تدعم أكثر من 40 لغة. لتغيير اللغة إلى الإسبانية:

```csharp
ocrEngine.Language = Language.Spanish;
```

يمكنك أيضًا تعديل `ocrEngine.Settings` لتفعيل **auto‑rotate**، **noise removal**، أو **dictionary‑based correction**—كلها تحسن جودة الـ JSON الذي تحصل عليه.

### حفظ JSON بصيغة منسقة (Pretty‑Printed)

إذا كنت تفضّل JSON مُنَسَّق لسهولة القراءة:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – المشكلات الشائعة والنصائح

عند **load image file c#** قد تواجه:

- **File not found** – تأكد أن المسار مطلق أو استخدم `Path.Combine` مع `Environment.CurrentDirectory`.  
- **Unsupported format** – Aspose يدعم PNG، JPEG، BMP، TIFF، وPDF. بالنسبة للصور بصيغ RAW، حوّلها أولًا.  
- **Large file memory pressure** – استخدم `ImageStream.FromFile(path, maxSizeInKB)` لتقليل الحجم عند التحميل.

معالجة هذه القضايا مبكرًا توفر عليك استثناءات غامضة لاحقًا في خط أنابيب OCR.

## Extract Text Image C# – التحقق من النتائج

بعد حصولك على الـ JSON، قد ترغب فقط في النص الصافي:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

هذا المقتطف يوضح **extract text image c#** بدون تفاصيل التخطيط—مفيد للبحث السريع أو التسجيل.

---

![Diagram showing OCR workflow – how to perform OCR, convert image to JSON, and extract text image c#](/images/ocr-workflow.png "how to perform OCR workflow")
*نص بديل للصورة: "مخطط سير عمل OCR يوضح كيفية تنفيذ OCR، تحويل الصورة إلى JSON، واستخراج نص الصورة c#"*  

*(الصورة مجرد عنصر نائب؛ استبدلها بمخطط فعلي عند النشر.)*

---

## الخاتمة

غطينا **how to perform OCR** في C# من البداية إلى النهاية، وأظهرنا لك كيفية **convert image to JSON**، وشرحنا تفاصيل **load image file c#** و**extract text image c#**. مثال الكود الكامل جاهز للإدماج في أي مشروع .NET، ومخرجات الـ JSON تمنحك كلًا من النص الخام وبيانات التخطيط الدقيقة للتحليلات اللاحقة.

ما الخطوة التالية؟ جرّب إدخال الـ JSON في قاعدة بيانات، أو تصور الصناديق المحيطة على واجهة مستخدم، أو ربط عدة عمليات OCR لمعالجة دفعات كبيرة. يمكنك أيضًا تجربة ميزات Aspose الأخرى مثل التعرف على الخط اليدوي أو اكتشاف الباركود—كلاهما يتكامل بسلاسة مع نفس الخط الأنابيب.

إذا واجهت أي صعوبات، راجع نصائح استكشاف الأخطاء في قسم “Load Image File C#”، أو استكشف وثائق Aspose الواسعة لإعدادات متقدمة. برمجة سعيدة، واستمتع بتحويل الصور إلى بيانات منظمة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}