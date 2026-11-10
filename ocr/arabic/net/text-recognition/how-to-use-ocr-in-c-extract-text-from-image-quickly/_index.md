---
category: general
date: 2026-04-08
description: كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور. تعلم قراءة النص
  من JPG، إجراء تحويل الصورة إلى نص، وتحويل الصورة إلى سلسلة باستخدام Aspose.Ocr.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from jpg
- image to text conversion
- convert image to string
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من الصور. يوضح لك هذا الدرس
  كيفية قراءة النص من ملفات JPG، وإجراء تحويل الصورة إلى نص، وتحويل الصورة إلى سلسلة.
og_title: كيفية استخدام OCR في C# – دليل سريع لتحويل الصورة إلى نص
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص من الصورة بسرعة
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصورة بسرعة

هل تساءلت يومًا **كيف تستخدم OCR** عندما تحتاج إلى استخراج الكلمات من صورة؟ ربما لديك إيصالًا ممسوحًا ضوئيًا، أو لقطة شاشة لعلامة، أو صفحة من صحيفة هندية ولا يمكنك نسخ‑لصق النص. هذا سيناريو كلاسيكي لـ *استخراج النص من الصورة*، والخبر السار هو أنك لا تحتاج إلى خدمة سحابية أو إلى درجة دكتوراه في رؤية الحاسوب.

في هذا الدليل سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح **كيفية استخدام OCR** مع مكتبة Aspose.OCR، قراءة النص من ملف JPG، والانتهاء بـ **تحويل الصورة إلى نص** يمنحك سلسلة C# عادية. في النهاية ستعرف بالضبط كيف **تحول الصورة إلى سلسلة** وستمتلك أساسًا قويًا لأي مشروع متعلق بـ OCR تتعامل معه لاحقًا.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+ – الـ API يعمل بنفس الطريقة)
- **Visual Studio 2022** أو أي محرر تفضله
- حزمة **Aspose.OCR** على NuGet (`Install-Package Aspose.OCR`)
- صورة عينة (`hindi_sample.jpg`) موجودة في مكان ما على القرص
- قليل من الفضول والرغبة في التجربة

هذا كل شيء—بدون خدمات إضافية، بدون استدعاءات إنترنت (سنقوم حتى بتمكين **وضع عدم الاتصال**). لنبدأ.

## كيفية استخدام OCR: إعداد البيئة

الشيء الأول الذي عليك فعله قبل أن تتمكن من **استخدام OCR** هو جعل المكتبة متاحة لمشروعك.

```csharp
// Open a terminal in your solution folder and run:
dotnet add package Aspose.OCR
```

> **لماذا هذا مهم:** إضافة الحزمة تجلب جميع الثنائيات الأصلية التي تحتاجها Aspose لحزم اللغات، وفك تشفير الصور، ومحرك OCR نفسه. تخطي هذه الخطوة سيؤدي إلى حدوث `FileNotFoundException` أثناء التشغيل.

بمجرد تثبيت الحزمة، افتح ملف `Program.cs` (أو أي فئة تريدها) وأضف توجيهات `using` المطلوبة:

```csharp
using Aspose.Ocr;
using System;
```

الآن أنت جاهز لـ **قراءة النص من ملفات JPG**.

## استخراج النص من الصورة – التعرف على JPG هندي

فيما يلي برنامج **كامل ومستقل** يوضح سير العمل الأساسي. انتبه إلى التعليقات؛ فهي تشرح *السبب* وراء كل سطر.

```csharp
using Aspose.Ocr;
using System;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance – this object holds all settings.
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable offline mode so the engine works without network access.
            //    Offline mode uses the language data that ships with the package.
            ocrEngine.Options.OfflineMode = true;

            // 3️⃣ Choose the language. "hi" is the ISO code for Hindi.
            //    You can replace this with "en" for English, "fr" for French, etc.
            ocrEngine.Language = "hi";

            // 4️⃣ Provide the path to the image you want to process.
            //    Make sure the file exists; otherwise you'll get an exception.
            string imagePath = @"YOUR_DIRECTORY\hindi_sample.jpg";

            // 5️⃣ Run the recognition. The result object contains the extracted text.
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### الناتج المتوقع

إذا كان `hindi_sample.jpg` يحتوي على العبارة “नमस्ते दुनिया” (Hello World)، فستظهر وحدة التحكم شيئًا مثل:

```
=== OCR Result ===
नमस्ते दुनिया
```

هذا هو **تحويل الصورة إلى نص** الذي كنت تبحث عنه—بدون خطوات إضافية، مجرد سلسلة نظيفة يمكنك تخزينها أو البحث فيها أو عرضها.

## قراءة النص من JPG – التعامل مع وضع عدم الاتصال

قد تتساءل، “ماذا لو كنت على جهاز بدون إنترنت؟” هذا هو المكان الذي يبرز فيه **وضع عدم الاتصال**. عندما تضبط `ocrEngine.Options.OfflineMode = true`، تستخدم Aspose حزم اللغات المدمجة بدلاً من الاتصال بنقطة سحابية. هذا يضمن:

- **أداء حتمي** – بدون تقلبات في الكمون.
- **الامتثال** – البيانات لا تغادر الجهاز المضيف أبداً.
- **قابلية النقل** – يمكنك توزيع الثنائي إلى بيئات معزولة.

إذا احتجت في أي وقت للعودة إلى وضع الاتصال (للحصول على أحدث تحديثات اللغات)، فقط اضبط `OfflineMode = false` وقدم مفتاح API عبر `ocrEngine.License = new License("your_license_file.lic")`.

## تحويل الصورة إلى نص – الحصول على النتيجة كسلسلة

خاصية `ocrResult.Text` تعطيك بالفعل نتيجة **تحويل الصورة إلى سلسلة**، لكن هناك بعض التحسينات التي قد ترغب في تطبيقها:

```csharp
string rawText = ocrResult.Text;

