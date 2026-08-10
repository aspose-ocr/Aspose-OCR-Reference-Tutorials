---
category: general
date: 2026-03-26
description: دليل C# OCR يوضح كيفية استخراج النص من الصورة، التعرف على النص من ملف
  JPEG وتحميل الصورة للـ OCR – يتضمن دعم اللغة السيريلي.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpeg
- load image for ocr
- recognize cyrillic text
language: ar
og_description: دروس C# OCR التي ترشدك خطوة بخطوة لتحميل صورة للـ OCR، والتعرف على
  النص من JPEG واستخراج النص السيريلي في بضع خطوات سهلة.
og_title: دليل c# OCR – استخراج النص من الصورة باستخدام Aspose OCR
tags:
- OCR
- C#
- Aspose
- ImageProcessing
title: دروس OCR بلغة C# – استخراج النص من الصورة باستخدام Aspose OCR
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – استخراج النص من الصورة باستخدام Aspose OCR

هل احتجت يومًا إلى **c# ocr tutorial** الذي ينقلك فعليًا من صورة JPEG فارغة إلى نص يونيكود قابل للقراءة؟ ربما تكون تبني أداة أرشفة مستندات، أو ماسح إيصالات، أو مجرد فضول حول استخراج النص من الصور. على أي حال، أنت في المكان المناسب. في هذا الدليل سنوضح لك كيفية **extract text from image**، **recognize text from jpeg**، وحتى التعامل مع سيناريو **recognize cyrillic text** الصعب—دون الحاجة إلى استدعاءات سحابة.

سنستخدم Aspose.OCR، مكتبة تعمل بالكامل دون اتصال وتوفر وحدات لغات يمكنك الإشارة إليها على القرص. بنهاية هذا الدرس ستحصل على تطبيق console مستقل يحمل صورة للـ OCR، يشغل المحرك، ويطبع النتيجة في وحدة التحكم. لا خدمات خارجية، لا مفاتيح API—فقط C# نقي.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)
- Visual Studio 2022 أو أي بيئة تطوير تفضلها
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) ومجلد `Aspose.OCR.Resources` المطابق
- صورة JPEG تحتوي على أحرف سيريليّة (أو أي لغة تريد اختبارها)

إذا كنت تفتقد أيًا منها، احصل على حزمة NuGet عبر وحدة تحكم مدير الحزم:

```powershell
Install-Package Aspose.OCR
```

وقم بتنزيل موارد اللغة من موقع Aspose، فك ضغطها في مجلد مثل `C:\OCR\Aspose.OCR.Resources`.

الآن، لنبدأ.

## الخطوة 1: تحميل موارد OCR – load image for ocr

أول شيء يحتاجه المحرك هو مسار وحدات اللغة. فكر فيه كأنك تخبر OCR أين يعيش القاموس الخاص به.

```csharp
using Aspose.OCR;
using Aspose.OCR.Resources;

// Point to the folder that contains the language modules
ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");
```

> **نصيحة احترافية:** استخدم مسارًا مطلقًا أثناء التطوير. عندما تنشر التطبيق، فكر في تضمين الموارد أو نسخها بجانب الملف التنفيذي.

## الخطوة 2: اختيار اللغة – recognize cyrillic text

يدعم Aspose عشرات اللغات، لكن عليك اختيار اللغة التي تحتاجها. للنص السيريلي نستخدم `OcrLanguage.CyrillicExtended`. إذا كنت تحتاج فقط أحرف لاتينية، استبدلها بـ `OcrLanguage.English`.

```csharp
// Create the OCR engine and set the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.CyrillicExtended   // This enables Cyrillic recognition
};
```

لماذا هذا مهم؟ المحرك يحمل مصنّفات خاصة باللغة؛ اختيار اللغة الخاطئة قد يقلل الدقة بشكل كبير.

## الخطوة 3: تحميل JPEG – recognize text from jpeg

الآن نقوم بتحميل الصورة التي نريد مسحها. يستطيع Aspose قراءة الصيغ الشائعة مثل JPEG، PNG، BMP، و TIFF.

```csharp
// Load the image file (replace with your own path)
var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");
```

إذا كانت الصورة كبيرة، قد ترغب في تقليل حجمها قبل إمداده إلى المحرك—هذا يسرّع المعالجة ويقلل استهلاك الذاكرة.

## الخطوة 4: تشغيل التعرف – extract text from image

مع تكوين المحرك والصورة في الذاكرة، خطوة التعرف هي سطر واحد فقط.

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

