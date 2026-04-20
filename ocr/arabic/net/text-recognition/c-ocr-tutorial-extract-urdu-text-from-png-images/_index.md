---
category: general
date: 2026-03-21
description: 'دليل C# OCR: تعلم كيفية استخراج النص الأردي من صورة PNG باستخدام OCR
  في C#. يتضمن كودًا خطوة بخطوة، وإعداد اللغة، ونصائح عملية.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: ar
og_description: 'دروس C# OCR: تعلم كيفية استخراج النص الأردي من صورة PNG باستخدام
  OCR في C#. دليل كامل مع الشيفرة والنصائح.'
og_title: دروس C# OCR – استخراج النص الأردي من صور PNG
tags:
- OCR
- C#
- Urdu
- Image Processing
title: دليل OCR بلغة C# – استخراج النص الأردي من صور PNG
url: /ar/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – استخراج نصّ أردو من صور PNG

هل احتجت إلى **c# ocr tutorial** يَستخرج فعلاً نصّ أردو من ملف PNG؟ لست وحدك. في العديد من المشاريع—معالجة الفواتير، أرشفة المستندات، أو حتى أداة ترجمة سريعة—ستصادف النقطة التي يجب فيها التعرف على بيانات نصّ الصورة، وتكون اللغة مهمة.  

في هذا الدليل سنستعرض حلًا كاملاً وجاهزًا للتنفيذ يُستخرج نصّ أردو من PNG باستخدام محرك OCR. ستعرف لماذا كل سطر موجود، وكيفية التعامل مع حزم اللغة المفقودة، وماذا تفعل إذا لم تكن الصورة مثالية. بنهاية الدليل ستكون واثقًا بما يكفي لتكييف الشيفرة مع لغات أو أنواع ملفات أخرى.

## ما ستتعلمه

- كيفية إعداد مكتبة OCR للـ C# (بدون سحر مخفي)  
- الخطوات الدقيقة **لاستخراج نصّ أردو** من ملف PNG  
- لماذا تكوين اللغة إلى أردو مهم وكيف يقوم المحرك بتنزيل البيانات المفقودة تلقائيًا  
- طرق التحقق من المخرجات واستكشاف الأخطاء الشائعة  

لا توجد حاجة لروابط توثيق خارجية—كل ما تحتاجه موجود هنا.

