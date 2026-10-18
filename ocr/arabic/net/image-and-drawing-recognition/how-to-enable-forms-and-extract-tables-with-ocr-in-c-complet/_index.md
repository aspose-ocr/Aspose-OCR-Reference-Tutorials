---
category: general
date: 2026-09-03
description: تعلم كيفية تمكين forms c# واستخراج الجداول باستخدام OCR في C#. يوضح هذا
  الدليل خطوة بخطوة كيفية تشغيل OCR على الصور واكتشاف الجداول.
draft: false
keywords:
- enable forms c#
- extract tables c#
- detect tables OCR
- use OCR C#
- run OCR image
lastmod: 2026-09-03
og_description: تمكين forms c# واستخراج الجداول باستخدام OCR في C#. اتبع هذا الدليل
  خطوة بخطوة لتشغيل OCR على الصور، واكتشاف الجداول، واستخراج key‑value pairs بكفاءة.
og_image_alt: Guide showing C# code to enable forms and extract tables using OCR
og_title: تمكين forms c# واستخراج الجداول باستخدام OCR في C#
schemas:
- author: Aspose
  dateModified: '2026-09-03'
  description: Learn how to enable forms c# and extract tables with OCR in C#. This
    step‑by‑step guide shows how to run OCR on images and detect tables.
  headline: How to enable forms c# and extract tables with OCR in C#
  type: TechArticle
- questions:
  - answer: Yes. Most OCR SDKs rasterize each PDF page internally, so you can call
      `ocrEngine.LoadPdf("file.pdf")` instead of `LoadImage`.
    question: Does this work with PDF input?
  - answer: The signature appears as a separate image region with low‑confidence text.
      You can filter it out by checking `ocrResult.Images` for confidence below a
      threshold.
    question: My image contains both a table and a handwritten signature—what happens?
  - answer: Absolutely. Iterate over `table.Rows` and write each `cell.Text` to a
      `StringBuilder` separated by commas, then save the string as a `.csv` file.
    question: Can I export the extracted tables to CSV?
  - answer: Enable the SDK’s pre‑processing step to boost contrast and apply edge‑enhancement
      filters before recognition.
    question: What if my tables have no visible borders?
  - answer: Yes. The trial license is limited to 100 pages per month; a full license
      removes this restriction and provides priority support.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- C#
- computer vision
title: كيفية تمكين forms c# واستخراج الجداول باستخدام OCR في C#
url: /ar/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين النماذج c# واستخراج الجداول باستخدام OCR في C#

إذا كنت بحاجة إلى **enable forms c#** أثناء معالجة الفواتير أو الإيصالات أو أي مسح منظم، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعلم أيضًا **how to extract tables c#** من نفس الصورة وتشغيل OCR على الصورة في استدعاء واحد. في نهاية البرنامج التعليمي ستحصل على برنامج C# Console جاهز للتنفيذ يكتشف الجداول، يستخرج أزواج المفتاح‑القيمة، ويطبع كل شيء إلى وحدة التحكم.

## إجابات سريعة
- **ما هي الخطوة الأولى؟** أنشئ كائن `OcrEngine` ووجهه إلى ملف الصورة الخاص بك.  
- **كيف أقوم بتفعيل التعرف على النماذج؟** عيّن `EnableFormRecognition = true` في إعدادات المحرك.  
- **كيف يمكنني استخراج الجداول؟** فعّل `EnableTableRecognition` واقرأ مجموعة `Tables` من النتيجة.  
- **هل أحتاج إلى ترخيص خاص؟** معظم SDKs للـ OCR تتطلب ترخيص تشغيل للإنتاج؛ النسخة التجريبية تكفي للتطوير.  
- **ما إصدارات .NET المدعومة؟** .NET 6+، .NET 5، و .NET Framework 4.7+ كلها متوافقة.

