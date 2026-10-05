---
category: general
date: 2025-12-29
description: دليل C# OCR يوضح كيفية التعرف على النص من ملف JPG، إجراء OCR على الصورة
  وتحميل الصورة للـ OCR باستخدام Aspose.OCR. دليل سريع وشامل.
draft: false
keywords:
- c# ocr tutorial
- recognize text from jpg
- perform ocr on image
- load image for ocr
language: ar
og_description: دروس C# OCR التي ترشدك عبر التعرف على النص من JPG، وإجراء OCR على
  الصورة، وتحميل الصورة لـ OCR باستخدام Aspose.OCR.
og_title: دليل OCR بلغة C# – التعرف على النص من JPG بسرعة
tags:
- OCR
- C#
- Aspose
title: دورة C# OCR – التعرف على النص من JPG في دقائق
url: /ar/net/text-recognition/c-ocr-tutorial-recognize-text-from-jpg-in-minutes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# درس c# OCR – التعرف على النص من JPG في دقائق

هل احتجت يومًا إلى **دروس c# OCR** التي تأخذك فعليًا من الصفر إلى قراءة النص في ملف JPEG؟ لست وحدك. سواء كنت تبني ماسح جوازات السفر، أو مسجل إيصالات، أو مجرد فضولي حول استخراج الكلمات من الصور، هذا الدليل يوضح لك بالضبط كيفية **التعرف على النص من jpg** باستخدام Aspose.OCR.  

في الدقائق القليلة القادمة سنغطي كل ما تحتاجه: تثبيت المكتبة، تحميل صورة للـ OCR، إجراء التعرف، ومعالجة النتائج. لا إشارات غامضة—فقط مثال كامل قابل للتنفيذ يمكنك نسخه‑ولصقه وتشغيله اليوم.

## ما ستتعلمه

- كيفية تثبيت **Aspose.OCR** عبر NuGet.  
- كيفية إنشاء محرك OCR وطلب لغة غير مضمنة (مثل الروسية) مما يؤدي إلى تحميل عند الطلب.  
- كيفية **تحميل صورة للـ OCR**، تشغيل المحرك، وإخراج النص المُستخرج.  
- نصائح لتجنب المشكلات الشائعة مثل فقدان بيانات اللغة، الملفات الكبيرة، وإدارة الذاكرة.  

بنهاية الدرس ستحصل على تطبيق console يعمل ويمكنه **إجراء OCR على الصور** من أي صيغة مدعومة.

---

## درس c# OCR – الخطوة 1: تثبيت Aspose.OCR

قبل تشغيل أي كود تحتاج إلى حزمة Aspose.OCR. افتح الطرفية (أو Package Manager Console) ونفّذ:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل واجهة Visual Studio، انقر بزر الماوس الأيمن على مشروعك → **Manage NuGet Packages** → ابحث عن **Aspose.OCR** → **Install**.  
الحزمة تجلب محرك OCR الأساسي بالإضافة إلى مجموعة صغيرة من ملفات اللغات الافتراضية.

> **نصيحة احترافية:** احرص على أن يكون مشروعك مستهدفًا .NET 6 أو أحدث؛ Aspose.OCR يعمل بلا مشاكل مع .NET Core و .NET Framework.

## الخطوة 2: تهيئة محرك OCR

