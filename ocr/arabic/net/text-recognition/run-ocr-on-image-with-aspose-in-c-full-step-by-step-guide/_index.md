---
category: general
date: 2026-04-03
description: قم بتشغيل OCR على الصورة باستخدام Aspose OCR في C#. تعلم كيفية استخراج
  النص من الصورة، والتعرف على النص الهندي، وتحميل الصورة للـ OCR، وتعيين لغة الـ OCR
  بسهولة.
draft: false
keywords:
- run OCR on image
- extract text from image
- recognize Hindi text
- load image for OCR
- set OCR language
language: ar
og_description: تشغيل OCR على صورة في C# باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  استخراج النص من الصورة، التعرف على النص الهندي، تحميل الصورة للـ OCR، وتعيين لغة
  الـ OCR.
og_title: تشغيل OCR على الصورة باستخدام Aspose – دليل C# الكامل
tags:
- Aspose
- C#
- OCR
title: تشغيل OCR على الصورة باستخدام Aspose في C# – دليل كامل خطوة بخطوة
url: /ar/net/text-recognition/run-ocr-on-image-with-aspose-in-c-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على صورة باستخدام Aspose في C# – دليل كامل

هل احتجت يومًا إلى **تشغيل OCR على صورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج فورية؟ لست وحدك — المطورون يتعاملون باستمرار مع معالجة الصور مسبقًا، حزم اللغات، وأحيانًا موارد مفقودة.  

في هذا الدليل سنستعرض مثالًا جاهزًا **لاستخراج النص من صورة**، يوضح لك كيفية **التعرف على النص الهندي**، ويشرح الخطوة الصغيرة ولكن الحيوية **لتحميل الصورة لـ OCR** بينما تقوم **بتعيين لغة OCR** بشكل صحيح.

في النهاية ستحصل على تطبيق وحدة تحكم C# واحد يستخرج كل حرف قابل للطباعة من صورة، دون الحاجة لتنزيلات يدوية للغات. المتطلبات الوحيدة هي بيئة تطوير متوافقة مع .NET (Visual Studio، Rider، أو VS Code) ورخصة Aspose OCR (أو نسخة تجريبية مجانية).  

---

## ما ستحتاجه قبل البدء

- **Aspose.OCR for .NET** (حزمة NuGet `Aspose.OCR`).  
- **.NET 6.0** أو أحدث – الـ API يعمل مع .NET Core و .NET Framework على حد سواء.  
- صورة نموذجية تحتوي على نص هندي (مثال: `hindi_sign.jpg`).  
- اختياري: ملف ترخيص Aspose صالح (`Aspose.Total.lic`) لتجنب علامات مائية للتقييم.  

إذا كان أي من هذه غير مألوف لك، لا تقلق — سيتم توضيح كل نقطة من النقاط أثناء التقدم.

---

## الخطوة 1: تثبيت حزمة Aspose OCR عبر NuGet

أولاً، افتح مجلد المشروع في الطرفية ونفّذ:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → البحث عن “Aspose.OCR” والنقر على **Install**.  

هذا سيجلب ملف `Aspose.OCR.dll` وجميع تبعياته، مما يمنحك الوصول إلى الفئة `OcrEngine` التي سنحتاجها **لتشغيل OCR على صورة**.

---

## الخطوة 2: إنشاء هيكل تطبيق وحدة تحكم جديد

فيما يلي هيكل البرنامج الكامل. لا تتردد في نسخه ولصقه في `Program.cs`. التعليقات توضح سبب أهمية كل سطر.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – this object does all the heavy lifting.
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Enable auto‑download of language resources.
            //    If the Hindi pack isn’t present locally, Aspose will fetch it silently.
            ocrEngine.AutoDownloadResources = true;

            // 3️⃣ Set the OCR language to Hindi – this tells the engine what character set to expect.
            ocrEngine.Language = OcrLanguage.Hindi;

            // 4️⃣ Load the image you want to process.
            //    Replace the path with the actual location of your Hindi sign picture.
            Image sourceImage = Image.FromFile("YOUR_DIRECTORY/hindi_sign.jpg");

            // 5️⃣ Run the OCR process and capture the recognized text.
            string recognizedText = ocrEngine.Recognize(sourceImage);

            // 6️⃣ Output the result to the console.
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### لماذا علم `AutoDownloadResources` مهم

تقوم Aspose بتوزيع حزم اللغات كملفات منفصلة للحفاظ على خفة المكتبة الأساسية. عند تعيين `AutoDownloadResources` إلى `true`، تتجنب حدوث *FileNotFoundException* في المرة الأولى التي تحاول فيها **التعرف على النص الهندي**. يتواصل المحرك مع CDN الخاص بـ Aspose، يحصل على نموذج اللغة الهندية، يخزنه مؤقتًا محليًا، ويتابع تلقائيًا.

---

## الخطوة 3: فهم كيفية **تحميل الصورة لـ OCR**

`Image.FromFile` هو أبسط طريقة لجلب صورة bitmap إلى الذاكرة، لكنه يفترض وجود الملف وأنه بتنسيق يدعمه `System.Drawing`. إذا كنت بحاجة للتعامل مع ملفات PDF، أو TIFF متعددة الصفحات، أو روابط URL عن بُعد، فكر في البدائل التالية:

| السيناريو | النهج الموصى به |
|----------|----------------------|
| **صور كبيرة** ( > 5 MB ) | استخدم `Image.FromStream` مع `FileStream` واضبط `Image.FromStream(stream, useEmbeddedColorManagement: false, validateImageData: false)` لتقليل استهلاك الذاكرة. |
| **تنسيقات غير BMP** (مثال: WebP) | حوّلها إلى تنسيق مدعوم أولاً باستخدام `ImageMagick` أو `SkiaSharp`. |
| **صورة عن بُعد** | حمّلها باستخدام `HttpClient` → تدفق → `Image.FromStream`. |

