---
category: general
date: 2026-01-09
description: استخراج النص من PNG بسرعة باستخدام Aspose OCR. تعلم كيفية قراءة نص الصورة،
  تحسين دقة OCR، والحصول على نتائج نظيفة في C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: ar
og_description: استخراج النص من PNG بسرعة باستخدام Aspose OCR. تعلم كيفية قراءة نص
  الصورة، تحسين دقة OCR، والحصول على نتائج نظيفة في C#.
og_title: استخراج النص من PNG – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- Image Processing
title: استخراج النص من PNG – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PNG – دليل Aspose OCR الكامل

هل احتجت يوماً إلى **استخراج النص من PNG** لكن النتائج كانت مليئة بالخرابيش؟ لست وحدك. في العديد من المشاريع الواقعية – الفواتير، الإيصالات، أو النماذج الممسوحة ضوئياً – جودة مخرجات OCR يمكن أن تكون الفاصل بين نجاح أو فشل خطوط الأتمتة.  

في هذا الدليل سنظهر لك طريقة **خطوة‑بخطوة** لقراءة نص الصورة باستخدام Aspose OCR، مع إضافة قاموس مخصص **لتحسين دقة OCR**، وتنظيف الضوضاء، وأخيراً طباعة سلسلة نصية مرتبة. بنهاية الدليل ستحصل على تطبيق C# Console جاهز للتشغيل يستخرج النص من صور PNG بثبات.

> **ما ستحصل عليه**  
> * عينة كود كاملة قابلة للتنفيذ.  
> * فهم لماذا القاموس المخصص مهم.  
> * نصائح للتعامل مع الحالات الخاصة مثل المسحات منخفضة التباين.  

## المتطلبات المسبقة

- .NET 6 SDK أو أحدث (الكود يستهدف .NET 6، لكن .NET 5 يعمل أيضاً).  
- Visual Studio 2022 أو أي محرر تفضله.  
- صورة **PNG** تريد معالجتها – على سبيل المثال `invoice.png`.  
- حزمة **Aspose.OCR** من NuGet (`dotnet add package Aspose.OCR`).  

لا توجد ملفات إعداد إضافية مطلوبة؛ كل شيء موجود في ملف `.cs` واحد.

## الخطوة 1 – تثبيت وإضافة مرجع Aspose OCR

أولاً، احصل على المكتبة في مشروعك. افتح الطرفية في مجلد الحل وشغّل:

```bash
dotnet add package Aspose.OCR
```

هذا السطر الواحد يجلب أحدث نسخة مستقرة (اعتباراً من يناير 2026، النسخة 23.9). الحزمة تتضمن الفئة `OcrEngine` التي سنستخدمها طوال الدليل.

## الخطوة 2 – تهيئة محرك OCR

إنشاء كائن `OcrEngine` هو الأساس. فكر فيه كتشغيل ماسح ضوئي جاهز لتفسير البكسلات.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **نصيحة محترف:** إذا كنت تخطط لمعالجة العديد من الصور داخل حلقة، أعد استخدام نفس كائن `OcrEngine`. فهو يخزن موارد داخلية في الذاكرة ويسرّع الاستدعاءات اللاحقة.

## الخطوة 3 – تعزيز الدقة باستخدام قاموس مخصص

OCR الافتراضي جيد، لكنه قد يتعثر مع كلمات خاصة بالمجال مثل “Aspose”، “OCR”، أو “SDK”. إضافة هذه المصطلحات إلى **قاموس مخصص** تخبر المحرك أن هذه السلاسل صالحة، مما يقلل الأخطاء.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### لماذا يساعد القاموس المخصص

- **النماذج الإحصائية** وراء OCR تعطي وزنًا كبيرًا للأنماط اللغوية الشائعة. الكلمات غير الشائعة تحصل على احتمالية منخفضة وقد تُستبدل بأحرف تشبهها.  
- من خلال إدراجها صراحةً، تتجاوز تخمينات النموذج.  
- هذا مفيد بشكل خاص ل**قراءة نص الصورة** التي تحتوي على رموز منتجات، اختصارات، أو أسماء علامات تجارية.

## الخطوة 4 – التعرف على النص من ملف PNG

