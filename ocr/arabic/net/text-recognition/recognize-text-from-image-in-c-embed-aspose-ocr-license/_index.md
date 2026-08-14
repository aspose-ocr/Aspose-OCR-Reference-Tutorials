---
category: general
date: 2026-02-28
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلّم كيفية تضمين
  الترخيص واستخراج النص باستخدام OCR في بضع خطوات سهلة.
draft: false
keywords:
- recognize text from image
- extract text using OCR
- how to embed license
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR. يوضح هذا الدرس كيفية
  تضمين الترخيص واستخراج النص باستخدام OCR في C#.
og_title: التعرف على النص من الصورة في C# – دليل الترخيص الكامل
tags:
- Aspose OCR
- C#
- Licensing
title: التعرف على النص من الصورة في C# – تضمين ترخيص Aspose OCR
url: /ar/net/text-recognition/recognize-text-from-image-in-c-embed-aspose-ocr-license/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# – تضمين ترخيص Aspose OCR

هل احتجت يومًا إلى **التعرف على النص من صورة** في تطبيق C#؟ يصبح التعرف على النص من صورة باستخدام Aspose OCR سهلًا بمجرد تضمين الترخيص بشكل صحيح. في هذا الدليل سنوضح لك أيضًا كيفية **استخراج النص باستخدام OCR** وسنجيب على السؤال المتبقي **كيفية تضمين الترخيص** دون الحاجة إلى التعامل مع نظام الملفات.

إذا سبق لك وأن حدقت في فئة `LicenseDemo` الفارغة وتساءلت لماذا يستمر محرك OCR في إلقاء أخطاء “Trial version”، فأنت لست وحدك. سنمر على كل سطر، نشرح لماذا كل خطوة مهمة، وننتهي بعينة قابلة للتنفيذ تطبع السلسلة المستخرجة إلى وحدة التحكم. لا مستندات خارجية، لا تخمين—فقط شفرة جاهزة للنسخ واللصق.

---

## ما ستحتاجه قبل أن نبدأ

- **.NET 6** (أو أي نسخة أحدث من .NET) – لم يتغير سطح API منذ 2023، لذا أنت بأمان.  
- **Aspose.OCR for .NET** حزمة NuGet – قم بتثبيتها عبر `dotnet add package Aspose.OCR`.  
- ملف ترخيص **Aspose OCR** الخاص بك (`*.lic`). سنقوم بتضمينه كموارد حتى لا تحتاج أبدًا إلى شحن ملف منفصل.  
- صورة نموذجية (`sample.png`) موضوعة في جذر المشروع أو أي مجلد تفضله.

هذا كل شيء. لا إعدادات إضافية، لا محركات OCR ثقيلة، فقط بضع أسطر من C#.

---

## الخطوة 1 – تضمين ترخيص Aspose OCR (**كيفية تضمين الترخيص**)

تضمين الترخيص داخل التجميع يضمن أن الترخيص ينتقل مع ملف الـ DLL الخاص بك، مما يلغي الأخطاء المتعلقة بالمسار على الأجهزة المختلفة.

```csharp
using System;
using System.IO;
using System.Reflection;
using Aspose.OCR;

namespace OcrDemo
{
    public static class LicenseHelper
    {
        /// <summary>
        /// Loads the embedded Aspose OCR license.
        /// The license file must be added to the project as an Embedded Resource
        /// with the exact name "OcrDemo.Resources.AspectsOCR.lic".
        /// </summary>
        public static void ApplyLicense()
        {
            // Get the assembly that contains the embedded resource
            Assembly assembly = Assembly.GetExecutingAssembly();

            // Open the stream to the embedded .lic file
            using Stream? licenseStream = assembly.GetManifestResourceStream(
                "OcrDemo.Resources.AspectsOCR.lic");

            if (licenseStream == null)
            {
                throw new FileNotFoundException(
                    "Embedded license not found. Verify the resource name and Build Action.");
            }

            // Apply the license – after this the OCR engine works in full mode
            License license = new License();
            license.SetLicense(licenseStream);
        }
    }
}
```

**لماذا التضمين؟**  
عند نشر تطبيق سطح مكتب أو ويب، قد يختلف دليل العمل بشكل كبير (فكر في `bin\Debug` مقابل مجلد منشور). كتابة مسار ثابت (`C:\Licenses\my.lic`) يخلق اعتمادًا هشًا. المورد المضمن يعيش داخل الـ DLL، لذا يجد وقت التشغيل دائمًا الملف.

**نصيحة احترافية:** في Visual Studio، انقر بزر الماوس الأيمن على ملف `.lic` → *Properties* → عيّن **Build Action** إلى **Embedded Resource**. عادةً ما يتبع اسم المورد النمط `Namespace.Folder.FileName`. إذا غيرت اسم المجلد، عدّل السلسلة وفقًا لذلك.

---

## الخطوة 2 – تهيئة محرك OCR لـ **التعرف على النص من صورة**

الآن بعد أن أصبح الترخيص فعالًا، إنشاء نسخة من `OcrEngine` يمنحك كامل إمكانيات OCR.

```csharp
using Aspose.OCR;

namespace OcrDemo
{
    public class OcrProcessor
    {
        private readonly OcrEngine _engine;

        public OcrProcessor()
        {
            // The license must be applied before any OCR operation
            LicenseHelper.ApplyLicense();

            // Create a fully‑licensed engine
            _engine = new OcrEngine();
        }

        // Expose the engine for later calls
        public OcrEngine Engine => _engine;
    }
}
```

