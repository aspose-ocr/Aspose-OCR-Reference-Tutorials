---
category: general
date: 2026-04-06
description: كيفية تعيين الترخيص في Aspose OCR باستخدام C# – تعلّم كيفية تضمين المورد،
  الحصول على المورد المضمن، وتحميل الترخيص من ملف أو تدفق في بضع خطوات فقط.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: ar
og_description: يتم شرح كيفية تعيين الترخيص في Aspose OCR خطوة بخطوة. تعلّم كيفية
  تضمين الترخيص، استرجاعه، واستخدام تدفق الترخيص لتكامل سلس.
og_title: كيفية تعيين الترخيص في Aspose OCR – دليل C# كامل
tags:
- Aspose OCR
- C#
- .NET licensing
title: كيفية تعيين الترخيص في Aspose OCR – دليل C# الكامل
url: /ar/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين الترخيص في Aspose OCR – دليل C# الكامل

تعيين الترخيص في Aspose OCR هو عائق شائع للمطورين. في هذا الدرس سنستعرض الخطوات الدقيقة لتعيين الترخيص، تضمينه كموارد، وتحميله من تدفق—حتى تتمكن من بدء عملية OCR دون علامة مائية مزعجة لوضع التجربة.

هل سبق لك أن حاولت تشغيل مهمة OCR فقط لتظهر لك لافتة “إصدار تجريبي”؟ هذا هو عرض نقص أو تطبيق الترخيص بشكل غير صحيح. بنهاية هذا الدليل ستحصل على نسخة Aspose OCR مرخصة بالكامل، سواء احتفظت بملف `.lic` بجانب ملفاتك التنفيذية أو أخفته داخل التجميع الخاص بك.

## ما ستحتاجه

- **Aspose.OCR for .NET** (أحدث حزمة NuGet في وقت كتابة هذا الدليل – 23.10)
- **ملف ترخيص Aspose OCR صالح** (`Aspose.OCR.lic`)
- Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#
- إلمام أساسي بتضمين الموارد في .NET (سنغطي ذلك)

لا توجد مكتبات طرف ثالث إضافية مطلوبة؛ كل شيء موجود داخل حزمة Aspose.

![توضيح كيفية تعيين الترخيص](image.png "كيفية تعيين الترخيص")

## الخطوة 1: تثبيت حزمة Aspose.OCR NuGet

قبل أن تتمكن من كتابة أي كود للترخيص، تأكد من الإشارة إلى المكتبة:

```bash
dotnet add package Aspose.OCR
```

أو، عبر مدير NuGet في Visual Studio، ابحث عن **Aspose.OCR** واضغط *Install*. سيقوم هذا بجلب `Aspose.OCR.dll` وتبعياته.

> **نصيحة احترافية:** استهدف .NET 6 أو أحدث للاستفادة من أحدث واجهة برمجة التطبيقات وأداء أفضل.

## الخطوة 2: إنشاء كائن الترخيص – جوهر “كيفية تعيين الترخيص”

تستخدم Aspose فئة `License` بسيطة لتطبيق المفتاح التجاري. إنشاء كائن منها هو السطر الأول في أي سير عمل مرخص:

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

لماذا هذا مهم: كائن `License` يقرأ محتوى ملف `.lic` ويسجله عالميًا لـ AppDomain الحالي. بمجرد التسجيل، كل `OcrEngine` تنشئه سيعمل في وضع كامل المميزات.

## الخطوة 3: تطبيق الترخيص من ملف (طريقة “كيفية تحميل الترخيص” الكلاسيكية)

إذا كنت تفضل إبقاء ملف الترخيص بجوار الملف التنفيذي، استدعِ `SetLicense` مع مسار الملف:

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### أمور يجب الانتباه إليها

- **المسارات المطلقة مقابل النسبية:** يتم حل المسارات النسبية بالنسبة إلى *دليل العمل* للعملية، والذي غالبًا ما يكون مجلد `bin`.
- **أذونات الملف:** يجب أن يكون لدى الحساب الذي يشغل التطبيق صلاحية القراءة لملف `.lic`.
- **معالجة الاستثناءات:** `SetLicense` يطرح `FileNotFoundException` إذا كان المسار غير صحيح، لذا غلفه داخل `try/catch` إذا كنت تحتاج إلى تدهور سلس.

## الخطوة 4: كيفية تضمين المورد – تخزين الترخيص داخل التجميع الخاص بك

تضمين الترخيص يلغي الحاجة إلى شحن ملف منفصل. إليك كيفية **how to embed resource** في مشروع .NET:

