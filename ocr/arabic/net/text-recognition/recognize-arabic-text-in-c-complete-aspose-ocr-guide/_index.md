---
category: general
date: 2026-06-19
description: التعرف على النص العربي من الصور في C# باستخدام Aspose.OCR. تعلم استخراج
  النص من الصورة، التعامل مع صورة OCR عربية، وقراءة النص من اليمين إلى اليسار بكفاءة.
draft: false
keywords:
- recognize arabic text
- extract text from image
- ocr arabic image
- read right-to-left text
language: ar
og_description: التعرف على النص العربي من الصور في C#. يوضح هذا الدليل كيفية استخراج
  النص من الصورة، والعمل مع OCR للصور العربية، وقراءة النص من اليمين إلى اليسار.
og_title: التعرف على النص العربي في C# – Aspose.OCR خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize Arabic text from images in C# using Aspose.OCR. Learn to
    extract text from image, handle OCR Arabic image, and read right-to-left text
    efficiently.
  headline: Recognize Arabic Text in C# – Complete Aspose.OCR Guide
  type: TechArticle
tags:
- OCR
- Aspose
- C#
- Arabic
title: التعرف على النص العربي في C# – دليل Aspose.OCR الكامل
url: /ar/net/text-recognition/recognize-arabic-text-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص العربي في C# – دليل Aspose.OCR الكامل

هل تساءلت يوماً كيف **تتعرف على النص العربي** في صورة دون الحاجة إلى كتابته يدوياً؟ لست وحدك—المطورون الذين يبنون ماسحات الفواتير، الروبوتات المتعددة اللغات، أو أدوات الأرشفة يواجهون هذه المشكلة باستمرار. الخبر السار؟ مع Aspose.OCR يمكنك **استخراج النص من الصورة** ببضع أسطر من الشيفرة، والمكتبة تعتني أيضاً بخصائص الكتابة من اليمين إلى اليسار (RTL) نيابةً عنك.

في هذا الدرس سنستعرض مثالاً عملياً يوضح لك كيفية **معالجة صورة عربية**، الحفاظ على ترتيب Unicode، وأخيراً **قراءة النص من اليمين إلى اليسار** في تطبيق كونسول. في النهاية ستحصل على برنامج جاهز يمكنك إدراجه في أي مشروع .NET.

## المتطلبات المسبقة – ما ستحتاجه قبل البدء

- **.NET 6.0 أو أحدث** (الكود يعمل أيضاً على .NET Framework 4.7+)
- حزمة NuGet **Aspose.OCR for .NET** (`Aspose.OCR`)
- صورة نموذجية تحتوي على أحرف عربية أو أردية (مثال: `arabic_invoice.png`)
- بيئة تطوير (Visual Studio، Rider، أو VS Code)

إذا لم تقم بإضافة حزمة NuGet بعد، افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا كل ما تحتاجه—لا ملفات DLL أصلية، ولا ثنائيات خارجية. Aspose يتولى كل شيء، بما في ذلك تنزيل موارد حزمة اللغة العربية تلقائيًا.

## الخطوة 1: تكوين محرك OCR للغة العربية (والأردية) – الإعداد الأساسي

أول شيء يجب فعله هو إخبار محرك OCR أي لغة نتوقعها. العربية هي نص **من اليمين إلى اليسار**، والمكتبة توفر نموذج لغة مخصص يغطي أيضاً الأحرف الأردية.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

