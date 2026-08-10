---
category: general
date: 2026-05-02
description: تعلم كيفية اكتشاف لغة الصورة واستخراج النص من الصورة باستخدام Aspose
  OCR. يوضح هذا الدليل خطوة بخطوة كيفية تحويل الصورة إلى نص وإجراء OCR على ملفات JPG.
draft: false
keywords:
- detect image language
- extract text from image
- convert image to text
- recognize image text
- perform ocr jpg
language: ar
og_description: اكتشف لغة الصورة بسرعة باستخدام Aspose OCR. اتبع هذا الدليل لاستخراج
  النص من الصورة، تحويل الصورة إلى نص، وإجراء OCR للصور بصيغة JPG في C#.
og_title: اكتشاف لغة الصورة في C# – دليل OCR كامل
tags:
- C#
- OCR
- Aspose
title: اكتشاف لغة الصورة في C# – دليل كامل للتعرف الضوئي على الأحرف واستخراج النص
url: /ar/net/text-recognition/detect-image-language-in-c-complete-guide-to-ocr-text-extrac/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# اكتشاف لغة الصورة في C# – دليل شامل لتقنية OCR واستخراج النص

هل احتجت يوماً إلى اكتشاف لغة الصورة قبل استخراج النص؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير أو قارئات العلامات متعددة اللغات—يجب أولاً معرفة *ما* هي اللغة التي تحتويها الصورة، ثم يمكنك استخراج الأحرف بأمان.

في هذا الدرس سنوضح لك بالضبط كيفية اكتشاف لغة الصورة **و** استخراج النص من الصورة باستخدام مكتبة Aspose.OCR لـ .NET. سنغطي أيضاً كيفية تحويل الصورة إلى نص، التعرف على نص الصورة في ملفات JPG، ومعالجة بعض المشكلات الشائعة. لا مراجع غامضة للوثائق الخارجية؛ كل ما تحتاجه موجود هنا.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). الشيفرة تعمل مع أي بيئة تشغيل حديثة.
- حزمة NuGet **Aspose.OCR for .NET** (`Aspose.OCR`). ثبّتها باستخدام `dotnet add package Aspose.OCR`.
- صورة تحتوي فعلياً على نص أوكراني (أو أي لغة أخرى)، مثال: `ukrainian_sign.jpg`.
- بيئة تطوير مفضلة (Visual Studio، Rider، VS Code—اختر ما يناسبك).

هذا كل شيء. إذا كان لديك هذه المكوّنات، يمكنك القفز مباشرة إلى الشيفرة.

![اكتشاف لغة الصورة باستخدام Aspose OCR في C#](https://example.com/aspose-ocr-demo.png "اكتشاف لغة الصورة باستخدام Aspose OCR في C#")

## الخطوة 1: إعداد محرك OCR (اكتشاف لغة الصورة)

إنشاء كائن محرك OCR هو أول ما تقوم به. فكر في المحرك كالعقل الذي سيتفحص البكسلات، يقرر اللغة، ثم يقرأ الأحرف.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class UkrainianExample
{
    public static void Run()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which language to expect
        ocrEngine.Settings.Language = Language.Ukrainian;

        // Step 3: Run OCR on the image file
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Step 4: Show what the engine detected
        Console.WriteLine("Detected language: " + ocrResult.DetectedLanguage);
        Console.WriteLine(ocrResult.Text);
    }
}
```

**لماذا نحدد `Language.Ukrainian`** – بإخبار المحرك صراحةً باللغة المتوقعة، تحسّن الدقة بشكل كبير. إذا تركتها على `Auto`، سيحاول المحرك التخمين، ما قد يكون أبطأ وأحياناً خاطئاً، خصوصاً للخطوط المتشابهة.

## الخطوة 2: استخراج النص من الصورة (تحويل الصورة إلى نص)

استدعاء `RecognizeImage` يقوم بوظيفتين في آن واحد: **يكتشف لغة الصورة** و**يحوّل الصورة إلى نص**. خاصية `ocrResult.Text` تحتفظ بالتمثيل النصي الصافي للصورة.

```csharp
// After the OCR call:
string extracted = ocrResult.Text;
Console.WriteLine("Extracted text:");
Console.WriteLine(extracted);
```

إذا كنت تهتم فقط بالسلسلة النصية الخام، يمكنك تخطي فحص `DetectedLanguage`. ومع ذلك، طباعتها طريقة سريعة للتحقق من نجاح اكتشاف اللغة.

## الخطوة 3: التعامل مع أنواع ملفات مختلفة – تنفيذ OCR على JPG

يدعم Aspose.OCR صيغ PNG، BMP، TIFF، وبالطبع JPG. طريقة `RecognizeImage` نفسها تعمل مع أي منها، لكن ملفات JPG معروفة بوجود تشوهات ضغط. نصيحة سريعة: فعّل خيار `Preprocess` لتنظيف الضوضاء.

```csharp
// Enable preprocessing for JPEG images
ocrEngine.Settings.Preprocess = true;