هذه الاختيارات تضمن بقاء الكود قويًا، خاصةً عندما تقوم لاحقًا **باستخراج النص من صورة** من مصادر تتجاوز نظام الملفات المحلي.

---

## الخطوة 4: تشغيل التطبيق والتحقق من المخرجات

قم بتجميع البرنامج وتنفيذه:

```bash
dotnet run
```

إذا تم ربط كل شيء بشكل صحيح، يجب أن ترى شيئًا مشابهًا لـ:

```
=== Recognized Text ===
स्वागत है
```

المخرجات الفعلية تعتمد على جودة `hindi_sign.jpg`؛ كلما كان اللافتة أوضح، كانت النتائج أنقى.  

### المشكلات الشائعة وكيفية إصلاحها

- **حزمة اللغة مفقودة** – حتى مع `AutoDownloadResources`، قد يحظر جدار الحماية المؤسسي عملية التنزيل. قم بتنزيل حزمة اللغة الهندية يدويًا من بوابة Aspose وضعها في مجلد `Resources` بجوار الملف التنفيذي.  
- **مسار الصورة غير صحيح** – تحقق مرة أخرى من حساسية الأحرف في Linux/macOS؛ Windows يتسامح، لكن الأنظمة الأخرى لا.  
- **صورة منخفضة الدقة** – تتدهور دقة OCR بشكل كبير تحت 300 dpi. قم بزيادة دقة الصورة باستخدام مكتبة مثل `ImageSharp` قبل تمريرها إلى المحرك.

---

## الخطوة 5: اختياري – حفظ النص المُعترف به

غالبًا ما ترغب في حفظ النتيجة بدلاً من مجرد طباعتها. إليك مقتطفًا سريعًا يكتب النص إلى ملف UTF‑8:

```csharp
string outputPath = "output.txt";
File.WriteAllText(outputPath, recognizedText, System.Text.Encoding.UTF8);
Console.WriteLine($"Text saved to {Path.GetFullPath(outputPath)}");
```

الآن لم تقم فقط **بتشغيل OCR على صورة** بل أنشأت أيضًا خط أنابيب قابل لإعادة الاستخدام يمكن دمجه في أنظمة معالجة مستندات أكبر.

---

## مرجع بصري

فيما يلي لقطة شاشة placeholder لنتيجة وحدة التحكم. نص الـ alt يحتوي عمدًا على الكلمة المفتاحية الأساسية لأغراض تحسين محركات البحث.

![نتيجة مثال تشغيل OCR على صورة](example.png "تشغيل OCR على صورة – نتيجة وحدة التحكم تُظهر النص الهندي المُعترف به")

---

## ملخص وخطوات قادمة

لقد غطينا دورة الحياة الكاملة **لتشغيل OCR على صورة** باستخدام Aspose:

1. تثبيت حزمة NuGet.  
2. تهيئة `OcrEngine` وتمكين التحميل التلقائي.  
3. **تعيين لغة OCR** إلى Hindi (أو أي لغة مدعومة أخرى).  
4. **تحميل الصورة لـ OCR** باستخدام `System.Drawing`.  
5. استدعاء `Recognize` لـ **استخراج النص من صورة**.  
6. إخراج أو حفظ النتيجة.

إذا كنت مرتاحًا مع اللغة الهندية، جرّب استبدال `OcrLanguage.Hindi` بـ `OcrLanguage.English` أو `OcrLanguage.Arabic` أو أي من أكثر من 60 لغة تدعمها Aspose.  

### أين تذهب من هنا؟

- **معالجة دفعات:** تكرار عبر مجلد من الصور وكتابة كل نتيجة في ملف منفصل.  
- **ما قبل المعالجة:** تطبيق تحويل إلى تدرج الرمادي، تقليل الضوضاء، أو تصحيح الميل باستخدام `ImageSharp` قبل OCR لتحسين الدقة.  
- **التكامل:** ربط خطوة OCR بواجهة API ASP.NET Core بحيث يمكن للعملاء رفع الصور وتلقي النص المشفر بصيغة JSON.  

لا تتردد في التجربة — OCR متسامح بشكل مفاجئ بمجرد إتقان الأساسيات.  

---

### الأسئلة المتكررة

**س: هل يعمل هذا على .NET Framework 4.8؟**  
ج: نعم. نفس تجميع `Aspose.OCR` يستهدف كلًا من .NET Core و .NET Framework. فقط قم بتغيير ملف المشروع إلى إطار العمل المستهدف المناسب.  

**س: ماذا لو احتجت إلى التعرف على عدة لغات في نفس الصورة؟**  
ج: عيّن `ocrEngine.Language = OcrLanguage.MultiLanguage;` ويمكنك اختيارياً تمرير سلسلة مفصولة بفواصل لأكواد اللغات عبر `ocrEngine.Language = OcrLanguage.FromString("Hindi,English");`.  

**س: هل يمكن تشغيل هذا على Linux؟**  
ج: بالتأكيد — فقط تأكد من تثبيت حزمة `libgdiplus` لأن `System.Drawing.Common` يعتمد عليها على المنصات غير Windows.  

**هل أنت مستعد لتطبيق مهارات OCR الجديدة؟** احصل على مجموعة من العلامات متعددة اللغات، عدّل خاصية `Language`، وشاهد Aspose يحول الصور إلى نص قابل للبحث في ثوانٍ. برمجة سعيدة!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}