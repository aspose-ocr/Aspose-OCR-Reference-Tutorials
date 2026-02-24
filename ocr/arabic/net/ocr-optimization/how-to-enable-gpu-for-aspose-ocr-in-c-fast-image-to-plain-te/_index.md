---
category: general
date: 2026-02-24
description: كيفية تمكين وحدة معالجة الرسومات (GPU) في مثال Aspose OCR بلغة C# – تحويل
  الصورة إلى نص عادي بسرعة. يتضمن تعيين معرف جهاز GPU وقراءة نص الصورة دليل C#.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: ar
og_description: كيفية تمكين GPU في مثال Aspose OCR بلغة C#. تعلّم تعيين معرف جهاز
  GPU وقراءة نص الصورة باستخدام C# بكفاءة.
og_title: كيفية تمكين وحدة معالجة الرسومات (GPU) لتقنية Aspose OCR في C# – تحويل سريع
  من الصورة إلى نص عادي
tags:
- Aspose OCR
- C#
- GPU acceleration
title: كيفية تمكين وحدة معالجة الرسومات (GPU) لـ Aspose OCR في C# – تحويل الصورة إلى
  نص عادي بسرعة
url: /ar/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين GPU لـ Aspose OCR في C# – تحويل الصورة إلى نص عادي بسرعة

هل تساءلت يومًا **كيف يمكنك تمكين GPU** عند استخدام Aspose OCR لتحويل صورة إلى نص قابل للتحرير؟ لست وحدك—العديد من المطورين يواجهون جدار الأداء عند معالجة فواتير كبيرة أو عقود ممسوحة ضوئيًا. الخبر السار؟ تحويل الصورة إلى نص عادي يمكن أن يكون سريعًا كالبرق بمجرد الاستفادة من بطاقة الرسومات الخاصة بك.

في هذا الدليل سنستعرض مثالًا كاملًا **Aspose OCR** يوضح لك بالضبط كيفية تمكين GPU، تعيين معرف جهاز GPU، و**قراءة نص الصورة في C#**. في النهاية ستحصل على برنامج قابل للتنفيذ يستخرج النص من أي صورة مدعومة في جزء من الوقت الذي يحتاجه النهج القائم على CPU فقط.

## ما ستحتاجه