// Now run OCR on a JPEG file
var jpegResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/sample_photo.jpg");
Console.WriteLine("JPEG text: " + jpegResult.Text);
```

**نصيحة محترف:** إذا كانت الصورة مظلمة أو ذات تباين منخفض، اضبط `ocrEngine.Settings.Binarization` قبل استدعاء `RecognizeImage`. هذا غالباً ما ينتج مخرجات `recognize image text` أنظف.

## الخطوة 4: التعرف على نص الصورة بلغات متعددة

أحياناً يكون لديك مجموعة من الصور، قد تكون كل واحدة بلغة مختلفة. يمكنك المرور عليها وضبط اللغة ديناميكياً بناءً على خوارزمية بسيطة أو خطوة اكتشاف سابقة.

```csharp
string[] files = { "ukrainian_sign.jpg", "english_notice.jpg", "russian_banner.jpg" };
foreach (var file in files)
{
    // Let the engine guess the language first
    var guessResult = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{file} – guessed language: {guessResult.DetectedLanguage}");

    // If you know the language, set it for a second pass (higher accuracy)
    if (guessResult.DetectedLanguage == "Ukrainian")
        ocrEngine.Settings.Language = Language.Ukrainian;
    else if (guessResult.DetectedLanguage == "English")
        ocrEngine.Settings.Language = Language.English;
    // Add more branches as needed

    var finalResult = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"Final text from {file}:");
    Console.WriteLine(finalResult.Text);
}
```

هذا النمط يوضح كيفية **التعرف على نص الصورة** بفعالية مع الاستفادة من قدرة اكتشاف اللغة.

## الخطوة 5: جمع كل شيء معاً – مثال كامل يعمل

فيما يلي برنامج مستقل يمكنك نسخه ولصقه في مشروع Console. يوضح اكتشاف اللغة، استخراج النص، التعامل مع خصوصيات JPG، وطباعة كل شيء بشكل منسق.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise the engine once – reuse it for every image
            var engine = new OcrEngine
            {
                Settings =
                {
                    // Turn on preprocessing for noisy JPEGs
                    Preprocess = true,
                    // Optional: you could start with Auto detection
                    Language = Language.Auto
                }
            };

            string[] images = {
                "YOUR_DIRECTORY/ukrainian_sign.jpg",
                "YOUR_DIRECTORY/sample_photo.jpg"
            };

            foreach (var path in images)
            {
                // First pass – let the engine guess the language
                var preliminary = engine.RecognizeImage(path);
                Console.WriteLine($"File: {path}");
                Console.WriteLine($"Detected language (pre‑check): {preliminary.DetectedLanguage}");

                // If we have a confident guess, lock it in for a second pass
                if (preliminary.DetectedLanguage != null)
                {
                    // Map string to enum – simple switch works for demo purposes
                    engine.Settings.Language = preliminary.DetectedLanguage switch
                    {
                        "Ukrainian" => Language.Ukrainian,
                        "English"   => Language.English,
                        "Russian"   => Language.Russian,
                        _           => Language.Auto
                    };
                }

                // Second pass – actual text extraction
                var finalResult = engine.RecognizeImage(path);
                Console.WriteLine("Final detected language: " + finalResult.DetectedLanguage);
                Console.WriteLine("Extracted text:");
                Console.WriteLine(finalResult.Text);
                Console.WriteLine(new string('-', 40));
            }

            Console.WriteLine("All done! You've successfully detected image language and extracted text.");
        }
    }
}
```