إنشاء المحرك سهل. الفئة `OcrEngine` هي نقطة الدخول لجميع عمليات OCR.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize the OCR engine (uses the basic core)
var ocrEngine = new OcrEngine();
```

لماذا نقوم بإنشاء المحرك أولًا؟ المحرك يحتفظ بالإعدادات مثل اللغة، وضع التعرف، والذاكرة الداخلية. تهيئته مبكرًا يضمن إمكانية تعديل الإعدادات قبل معالجة أي صورة.

## الخطوة 3: اختيار لغة وتفعيل التحميل عند الطلب

Aspose يوزع عددًا قليلًا من اللغات مدمجة (English, Chinese, إلخ). إذا كنت بحاجة إلى لغة مثل الروسية، ما عليك سوى ضبط خاصية `Language`؛ المكتبة ستحمّل البيانات اللازمة في أول تشغيل لك.

```csharp
// Step 3: Request Russian language – this triggers an on‑demand download
ocrEngine.Language = Language.Russian;
```

> **لماذا هذا مهم:** بتحميل اللغات التي تستخدمها فقط، تحافظ على خفة التطبيق. التحميل يحدث مرة واحدة لكل جهاز ويُخزن في الذاكرة المؤقتة للتشغيلات المستقبلية.

إذا كنت تفضّل العمل دون اتصال، حمّل حزمة اللغة يدويًا من مستودع Aspose ووجه المحرك إلى المجلد المحلي عبر `ocrEngine.SetLanguageFolder("path/to/languages")`.

## الخطوة 4: تحميل صورة للـ OCR

الآن نجلب ملف JPEG إلى الذاكرة. Aspose.OCR يمكنه قراءة صيغ متعددة (`jpg`, `png`, `tif`, `bmp`). إليك كيفية تحميل ملف اسمه `russian_passport.jpg` موجود في مجلد اسمه `Images` نسبةً إلى جذر المشروع.

```csharp
// Step 4: Load the image you want to recognize
using (var image = Image.Load(@"Images/russian_passport.jpg"))
{
    // The using‑statement ensures the image is disposed properly.
    // If you need to work with a Bitmap first, you can also pass a System.Drawing.Image.
```

> **نصيحة الصورة:** للحصول على أفضل دقة، زوّد المحرك بصورة عالية الدقة (300 dpi أو أعلى). إذا كان المصدر منخفض الدقة، فكر في استخدام `ocrEngine.PreprocessImage(image)` قبل التعرف.

## الخطوة 5: التعرف على النص من JPG ومعالجة النتائج

بعد تحميل الصورة، استدعِ `Recognize`. تُعيد الطريقة كائن `OcrResult` يحتوي على النص المستخرج ودرجات الثقة.

```csharp
    // Step 5: Run OCR on the loaded image
    var result = ocrEngine.Recognize(image);

    // Output the recognized text to the console
    Console.WriteLine("=== Recognized Text ===");
    Console.WriteLine(result.Text);
}
```

ستظهر وحدة التحكم شيئًا مثل:

```
=== Recognized Text ===
ПАСПОРТ РФ
ФИО: ИВАНОВ ИВАН ИВАНОВИЧ
...
```

إذا لم تتوفر بيانات اللغة بعد، سيُطلق المحرك استثناءً توضيحيًا—التقطه واطلب من المستخدم التحقق من اتصال الإنترنت.

```csharp
try
{
    var result = ocrEngine.Recognize(image);
    Console.WriteLine(result.Text);
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
}
```

## الخطوة 6: المشكلات الشائعة وأفضل الممارسات (إجراء OCR على الصورة بفعالية)

| المشكلة | لماذا يحدث | كيفية الإصلاح |
|-------|----------------|------------|
| **حزمة اللغة مفقودة** | التشغيل الأول بلغة جديدة ي trigger التحميل؛ البيئات غير المتصلة لا يمكنها الوصول إلى خوادم Aspose. | قم بتحميل الحزم مسبقًا أو قم بتكوين مستودع محلي. |
| **صورة غير واضحة أو منخفضة الدقة** | دقة OCR تنخفض بشكل كبير تحت 200 dpi. | قم بزيادة حجم الصورة أو اطلب من المستخدم توفير مسح بدقة أعلى. |
| **صور كبيرة (>10 MB)** | ضغط الذاكرة قد يسبب `OutOfMemoryException`. | قم بتغيير حجم الصورة أو تقسيمها قبل التعرف (`image = image.Resize(1024, 0)`). |
| **مسار ملف غير صحيح** | المسارات النسبية تختلف عند التشغيل من VS مقابل `dotnet run`. | استخدم `Path.Combine(AppContext.BaseDirectory, "Images", "file.jpg")`. |
| **حروف غير متوقعة** | بعض الخطوط غير مدعومة من نموذج اللغة. | فعّل `ocrEngine.UseDictionary = true` لتحسين المعالجة اللاحقة. |

> **نصيحة احترافية:** احرص دائمًا على تغليف استدعاءات OCR داخل كتلة `try/catch` وسجّل `result.Confidence` إذا احتجت لتصفية النتائج ذات الثقة المنخفضة.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي برنامج console مستقل يدمج كل خطوة تمت مناقشتها. احفظه باسم `Program.cs` في مشروع console جديد وشغّله بـ `dotnet run`.

```csharp
// Program.cs
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Install Aspose.OCR via NuGet before running this code.
            // 2️⃣ Ensure the image exists at the specified path.

            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Request Russian language – triggers on‑demand download if needed
            ocrEngine.Language = Language.Russian;

            // Build absolute path for reliability
            string imagePath = Path.Combine(AppContext.BaseDirectory, "Images", "russian_passport.jpg");

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }

            // Load the image inside a using block for proper disposal
            using (var image = Image.Load(imagePath))
            {
                try
                {
                    // Perform OCR
                    var result = ocrEngine.Recognize(image);

                    // Display the extracted text
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"OCR operation failed: {ex.Message}");
                }
            }

            // Optional: Release engine resources (good practice for long‑running apps)
            ocrEngine.Dispose();
        }
    }
}
```

**الناتج المتوقع** (مقتطع للختصار):

```
=== Recognized Text ===
ПАСПОРТ РФ
ФИО: ИВАНОВ ИВАН ИВАНОВИЧ
Дата рождения: 01.01.1990
...
```

## الخلاصة

لقد أتممت للتو **دروس c# OCR** الذي يوضح كيفية **التعرف على النص من jpg**، **إجراء OCR على الصورة**، وتحميل صورة للـ OCR بشكل صحيح باستخدام Aspose.OCR. الحل كامل ذاتيًا، يعمل دون اتصال بعد أول تحميل للغة، ويتضمن نصائح عملية للسيناريوهات الواقعية.  

من هنا قد تستكشف:

- تبديل إلى لغات أخرى (العربية، الهندية) بتغيير `ocrEngine.Language`.  
- إدخال صفحات PDF مباشرة (`PdfDocument.Load`) واستخراج النص صفحةً بصفحة.  
- دمج خطوة OCR في واجهة ويب API لمعالجة الصور في الوقت الفعلي.  

لا تتردد في تجربة جودة صور مختلفة، إضافة معالجة مسبقة (إزالة الضوضاء، التحويل إلى ثنائي)، أو دمج الناتج مع قاعدة بيانات لأرشفة قابلة للبحث. برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالكريستال!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}