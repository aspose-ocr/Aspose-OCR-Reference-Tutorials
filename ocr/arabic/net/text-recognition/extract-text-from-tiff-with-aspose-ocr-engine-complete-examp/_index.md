---
category: general
date: 2026-04-04
description: تعلم كيفية استخراج النص من ملفات TIFF باستخدام مثال محرك OCR بلغة C#.
  دليل خطوة بخطوة مع إخراج بصيغة JSON وXML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: ar
og_description: استخراج النص من ملفات TIFF باستخدام محرك OCR مثال في C#. خطوات مفصلة،
  كود كامل، ونصائح لإخراج JSON/XML.
og_title: استخراج النص من ملف TIFF باستخدام محرك التعرف الضوئي على الأحرف Aspose –
  دليل كامل
tags:
- C#
- OCR
- Aspose
- Image Processing
title: استخراج النص من ملف TIFF باستخدام محرك OCR من Aspose – مثال كامل
url: /ar/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من TIFF – مثال كامل لمحرك OCR بلغة C#

هل احتجت يوماً إلى **استخراج النص من صور TIFF** لكنك لم تكن متأكدًا أي مكتبة يمكنها التعامل مع ملفات متعددة الصفحات دون الحاجة إلى حلول معقدة؟ لست وحدك. في العديد من الأنظمة القديمة، تصل المستندات كمسح ضوئي متعدد الصفحات بصيغة TIFF، واستخراج النص الخام منها أمر ضروري للبحث، والامتثال، أو أتمتة إدخال البيانات.

الخبر السار؟ مع Aspose OCR يمكنك القيام بذلك ببضع أسطر فقط—دون الحاجة إلى التعامل مع مخازن البكسل منخفضة المستوى. يوضح هذا الدليل **مثالًا كاملاً لمحرك OCR** يقوم بتحميل ملف TIFF متعدد الصفحات، يتعرف على كل صفحة، ويُخرج كل من JSON المنسق وXML اختياري. في النهاية ستحصل على تطبيق C# Console جاهز للتشغيل يستخرج النص من ملفات TIFF في ثوانٍ.

## ما ستتعلمه

- كيفية إعداد محرك Aspose OCR في مشروع .NET.  
- الكود الدقيق المطلوب **لاستخراج النص من ملفات TIFF**، بما في ذلك معالجة الصفحات المتعددة.  
- لماذا قد تفضّل إخراج JSON بدلاً من XML وكيفية توليد كلاهما.  
- نصائح لتصحيح الأخطاء الشائعة (مثل DPI الصورة، استهلاك الذاكرة).  

### المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework).  
- ترخيص Aspose OCR صالح (أو مفتاح تجربة مجانية).  
- Visual Studio 2022 أو أي محرر C# تفضله.  
- ملف TIFF متعدد الصفحات تجريبي (مسمى `multi-page.tiff` في المثال).  

> **نصيحة احترافية:** إذا كنت بميزانية محدودة، فإن النسخة التجريبية المجانية تسمح لك باستخراج النص من حتى 100 صفحة شهريًا—مثالية للاختبار.

---

## الخطوة 1 – تهيئة محرك OCR (ocr engine example)

قبل أن نتمكن من **استخراج النص من TIFF**، نحتاج إلى إنشاء نسخة من محرك OCR. هذا الكائن يحتفظ بجميع الإعدادات التي قد ترغب في تعديلها لاحقًا (اللغة، الدقة، إلخ).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*لماذا هذا مهم:* فئة `OcrEngine` تُجرد عنك الأعمال الثقيلة. إنشاء نسخة واحدة وإعادة استخدامها لعدة صور أكثر كفاءة في الذاكرة مقارنة بإنشاء محرك جديد لكل صفحة.

---

## الخطوة 2 – تحميل ملف TIFF متعدد الصفحات (extract text from TIFF)

الآن نوجه المحرك إلى ملف المصدر. `ImageStream.FromFile` يدعم TIFF، JPEG، PNG، والعديد غيرها، لكن في هذا الدليل نركز على TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد على جهازك.  
> **نصيحة:** إذا كان ملف TIFF الخاص بك ذو DPI منخفض (أقل من 150)، فكر في معالجته مسبقًا لتحسين دقة OCR.

---

## الخطوة 3 – التعرف على جميع الصفحات

استدعاء `Recognize()` يُشغّل خوارزمية OCR عبر **كل صفحة** في ملف TIFF. يحتوي كائن النتيجة على النص الخام، درجات الثقة، وتقسيم الصفحات.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*ما ستحصل عليه:* `ocrResult` يحتوي على مجموعة من كائنات `PageResult`. يمكن الوصول إلى نص كل صفحة عبر `ocrResult.Pages[i].Text`. كما يوفر المحرك مستويات الثقة، والتي قد تكون مفيدة لفحص الجودة.

