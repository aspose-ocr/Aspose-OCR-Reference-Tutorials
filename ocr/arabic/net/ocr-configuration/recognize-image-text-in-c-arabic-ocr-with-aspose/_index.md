---
category: general
date: 2025-12-30
description: التعرف على نص الصورة من الإيصالات العربية باستخدام Aspose OCR. تعلم استخراج
  النص العربي، تنزيل نموذج اللغة، وتحميل اللغة العربية في مثال OCR بلغة C#.
draft: false
keywords:
- recognize image text
- extract arabic text
- download language model
- c# ocr example
- load arabic language
language: ar
og_description: التعرف على نص الصورة من الإيصالات العربية باستخدام Aspose OCR. يوضح
  هذا الدليل كيفية استخراج النص العربي، تنزيل نموذج اللغة، وتحميل اللغة العربية في
  مثال OCR بلغة C#.
og_title: التعرف على نص الصورة في C# – التعرف الضوئي على الأحرف العربية باستخدام Aspose
tags:
- OCR
- C#
- Aspose
title: التعرف على نص الصورة في C# – OCR عربي مع Aspose
url: /ar/net/ocr-configuration/recognize-image-text-in-c-arabic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على نص الصورة في C# – OCR عربي باستخدام Aspose

هل احتجت يومًا إلى **التعرف على نص الصورة** من إيصال مكتوب بالعربية ولكن لم تعرف من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند التعامل مع النصوص من اليمين إلى اليسار. في هذا الدرس سنستعرض مثالًا كاملاً وجاهزًا للتنفيذ بلغة C# يستخدّم OCR لاستخراج النص العربي، يقوم بتنزيل نموذج اللغة المطلوب تلقائيًا، ويطبع النتيجة على وحدة التحكم.

سنغطي كل ما قد تتساءل عنه: لماذا يجب تحميل اللغة العربية صراحةً، كيف يعمل تنزيل نموذج اللغة عند الطلب، وماذا تفعل إذا لم تكن جودة الصورة مثالية. في النهاية ستحصل على مقطع شفرة جاهز للإنتاج يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

- **كيفية التعرف على نص الصورة** باستخدام Aspose OCR في C#  
- الخطوات الدقيقة **لاستخراج النص العربي** من ملف صورة  
- كيف يقوم SDK **بتنزيل نموذج اللغة** تلقائيًا عندما يكون مفقودًا  
- مثال كامل **c# ocr** يمكنك نسخه ولصقه وتشغيله فورًا  
- لماذا وكيفية **تحميل اللغة العربية** قبل التعرف للحصول على أفضل دقة  

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- حزمة NuGet صالحة لـ Aspose.OCR (يمكنك تثبيتها باستخدام `dotnet add package Aspose.OCR`).  
- صورة إيصال عربية محفوظة محليًا (سنشير إليها باسم `arabic_receipt.jpg`).  

لا توجد أدوات طرف ثالث أخرى مطلوبة؛ Aspose يتولى كل شيء من فك ترميز الصورة إلى إدارة نماذج اللغة.

![recognize image text example](/images/recognize-image-text-arabic-receipt.png "Diagram showing recognize image text from an Arabic receipt")

## الخطوة 1: إعداد المشروع وتثبيت Aspose OCR

أولًا، أنشئ مشروع وحدة تحكم (أو استخدم مشروعًا موجودًا) وأضف مكتبة Aspose OCR.

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
dotnet add package Aspose.OCR
```

*نصيحة:* إذا كنت تستخدم Visual Studio، يمكنك إضافة الحزمة عبر واجهة مدير الحزم NuGet—فقط ابحث عن **Aspose.OCR**.

## الخطوة 2: تهيئة محرك OCR

إنشاء كائن `OcrEngine` هو الأساس لأي سير عمل Aspose OCR. هذا الكائن يحمل الإعدادات، نماذج اللغة، وإعدادات وقت التشغيل.

```csharp
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // The rest of the code will follow...
        }
    }
}
```

لماذا ننشئ المحرك *قبل* تحميل اللغة؟ لأن المحرك يحتاج إلى معرفة نماذج اللغة المتوفرة، وتحميلها لاحقًا سيؤدي إلى تهيئة داخلية ثانية—وهو ما نريد تجنبه لأداء أفضل.

## الخطوة 3: تنزيل وتحميل نموذج اللغة العربية

Aspose OCR يأتي بنواة صغيرة ويسحب نماذج اللغة عند الطلب. السطر أدناه يطلب من المحرك جلب نموذج اللغة العربية إذا لم يكن مخزنًا محليًا بالفعل.

```csharp
// Step 3: Load the Arabic language model (downloaded on demand if missing)
ocrEngine.LoadLanguage(LanguageModel.Arabic);
```

عند تشغيلك لهذا الكود للمرة الأولى، ستظهر طلب شبكة قصير في مخرجات وحدة التحكم. التشغيلات اللاحقة تكون فورية لأن النموذج مخزن مؤقتًا على القرص. سلوك **download language model** هذا يضمن بقاء تطبيقك خفيفًا حتى يحتاج إلى البيانات الإضافية.

## الخطوة 4: التعرف على النص من صورة الإيصال العربي

الآن نوجه المحرك إلى ملف الصورة. Aspose OCR يكتشف تنسيق الصورة تلقائيًا، يتعامل مع ما قبل المعالجة، ويحترم ترتيب النص من اليمين إلى اليسار للعربية.

```csharp
// Step 4: Recognize text from the Arabic receipt image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/arabic_receipt.jpg");

