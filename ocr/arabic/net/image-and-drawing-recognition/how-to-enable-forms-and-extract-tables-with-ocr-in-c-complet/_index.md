---
category: general
date: 2026-01-04
description: تعلم كيفية تمكين النماذج واستخراج الجداول من الصور باستخدام OCR في C#.
  يوضح هذا الدليل خطوة بخطوة أيضًا كيفية تشغيل OCR على الصورة واكتشاف الجداول باستخدام
  OCR.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: ar
og_description: دليل خطوة بخطوة حول كيفية تمكين النماذج، استخراج الجداول، تشغيل التعرف
  الضوئي على الأحرف للصور واكتشاف جداول التعرف الضوئي على الأحرف باستخدام C#.
og_title: كيفية تمكين النماذج واستخراج الجداول باستخدام OCR في C#
tags:
- OCR
- C#
- Computer Vision
title: كيفية تمكين النماذج واستخراج الجداول باستخدام OCR في C# – دليل كامل
url: /ar/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين النماذج واستخراج الجداول باستخدام OCR في C# – دليل شامل

هل تساءلت يومًا **كيف يتم تمكين النماذج** عند مسح الفواتير أو الإيصالات أو أي مستند منظم؟ لست وحدك. في العديد من المشاريع الواقعية، تكون أكبر نقطة احتكاك هي جعل OCR يفهم حقول النموذج **والجداول** دون الحاجة إلى ملايين سطر من التحليل المخصص.  

في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية يُظهر **كيفية تمكين النماذج**، **كيفية استخراج الجداول**، وحتى **كيفية تشغيل معالجة صورة OCR** في برنامج C# واحد. في النهاية ستحصل على مقتطف جاهز للتنفيذ يكتشف الجداول بنمط OCR، يستخرج أزواج المفتاح‑القيمة، ويطبعها على وحدة التحكم.

> **المتطلبات المسبقة** – .NET 6+ (أو .NET Framework 4.7+)، إشارة إلى SDK الـ OCR الذي تستخدمه (المثال يفترض وجود فئة عامة `OcrEngine`)، وملف صورة (`invoice_table.png`) يحتوي على جدول أو نموذج. لا توجد مكتبات خارجية أخرى مطلوبة.

