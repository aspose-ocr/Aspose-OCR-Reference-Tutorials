---
category: general
date: 2026-02-25
description: التعرف على النص من الصورة بسرعة باستخدام OCR المدعوم بوحدة معالجة الرسومات.
  تعلم كيفية ضبط وضع GPU، تحميل الصورة للـ OCR، واستخراج النص من ملف TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: ar
og_description: التعرف على النص من الصورة فورًا باستخدام OCR مدعوم بتقنية GPU. دليل
  خطوة بخطوة بلغة C# يغطي ضبط وضع GPU، تحميل الصورة للـ OCR، واستخراج النص من ملف
  TIFF.
og_title: التعرف على النص من الصورة باستخدام OCR المعجل بوحدة معالجة الرسومات – دليل
  C#
tags:
- Aspose OCR
- C#
- GPU computing
title: التعرف على النص من الصورة باستخدام OCR المعجل بوحدة معالجة الرسومات في C#
url: /ar/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام OCR المدعوم بالـ GPU في C#

هل احتجت يومًا إلى **التعرف على النص من الصورة** لكن وحدة المعالجة المركزية كانت تعاني من صورة عالية الدقة؟ لست وحدك. في العديد من المشاريع الواقعية—مثل رقمنة الفواتير أو أرشفة الصحف القديمة—يمكن لملف TIFF واحد أن يوقف خط الأنابيب لديك لعدة دقائق. الخبر السار؟ Aspose.OCR يتيح لك تبديل الوضع وتسليم العبء الثقيل إلى الـ GPU، مما يحول العملية البطيئة إلى عملية شبه فورية.

في هذا الدرس سنستعرض العملية بالكامل: كيفية **تعيين وضع GPU**، كيفية **تحميل الصورة للـ OCR**، وكيفية **استخراج النص من ملفات TIFF**. في النهاية ستحصل على مثال جاهز للإنتاج يمكنك إدراجه في أي مشروع .NET 6+.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6 SDK (أو أحدث) مثبت.
- Visual Studio 2022 أو أي محرر تفضله.
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) مضافة إلى مشروعك.
- بطاقة رسومية تدعم DirectX 11 أو أحدث (معظم البطاقات الحديثة تفي بهذا الشرط).  
  *إذا لم يكن لديك GPU، لا يزال بإمكانك تشغيل الكود باستخدام `GpuMode.Auto`—ستعود المكتبة تلقائيًا إلى المعالج المركزي.*

> **نصيحة احترافية:** تأكد من أن برنامج تشغيل الـ GPU محدث؛ قد تتسبب التعريفات القديمة في حدوث أخطاء تهيئة غير واضحة.

## الخطوة 1 – إنشاء محرك OCR وتعيين وضع GPU

أول شيء تحتاجه هو نسخة من `OcrEngine`. هذا الكائن يحمل جميع الإعدادات، بما في ذلك ما إذا كان يجب على المحرك استخدام الـ GPU.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**لماذا هذا مهم:** تفعيل وضع GPU ينقل عمليات ما قبل المعالجة المكثفة (مثل التحويل إلى ثنائي، إزالة الضوضاء، إلخ) إلى بطاقة الرسوميات. على بطاقة RTX 3060 متوسطة المستوى، يمكنك ملاحظة **زيادة سرعة 3‑5×** مقارنة بالمعالجة على المعالج المركزي فقط.

## الخطوة 2 – تحميل الصورة للـ OCR (مثال TIFF)

تقبل Aspose.OCR العديد من الصيغ، لكن TIFF شائع للوثائق الممسوحة لأنه يحافظ على الجودة بدون فقدان. استخدم `ImageStream.FromFile` لقراءة الملف إلى الذاكرة.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**حالة خاصة:** بعض ملفات TIFF تحتوي على صفحات متعددة. `ImageStream.FromFile` سيقرأ الصفحة الأولى فقط. إذا كنت بحاجة لمعالجة كل الصفحات، قم بالتكرار عبر `ImageInfo.Pages` ومرّر كل صفحة إلى المحرك على حدة.

