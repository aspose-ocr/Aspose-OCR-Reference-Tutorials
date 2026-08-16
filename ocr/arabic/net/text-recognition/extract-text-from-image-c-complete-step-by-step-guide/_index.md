---
category: general
date: 2026-03-29
description: استخراج النص من صورة باستخدام C# و Aspose OCR. تعلّم كيفية الحصول على
  JSON يحتوي على قيم الثقة، ومعالجة الحالات الخاصة، وحفظ النتائج في دقائق.
draft: false
keywords:
- extract text from image c#
- c# ocr library
- aspose ocr c#
- image to text c#
- json output c#
language: ar
og_description: استخراج النص من صورة باستخدام C# و Aspose OCR. يوضح هذا الدليل كيفية
  التعرف على النص، وتضمين درجات الثقة، وحفظ الناتج بصيغة JSON.
og_title: استخراج النص من الصورة C# – دليل برمجي كامل
tags:
- C#
- OCR
- Aspose
- JSON
title: استخراج النص من الصورة باستخدام C# – دليل خطوة بخطوة كامل
url: /ar/net/text-recognition/extract-text-from-image-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام C# – دليل شامل خطوة بخطوة

هل تساءلت يومًا كيف **استخراج النص من صورة C#** دون الحاجة إلى معالجة البكسل منخفض المستوى؟ لست وحدك. في العديد من المشاريع—مسح الفواتير، رقمنة الإيصالات، أو مجرد تحويل لقطات الشاشة إلى نص قابل للبحث—يعد استخراج الكلمات من صورة مهارة أساسية.

في هذا الدرس سنستعرض حلًا عمليًا باستخدام مكتبة Aspose.OCR. بنهاية الدرس ستحصل على تطبيق console جاهز للتنفيذ يقرأ صورة، يستخرج كل كلمة مع درجة الثقة الخاصة بها، ويكتب ملف JSON منظم يمكنك إمداده إلى أي نظام لاحق. لا مراجع غامضة، مجرد مثال كامل يمكن نسخه ولصقه.

## ما ستتعلمه

* كيفية تثبيت حزمة **C# OCR** عبر NuGet.
* لماذا يهم تهيئة محرك OCR باللغة الصحيحة.
* الكود الدقيق المطلوب **لتعرف النص من صورة** وتصديره كـ JSON.
* نصائح للتعامل مع الملفات المفقودة، صيغ الصور المختلفة، وع thresholds الثقة.
* كيفية التحقق من المخرجات ودمجها في سير عمل أكبر.

**المتطلبات المسبقة** – تحتاج إلى .NET 6 أو أحدث، Visual Studio 2022 (أو أي محرر تفضله)، وملف صورة تريد معالجته. لا تحتاج إلى خبرة سابقة في OCR.