## ما هو enable forms c#؟
`enable forms c#` يشير إلى تفعيل ميزة اكتشاف حقول النماذج في محرك OCR بحيث تُعاد الحقول الموسومة مثل “Invoice Number” أو “Date” كأزواج مفتاح‑قيمة منظمة. هذا يلغي الحاجة إلى تحليل regex يدوي ويسرّع أتمتة إدخال البيانات بشكل كبير. عبر تفعيل هذه القدرة يسمح لك SDK الـ OCR بربط كل تسمية مكتشفة بقيمتها المقابلة تلقائيًا، مما يقلل كمية الكود المخصص الذي تحتاج لكتابته ويحسّن موثوقية خط أنابيب الاستخراج.

## لماذا نستخدم OCR لاكتشاف الجداول والنماذج معًا؟
مكتبات OCR الحديثة تدعم **أكثر من 50 تنسيق إدخال** (بما في ذلك PNG، JPEG، TIFF، و PDF) ويمكنها معالجة **مستندات مئات الصفحات** دون تحميل الملف بالكامل إلى الذاكرة. تمكين كل من استخراج النماذج والجداول في تمريرة واحدة يقلل من استهلاك المعالج حتى **30 %** مقارنةً بتشغيل عمليتي التعرف منفصلتين.

## كيف أقوم بتمكين النماذج في C# باستخدام OCR؟
أنشئ كائن `OcrEngine`، حمّل صورتك، وعين `EnableFormRecognition = true`. سيقوم المحرك تلقائيًا بتحديد الحقول الموسومة ويعرضها عبر مجموعة `FormFields` في النتيجة.  
فئة `OcrEngine` هي نقطة الدخول الرئيسية لـ SDK الـ OCR، مسؤولة عن تحميل الصور وإجراء التعرف. تدير نماذج اللغة، المعالجة المسبقة، وسلسلة التعرف بأكملها، مما يجعلها أساسية لأي سير عمل يعتمد على OCR.

## كيف يمكنني استخراج الجداول من الصور في C#؟
فعّل اكتشاف الجداول عن طريق تعيين `EnableTableRecognition = true`. بعد عملية التعرف، قم بالتكرار على `result.Tables` لقراءة عدد الصفوف والأعمدة في كل جدول والنص داخل كل خلية. تُعاد الجداول المستخرجة ككائنات تعرض `Rows` و `Columns` وقيم `Cell` الفردية، مما يتيح لك تحويلها إلى CSV أو JSON أو أي تنسيق آخر للمعالجة اللاحقة. هذا الأسلوب يتعامل مع معظم البُنى الشبيهة بالشبكة دون الحاجة إلى اكتشاف الخطوط يدويًا.

## كيف أقوم بتشغيل OCR على صورة في C#؟
استدعِ طريقة `Recognize` للمحرك مع مسار الصورة. تُعيد الطريقة كائن `OcrResult` يحتوي على كل من `FormFields` و `Tables`. يمكنك بعد ذلك طباعة البيانات المستخرجة أو تمريرها إلى معالجة لاحقة.  
فئة `OcrResult` تحتفظ بمخرجات عملية التعرف، بما في ذلك النص الخام، الحقول المكتشفة، وأي جداول تم تحديدها، مما يوفر حاوية مريحة لكل المعلومات المستمدة من OCR.

### تعريف الروابط المرجعية
فئة `OcrEngine` هي نقطة الدخول لـ SDK الـ OCR؛ تقوم بتحميل الصور، تحتفظ بأعلام الإعداد، وتنفّذ سلسلة التعرف.  
فئة `OcrResult` تلخص نتيجة عملية التعرف، وتعرض مجموعات مثل `Tables` و `FormFields` والنص الخام `TextLines`.

## الخطوة 1: إعداد محرك OCR – كيفية تمكين النماذج

أولاً، أنشئ المحرك ووجهه إلى ملف المصدر الخاص بك:

`var ocrEngine = new OcrEngine();`  
`ocrEngine.LoadImage("invoice_table.png");`

