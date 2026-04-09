---
category: general
date: 2026-04-08
description: يتيح التعرف الضوئي على الحروف (OCR) للملفات PDF دفعةً واحدةً باستخدام
  وحدة معالجة الرسومات (GPU) استخراج النص بسرعة من ملفات PDF. تعلم كيفية ضبط لغة OCR
  واستخدام OCR المعجل بوحدة معالجة الرسومات في C#.
draft: false
keywords:
- batch pdf ocr
- extract text from pdf
- gpu accelerated ocr
- set ocr language
language: ar
og_description: يتيح لك التعرف الضوئي على الحروف (OCR) للملفات PDF باستخدام وحدة معالجة
  الرسومات (GPU) استخراج النص بسرعة من ملفات PDF. يوضح هذا الدليل كيفية ضبط لغة OCR
  والاستفادة من تسريع GPU.
og_title: معالجة دفعة OCR لملفات PDF باستخدام GPU – دليل استخراج النص السريع
tags:
- Aspose.OCR
- C#
- GPU
title: دليل استخراج النص السريع من ملفات PDF دفعيًا باستخدام GPU.
url: /ar/net/ocr-optimization/batch-pdf-ocr-with-gpu-fast-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR دفعي لملفات PDF باستخدام GPU – دليل استخراج النص السريع

هل تحتاج إلى تشغيل **OCR دفعي لملفات PDF باستخدام GPU** لتسريع معالجة المستندات الضخمة؟ في هذا الدليل سنوضح لك كيفية **استخراج النص من ملفات PDF** باستخدام محرك **OCR المدعوم بـ GPU** من Aspose.OCR. سواء كنت تتعامل مع آلاف الفواتير أو تقوم بمسح أرشيفات قانونية، فإن القدرة على ضبط لغة OCR وتشغيل الـ GPU يمكن أن توفر دقائق – أو حتى ساعات – من وقت العمل.

الواقع هو أن معظم المطورين يستخدمون OCR على الـ CPU فقط ويتساءلون لماذا يكون بطيئًا. بنهاية هذا البرنامج التعليمي ستفهم لماذا الـ GPU مهم، وكيفية تكوين المحرك، وكيفية استخراج نص نظيف من كل صفحة PDF في مهمة دفعية. لا أدوات خارجية، فقط C# نقي وعدد قليل من الأسطر البرمجية.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يتوافق مع .NET Core أيضًا)  
- Aspose.OCR for .NET 2024‑R3 (أو أحدث) – حزمة NuGet `Aspose.OCR`  
- بطاقة NVIDIA واحدة على الأقل تدعم CUDA 11+ (أو AMD متوافق إذا كان لديك التعريف المناسب)  
- إلمام أساسي بـ C# async/await (اختياري لكنه مفيد)  

إذا كان لديك هذه المكونات جاهزة، عظيم—لنبدأ. إذا لم يكن كذلك، فإن خطوة **ضبط لغة OCR** تعمل على الـ CPU أيضًا، لذا يمكنك اختبار المنطق قبل ربط الـ GPU.

---

## OCR دفعي لملفات PDF – تهيئة محرك GPU

الخطوة الأولى هي إنشاء محرك OCR يدعم الـ GPU وتفعيل المعجل. توفر Aspose الفئة `GpuOcrEngine` التي ترث من `OcrEngine` العادية. تفعيل الـ GPU بسيط كقلب زر.

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

