---
category: general
date: 2026-03-29
description: تعلم كيفية التحقق من علم الترخيص في Aspose OCR وكيفية الاستعلام عن حالة
  الترخيص برمجياً. مثال بسيط بلغة C# يوضح اكتشاف وضع التقييم.
draft: false
keywords:
- check license flag
- how to query license
- Aspose OCR license status
- OcrEngine.IsLicensed
- evaluation mode detection
language: ar
og_description: تحقق من علم الترخيص في Aspose OCR بسهولة. اكتشف كيفية الاستعلام عن
  حالة الترخيص باستخدام OcrEngine.IsLicensed وتعامل مع وضع التقييم.
og_title: تحقق من علم الترخيص في Aspose OCR – التحقق من الترخيص في C#
tags:
- Aspose OCR
- C#
- Licensing
title: تحقق من علامة الترخيص في Aspose OCR – دليل سريع للتحقق من الترخيص
url: /ar/net/ocr-configuration/check-license-flag-in-aspose-ocr-quick-guide-to-verify-licen/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحقق من علم الترخيص – Verify Aspose OCR Licensing in C#

هل تساءلت يومًا كيف **تتحقق من علم الترخيص** لـ Aspose OCR دون الغوص في مستندات لا تنتهي؟ لست وحدك. يواجه العديد من المطورين صعوبة في معرفة ما إذا كان تطبيقهم يعمل بترخيص كامل أو عالق في وضع التقييم. الخبر السار؟ إنه سطر واحد في C#، وسترى النتيجة فورًا.

في هذا الدرس سنستعرض **كيفية استعلام الترخيص** باستخدام الخاصية `OcrEngine.IsLicensed`، ونشرح لماذا هذا مهم، ونقدم لك برنامجًا كاملًا جاهزًا للتشغيل. في النهاية ستعرف بالضبط متى يكون الكود مرخصًا، وكيف يبدو الإخراج، وكيفية التعامل إذا كنت في وضع التقييم.

سنغطي:
- المتطلبات المسبقة (حزمة Aspose OCR NuGet، .NET 6+)
- تحليل الكود خطوة بخطوة
- الإخراج المتوقع في وحدة التحكم
- المشكلات الشائعة ونصائح احترافية

بدون إطالة، مجرد حل عملي يمكنك نسخه ولصقه في Visual Studio اليوم.

## المتطلبات المسبقة