![extract text from image c# example](https://example.com/placeholder.png "extract text from image c# screenshot")

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

قبل كتابة أي كود، أول شيء هو إضافة مكتبة Aspose OCR إلى مشروعك. الحزمة تتضمن جميع النماذج الأصلية وتوفر لك API نظيفًا بلغة C#.

```bash
dotnet add package Aspose.OCR
```

*نصيحة:* إذا كنت تستخدم Visual Studio، يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** → البحث عن “Aspose.OCR” والنقر على **Install**. هذا يضمن حصولك على أحدث نسخة مستقرة (حاليًا 23.12).

## الخطوة 2: تهيئة محرك OCR

إنشاء المحرك سهل، لكن **السبب** مهم: ضبط خاصية `Language` يخبر المحرك بمجموعة الأحرف المتوقعة، مما يحسن الدقة بشكل كبير.

```csharp
using Aspose.OCR;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine and tell it we’re processing English text
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // English works for most Latin‑based documents
        };
```

إذا كنت بحاجة للعمل مع الفرنسية أو الألمانية، استبدل `Language.English` بـ `Language.French` أو `Language.German`. المكتبة تدعم أكثر من 40 لغة مباشرةً.

## الخطوة 3: التعرف على النص من صورة

الآن نمرر للمحرك مسار الملف. طريقة `RecognizeImage` تقرأ الـ bitmap، تشغل الشبكة العصبية، وتعيد كائن `OcrResult` يحتوي على كل كلمة، صندوقها المحيط، وقيمة الثقة (0‑100).

```csharp
        // Path to the image you want to process – adjust as needed
        string inputPath = "YOUR_DIRECTORY/input.png";

        // Make sure the file exists before we try to read it
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"Error: Cannot find {inputPath}");
            return;
        }

        // Perform the OCR operation
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);
```

**حالة حافة:** إذا كانت الصورة كبيرة (>5 MB) قد تواجه حدود الذاكرة. في هذه الحالة، قم بتصغير الصورة أولًا (مثلاً باستخدام `System.Drawing`) أو مرّر `Stream` بدلاً من مسار الملف.

## الخطوة 4: تحويل نتيجة OCR إلى JSON مع قيم الثقة

المكتبة توفر طريقة `ToJson` مفيدة. بتمرير `includeConfidence: true` نحصل على حمولة مفصلة تشبه ما يلي:

```json
{
  "Text": "Hello World",
  "Words": [
    { "Text": "Hello", "Confidence": 98.5 },
    { "Text": "World", "Confidence": 96.2 }
  ]
}
```

إليك الكود الذي ينتج سلسلة JSON ويكتبها إلى القرص:

```csharp
        // Serialize the result, including per‑word confidence
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // Destination file – feel free to change the name or folder
        string outputPath = "YOUR_DIRECTORY/output.json";

        // Write the JSON to a file (overwrites if it already exists)
        File.WriteAllText(outputPath, jsonResult);
```

*لماذا نحتفظ بالثقة؟* إذا قمت لاحقًا بإدخال النص في قاعدة بيانات، يمكنك تصفية الكلمات ذات الثقة المنخفضة (مثلاً `< 80%`) لتحسين جودة المعالجة اللاحقة.

## الخطوة 5: حفظ JSON والتحقق من المخرجات

الخطوة الأخيرة هي إبلاغ المستخدم بأن كل شيء نجح، وربما عرض أول بضعة أسطر من JSON لتفحص النتيجة يدويًا.

```csharp
        // Let the user know we’re done
        Console.WriteLine("JSON saved with confidence values.");
        Console.WriteLine($"Output file: {outputPath}");

        // Optional: print a short preview (first 200 chars)
        Console.WriteLine("Preview:");
        Console.WriteLine(jsonResult.Substring(0, Math.Min(200, jsonResult.Length)) + "...");
    }
}
```

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى شيئًا مثل:

```
JSON saved with confidence values.
Output file: YOUR_DIRECTORY/output.json
Preview:
{
  "Text":"Hello World",
  "Words":[
    {"Text":"Hello","Confidence":98.5},
    {"Text":"World","Confidence":96.2}
  ]
}...
```

افتح `output.json` في أي محرر، وستحصل على تمثيل قابل للقراءة آليًا للنص المستخرج، جاهز للمعالجة الإضافية.

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني معالجة ملفات PDF مباشرة؟** | Aspose.OCR يعمل على الصور النقطية. حوّل صفحات PDF إلى PNG/JPEG أولًا (مثلاً باستخدام Aspose.PDF) ثم مرّرها إلى محرك OCR. |
| **ماذا لو احتجت إلى دعم متعدد اللغات؟** | اضبط `ocrEngine.Language = Language.Multilingual` أو غيّر اللغة حسب الصورة. |
| **كيف أتعامل مع صورة تالفة؟** | غلف `RecognizeImage` بكتلة `try/catch` للـ `ImageCorruptedException` واحتفظ بصورة بديلة أو سجّل الخطأ. |
| **هل تنسيق JSON ثابت؟** | نعم، لكن يمكنك تحويله إلى فئة C# مخصصة إذا رغبت في نموذج قوي النوع. |

## نصائح احترافية لـ OCR جاهز للإنتاج

* **معالجة دفعات:** كرّر عبر مجلد من الصور، وأضف كل نتيجة JSON إلى ملف رئيسي.
* **تصفية الثقة:** `ocrResult.Words.Where(w => w.Confidence < 80).ToList()` لتحديد الكلمات غير المؤكدة.
* **التوازي:** استخدم `Parallel.ForEach` للدفعات الكبيرة، لكن حدّ عدد المتزامنين لتجنب استنزاف المعالج.
* **التسجيل:** دمج مع `Serilog` أو `NLog` لتسجيل أوقات OCR ومعدلات الأخطاء.

## الخطوات التالية

الآن بعد أن أصبحت قادرًا على **استخراج النص من صورة C#**، فكر في:

* **تخزين النتائج في قاعدة بيانات SQL** – اربط كل كلمة وثقتها بجدول للتحليلات.
* **الدمج مع Azure Cognitive Services** للكشف عن اللغة أو الترجمة.
* **إنشاء API بسيط** (ASP.NET Core) يقبل صورة مرفوعة ويعيد JSON في الوقت الفعلي.

كل من هذه الامتدادات يبني على المفاهيم الأساسية التي غطيناها هنا، وتستفيد جميعها من بنية OCR موثوقة.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أدناه أو راجع وثائق Aspose.OCR للحصول على خيارات تكوين متقدمة.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}