/// <summary>
/// Demonstrates batch PDF OCR using a GPU‑accelerated engine.
/// </summary>
public static class PdfBatchOcrDemo
{
    public static void BatchPdfWithGpu()
    {
        // 1️⃣ Create a GPU‑aware OCR engine and enable the GPU.
        var ocrEngine = new GpuOcrEngine
        {
            Options = { EnableGpu = true, GpuDeviceId = 0 } // 0 = first GPU in the system
        };
```

**لماذا هذا مهم:**  
- **EnableGpu = true** يخبر Aspose بتوجيه مهام معالجة الصور الثقيلة إلى بطاقة الرسوميات.  
- **GpuDeviceId = 0** يختار أول بطاقة GPU؛ غيّر الفهرس إذا كان لديك عدة بطاقات.  
- استخدام `GpuOcrEngine` بدلاً من `OcrEngine` يمنحك نفس واجهة البرمجة مع تحسين في الأداء.

> **نصيحة احترافية:** إذا كنت تعمل على خادم بدون واجهة (headless)، تأكد من تثبيت تعريف NVIDIA وبيئة تشغيل CUDA على مستوى النظام؛ وإلا سيتراجع المحرك إلى الـ CPU بصمت.

---

## ضبط لغة OCR (set OCR language)

بعد ذلك، أخبر المحرك أي لغة يجب التعرف عليها. تقوم Aspose بتنزيل حزم اللغات تلقائيًا في المرة الأولى التي تطلبها فيها، لذا لا تحتاج إلى تضمين ملفات كبيرة بنفسك.

```csharp
        // 2️⃣ Set the language for recognition – “en” for English.
        ocrEngine.Language = "en";
```

يمكنك استبدال `"en"` بأي رمز ISO‑639‑1 (`"fr"`، `"de"`، `"es"`، إلخ). إذا كنت تحتاج دعمًا متعدد اللغات، مرّر قائمة مفصولة بفواصل مثل `"en,fr"`.

**لماذا يجب ضبط اللغة:**  
- يستخدم محرك OCR قواميس خاصة بكل لغة لتحسين الدقة.  
- عدم ضبطها يجعل اللغة الافتراضية هي الإنجليزية، مما قد يخطئ في تفسير الأحرف في الأبجديات الأخرى.  
- التنزيل التلقائي يضمن حصولك دائمًا على أحدث النماذج دون تحديثات يدوية.

---

## استخراج النص من صفحات PDF

الآن نقوم بإدراج ملفات PDF التي نريد معالجتها. في سيناريو واقعي قد تقرأ أسماء الملفات من دليل أو قاعدة بيانات؛ هنا سنكتب قائمة قصيرة يدويًا للتوضيح.

```csharp
        // 3️⃣ List the PDF pages to be processed.
        var pdfPagePaths = new List<string>
        {
            @"YOUR_DIRECTORY\page1.pdf",
            @"YOUR_DIRECTORY\page2.pdf",
            @"YOUR_DIRECTORY\page3.pdf"
        };
```

> **ملاحظة:** استخدم السلاسل النصية الحرفية (`@""`) لتجنب هروب الشرطات المائلة في نظام Windows.

مع إعداد القائمة، نمر على كل ملف، نشغّل OCR، ونطبع عدد الأحرف – فحص سريع للتأكد من أن المحرك قرأ شيئًا فعليًا.

```csharp
        // 4️⃣ Recognize each page and output the character count.
        foreach (var pagePath in pdfPagePaths)
        {
            // RecognizePdf returns an OcrResult containing the extracted text.
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");
        }
    }
}
```

**الناتج المتوقع (مثال):**

```
Page YOUR_DIRECTORY\page1.pdf → 1284 characters
Page YOUR_DIRECTORY\page2.pdf → 1120 characters
Page YOUR_DIRECTORY\page3.pdf → 1439 characters
```

إذا رأيت `0 characters`، تحقق من أن ملف PDF يحتوي فعلاً على نص قابل للاختيار أو صور مدمجة؛ Aspose OCR يعمل على الصفحات المرسومة، لذا ملفات PDF الممسوحة ضوئيًا تكون مناسبة، لكن ملفات PDF الأصلية التي تحتوي على نص مخفي قد تحتاج إلى نهج مختلف.

---

## التحقق من النتائج ومعالجة الحالات الخاصة

تشغيل OCR في مهمة دفعية ليس دائمًا سلسًا. إليك بعض المشكلات الشائعة وكيفية معالجتها.

| المشكلة | العرض | الحل |
|-------|----------|-----|
| **غياب تعريف GPU** | `Aspose.Ocr.Exceptions.OcrException: GPU not available` | ثبّت أحدث تعريف NVIDIA وأدوات CUDA. |
| **نفاد الذاكرة في ملفات PDF الكبيرة** | يتعطل البرنامج بعد عدة صفحات | زد قيمة `Options.MaxMemoryUsage` أو عالج PDF صفحةً بصفحة باستخدام `RecognizePdfPage`. |
| **حزمة اللغة لم تُنزّل** | النص مشوش أو فارغ | تأكد من أن الجهاز يملك اتصال إنترنت في المرة الأولى التي تضبط فيها `ocrEngine.Language`. |
| **ملف PDF تالف** | `System.IO.IOException: Cannot read file` | تحقق من سلامة الملف قبل إرساله إلى OCR، ربما باستخدام `PdfDocument.Load`. |

يمكنك أيضًا التقاط النص الخام الناتج عن OCR لمعالجة لاحقة – حفظه في ملف `.txt`، إرساله إلى فهرس بحث، أو تمريره إلى نموذج لغة للتلخيص.

```csharp
        // Example: Save each OCR result to a .txt file.
        foreach (var pagePath in pdfPagePaths)
        {
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
            System.IO.File.WriteAllText(txtPath, ocrResult.Text);
            Console.WriteLine($"Saved OCR text to {txtPath}");
        }