// Step 1: Set up OCR configuration for Arabic
var ocrConfig = new OcrEngineConfig
{
    Language = Language.Arabic,          // Enables Arabic & Urdu support
    AutoDownloadResources = true        // Downloads language data on first run
};
```

> **لماذا هذا مهم:**  
> بتعيين `Language.Arabic` صراحةً، يطبق المحرك مجموعة الأحرف وقواعد التخطيط الصحيحة. علم `AutoDownloadResources` يوفر عليك وضع ملفات اللغة يدوياً على الخادم—Aspose يقوم بتنزيلها في المرة الأولى التي تشغّل فيها الكود.

## الخطوة 2: إنشاء محرك OCR باستخدام التكوين

الآن بعد أن أصبح كائن التكوين جاهزًا، يمكنك إنشاء محرك OCR الفعلي. استخدام جملة `using` يضمن تحرير الموارد غير المُدارة بشكل صحيح.

```csharp
// Step 2: Create the OCR engine with the Arabic configuration
using var ocrEngine = new OcrEngine(ocrConfig);
```

> **نصيحة احترافية:**  
> إذا كنت تخطط لمعالجة العديد من الصور دفعة واحدة، احتفظ بـ `OcrEngine` فعالاً طوال الدفعة بدلاً من إنشائه لكل صورة. هذا يقلل من الحمل الزائد ويسرّع المعالجة.

## الخطوة 3: التعرف على النص من صورة من اليمين إلى اليسار

مع المحرك في يدك، استدعِ `RecognizeImage` ووجهه إلى ملفك. تُعيد الطريقة كائن `OcrResult` يحتوي على سلسلة Unicode التي تم التعرف عليها.

```csharp
// Step 3: Perform OCR on an Arabic image file
var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/arabic_invoice.png");
```

> **ملاحظة حول الحالات الحدية:**  
> إذا كان مسار الصورة غير صحيح أو الملف غير قابل للوصول، فإن `RecognizeImage` يطرح استثناءً. احرص على تغليف الاستدعاء داخل كتلة `try/catch` في الكود الإنتاجي.

## الخطوة 4: إخراج النص Unicode المُعترف به – الحفاظ على اتجاه RTL

أخيرًا، اكتب النص المستخرج إلى الكونسول (أو أي مخرج آخر). محرك OCR يُعيد النص بالفعل بالترتيب المنطقي الصحيح، لذا لا تحتاج إلى أي معالجة إضافية للسلسلة.

```csharp
// Step 4: Print the recognized text – RTL direction is preserved
System.Console.WriteLine(ocrResult.Text);
```

تشغيل البرنامج يجب أن يعرض شيئًا مشابهًا لـ:

```
فاتورة رقم 12345
التاريخ: 01/09/2023
المبلغ: ٥٠٠٠ ريال
```

هذا هو **قراءة النص من اليمين إلى اليسار** الذي كنت تبحث عنه—بدون الحاجة إلى معالجة تخطيط إضافية.

### مثال كامل يعمل

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه ولصقه في مشروع كونسول جديد.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;

class RtlDemo
{
    static void Main()
    {
        // Configure OCR for Arabic (includes Urdu) and enable auto‑download
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.Arabic,
            AutoDownloadResources = true
        };

        // Create OCR engine with the configuration
        using var ocrEngine = new OcrEngine(ocrConfig);

        // Recognize text from the Arabic image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/arabic_invoice.png");

        // Output the recognized Unicode text (preserves RTL direction)
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **الناتج المتوقع:** يطبع الكونسول النص العربي تمامًا كما يظهر في الصورة المصدر، مع الحفاظ على الأرقام وعلامات الترقيم وفواصل الأسطر.

## كيفية استخراج النص من ملفات صور غير PNG

Aspose.OCR لا يقتصر على PNG فقط. يمكنك تمرير JPEG، BMP، TIFF، أو حتى صفحات PDF مباشرة:

```csharp
// Recognize a JPEG image
var jpegResult = ocrEngine.RecognizeImage("sample.jpg");

// Recognize a TIFF (multi‑page) – choose the first page
var tiffResult = ocrEngine.RecognizeImage("multi_page.tiff", pageIndex: 0);
```

إذا كنت بحاجة إلى **استخراج النص من الصورة** عبر تدفقات (مثلاً عند الرفع عبر API ويب)، استخدم النسخة التي تقبل `byte[]` أو `Stream`:

```csharp
using var stream = File.OpenRead("upload.png");
var streamResult = ocrEngine.RecognizeImage(stream);
```

## المشكلات الشائعة عند العمل مع ملفات صور OCR عربية

| المشكلة | السبب | الحل السريع |
|-------|--------|-------------|
| ظهور أحرف مشوشة | دقة الصورة منخفضة أو وجود ضوضاء ضغط | استخدم مصدرًا بدقة أعلى (≥300 dpi) |
| فقدان الحركات | نموذج اللغة غير محمّل | تأكد من `AutoDownloadResources = true` أو ضع نموذج العربية يدويًا في مجلد الموارد |
| النص يظهر من اليسار إلى اليمين | عرض الإخراج في واجهة تُجبر على LTR | استخدم عناصر تحكم تدعم Unicode (`RichTextBox`، `TextMeshPro` في Unity) أو عيّن `FlowDirection = RightToLeft` في WPF/WinForms |
| بطء التشغيل الأول | تنزيل حزمة اللغة | شغّل مرة واحدة على جهاز متصل بالإنترنت أو حمّل ملفات اللغة مسبقًا |

معالجة هذه القضايا مبكرًا توفر عليك وقتًا ثمينًا وتجنبك الأخطاء الغامضة لاحقًا.

## إضافي: حفظ النص المُعترف به إلى ملف

إذا كنت تفضّل تخزين نتيجة OCR بدلاً من طباعتها، يكفي استدعاء `File.WriteAllText` بسيط:

```csharp
string outputPath = "extracted_arabic.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
System.Console.WriteLine($"Text saved to {outputPath}");
```

سيحتفظ ملف الإخراج بترميز UTF‑8، مما يضمن بقاء الأحرف العربية سليمة.

## الخلاصة – ما أنجزناه

لقد أظهرنا لك كيفية **التعرف على النص العربي** باستخدام Aspose.OCR، **استخراج النص من الصورة**، وقراءة **النص من اليمين إلى اليسار** بشكل صحيح في تطبيق كونسول .NET. تدفق الخطوات الأربع—التكوين، الإنشاء، التعرف، والإخراج—يغطي النمط الأساسي الذي ستعيد استخدامه لأي لغة RTL، سواء كانت عربية، أردية، أو عبرية.

هل أنت مستعد للتحدي التالي؟ جرّب معالجة دفعة من الفواتير، ربط النتائج بخدمة ترجمة، أو دمج الكود في API ASP .NET Core يُعيد سلاسل JSON مشفّرة بالعربية. الاحتمالات لا حصر لها، والمبادئ نفسها تنطبق: تكوين اللغة الصحيح، إدارة الموارد، وإخراج يدعم Unicode.

هل لديك أسئلة حول معالجة ملفات PDF متعددة الصفحات أو تعديل عتبات الثقة؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}