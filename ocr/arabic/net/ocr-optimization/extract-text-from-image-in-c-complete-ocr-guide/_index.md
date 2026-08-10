---
category: general
date: 2026-02-11
description: استخراج النص من الصورة في C# باستخدام Aspose OCR. تعلّم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، تحسين دقة التعرف الضوئي، وإصلاح أخطاء التعرف الضوئي باستخدام
  التدقيق الإملائي.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: ar
og_description: استخراج النص من الصورة في C# باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف، تحسين دقة التعرف الضوئي على الأحرف،
  وإصلاح أخطاء التعرف الضوئي على الأحرف.
og_title: استخراج النص من الصورة في C# – دليل OCR الكامل
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: استخراج النص من الصورة في C# – دليل OCR الكامل
url: /ar/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل OCR كامل

هل احتجت يوماً إلى **استخراج النص من الصورة** لكن النتائج بدت غير مفهومة؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل مسح الفواتير، رقمنة الملاحظات، أو ترحيل المستندات القديمة—الحصول على نص نظيف من صورة هو العائق الأول، وغالباً الأصعب.

لحسن الحظ، مع Aspose OCR يمكنك **load image for OCR**، تشغيل تدقيق إملائي، والحصول على نص منظم وقابل للبحث. في هذا الدرس سنستعرض كامل سير العمل، من قراءة ملف JPEG إلى تحسين المخرجات، وسترى بالضبط كيف **تحسين دقة OCR** أثناء العملية.

> **ما ستحصل عليه في النهاية:** برنامج C# Console جاهز للتنفيذ يقوم باستخراج النص من الصورة، يصحح الأخطاء الشائعة في OCR، ويطبع كل من النتائج الأولية والنص المنقح.

---

## ما ستحتاجه

- .NET 6 أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)
- مفتاح تجريبي مجاني لـ Aspose OCR أو نسخة مرخصة
- ملف صورة يحتوي على نص مكتوب أو مطبوع (مثال: `typed_note.jpg`)

لا توجد مكتبات طرف ثالث أخرى مطلوبة—Aspose يتعامل مع نماذج اللغة والتدقيق الإملائي تلقائياً.

## الخطوة 1 – تثبيت حزمة Aspose OCR عبر NuGet

قبل أن نتمكن من **استخراج النص من الصورة**، يجب أن يكون محرك OCR متاحاً على الجهاز.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

أو، إذا كنت تفضل سطر الأوامر:

```bash
dotnet add package Aspose.OCR
```

الحزمة تتضمن بيانات اللغة، لكن ضبط `AutomaticResourceDownload = true` (كما سنفعل لاحقاً) يضمن تحميل أي قواميس مفقودة أثناء التشغيل.

## الخطوة 2 – تحميل الصورة لـ OCR

أول شيء يحتاجه المحرك هو صورة bitmap. يمكنك تزويده بأي تنسيق يدعمه `System.Drawing.Image`، مثل PNG، JPEG، BMP، أو TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **لماذا نستخدم كتلة `using`؟** فهي تقوم بتحرير كائن `Image` تلقائياً، مما يمنع مشاكل قفل الملفات التي غالباً ما تواجه المطورين الذين ينسون تحرير الموارد.

## الخطوة 3 – تنفيذ OCR – “Image to Text C#” عملياً

الآن نقوم فعلياً بـ **استخراج النص من الصورة**. فئة `OcrEngine` تقوم بالعمل الشاق.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

في هذه المرحلة لديك سلسلة نصية تعكس ما يراه المحرك في الصورة. عملياً، قد يحتوي الناتج على أحرف عشوائية، كلمات تم التعرف عليها خطأً، أو مشاكل في فواصل الأسطر—ولهذا يأتي الخطوة التالية.

## الخطوة 4 – تحسين دقة OCR باستخدام التدقيق الإملائي