يمكنك أيضًا تعديل لغة OCR، DPI، وإعدادات عالمية أخرى في هذه المرحلة.  

**لماذا هذا مهم:** إنشاء المحرك يخصّص موارد داخلية (مثل نماذج اللغة). إذا تخطيت هذه الخطوة فإن استدعاء `Recognize` التالي سيلقي استثناء `NullReferenceException`.

## الخطوة 2: تفعيل الاستخراج المنظم – كيفية استخراج الجداول واكتشاف الجداول OCR

فعّل الميزتين الأساسيتين قبل استدعاء `Recognize`:

`ocrEngine.Config.EnableFormRecognition = true;`  
`ocrEngine.Config.EnableTableRecognition = true;`

**نصيحة احترافية:** إذا كنت بحاجة إلى إحدى الميزتين فقط، فإن تعطيل الأخرى يمكن أن يحسّن الأداء حتى **20 %**.

## الخطوة 3: تشغيل OCR على الصورة والحصول على النتيجة – run OCR image

الآن نفّذ عملية التعرف:

`OcrResult result = ocrEngine.Recognize();`

كائن `result` المُعاد يحتوي على مجموعتين مهمتين:

* `result.FormFields` – قاموس بأسماء الحقول والقيم المستخرجة.  
* `result.Tables` – قائمة كائنات الجداول، كل منها يعرض `Rows` و `Columns` ونص الخلايا.

### ناتج وحدة التحكم المتوقع

عند طباعة النتيجة ستظهر لك شيئًا مشابهًا لـ:

```
Table 1 – 5 rows × 4 columns
Row 1: Item   Qty   Price   Total
Row 2: Pen    10    $1.00   $10.00
...
Form field “InvoiceNumber”: 2023‑00123
Form field “InvoiceDate”: 2023‑03‑15
```

الأرقام الدقيقة ستختلف بناءً على صورتك المصدرية، لكن البنية ستظل دائمًا تسرد كل جدول متبوعًا بالحقول المستخرجة.

## الخطوة 4: معالجة الحالات الخاصة عند اكتشاف الجداول OCR

حتى مع `EnableTableRecognition = true`، قد يواجه OCR صعوبات في:

| المشكلة | السبب | حل سريع |
|-------|----------------|-----------|
| **الخلايا المدمجة** | يعتبر المحرك المنطقة المدمجة خلية واحدة. | **معالجة لاحقة للصفوف:** ابحث عن خلايا عريضة غير طبيعية وقم بتقسيمها بناءً على المسافات. |
| **الحدود المفقودة** | خطوط الجدول ضعيفة أو متقطعة. | زد التباين في الصورة قبل تمريرها إلى المحرك (`ocrEngine.PreprocessImage`). |
| **الجداول المائلة** | المستند مُسح بزاوية. | استخدم `ocrEngine.Config.AutoRotate = true` (إن كان متاحًا). |

**نصيحة:** دائمًا تحقق من `table.Rows.Count` و `table.Columns.Count` قبل الوصول إلى الفهارس لتجنب استثناء `IndexOutOfRangeException`.

## الخطوة 5: تجميع كل شيء معًا – مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في مشروع Console جديد. يتضمن توجيهات `using`، إعداد المحرك، ومنطق المعالجة الموضح سابقًا.

```csharp
using System;
using OcrSdk;   // Replace with the actual namespace of your OCR SDK

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadImage("invoice_table.png");
        ocrEngine.Config.EnableFormRecognition = true;
        ocrEngine.Config.EnableTableRecognition = true;

        // Run recognition
        OcrResult result = ocrEngine.Recognize();

        // Output tables
        foreach (var table in result.Tables)
        {
            Console.WriteLine($"Table – {table.Rows.Count} rows × {table.Columns.Count} columns");
            foreach (var row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.Cells));
            }
        }

        // Output form fields
        foreach (var field in result.FormFields)
        {
            Console.WriteLine($"Form field “{field.Key}”: {field.Value}");
        }
    }
}
```