خلف الكواليس، يقوم المحرك بسلسلة من عمليات ما قبل المعالجة (إزالة الضوضاء، التثنيم) ثم يطابق الأنماط البصرية مع نموذج اللغة المختار.

## الخطوة 5: عرض النتيجة – extract text from image

أخيرًا، نعرض السلسلة التي تم التعرف عليها. في تطبيق واقعي قد تكتبها إلى ملف، قاعدة بيانات، أو تغذيها إلى فهرس بحث.

```csharp
// Print the extracted text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**الإخراج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على “Привет мир!”):

```
=== OCR Output ===
Привет мир!
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من اختيار اللغة الصحيحة وأن الصورة ليست صاخبة جدًا.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. احفظه كـ `Program.cs` داخل مشروع console جديد وشغّله.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Resources;

class OfflineOcrDemo
{
    static void Main()
    {
        // Step 1: Point the OCR engine to the folder that contains the language modules
        ResourceManager.SetLocalResourcesPath(@"C:\OCR\Aspose.OCR.Resources");

        // Step 2: Create the OCR engine and select the required language (Cyrillic Extended)
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.CyrillicExtended
        };

        // Step 3: Load the image that contains the text to be recognized
        var ocrImage = OcrImage.FromFile(@"C:\OCR\Samples\cyrillic_doc.jpg");

        // Step 4: Perform the recognition operation
        OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 5: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **ملاحظة:** استبدل المسارات بالمواقع الفعلية على جهازك. البرنامج يعمل دون اتصال؛ لا حاجة لاتصال بالإنترنت بمجرد توفر الموارد.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت صورتي PNG بدلاً من JPEG؟

يتعامل Aspose.OCR مع PNG بنفس طريقة JPEG. فقط غيّر امتداد الملف في `FromFile`. خطوة **recognize text from jpeg** تعمل مع أي صيغة مدعومة.

### كيف أحسن الدقة في المسحات منخفضة الجودة؟

- قم بعملية ما قبل المعالجة للصورة (زيادة التباين، تصحيح الميل) باستخدام `ocrImage.AdjustContrast(1.2)` أو طرق مشابهة.
- استخدم `OcrEngine.PreprocessImage` قبل استدعاء `Recognize`.
- اختر لغة تتطابق مع النص؛ للخلط بين اللاتينية/السيريلي يمكنك تعيين `Language = OcrLanguage.Multilingual`.

### هل يمكنني استخراج الأرقام أو التواريخ فقط؟

نعم. بعد حصولك على `ocrResult.Text`، استخدم التعبيرات النمطية لتصفية الأجزاء التي تحتاجها. الـ OCR نفسه يُعيد السلسلة الخام؛ التحليل اللاحق متروك لك.

### هل يمكن تشغيل هذا على Linux؟

بالطبع. Aspose.OCR متعدد المنصات. فقط قم بتثبيت .NET runtime على جهاز Linux الخاص بك وعيّن `SetLocalResourcesPath` إلى المجلد المناسب.

## نصائح احترافية للإنتاج

- **Cache the OcrEngine**: إنشاء محرك جديد لكل طلب يضيف عبءً. احتفظ بـ singleton إذا كنت تعالج العديد من الصور.
- **Thread safety**: المحرك غير آمن للـ thread بشكل افتراضي. إما أن تقفل حول `Recognize` أو تنشئ محركات منفصلة لكل thread.
- **Memory management**: حرّر كائنات `OcrImage` بعد الاستخدام (`ocrImage.Dispose()`) لتحرير الذاكرة الأصلية.
- **Logging**: احصل على `ocrResult.Confidence` (إن كان متاحًا) لاكتشاف المسحات منخفضة الثقة وتفعيل بديل.

## الخلاصة

أصبح لديك الآن **c# ocr tutorial** الذي يرشّحك عبر كل خطوة لـ **load image for ocr**، **recognize text from jpeg**، **extract text from image**، و **recognize cyrillic text** باستخدام Aspose.OCR. الكود النموذجي جاهز للتنفيذ، والشروحات توضح لماذا كل سطر مهم—not just how.

من هنا يمكنك تجربة لغات أخرى، دمج OCR في واجهة ويب API، أو إمداد السلاسل المستخرجة إلى محرك بحث. الاحتمالات واسعة بقدر الصور التي تغذيها.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع وثائق Aspose للحصول على خيارات تكوين أعمق. برمجة سعيدة، ولتكن صورك دائمًا واضحة كالبلور!

![لقطة شاشة من درس c# OCR تُظهر ناتج وحدة التحكم للنص المستخرج](/images/ocr-demo.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}