### النتيجة المتوقعة

```
File: YOUR_DIRECTORY/ukrainian_sign.jpg
Detected language (pre‑check): Ukrainian
Final detected language: Ukrainian
Extracted text:
Вітаємо! Це українська вивіска.
----------------------------------------
File: YOUR_DIRECTORY/sample_photo.jpg
Detected language (pre‑check): English
Final detected language: English
Extracted text:
Welcome to the OCR demo.
----------------------------------------
All done! You've successfully detected image language and extracted text.
```

إذا شغّلت البرنامج ورأيت شيئاً مشابهاً، تهانينا—لقد **حوّلت الصورة إلى نص** وتأكدت من اكتشاف اللغة بنجاح.

## المشكلات الشائعة وكيفية حلها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| أحرف مشوشة، خصوصاً مع السيريالية | ضبط `Language` غير صحيح أو عدم وجود دعم Unicode | تأكد أن `ocrEngine.Settings.Language` يطابق اللغة الفعلية؛ ثبّت حزمة Aspose OCR الكاملة (تحتوي على جداول Unicode). |
| خروج سلسلة فارغة | الصورة مظلمة جداً، دقة منخفضة، أو `Preprocess` معطل لملفات JPG | فعّل `Preprocess = true` وفكّر بزيادة DPI الصورة إلى ≥300. |
| اكتشاف لغة خاطئة للعلامات متعددة اللغات | المحرك يتوقف عند أول نص قابل للتعرف | استخدم نهج **مرتين**: اكتشاف تلقائي، ثم تثبيت اللغة للتمرير الثاني (كما هو موضح في الخطوة 5). |
| بطء الأداء عند معالجة دفعات كبيرة | إنشاء `OcrEngine` جديد لكل ملف | أعد استخدام كائن `OcrEngine` واحد؛ غير `Settings.Language` فقط عند الحاجة. |

## توسيع الحل

- **معالجة دفعات:** غلف الحلقة داخل `Parallel.ForEach` للاستفادة من تعدد الأنوية.
- **صيغ الإخراج:** احفظ `ocrResult.Text` في ملف `.txt` أو قاعدة بيانات.
- **التكامل مع ASP.NET:** قدّم منطق OCR عبر نقطة نهاية Web API تستقبل صور بصيغة multipart/form‑data.

كل هذه الإضافات لا تزال تعتمد على الفكرة الأساسية: **اكتشاف لغة الصورة** أولاً، ثم **استخراج النص من الصورة**.

## الخلاصة

أصبح لديك الآن مثال شامل من البداية إلى النهاية ي **اكتشف لغة الصورة**، ي **تعرف على نص الصورة**، وي **حوّل الصورة إلى نص** باستخدام Aspose OCR في C#. غطى الدرس كل شيء من إعداد المحرك، التعامل مع خصائص JPEG، التكرار على ملفات متعددة، وحل المشكلات الشائعة.

الخطوة التالية: جرّب استبدال `Language.Ukrainian` بلغات أخرى مدعومة أو مرّر ناتج OCR إلى واجهة برمجة تطبيقات ترجمة. هل تريد معالجة ملفات PDF أو مستندات ممسوحة؟ نفس النمط يُطبق—فقط مرّر bitmap مستخرج من صفحة PDF.

لا تتردد في التجربة، مشاركة النتائج، أو طرح الأسئلة في التعليقات. برمجة سعيدة، ولتكن مشاريع OCR دقيقة دائماً!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}