1. أضف ملف `.lic` إلى مشروعك (مثلاً داخل مجلد يُسمى `Resources`).
2. انقر بزر الماوس الأيمن على الملف → *Properties* → اضبط **Build Action** إلى **Embedded Resource**.
3. ابنِ المشروع؛ يصبح الترخيص جزءًا من ملف الـ DLL المترجم.

الآن يمكنك استرجاعه باستخدام منطق **get embedded resource**.

## الخطوة 5: الحصول على تدفق المورد المضمّن

المقتطف التالي يوضح **get embedded resource** باستخدام الانعكاس. عدّل مساحة الاسم واسم المورد لتطابق بنية مشروعك:

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **لماذا الانعكاس؟** `Assembly.GetExecutingAssembly()` يشير إلى التجميع الجاري تشغيله، مما يضمن أن الكود يعمل سواء كنت في تطبيق كونسول، موقع ويب، أو Azure Function.

## الخطوة 6: استخدام تدفق الترخيص – نمط “use license stream”

الآن بعد أن لديك التدفق، استخدم **use license stream** لتطبيق الترخيص دون لمس نظام الملفات:

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

عند تلقي `SetLicense` لـ `Stream`، تقوم Aspose بقراءة البايتات مباشرة، تسجل الترخيص، وتغلق التدفق عند خروجك من كتلة `using`. هذه هي الطريقة الأنظف لإبقاء الترخيص مخفيًا.

### مثال كامل يعمل

بدمج كل شيء معًا، إليك برنامج مستقل يوضح جميع الأساليب الثلاثة (ملف، مورد مضمّن، وتدفق). علق الأقسام التي لا تحتاجها.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**الناتج المتوقع**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

إذا لم يتم تطبيق الترخيص، ستطرح Aspose استثناء `LicenseException` أو ستظهر علامة مائية للتقييم في نتائج OCR.

## المشكلات الشائعة وكيفية تجنبها

| العرض | السبب المحتمل | الحل |
|-------|---------------|------|
| لا يزال يظهر شريط “إصدار تجريبي” | الترخيص غير محمّل أو المسار خاطئ | تحقق مرة أخرى من مسار الملف أو اسم المورد المضمّن. |
| `NullReferenceException` على `GetManifestResourceStream` | خطأ إملائي في اسم المورد أو عدم ضبط Build Action إلى Embedded Resource | تحقق من الاسم المؤهل للمساحة الاسم وضبط Build Action بشكل صحيح. |
| الترخيص يعمل محليًا لكنه يفشل بعد النشر | نقص أذونات القراءة على الخادم | امنح هوية مجموعة التطبيقات صلاحية القراءة لملف `.lic`، أو قم بتضمين الترخيص لتجنب مشاكل نظام الملفات. |
| وجود عدة كائنات `License` لا يحدث أي تأثير | قمت باستدعاء `SetLicense` على *كائن مختلف* بعد الأول | احتفظ بكائن `License` واحد لكل AppDomain؛ أعد استخدامه أو استدعِ `SetLicense` مرة واحدة عند بدء التشغيل. |

## متى تختار كل نهج

- **معتمد على الملف** – نمذجة سريعة، سهل الاستبدال دون إعادة بناء.
- **مورد مضمّن** – مثالي لتوزيع تطبيقات سطح المكتب أو المكتبات حيث لا تريد أن يكون الترخيص ظاهرًا.
- **معتمد على التدفق** – مثالي لبيئات السحابة (Azure Functions، AWS Lambda) حيث قد تجلب الترخيص من مخزن آمن وتغذيه مباشرة.

## الخطوات التالية – توسيع معرفتك بالترخيص

الآن بعد أن أتقنت **how to set license**، قد ترغب في استكشاف:

- **How to embed resource** في حلول متعددة المشاريع أكثر تعقيدًا.
- **Get embedded resource** من التجميعات التابعة لسيناريوهات التعريب.
- **How to load license** بشكل ديناميكي من Azure Key Vault أو AWS Secrets Manager.
- **Use license stream** مع حقن الاعتمادية للحصول على شفرة بدء تشغيل أنظف.

كل من هذه المواضيع يبني على الأساسيات التي غطيناها هنا ويساعدك على الحفاظ على استراتيجية ترخيص آمنة وقابلة للصيانة.

---

### TL;DR

لقد أوضحنا لك **how to set license** في Aspose OCR باستخدام ثلاث تقنيات موثوقة: التحميل من ملف، تضمين `.lic` كمورد، وتطبيقه عبر تدفق. اتبع الكود، واحترس من المشكلات المذكورة، وستعمل محرك OCR بأقصى سرعة—بدون علامات مائية تجريبية، دون مفاجآت.

برمجة سعيدة، ولتكن نتائج OCR واضحة كالكريستال!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}