الآن نمرر مسار الصورة إلى المحرك. طريقة `RecognizeImage` تُعيد سلسلة خام لا تزال تحتوي على رموز غير معروفة (مثل “#@!”) لم يتمكن المحرك من تعيينها.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **حالة حافة:** إذا لم يُعثر على الملف، فإن `RecognizeImage` تُطلق استثناء `FileNotFoundException`. لذا احرص على وضع الاستدعاء داخل كتلة try‑catch في الكود الإنتاجي.

## الخطوة 5 – تنظيف النتيجة باستخدام `CleanText`

Aspose OCR يأتي مع أداة مساعدة تُزيل الأحرف التي يُصنّفها كـ “غير معروفة”. هذه الخطوة حاسمة لمشاريع **استخراج النص من الصورة** حيث يتوقع المعالج اللاحق وجود أحرف أبجدية رقمية وعلامات ترقيم أساسية فقط.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

طريقة `CleanText` تُعيد أيضًا تطبيع نهايات الأسطر، مما يجعل المخرجات آمنة للتخزين في قواعد البيانات أو تمريرها إلى خدمات أخرى.

## الخطوة 6 – إخراج النص المنظف

أخيراً، اعرض أو احفظ النتيجة. في تطبيق Console، يكفي استدعاء `Console.WriteLine`.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

عند تشغيل البرنامج، يجب أن ترى كتلة نصية مرتبة تعكس محتوى `invoice.png`. إذا احتوت الصورة على كلمة “Aspose”، يضمن القاموس المخصص ظهورها بشكل صحيح بدلاً من شيء مثل “A5p0se”.

## مثال كامل يعمل

بدمج كل ما سبق، إليك ملف `Program.cs` الكامل الذي يمكنك نسخه‑لصقه في مشروع Console جديد:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع** (بافتراض أن PNG يحتوي على فاتورة بسيطة):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

إذا رأيت رموزاً غريبة، تحقق من جودة الصورة أو وسّع القاموس المخصص بإضافة المزيد من المصطلحات.

## إضافي: التعامل مع المسحات منخفضة الجودة

أحياناً تكون PNGات ممسوحة بدقة 72 dpi أو تحتوي على ضوضاء ضغط عالية. إليك بعض الحيل السريعة **لتحسين دقة OCR** دون مغادرة C#:

1. **معالجة مسبقة للصورة** باستخدام مكتبة مثل `SixLabors.ImageSharp` – زيادة التباين، التحويل إلى تدرج رمادي، أو تطبيق تمويه خفيف لتقليل الضوضاء.  
2. **تعيين خاصية `Resolution`** على `OcrEngine` (مثال: `ocrEngine.Resolution = 300;`) لإخبار المحرك بأن يتعامل مع الصورة كأنها ذات دقة أعلى.  
3. **تمكين حزم اللغات** إذا كنت تتعامل مع نص غير إنجليزي (`ocrEngine.Language = Language.English;`).

يمكن إضافة جميع هذه الأساليب قبل استدعاء `RecognizeImage`.

## الأسئلة المتكررة

- **هل يعمل هذا مع صيغ صور أخرى؟**  
  نعم. `RecognizeImage` تقبل JPEG، BMP، TIFF، وحتى PDF (كحاوية صور). الخطوات نفسها تُطبق.

- **هل يمكن استخراج النص من عدة PNGs في مجلد؟**  
  بالتأكيد. غلف المنطق الأساسي داخل حلقة `foreach (var file in Directory.GetFiles(folder, "*.png"))` واحفظ كل نتيجة في قائمة أو اكتبها إلى ملفات منفصلة.

- **ماذا لو احتجت إحداثيات النص؟**  
  Aspose OCR يوفر أيضاً كائنات `OcrResult` التي تشمل مربعات الإحاطة. استخدم `ocrEngine.RecognizeImageToResult(imagePath)` لهذا السيناريو المتقدم.

## الخلاصة

لقد استعرضنا حلًا **متكاملاً من البداية إلى النهاية** لـ **استخراج النص من PNG** باستخدام Aspose OCR. من خلال تهيئة المحرك، إضافة **قاموس مخصص**، تنظيف المخرجات الخام، ومعالجة بعض المشكلات الشائعة، يمكنك قراءة نص الصورة بثقة وتحسين دقة OCR في تطبيقات C# الخاصة بك.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال PNG بإيصال ممسوح، أضف المزيد من الكلمات الخاصة بمجالك إلى القاموس، أو دمج الناتج مع قاعدة بيانات لمعالجة الفواتير تلقائيًا. السماء هي الحد عندما تجمع بين Aspose OCR وإيكولوجية .NET الغنية.

برمجة سعيدة، ولتكن OCR دائمًا دقيقة! 

![مثال استخراج النص من PNG](/images/extract-text-from-png.png "استخراج النص من PNG – عرض Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}