## الخطوة 3 – تنفيذ التعرف

الآن بعد أن تم تكوين المحرك وتحميل الصورة، استدعِ `Recognize()`. تُعيد هذه الطريقة كائن `OcrResult` يحتوي على النص العادي الناتج وبيانات وصفية إضافية.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**ماذا لو ظهر النص مشوشًا؟**  
- تأكد من أن الصورة في وضعية قراءة صحيحة (قم بالدوران إذا لزم الأمر).  
- اضبط خيارات ما قبل المعالجة مثل `ocrEngine.Config.DeskewEnabled = true;`.  
- للوثائق متعددة اللغات، عيّن `ocrEngine.Config.Language = Language.English;` أو أي قيمة مناسبة من الـ enum.

## الخطوة 4 – التحقق من النتيجة ومعالجة الأخطاء

تنفيذ قوي يتحقق من عدم وجود نتائج فارغة ويصطاد الاستثناءات المحتملة (مثل عدم وجود تعريفات GPU).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**لماذا نغلف الكود؟** قد تُسبب تهيئة الـ GPU استثناء `DllNotFoundException` إذا لم تتوفر المكتبات الأصلية المطلوبة. يوفّر كتلة الـ catch مسارًا للانخفاض السلس.

## مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك برنامج كامل يمكنك تجميعه وتشغيله الآن. استبدل مسار الملف بملف TIFF حقيقي على جهازك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**الناتج المتوقع**

إذا كان ملف TIFF يحتوي على نص إنجليزي مقروء، سترى شيئًا مشابهًا لـ:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

إذا كانت الصورة فارغة أو غير قابلة للقراءة، سيُظهر الطرفية رسالة تنصحك بفحص ملف المصدر.

## أسئلة شائعة & تنويعات

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني معالجة JPEG أو PNG بدلاً من TIFF؟** | بالتأكيد. `ImageStream.FromFile` يعمل مع أي صيغة يدعمها Aspose.OCR (PNG، JPEG، BMP، إلخ). |
| **ماذا لو كان لدي عدة صفحات في ملف TIFF واحد؟** | قم بالتكرار عبر `ImageInfo.Pages` وعيّن كل صفحة إلى `ocrEngine.Image` قبل استدعاء `Recognize()`. |
| **هل أحتاج إلى ترخيص لـ Aspose.OCR؟** | التقييم المجاني يعمل حتى 100 صفحة. للإنتاج، اشترِ ترخيصًا لإزالة علامة التقييم. |
| **كيف أغيّر نموذج اللغة؟** | عيّن `ocrEngine.Config.Language = Language.Spanish;` (أو أي enum مدعوم). |
| **هل هناك طريقة للحصول على درجات الثقة؟** | فعّل `ocrEngine.Config.EnableConfidence = true;` وتفحص `result.Confidence` لكل سطر. |

## الخلاصة

أنت الآن تعرف كيف **تتعرف على النص من الصورة** باستخدام **خط أنابيب OCR مدعوم بالـ GPU** في C#. من خلال **تعيين وضع GPU**، **تحميل صورة للـ OCR**، و**استخراج النص من ملفات TIFF**، قمت ببناء حل سريع وقابل للتوسع جاهز للعب workloads الواقعية.

ما الخطوة التالية؟ جرّب ربط هذا الكود مع مولّد PDF لإنشاء ملفات PDF قابلة للبحث، أو مرّر السلاسل المستخرجة إلى خط أنابيب معالجة لغة طبيعية. يمكنك أيضًا تجربة `GpuMode.Auto` لجعل تطبيقك يتكيف مع البيئات التي لا تتوفر فيها بطاقة رسومية.

برمجة سعيدة، ولتكن عمليات OCR لديك سريعة كالبرق!

![مثال على التعرف على النص من الصورة](https://example.com/ocr-demo.png "التعرف على النص من الصورة باستخدام OCR المدعوم بالـ GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}