---

## الخطوة 4 – حفظ النتائج كـ JSON (وXML اختياري)

معظم خطوط الأنابيب الحديثة تفضّل JSON، لكن الأنظمة القديمة لا تزال تستخدم XML. إليك كيفية توليد كلاهما، منسقين بشكل جميل.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### مثال على مخرجات JSON (مقتطع)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

الـ JSON قابل للقراءة البشرية، مما يجعل عملية التصحيح سهلة. الـ XML يعكس نفس البنية إذا احتجت إليه.

---

## الخطوة 5 – التحقق من الاستخراج (extract text from TIFF)

بعد كتابة الملفات، يساعد فحص سريع على التأكد من عدم حدوث أي أخطاء.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

إذا رأيت المقتطف مطبوعًا، فقد نجحت في **استخراج النص من TIFF** وحفظه. من هنا يمكنك تمرير الـ JSON إلى فهرس بحث، قاعدة بيانات، أو أي خدمة لاحقة.

---

## لماذا تستخدم Aspose OCR لاستخراج النص من TIFF؟

- **دعم متعدد الصفحات مباشرة** – لا حاجة لتقسيم ملف TIFF يدويًا.  
- **دقة عالية** بفضل نماذج الشبكات العصبية المملوكة.  
- **متعدد المنصات** – يعمل على Windows، Linux، و macOS runtimes الخاصة بـ .NET.  
- **تنسيقات إخراج غنية** (JSON، XML، نص عادي) تناسب كل من البنى الحديثة والقديمة.  

إذا ما زلت مترددًا، جرّب النسخة التجريبية على مستند عيني. ستلاحظ السرعة والبساطة مقارنةً بالبدائل مفتوحة المصدر التي غالبًا ما تتطلب معالجة إضافية للصور.

---

## المشكلات الشائعة وكيفية تجنّبها

| المشكلة | العرض | الحل |
|--------|-------|------|
| TIFF منخفض الدقة | فقدان أحرف، ثقة منخفضة | رفع دقة الصورة إلى ≥150 DPI قبل OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| اللغة غير الصحيحة | كلمات مشوهة، خاصة للنص غير الإنجليزي | ضبط `ocrEngine.Language = Language.Spanish` (أو اللغة المناسبة) قبل `Recognize()` |
| نفاد الذاكرة على ملفات ضخمة | `OutOfMemoryException` | معالجة الصفحات على دفعات: حلقة عبر `ocrEngine.Image.Pages` واستدعاء `RecognizePage(i)` |
| الترخيص غير مُطبق | علامة مائية “Evaluation” في المخرجات | تسجيل الترخيص: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## مثال كامل جاهز للتنفيذ (Copy‑Paste Ready)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في مشروع Console جديد. يتضمن جميع الأجزاء التي ناقشناها—التهيئة، التحميل، التعرف، والحفظ.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

احفظ الملف باسم `Program.cs`، نفّذ الأمر `dotnet run`، وستظهر لك رسائل توضح مكان حفظ JSON وXML. هذا كل شيء—لقد أكملت **مثال محرك OCR** الذي يستخرج النص من TIFF.

---

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة الدفعية:** غلف المنطق السابق داخل حلقة `foreach` لمعالجة عشرات ملفات TIFF تلقائيًا.  
- **دمج البحث:** ادفع الـ JSON إلى Elasticsearch أو Azure Cognitive Search لتمكين البحث النصي الكامل عبر المستندات الممسوحة.  
- **معالجة مسبقة للصور:** استكشف API `ImageProcessing` من Aspose لتصحيح الميل، إزالة الضوضاء، أو تعديل التباين قبل OCR.  
- **إخراج بديل:** استخدم `ocrResult.ToPlainText()` إذا كنت تحتاج فقط إلى سلاسل نصية خام دون بيانات وصفية.  

إذا كنت مهتمًا بصيغ صور أخرى، فإن النمط نفسه يعمل مع ملفات PDF (فقط غير مصدر الملف) أو PNG. الفكرة الأساسية هي أنه بمجرد إعداد المحرك، يصبح باقي العملية خط أنابيب قابل لإعادة الاستخدام.

---

## الخلاصة

استعرضنا **مثالًا كاملاً لمحرك OCR** يتيح لك **استخراج النص من ملفات TIFF** باستخدام Aspose OCR، مع إخراج JSON منسق وXML اختياري لأي سير عمل لاحق. الكود مستقل، والشروحات تغطي “السبب” وراء كل خطوة.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}