- .NET 6.0 أو أحدث (تعمل الواجهة البرمجية مع .NET Core و .NET Framework)
- بطاقة GPU متوافقة مع CUDA مع أحدث برنامج تشغيل مثبت
- ترخيص Aspose.OCR لـ .NET (أو نسخة تجريبية مجانية، تعمل للتطوير)
- Visual Studio 2022 (أو أي محرر C# تفضله)

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.OCR`—فقط المكتبة نفسها.

---

## الخطوة 1 – تثبيت حزمة Aspose OCR عبر NuGet

أولاً، أضف مكتبة Aspose OCR الرسمية إلى مشروعك. افتح نافذة Package Manager Console وشغّل:

```powershell
Install-Package Aspose.OCR
```

هذا سيجلب `Aspose.OCR.dll` وجميع تبعياته. إذا كنت تفضّل الواجهة الرسومية، انقر بزر الماوس الأيمن على مشروعك → **Manage NuGet Packages** → ابحث عن *Aspose.OCR* وانقر **Install**.  

*نصيحة احترافية:* بعد التثبيت، تأكد من ظهور مجلد `Aspose.OCR` ضمن **Dependencies** في مستكشف الحلول.

## الخطوة 2 – إنشاء هيكل تطبيق Console بسيط

سنُنشئ تطبيق console صغير يوضح سير العمل بالكامل. أنشئ مشروعًا جديدًا:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

استبدل ملف `Program.cs` المُولد بالكود الكامل الموضح لاحقًا. هذا الهيكل يمنحنا نقطة دخول نظيفة ويسمح لنا بالتركيز على منطق OCR.

## الخطوة 3 – كيفية تمكين GPU وتعيين معرف جهاز GPU

الآن نصل إلى نجمة العرض: **كيفية تمكين GPU** في Aspose OCR. تُوفر المكتبة كائن `OcrSettings` حيث يمكنك تفعيل `UseGpu` واختيار جهاز CUDA محدد عبر `GpuDeviceId`. إليك المقتطف الدقيق الذي ستدمجه في برنامجك:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### لماذا تمكين GPU؟

تمكين GPU يخفّف العبء الثقيل—معالجة البكسل المسبق، تجزئة الأحرف، واستنتاج الشبكة العصبية—إلى بطاقة الرسومات. على بطاقة GTX 1650 متوسطة، يمكنك ملاحظة **زيادة سرعة 2‑3×** مقارنةً بوضع CPU‑only، خاصةً مع المستندات عالية الدقة.

### اختيار معرف الجهاز

إذا كان جهازك يحتوي على عدة بطاقات GPU، يتيح لك `GpuDeviceId` استهداف بطاقة معينة. `0` يختار الجهاز الأول؛ `1` يختار الثاني، وهكذا. يمكنك اكتشاف المعرفات المتاحة باستخدام أداة NVIDIA `nvidia-smi` أو عبر استعلام فئة `GpuInfo` في Aspose (غير موضّحة هنا لتقليل الإطالة).

## الخطوة 4 – مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في `Program.cs`، استبدل مسار الصورة بملف فعلي على قرصك، ثم اضغط **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### النتيجة المتوقعة

إذا كانت الصورة المقدمة تحتوي على السطر *“Invoice #12345 – Total $1,250.00”*، سيطبع الـ console:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

النتيجة نص عادي، جاهز لمعالجة إضافية (مثل إدخاله في قاعدة بيانات أو محلل لغة طبيعية).

## الخطوة 5 – التحقق من استخدام GPU (اختياري)

للتأكد من أن GPU يُستَخدم فعليًا، افتح أداة مراقبة GPU (مثل **NVIDIA‑Smi** أو **GPU‑Z**) أثناء تشغيل البرنامج. يجب أن ترى ارتفاعًا في استهلاك الحوسبة للجهاز المحدد. إذا رأيت نشاطًا فقط للـ CPU، تحقق مرة أخرى من:

- أن برنامج تشغيل GPU محدث.
- أن علم `UseGpu` مضبوط على `true`.
- أن صيغة الصورة مدعومة (PNG, JPEG, TIFF, إلخ).

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل السريع |
|-------|----------------|-----------|
| **GPU غير مكتشف** | برنامج تشغيل قديم أو عدم وجود بيئة تشغيل CUDA | تثبيت أحدث برنامج تشغيل NVIDIA وحزمة أدوات CUDA |
| **`Aspose.OCR` يُظهر “GPU غير مدعوم”** | تشغيل على GPU غير CUDA (مثل AMD قديم) | ضبط `UseGpu = false` أو استبدال البطاقة بواحدة متوافقة |
| **مسار الصورة غير صحيح** | المسار النسبي يشير إلى المجلد الخطأ | استخدم مسارًا مطلقًا أو مرّر المسار كمعامل سطر أوامر |
| **الترخيص غير مفعّل** | وضع التقييم قد يحد من استخدام GPU | سجّل الترخيص بـ `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

## توسيع المثال: معالجة دفعات باستخدام GPU

إذا كنت بحاجة لمعالجة عشرات الفواتير، غلف نداء التعرف داخل حلقة. لأن GPU يبقى “دافئًا”، تستفيد الصور اللاحقة من **التخزين المؤقت للإحماء**، مما يقلل المزيد من الميلي ثانية لكل تشغيل.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

تذكر أن تحتفظ بنفس نسخة `OcrEngine`—إنشاء محرك جديد لكل ملف سيعيد تهيئة سياق GPU ويقضي على الأداء.

## الخلاصة

أصبح لديك الآن مثال **Aspose OCR** شامل يُظهر **كيفية تمكين GPU**، كيفية **تعيين معرف جهاز GPU**، وكيفية **قراءة نص الصورة في C#**. عبر تبديل `UseGpu` وتوجيهه إلى الجهاز الصحيح، تحوّل مهمة OCR البطيئة المعتمدة على CPU إلى خط أنابيب عالي الإنتاجية يمكنه معالجة فواتير، إيصالات أو أي مستند ممسوح ضوئيًا كبير.

لا تتردد في التجربة: جرّب صيغ صور مختلفة، عدّل `GpuDeviceId` على أنظمة متعددة الـ GPU، أو اجمع هذا مع مكتبات Aspose أخرى لتوليد PDF. السماء هي الحد عندما يكون GPU في اللعب.

<img src="gpu-ocr.png" alt="كيفية تمكين GPU مع Aspose OCR في C# – تحويل الصورة إلى نص عادي بسرعة">

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو اطلع على منتديات Aspose الرسمية للمزيد من التفاصيل.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}