قبل أن نغوص، تأكد من أنك تمتلك:
- بيئة تطوير .NET (Visual Studio 2022 أو VS Code مع امتداد C#)
- حزمة **Aspose.OCR** NuGet مثبتة (`dotnet add package Aspose.OCR`)
- إما ملف ترخيص Aspose OCR صالح أو أنك مرتاح للعمل في وضع التقييم للاختبار

إذا كنت تفتقد أيًا من هذه، احصل على حزمة NuGet أولًا—`dotnet add package Aspose.OCR`— وستكون جاهزًا للبدء.

## الخطوة 1 – استيراد مساحة الأسماء Aspose OCR

أول شيء تحتاجه هو توجيه `using` المناسب حتى يعرف المترجم مكان وجود `OcrEngine`.

```csharp
using Aspose.OCR;   // <-- brings OcrEngine into scope
```

> **لماذا؟**  
> بدون هذا الاستيراد ستحصل على خطأ “type or namespace name could not be found”. تجمع مساحة الأسماء جميع الفئات المتعلقة بـ OCR، و`OcrEngine` هو نقطة الدخول لفحص الترخيص.

## الخطوة 2 – إنشاء تطبيق وحدة تحكم بسيط

سنضع فحص الترخيص داخل تطبيق وحدة تحكم صغير. هذا يجعل المثال مستقلًا وسهل الاختبار.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 2a: Retrieve the license flag
        bool isLicensed = OcrEngine.IsLicensed;

        // Step 2b: Display the current mode
        Console.WriteLine(isLicensed ? "Licensed" : "Running in evaluation mode");
    }
}
```

### الشرح

- `OcrEngine.IsLicensed` هي **خاصية ثابتة من نوع Boolean** تُعيد `true` عندما يتم تحميل ترخيص صالح إلى فئة `OcrEngine`.  
- نخزن هذه القيمة في المتغير `isLicensed` لسهولة القراءة.  
- المعامل الشرطي (`? :`) يطبع رسالة ودية. إذا كان لديك ملف ترخيص تم تحميله مسبقًا (مثال: `OcrEngine.SetLicense("Aspose.OCR.lic")`)، سيكون الإخراج **Licensed**؛ وإلا سترى **Running in evaluation mode**.

## الخطوة 3 – تحميل ترخيص (اختياري لكن يُنصح به)

إذا كان لديك ملف ترخيص، فحمّله قبل فحص العلم. هذه الخطوة ليست مطلوبة للعلم نفسه—`IsLicensed` سيكون `false` حتى يتم تعيين ترخيص—لكنها تُظهر سير العمل الكامل.

```csharp
// Load the license file (adjust the path as needed)
try
{
    OcrEngine.SetLicense("Aspose.OCR.lic");
    Console.WriteLine("License file loaded successfully.");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load license: {ex.Message}");
}
```

ضع الكتلة أعلاه **قبل** السطر `bool isLicensed = OcrEngine.IsLicensed;`. إذا كان الملف مفقودًا أو تالفًا، سيُظهر لك كتلة الـ catch رسالة، وستظل قيمة `IsLicensed` `false`.

## الخطوة 4 – تشغيل والتحقق من الإخراج

ابنِ البرنامج وشغّله:

```bash
dotnet run
```

الإخراج النموذجي في وحدة التحكم عندما يكون الترخيص **موجودًا**:

```
License file loaded successfully.
Licensed
```

وعندما تكون في **وضع التقييم**:

```
Failed to load license: File not found.
Running in evaluation mode
```

## الخطوة 5 – التعامل مع وضع التقييم بأناقة

في التطبيقات الواقعية ربما لا تريد أن يتعطل البرنامج أو يتدهور بصمت. إليك نمطًا سريعًا لحماية الوظائف المميزة:

```csharp
if (!OcrEngine.IsLicensed)
{
    Console.WriteLine("Warning: Running in evaluation mode. Some features may be limited.");
    // Optionally, disable high‑resolution OCR or watermarks
}
else
{
    // Proceed with full‑feature OCR processing
}
```

> **نصيحة احترافية:** النسخة التجريبية تضيف علامة مائية إلى كل صورة معالجة. فحص العلم مبكرًا يساعدك على اتخاذ قرار إما إبلاغ المستخدم أو إخفاء عناصر واجهة المستخدم المتعلقة بالعلامة المائية.

## الخطوة 6 – المشكلات الشائعة وكيفية تجنبها

| المشكلة | سبب حدوثها | الحل |
|---------|----------------|-----|
| نسيان استدعاء `SetLicense` | `IsLicensed` يبقى `false` حتى مع ملف صالح | احرص دائمًا على تحميل الترخيص عند بدء تشغيل التطبيق |
| استخدام مسار نسبي يشير إلى المجلد الخطأ | وقت التشغيل لا يستطيع العثور على `Aspose.OCR.lic` | استخدم مسارًا مطلقًا أو دمج الترخيص كموارد مدمجة |
| التشغيل على منصة يتم فيها حظر ملف الترخيص (مثل حاوية للقراءة فقط) | `SetLicense` يطرح استثناء | تأكد من أن الملف لديه أذونات قراءة، أو انسخه إلى مجلد مؤقت قابل للكتابة |
| الافتراض بأن `IsLicensed` يتغير بعد معالجة OCR | الخاصية تعكس فقط حالة تحميل الترخيص، وليس حالة كل عملية | حمّل الترخيص مرة واحدة؛ لا تعيد الفحص بعد كل استدعاء OCR إلا إذا قمت بإلغاء تحميله (وهو غير شائع) |

معالجة هذه المشكلات مسبقًا توفر ساعات من تصحيح الأخطاء لاحقًا.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع وحدة تحكم جديد (`dotnet new console`) وتشغيله دون تعديل (فقط ضع ملف `.lic` الخاص بك بجوار `Program.cs`).

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Attempt to load the license (optional)
        try
        {
            OcrEngine.SetLicense("Aspose.OCR.lic");
            Console.WriteLine("License file loaded successfully.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load license: {ex.Message}");
        }

        // Query the license flag
        bool isLicensed = OcrEngine.IsLicensed;

        // Inform the user of the current mode
        Console.WriteLine(isLicensed ? "Licensed" : "Running in evaluation mode");

        // Example of graceful handling
        if (!isLicensed)
        {
            Console.WriteLine("Warning: Some OCR features may be restricted in evaluation mode.");
        }

        // Keep the console window open when debugging
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

**الإخراج المتوقع** (مرخص):

```
License file loaded successfully.
Licensed
Press any key to exit...
```

**الإخراج المتوقع** (بدون ترخيص):

```
Failed to load license: File not found.
Running in evaluation mode
Warning: Some OCR features may be restricted in evaluation mode.
Press any key to exit...
```

## الخلاصة

أنت الآن تعرف بالضبط **كيفية التحقق من علم الترخيص** لـ Aspose OCR وكيفية **استعلام حالة الترخيص** باستخدام `OcrEngine.IsLicensed`. من خلال تحميل الترخيص مبكرًا، وفحص العلم البولياني، والتعامل مع سيناريو التقييم بأناقة، تحافظ على تطبيقك قويًا وسهل الاستخدام.

ما التالي؟ جرّب دمج هذا الفحص في خط أنابيب OCR أكبر، ربما تشغيل المعالجة عالية الدقة فقط عندما يكون الترخيص الكامل موجودًا. يمكنك أيضًا استكشاف ميزات أخرى في Aspose OCR—الكشف عن اللغة، معالجة الصور مسبقًا، أو المعالجة الدفعية—مع الحفاظ على منطق الترخيص نظيفًا ومركّزًا.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه. برمجة سعيدة، ولتظل عمليات OCR الخاصة بك مرخصة بالكامل! 

![لقطة شاشة للتحقق من علم الترخيص](/images/check-license-flag.png "التحقق من علم الترخيص في مخرجات وحدة تحكم Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}