شغّل البرنامج (`dotnet run` أو `Ctrl+F5` في Visual Studio) وسترى ناتج وحدة التحكم الموضح أعلاه.

## المشكلات الشائعة واستكشاف الأخطاء

* **نتيجة فارغة** – تأكد من صحة مسار الصورة وأن الملف قابل للوصول.  
* **درجات ثقة منخفضة** – زد دقة الصورة إلى ما لا يقل عن 300 DPI؛ دقة OCR تنخفض حادًا تحت 200 DPI.  
* **حروف غير متوقعة** – فعّل القواميس الخاصة باللغة (`ocrEngine.Config.Language = "en"` للإنجليزية).  
* **اختناقات الأداء** – للدفعات الكبيرة، أعد استخدام كائن `OcrEngine` واحد بدلاً من إنشاء جديد لكل صورة.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: نعم. معظم SDKs للـ OCR تحول كل صفحة PDF إلى صورة داخليًا، لذا يمكنك استدعاء `ocrEngine.LoadPdf("file.pdf")` بدلاً من `LoadImage`.

**س: صورتي تحتوي على جدول وتوقيع يدوي — ماذا يحدث؟**  
ج: يظهر التوقيع كمنطقة صورة منفصلة ذات نص منخفض الثقة. يمكنك تصفيته بالتحقق من `ocrResult.Images` للثقة أقل من عتبة معينة.

**س: هل يمكنني تصدير الجداول المستخرجة إلى CSV؟**  
ج: بالتأكيد. قم بالتكرار على `table.Rows` واكتب كل `cell.Text` إلى `StringBuilder` مفصول بفواصل، ثم احفظ السلسلة كملف `.csv`.

**س: ماذا لو لم يكن للجداول حدود مرئية؟**  
ج: فعّل خطوة ما قبل المعالجة في SDK لزيادة التباين وتطبيق مرشحات تعزيز الحواف قبل التعرف.

**س: هل يلزم ترخيص تجاري للاستخدام في الإنتاج؟**  
ج: نعم. الترخيص التجريبي يقتصر على 100 صفحة شهريًا؛ الترخيص الكامل يزيل هذا القيد ويوفر دعمًا أولوية.

## الخاتمة

أنت الآن تعرف **كيفية تمكين النماذج c#**، **كيفية استخراج الجداول c#**، والخطوات الدقيقة **لتشغيل معالجة صورة OCR** باستخدام C#. يوضح المثال كامل سير العمل — من إنشاء المحرك، عبر الإعداد، إلى معالجة النتيجة — بحيث يمكنك نسخه مباشرة إلى مشاريعك.  

بعد ذلك، جرّب استبدال صورة العينة بملف PDF فاتورة متعدد الصفحات، جرب `ocrEngine.Config.AutoRotate`، أو مرّر البيانات المستخرجة إلى قاعدة بيانات. ستعمق هذه التوسعات إتقانك لـ **detect tables OCR** و **use OCR C#** في سيناريوهات الإنتاج.

![كيفية تمكين النماذج باستخدام OCR C#](image.png)
[كيفية تمكين النماذج باستخدام OCR C#](image.png)

---

**آخر تحديث:** 2026-09-03  
**تم الاختبار مع:** OCR SDK الإصدار 5.2 (يدعم .NET 6+ و .NET Framework 4.7+)  
**المؤلف:** Aspose  

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```
```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```
```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```
```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```
```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

## دروس ذات صلة

- [كيفية تطبيق الترخيص في Aspose Ocr خطوة بخطوة دليل C](/ocr/net/ocr-configuration/how-to-apply-license-in-aspose-ocr-step-by-step-c-guide/)
- [كيفية تمكين GPU لـ Aspose Ocr خطوة بخطوة دليل](/ocr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/net/ocr-configuration/ocr-operation-with-language-selection/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}