لاحظ أننا نستدعي `LicenseHelper.ApplyLicense()` **داخل المُنشئ**. هذا يضمن أن أي مستهلك لـ `OcrProcessor` لا ينسى ترخيص المحرك—طريقة سهلة لتجنب استثناء “Trial mode” المزعج.

---

## الخطوة 3 – تحميل صورة و **استخراج النص باستخدام OCR**

مع محرك مرخص جاهز، تمرير صورة إليه أمر بسيط. أدناه نقوم بتحميل PNG، تشغيل التعرف، وطباعة النتيجة.

```csharp
using System;
using System.Drawing;          // Requires System.Drawing.Common on non‑Windows
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare the processor (license applied automatically)
            OcrProcessor processor = new OcrProcessor();

            // 2️⃣ Load the image – adjust the path as needed
            string imagePath = Path.Combine(AppContext.BaseDirectory, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }

            using Image image = Image.FromFile(imagePath);
            processor.Engine.SetImage(image);

            // 3️⃣ Perform recognition
            string extractedText = processor.Engine.Recognize();

            // 4️⃣ Output the result
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(extractedText);
        }
    }
}
```

**الناتج المتوقع** (بافتراض أن `sample.png` يحتوي على كلمة “Hello World”):

```
=== OCR Result ===
Hello World
```

إذا كانت الصورة مشوشة، قد تحصل على فواصل أسطر إضافية أو أحرف غير صحيحة. هنا يأتي الدور للخطوة التالية—ضبط المحرك.

---

## الخطوة 4 – ضبط المحرك بدقة (اختياري) – الحصول على نتائج أفضل عند **استخراج النص باستخدام OCR**

يقدم Aspose OCR مجموعة من الخصائص التي يمكنك تعديلها:

| الخاصية | ما تقوم به | الاستخدام الشائع |
|----------|--------------|-------------|
| `Engine.Language` | يحدد نموذج اللغة (مثال: `Language.English`). | يحسن الدقة للخطوط غير اللاتينية. |
| `Engine.ImagePreprocess` | يفعّل التحويل إلى ثنائي، تصحيح الميل، إلخ. | تنظيف المسحات ذات التباين المنخفض. |
| `Engine.IsAutoRotate` | يكتشف تلقائيًا اتجاه الصورة. | يتعامل مع الصور المدوَّرة. |

مثال على تمكين بعض المساعدات:

```csharp
processor.Engine.Language = Language.English;
processor.Engine.ImagePreprocess = ImagePreprocess.Binarization | ImagePreprocess.Deskew;
processor.Engine.IsAutoRotate = true;
```

**لماذا العناء؟** يعمل المحرك الافتراضي جيدًا للقطات الشاشة الواضحة، لكن المستندات الواقعية غالبًا ما تعاني من الظلال أو الدوران أو اللغات المختلطة. تعديل هذه العلامات يمكن أن يرفع درجة الثقة من ~70 % إلى >95 % في كثير من الحالات.

---

## الخطوة 5 – المشكلات الشائعة وكيفية تجنبها

1. **اسم المورد مفقود** – إذا حصلت على استثناء `FileNotFoundException`، تحقق مرة أخرى من سلسلة المورد المؤهلة بالكامل. استخدم `assembly.GetManifestResourceNames()` لسرد جميع الأسماء المضمنة أثناء التشغيل.  
2. **تنسيق صورة غير صحيح** – `Image.FromFile` يدعم BMP، PNG، JPEG، GIF، TIFF. بالنسبة إلى PDF أو TIFF متعدد الصفحات ستحتاج إلى تجاوزات `ImageStream`.  
3. **التشغيل على Linux/macOS** – `System.Drawing.Common` يعتمد على مكتبات أصلية (`libgdiplus`). قم بتثبيتها عبر `apt-get install libgdiplus` أو انتقل إلى `Aspose.OCR.ImageStream` الذي لا يعتمد على النظام.  
4. **الترخيص لم يُطبق مبكرًا بما فيه الكفاية** – يجب تعيين الترخيص **قبل** أي إنشاء لـ `OcrEngine`. وضع `LicenseHelper.ApplyLicense()` في مُنشئ ثابت أو في `Main` قبل أي `new OcrEngine()` هو الأكثر أمانًا.

---

## الخطوة 6 – التحقق من عمل الحل بالكامل

قم بتجميع البرنامج وتشغيله:

```bash
dotnet build
dotnet run --project OcrDemo
```

يجب أن ترى ناتج وحدة التحكم مع النص المستخرج. إذا استمر ظهور “Trial version”، راجع **الخطوة 1**—أكثر الأسباب شيوعًا هو مورد مضمّن غير صحيح.

---

## الخلاصة

أنت الآن تعرف كيف **تتعرف على النص من صورة** في C# باستخدام Aspose OCR، وكيف **تضمّن الترخيص** بحيث يعمل المحرك في الوضع الكامل، وأفضل الممارسات لـ **استخراج النص باستخدام OCR** بشكل موثوق. الشفرة الكاملة الجاهزة للنسخ واللصق أعلاه تغطي كل شيء من الترخيص إلى معالجة الصورة مسبقًا، لذا يمكنك إدماجها في أي مشروع .NET والبدء في استخراج النص من الصور فورًا.

ما الخطوة التالية؟ جرّب تمرير مجموعة من الملفات إلى المحرك، جرب حزم اللغات، أو وجه ناتج OCR إلى فهرس بحث. النمط نفسه—تضمين الترخيص → تهيئة المحرك → تحميل الصورة → التعرف—يعمل مع ملفات PDF، TIFF متعددة الصفحات، وحتى تدفقات الكاميرا الحية.

هل لديك أسئلة حول حالات خاصة أو تحتاج مساعدة في تصحيح صورة صعبة؟ اترك تعليقًا، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}