```

**لماذا الحفظ مفيد:**  
- يفصل خطوة OCR الثقيلة عن التحليلات اللاحقة، مما يتيح لك تشغيل الاستخراج مرة واحدة وإعادة استخدام ملفات النص العادي إلى ما لا نهاية.  
- ملفات النص أصغر بكثير مقارنة بملفات PDF، مما يجعلها مثالية للتحكم في الإصدارات أو المقارنة.

---

## مثال كامل يعمل

بدمج كل ما سبق، إليك تطبيق كونسول مستقل يمكنك لصقه في مشروع `.csproj` جديد وتشغيله. استبدل `YOUR_DIRECTORY` بالمسار الفعلي الذي يحتوي على صفحات PDF الخاصة بك.

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

namespace BatchPdfOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            BatchPdfWithGpu();
        }

        /// <summary>
        /// Executes batch PDF OCR using a GPU‑accelerated engine.
        /// </summary>
        public static void BatchPdfWithGpu()
        {
            // Step 1 – Initialize GPU engine.
            var ocrEngine = new GpuOcrEngine
            {
                Options = { EnableGpu = true, GpuDeviceId = 0 }
            };

            // Step 2 – Set the OCR language (auto‑download enabled).
            ocrEngine.Language = "en";

            // Step 3 – Define the PDFs to process.
            var pdfPagePaths = new List<string>
            {
                @"YOUR_DIRECTORY\page1.pdf",
                @"YOUR_DIRECTORY\page2.pdf",
                @"YOUR_DIRECTORY\page3.pdf"
            };

            // Step 4 – Run OCR on each file and write results.
            foreach (var pagePath in pdfPagePaths)
            {
                var ocrResult = ocrEngine.RecognizePdf(pagePath);
                Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");

                // Optional: persist the extracted text.
                var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
                System.IO.File.WriteAllText(txtPath, ocrResult.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }
        }
    }
}
```

الترجمة باستخدام:

```bash
dotnet build
dotnet run
```

يجب أن ترى عدد الأحرف وملفات `.txt` التي تم إنشاؤها تظهر بجانب كل PDF.

---

![Batch PDF OCR GPU processing diagram](https://example.com/image.png "Batch PDF OCR with GPU")

*نص بديل للصورة: **معالجة OCR دفعي لملفات PDF باستخدام GPU** توضح المخطط PDF → GPU OCR → مخرجات النص.*

---

## الخطوات التالية والمواضيع ذات الصلة

- **الأداء المدعوم بـ GPU مقابل الأداء على CPU فقط:** أجرِ اختبارًا سريعًا (معالجة 100 صفحة) وقارن الأوقات. توقع تسريعًا بمقدار 2‑5× على بطاقات GPU الحديثة.  
- **دفعات متعددة اللغات:** اضبط `ocrEngine.Language = "en,fr,es"` للتعامل مع مستندات متعددة اللغات في تمريرة واحدة.  
- **بث ملفات PDF الكبيرة:** استخدم `RecognizePdfPage` لمعالجة صفحة واحدة في كل مرة، مما يقلل الضغط على الذاكرة.  
- **التكامل مع Azure Functions أو AWS Lambda:** انقل مهمة الدفعة إلى السحابة، مستفيدًا من مثيلات GPU للتمدد حسب الطلب.  
- **فهرسة البحث:** أدخل النص المستخرج إلى Elasticsearch أو Azure Cognitive Search لاسترجاع المستندات بسرعة.

---

## الخاتمة

لقد أتقنت الآن **OCR دفعي لملفات PDF باستخدام GPU**، وتعلمت كيفية **استخراج النص من ملفات PDF** بفعالية، واكتشفت الطريقة الصحيحة لـ **ضبط لغة OCR** لتحقيق أعلى دقة. من خلال تفعيل تسريع الـ GPU، قللت زمن المعالجة بشكل كبير، ومع API البسيط من Aspose تجنبت الكثير من الكود الروتيني المعتاد في خطوط OCR.

جرّبه على مجموعة البيانات الخاصة بك—عدّل قائمة اللغات، جرب بطاقات GPU مختلفة، أو غلف المنطق في خدمة خلفية. السماء هي الحد عندما تجمع بين OCR عالي الأداء وأدوات .NET الحديثة.

هل لديك أسئلة، أو صادفت حالة خاصة لم تُغطى هنا؟ اترك تعليقًا أو افتح قضية في منتديات Aspose. برمجة سعيدة، ونتمنى أن تكون عمليات OCR سريعة وخالية من الأخطاء!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}