// Step 5: Display the recognized text (RTL ordering is handled automatically)
Console.WriteLine("=== Recognized Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى معلومات الصناديق المحيطة إذا احتجت إليها لاحقًا للتظليل. بالنسبة إلى مثال **c# ocr** بسيط، خاصية `Text` هي كل ما تحتاجه.

### النتيجة المتوقعة

إذا كانت صورة الإيصال تحتوي على شيء مثل:

```
المجموع: 120.00 ريال
التاريخ: 30/12/2025
```

ستظهر نفس السطور العربية مطبوعة على وحدة التحكم، مرتبة بشكل صحيح من اليمين إلى اليسار:

```
=== Recognized Arabic Text ===
المجموع: 120.00 ريال
التاريخ: 30/12/2025
```

## الخطوة 5: مثال كامل يعمل

بدمج كل ما سبق، إليك البرنامج الكامل الذي يمكنك تجميعه وتشغيله الآن.

```csharp
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Load (and download if needed) the Arabic language model
            ocrEngine.LoadLanguage(LanguageModel.Arabic);

            // Path to your Arabic receipt image – adjust as needed
            string imagePath = @"YOUR_DIRECTORY/arabic_receipt.jpg";

            // Perform OCR
            var ocrResult = ocrEngine.Recognize(imagePath);

            // Output the recognized Arabic text
            Console.WriteLine("=== Recognized Arabic Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

احفظ هذا الملف باسم `Program.cs`، شغّل `dotnet run`، ويجب أن ترى النص العربي يظهر في وحدة التحكم. إذا حصلت على خطأ “model not found”، تحقق من اتصال الإنترنت—فSDK يحتاج إلى **download language model** للمرة الأولى.

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت الصورة غير واضحة؟

Aspose OCR يتضمن فلاتر تحسين صورة مدمجة. يمكنك تفعيلها قبل استدعاء `Recognize`:

```csharp
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;
```

هذا غالبًا ما يحسّن الدقة للوصلات منخفضة الدقة.

### هل يمكن معالجة عدة صور في حلقة؟

بالطبع. المحرك يصبح خفيفًا بعد تحميل النموذج الأول، لذا يمكنك إعادة استخدام نفس كائن `ocrEngine`:

```csharp
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    Console.WriteLine($"--- {Path.GetFileName(file)} ---");
    Console.WriteLine(result.Text);
}
```

### هل أحتاج إلى ترخيص لـ Aspose OCR؟

ترخيص تجريبي مجاني يكفي للتطوير والاختبار. للإنتاج ستحتاج إلى ترخيص مدفوع؛ وإلا سيُقصَّ النص بعد عدد معين من الأحرف.

### كيف يؤثر **load arabic language** على الأداء؟

تحميل نموذج اللغة العربية مرة واحدة يضيف حوالي 5 ميغابايت إلى حجم النشر وتنزيل شبكة مرة واحدة (~2 ثانية على اتصال واسع النطاق عادي). بعد ذلك، يعمل التعرف بسرعة أصلية—بدون عبء إضافي لكل صورة.

## نصائح للحصول على أفضل النتائج

- **قم بقص الإيصال** لإزالة الفوضى المحيطة؛ محرك OCR يركز على المنطقة التي تزوده بها.  
- **استخدم PNG** بدلاً من JPEG عندما يكون ذلك ممكنًا؛ الضغط غير الفاقد يحافظ على الحواف الحادة التي تعتمد عليها الحروف العربية.  
- **حدد DPI الصحيح** (300 dpi هو الإعداد الآمن) إذا كنت تولد الصور برمجيًا.  
- **تحقق من `ocrResult.Confidence`** إذا كنت بحاجة لتصفية السطور ذات الثقة المنخفضة قبل تخزينها.

## الخلاصة

أنت الآن تعرف بالضبط كيف **تتعرف على نص الصورة** من إيصالات عربية باستخدام Aspose OCR في مثال **c# ocr** نظيف. بتحميل نموذج اللغة العربية، والسماح للـ SDK **download language model** عند الحاجة، واستدعاء `Recognize`، يمكنك استخراج النص العربي من أي صورة تواجهها تطبيقك بثقة.

من هنا يمكنك استكشاف:

- إيداع النص المستخرج في قاعدة بيانات لتتبع النفقات.  
- استخدام تحليل التخطيط في Aspose لاستخراج أزواج المفتاح‑القيمة (مثل المبلغ الإجمالي، التاريخ).  
- توسيع الحل ليشمل لغات أخرى من اليمين إلى اليسار مثل العبرية أو الفارسية.

جرّبه، عدّل خيارات ما قبل المعالجة، ودع OCR يتولى الجزء الصعب. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}