## المتطلبات المسبقة (ما تحتاجه قبل البدء)

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | واجهات برمجة تطبيقات حديثة ودعم غير متزامن |
| Visual Studio 2022 (or VS Code with C# extension) | بيئة تطوير متكاملة مع IntelliSense تجعل الشيفرة أوضح |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | توفر طرق `Language.Urdu` و `Recognize` |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | المصدر لعملية **recognize text image** |

إذا لم يكن لديك حزمة OCR بعد، نفّذ هذا السطر الواحد في وحدة تحكم مدير الحزم:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

سوف يجلب ذلك الفئة `OcrEngine` التي سنستخدمها لاحقًا.

> **نصيحة احترافية:** يقوم الـ SDK تلقائيًا بجلب بيانات اللغة عند الاستخدام الأول، لذا لا تحتاج إلى تنزيل حزم لغة الأردو يدويًا.

## الخطوة 1: تثبيت وإضافة مرجع لمكتبة OCR

قبل أن نتمكن من إنشاء محرك، يجب على المشروع إضافة مرجع لحزمة OCR. أضف توجيهات `using` التالية في أعلى ملفك:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

هذه المساحات الاسمية تمنحنا الوصول إلى `OcrEngine` و `Language` وأدوات تحميل الصور. إذا كنت تستخدم مكتبة مختلفة، ابحث عن مساحات اسمية مماثلة.

## الخطوة 2: إنشاء كائن محرك OCR  

الآن نقوم فعليًا بتشغيل المحرك. فكر في المحرك كالعقل الذي سيُفسّر نمط البكسلات كحروف.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**لماذا هذا مهم:** تُعيد `TryCreateFromLanguage` قيمة `null` إذا لم تكن بيانات اللغة موجودة، مما يمنحنا فرصة للفشل السريع بدلاً من التعطل لاحقًا.

## الخطوة 3: تحميل صورة PNG  

يعمل محرك OCR مع كائنات `SoftwareBitmap`، وليس مع مسارات الملفات الخام. الأداة المساعدة التالية تقوم بتحميل PNG من القرص وتحويله إلى الصيغة المطلوبة.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**حالة خاصة:** إذا كان PNG ملونًا، فإن التحويل إلى تدرج الرمادي (`Gray8`) غالبًا ما يحسن التعرف، خاصةً للخطوط مثل الأردو التي تحتوي على علامات تشكيل دقيقة.

## الخطوة 4: التعرف على النص من الصورة  

هذا هو جوهر **c# ocr tutorial**—طلب من المحرك قراءة الصورة.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

خاصية `OcrResult.Text` تحتوي على سلسلة Unicode الخام. لأننا ضبطنا اللغة إلى أردو مسبقًا، يطبق المحرك قواعد الخط الصحيحة.

## الخطوة 5: إخراج والتحقق من النص المستخرج  

أخيرًا، نطبع النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تقوم بتخزينها في قاعدة بيانات أو تمريرها إلى خدمة ترجمة.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**ما المتوقع:** إذا كانت الصورة واضحة، سترى شيئًا مثل:

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

إذا كان الإخراج مشوشًا، تحقق من جودة الصورة (التباين، الضوضاء) وفكّر في معالجتها مسبقًا (مثلًا، التحويل إلى ثنائي).

## كيفية استخراج نصّ أردو من ملف PNG – المشكلات الشائعة  

1. **تباين منخفض** – يواجه OCR صعوبة عندما تكون ألوان المقدمة والخلفية متشابهة. استخدم أدوات تحرير الصور لزيادة التباين قبل تشغيل الشيفرة.  
2. **دقة DPI غير صحيحة** – المسح بدقة 300 dpi أو أعلى يمنح المحرك تفاصيل أكثر للعمل معها.  
3. **حزمة لغة مفقودة** – قد يؤدي الاستدعاء الأول لـ `TryCreateFromLanguage` إلى تنزيل؛ تأكد من أن جهازك متصل بالإنترنت.  

معالجة هذه القضايا تحسن بشكل كبير معدل نجاح **recognize text image**.

## Recognize Text Image: التوسيع إلى صيغ أخرى  

بينما يركز هذا الدرس على PNG، فإن سير العمل نفسه يعمل مع JPEG أو BMP أو TIFF—فقط غيّر امتداد الملف وتأكد من أن المُفسّر يدعم ذلك. السطر الأساسي يبقى `await ocrEngine.RecognizeAsync(bitmap);`.

## نصائح لـ OCR من ملف PNG – الأداء والتوسيع  

- **معالجة دفعات:** حمّل عدة صور في قائمة وشغّل `Task.WhenAll` لتوازي التعرف.  
- **تخزين المحرك مؤقتًا:** أنشئ كائن `OcrEngine` واحد وأعد استخدامه عبر الاستدعاءات؛ إنشاءه مرارًا يضيف عبئًا.  
- **إدارة الذاكرة:** حرّر كائنات `SoftwareBitmap` بعد الاستخدام (`bitmap.Dispose()`) للحفاظ على خفة العملية.  

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله. يتضمن جميع عبارات `using`، معالجة الـ async، وفحوصات الأخطاء.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**الناتج المتوقع:** تطبع وحدة التحكم الأحرف الأردوية الدقيقة الموجودة في الصورة، مع الحفاظ على ترتيب من اليمين إلى اليسار.

## الخلاصة  

لقد أكملت للتو **c# ocr tutorial** يوضح كيفية **استخراج نصّ أردو** من PNG، وضبط اللغة، ومعالجة النتيجة بأمان. الخطوات—تثبيت المكتبة، إنشاء المحرك، تحميل الصورة، التعرف على النص، وإخراجه—تشكل نمطًا قابلًا لإعادة الاستخدام يمكنك تطبيقه على أي خط أو نوع ملف.  

بعد ذلك، فكر في تجربة **recognize text image** على ملفات PDF متعددة الصفحات (حوّل كل صفحة إلى PNG أولاً) أو دمج واجهة برمجة تطبيقات ترجمة لتحويل الأردو المستخرج إلى الإنجليزية تلقائيًا. السماء هي الحد عندما تتقن هذا سير العمل الأساسي.

برمجة سعيدة، ولتكن نتائج OCR واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}