![كيفية تمكين النماذج باستخدام OCR C#](image.png)

## ما يغطيه هذا الدرس

- **تمكين التعرف على النماذج** بحيث يتم التعرف تلقائيًا على حقول مثل “Invoice Number” أو “Date”.  
- **استخراج الجداول** من المستندات الممسوحة، مع إعطائك عدد الصفوف/الأعمدة ومحتويات الخلايا.  
- **تشغيل معالجة صورة OCR** في استدعاء واحد ومعالجة النتيجة برمجيًا.  
- نصائح لـ **detect tables OCR** في حالات الحافة، مثل الخلايا المدمجة أو الحدود المفقودة.  

هيا نبدأ.

## الخطوة 1: إعداد محرك OCR – كيفية تمكين النماذج

قبل أن يحدث أي تعرّف، تحتاج إلى إنشاء مثال لمحرك OCR. معظم SDKs توفر مُنشئًا بسيطًا؛ سنشير أيضًا إلى الأماكن التي يمكنك فيها تعديل خيارات التكوين لاحقًا.

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

**لماذا هذا مهم:** إنشاء المحرك يخصّص موارد داخلية (مثل نماذج اللغة). إذا تخطيت هذه الخطوة، سيتسبب استدعاء `Recognize` التالي في رمي `NullReferenceException`.

## الخطوة 2: تشغيل الاستخراج الهيكلي – كيفية استخراج الجداول & detect tables OCR

الآن نقوم بتمكين الميزتين الأساسيتين: التعرف على الجداول واستخراج حقول النموذج. معظم محركات OCR الحديثة توفر أعلامًا منطقية أو كائن `Config` أكثر تفصيلًا.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**نصيحة احترافية:** إذا كنت تحتاج فقط إلى إحدى الميزتين، فإن تعطيل الأخرى يمكن أن يحسّن الأداء بنسبة تصل إلى 20 ٪.  

## الخطوة 3: تشغيل OCR على الصورة والحصول على النتيجة – run OCR image

مع تكوين المحرك، استدعاء طريقة واحدة يقوم بالعمل الشاق. الـ `OcrResult` المرتجع يحتوي على مجموعات للجداول وحقول النموذج.

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

### النتيجة المتوقعة على وحدة التحكم

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

ستختلف الأرقام الفعلية بناءً على صورتك المصدرية، لكنك ستلاحظ سطر ملخص لكل جدول يليه قيم خلايا الصف الأول، ثم قائمة بأزواج المفتاح‑القيمة لحقول النموذج.

## الخطوة 4: التعامل مع حالات الحافة عند Detect Tables OCR

حتى مع `EnableTableRecognition = true`، قد يواجه OCR صعوبات في:

| المشكلة | لماذا يحدث ذلك | حل سريع |
|-------|----------------|-----------|
| **الخلايا المدمجة** | يعتبر المحرك المنطقة المدمجة خلية واحدة. | بعد‑معالجة الصفوف: ابحث عن خلايا عريضة غير عادية وقم بتقسيمها بناءً على المسافات. |
| **الحدود المفقودة** | خطوط الجدول ضعيفة أو متقطعة. | زد تباين الصورة قبل تمريرها إلى المحرك (`ocrEngine.PreprocessImage`). |
| **الجداول المائلة** | تم مسح المستند بزاوية. | استخدم `ocrEngine.Config.AutoRotate = true` (إن كان متوفرًا). |

**نصيحة:** دائمًا تحقق من `table.Rows.Count` و `table.Columns.Count` قبل الوصول إلى الفهارس لتجنب `IndexOutOfRangeException`.

## الخطوة 5: جمع كل شيء معًا – مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في مشروع وحدة تحكم جديد. يتضمن توجيهات `using`، إعداد المحرك، ومنطق المعالجة الموضح سابقًا.

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

شغّل البرنامج (`dotnet run` أو `Ctrl+F5` في Visual Studio) وسترى مخرجات وحدة التحكم الموضحة أعلاه.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات PDF؟**  
ج: معظم SDKs للـ OCR تقبل ملفات PDF عن طريق تحويل كل صفحة إلى صورة داخليًا. ما عليك سوى استدعاء `ocrEngine.LoadPdf("file.pdf")` بدلًا من `LoadImage`.

**س: ماذا لو احتوت صورتي على جدول *و* توقيع؟**  
ج: سيظهر التوقيع كمنطقة صورة منفصلة. يمكنك تجاهله بفحص `ocrResult.Images` للعثور على نص منخفض الثقة.

**س: هل يمكنني تصدير الجداول إلى CSV؟**  
ج: بالتأكيد. بعد التكرار على `table.Rows`، اكتب كل `cell.Text` إلى `StringBuilder` مفصولًا بفواصل، ثم احفظ السلسلة في ملف `.csv`.

## الخلاصة

أنت الآن تعرف **كيفية تمكين النماذج**، **كيفية استخراج الجداول**، والخطوات الدقيقة لـ **run OCR image** باستخدام C#. يوضح المثال سير العمل الكامل—من إنشاء المحرك، مرورًا بالتكوين، إلى معالجة النتيجة—حتى يمكنك نسخه مباشرة إلى مشاريعك.  

بعد ذلك، جرّب استبدال صورة العينة بملف PDF لفاتورة متعددة الصفحات، جرب `ocrEngine.Config.AutoRotate`، أو صلّ البيانات المستخرجة بقاعدة بيانات. ستعمّق هذه التوسعات مهاراتك في **detect tables OCR** واستخدام **OCR C#** في بيئات الإنتاج.

إذا واجهت أي صعوبات، لا تتردد في ترك تعليق أدناه. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}