تقدم Aspose أداة `SpellChecker` مخصصة تعرف اللغة التي تعالجها. تشغيلها على السلسلة الأولية غالباً ما يصلح الأخطاء الأكثر وضوحاً.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **نصيحة احترافية:** إذا كنت تتعامل مع مفردات خاصة بمجال معين (مثل المصطلحات الطبية)، يمكنك تزويد `SpellChecker` بقاموس مخصص عبر الدوال الزائدة.

## الخطوة 5 – تصحيح أخطاء OCR يدوياً (اختياري)

حتى أفضل مدقق إملائي قد يغفل عن الأخطاء التي تعتمد على السياق. تمريرة سريعة للمعالجة اللاحقة يمكن أن تلتقط أشياء مثل “l” مقابل “1” أو “O” مقابل “0”.

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

لا تتردد في توسيع هذا القسم باستخدام خوارزمياتك الخاصة—ربما جدول بحث لأكواد المنتجات أو قائمة بالاختصارات المعروفة.

## مثال عملي كامل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع Console App جديد. يتضمن كل خطوة تم مناقشتها، بالإضافة إلى تعليقات مفيدة.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### النتيجة المتوقعة

بافتراض أن `typed_note.jpg` يحتوي على الجملة “Hello world, this is a test 123”، سيظهر في وحدة التحكم شيء مشابه لـ:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

لاحظ كيف قام المدقق الإملائي بتحويل “H3llo” إلى “Hello”، وكيف قامت الـ regex بتنظيف الرقم العشوائي “1” الذي ظهر في “th1s”.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني استخدام لغة مختلفة؟** | نعم. اضبط `ocrEngine.Language = OcrLanguage.Spanish` (أو أي قيمة enum مدعومة) ومرّر نفس اللغة إلى `SpellChecker`. |
| **ماذا لو كانت صورتي كبيرة جداً؟** | قلل حجمها قبل تمريرها إلى OCR؛ فئة `Image` تحتوي على `GetThumbnailImage` لتغيير الحجم بسرعة. |
| **هل أحتاج إلى اتصال بالإنترنت؟** | فقط في المرة الأولى التي يكون فيها حزمة اللغة مفقودة؛ بعد ذلك تُخزن الموارد محلياً. |
| **كيف أتعامل مع ملفات PDF متعددة الصفحات؟** | حوّل كل صفحة إلى صورة (مثلاً باستخدام `PdfRenderer`) وشغّل نفس سير العمل لكل صفحة. |
| **هل المدقق الإملائي يدرك اللغة؟** | بالطبع. يستخدم نفس نموذج اللغة الذي قدمته لمحرك OCR، مما يضمن التناسق. |

## الخطوات التالية والمواضيع ذات الصلة

- **معالجة دفعات:** غلف الكود داخل حلقة `foreach` للتعامل مع مجلد من الصور.
- **نص مكتوب يدويًا:** استبدل `OcrLanguage.EnglishHandwritten` للحصول على نتائج أفضل على الملاحظات المتصلة.
- **التوازي:** استخدم `Parallel.ForEach` لتسريع الأحمال الكبيرة على الأجهزة متعددة الأنوية.
- **التصدير إلى JSON/CSV:** سَلّس `finalText` مع البيانات الوصفية (اسم الملف، درجات الثقة) للتحليلات اللاحقة.

إذا كنت مهتماً بتحويل السلاسل المستخرجة إلى ملفات PDF قابلة للبحث، اطلع على دليلنا حول **“Create searchable PDF from image in C#”**. فهو يبني مباشرةً على نفس خط أنابيب OCR الذي غطيناه للتو.

## الخلاصة

لقد عرضنا للتو طريقة عملية لـ **استخراج النص من الصورة** في C# باستخدام Aspose OCR، مع إظهار كيفية **load image for OCR**، **تحسين دقة OCR**، و**تصحيح أخطاء OCR** باستخدام مدقق إملائي مدمج وتنظيف بسيط باستخدام regex. المثال الكامل يعمل مباشرةً، يتطلب حزمة NuGet واحدة فقط، ويمكن توسيعه ليتناسب مع أي سيناريو رقمنة مستندات تقريباً.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}