// Trim whitespace and normalize line endings for easier downstream processing.
string cleanedText = rawText.Trim().Replace("\r\n", "\n");

// Optional: Remove any non‑Unicode characters that the OCR might have mis‑read.
cleanedText = System.Text.RegularExpressions.Regex.Replace(cleanedText, @"[^\u0000-\uFFFF]", string.Empty);

Console.WriteLine("Cleaned OCR Output:");
Console.WriteLine(cleanedText);
```

هذه الخطوات الإضافية تحول ناتج OCR الخام إلى سلسلة مرتبة جاهزة للتخزين في قاعدة بيانات، أو لإدخالها في فهرس بحث، أو لتغذيتها إلى API ترجمة.

## المشكلات الشائعة والنصائح الاحترافية

| المشكلة | سبب حدوثه | كيفية الإصلاح / التجنب |
|-------|----------------|--------------------|
| **الملف غير موجود** | مسار غير صحيح أو صورة مفقودة. | استخدم `Path.Combine` وتحقق من وجود الملف باستخدام `File.Exists(imagePath)` قبل استدعاء `RecognizeImage`. |
| **حروف غير مفهومة** | صورة منخفضة الدقة أو حزمة لغة غير مدعومة. | قم بمعالجة مسبقة للصورة: زيادة DPI، تحويل إلى تدرج الرمادي، أو استخدم `ocrEngine.Options.ImagePreprocess = true`. |
| **نتيجة فارغة** | وضع عدم الاتصال بدون بيانات اللغة المطلوبة. | تأكد من أن رمز اللغة (`ocrEngine.Language`) يطابق حزمة مدمجة، أو قم بتحميل الحزمة من Aspose واضبط `ocrEngine.Options.LanguageDataPath`. |
| **تأخر الأداء** | معالجة دفعات كبيرة دون إعادة استخدام المحرك. | أعد استخدام كائن `OcrEngine` واحد لعدة صور؛ غير `Language` فقط إذا لزم الأمر. |
| **استثناءات الترخيص** | تشغيل نسخة التجربة بعد انتهاء فترة التقييم. | استخدم ملف ترخيص صالح عبر `ocrEngine.License = new License("Aspose.OCR.lic");`. |

> **نصيحة احترافية:** إذا كنت تخطط لمعالجة العديد من الصور، غلف استدعاء OCR داخل حلقة `Parallel.ForEach` مع الحفاظ على أن المحرك آمن للخطوط (`ocrEngine.IsThreadSafe = true`). هذا يمكن أن يقلل وقت المعالجة بشكل كبير على الأجهزة متعددة الأنوية.

## مثال كامل يعمل (جميع الخطوات في ملف واحد)

لمن يحب النسخ‑اللصق، إليكم البرنامج الكامل من البداية إلى النهاية، بما في ذلك منطق التنظيف الاختياري:

```csharp
using Aspose.Ocr;
using System;
using System.IO;
using System.Text.RegularExpressions;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Verify the image exists
            string imagePath = @"YOUR_DIRECTORY\hindi_sample.jpg";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }

            // Initialize OCR engine
            var ocrEngine = new OcrEngine
            {
                // Work offline – no network calls
                Options = { OfflineMode = true },

                // Set language (Hindi in this case)
                Language = "hi"
            };

            // Recognize the image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // Basic output
            Console.WriteLine("=== Raw OCR Result ===");
            Console.WriteLine(ocrResult.Text);

            // Clean the text for further use
            string cleaned = ocrResult.Text
                .Trim()
                .Replace("\r\n", "\n");
            cleaned = Regex.Replace(cleaned, @"[^\u0000-\uFFFF]", string.Empty);

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
    }
}
```

شغّل البرنامج (`dotnet run` من مجلد المشروع) وسترى كل من السلاسل الخام والمنقحة مطبوعة في وحدة التحكم. هذا هو جوهر **تحويل الصورة إلى سلسلة** باستخدام Aspose.OCR.

## المواضيع ذات الصلة التي قد تستكشفها لاحقًا

- **Batch OCR processing** – تكرار عبر مجلد من ملفات JPG وكتابة كل نتيجة إلى ملف نصي.
- **Language detection** – السماح للمحرك بتخمين اللغة قبل ضبط `ocrEngine.Language`.
- **PDF OCR** – استخراج النص من ملفات PDF الممسوحة ضوئيًا عن طريق تحويل كل صفحة إلى صورة أولاً.
- **Integrating with Azure Functions** – تقديم OCR كواجهة برمجة تطبيقات خالية من الخوادم للتحويل الفوري من صورة إلى نص.

## الخلاصة

لقد غطينا **كيفية استخدام OCR** في C# من تثبيت المكتبة إلى تنفيذ **تحويل الصورة إلى نص** نظيف. الآن تعرف كيف **استخراج النص من الصور**، **قراءة النص من ملفات JPG**، و**تحويل الصورة إلى سلسلة** للمعالجة اللاحقة—كل ذلك دون الحاجة للإنترنت بفضل وضع عدم الاتصال.

جرّبه مع حزمة لغة مختلفة، أو استخدم صورة ذات دقة أعلى، أو غلف المنطق في خدمة ويب. السماء هي الحد، ولديك أساس قوي وجدير بالاستشهاد لتبني عليه.

---

![how to use OCR on a sample JPG image](image-placeholder.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}