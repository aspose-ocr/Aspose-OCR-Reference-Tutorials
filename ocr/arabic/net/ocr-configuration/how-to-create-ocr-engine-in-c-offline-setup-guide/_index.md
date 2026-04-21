---
category: general
date: 2026-03-04
description: تعلم كيفية إنشاء OCR باستخدام C# دون الحاجة إلى الإنترنت. يوضح هذا الدليل
  خطوة بخطوة أيضًا كيفية تشغيل OCR دون اتصال باستخدام الموارد المحلية.
draft: false
keywords:
- how to create OCR
- how to run OCR
- offline OCR C#
- local OCR resources
- OcrEngine setup
language: ar
og_description: كيفية إنشاء OCR في C# دون أي مكالمات شبكة. اتبع هذا الدليل لتعلم كيفية
  تشغيل OCR محليًا باستخدام LocalResourceProvider.
og_title: كيفية إنشاء محرك OCR في C# – الإعداد دون اتصال
tags:
- OCR
- C#
- Offline Processing
title: كيفية إنشاء محرك OCR في C# – دليل الإعداد دون اتصال
url: /ar/net/ocr-configuration/how-to-create-ocr-engine-in-c-offline-setup-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء محرك OCR في C# – دليل الإعداد غير المتصل

هل تساءلت يومًا **كيفية إنشاء OCR** لا يتصل بالإنترنت أبداً؟ ربما تبني تطبيق سطح مكتب آمن، أو ببساطة لا تحب المكالمات الشبكية غير المستقرة. في كلتا الحالتين، ستحتاج إلى محرك OCR يعيش بالكامل على جهاز العميل.  

الخبر السار؟ إنه بسيط إلى حد ما. في هذا الدرس سنستعرض **كيفية إنشاء OCR** خطوة بخطوة، ثم نوضح لك **كيفية تشغيل OCR** في وضع غير متصل باستخدام `LocalResourceProvider`. في النهاية ستحصل على مقتطف C# مستقل يمكنك إدراجه في أي مشروع .NET—بدون الحاجة إلى خدمات خارجية.

## ما ستتعلمه

- المتطلبات الأساسية لإعداد OCR غير متصل.  
- كيفية إنشاء كائن `OcrEngine` وتوجيهه إلى مجلد موارد محلي.  
- لماذا يزيل استخدام موفر محلي زمن الاستجابة الشبكي ويحسن الخصوصية.  
- المشكلات الشائعة (ملفات مفقودة، مسارات خاطئة) وكيفية تجنبها.  

جميع الشيفرات التي تحتاجها مضمونة، بالإضافة إلى خطوة تحقق سريعة لتتمكن من رؤية المحرك يعمل مباشرة بعد النسخ‑اللصق.

## المتطلبات المسبقة

قبل أن نغوص، تأكد من وجود ما يلي:

1. **.NET 6.0 أو أحدث** – مكتبة OCR التي سنستخدمها تستهدف .NET Standard 2.0، لذا أي بيئة تشغيل حديثة تعمل.  
2. **مجلد يحتوي على موارد OCR** – حزم اللغات، ملفات البيانات المدربة، وأي ثنائيات مساعدة. إذا لم تكن لديك بعد، قم بتنزيل الحزمة المناسبة من حزمة البائع غير المتصلة وفك ضغطها إلى `C:\MyApp\OcrResources`.  
3. **Visual Studio 2022** (أو أي بيئة تطوير تفضلها).  

هذا كل شيء—بدون حزم NuGet تتصل بالإنترنت أثناء التشغيل.

![مخطط يوضح تدفق OCR غير المتصل – كيفية إنشاء محرك OCR دون استدعاءات شبكة](offline-ocr-diagram.png)

*نص بديل الصورة: مخطط كيفية إنشاء محرك OCR غير متصل*

---

## الخطوة 1: إضافة مرجع مكتبة OCR

أولاً، أضف مرجع تجميع OCR SDK إلى مشروعك. إذا كان لديك ملف `.dll` من البائع، انقر بزر الماوس الأيمن **References → Add Reference** وتصفح إلى `OcrSdk.dll`. بدلاً من ذلك، إذا كان SDK يُوزع كحزمة NuGet تدعم الوضع غير المتصل، نفّذ:

```bash
dotnet add package OcrSdk --version 3.2.1
```

> **نصيحة احترافية:** ثبّت رقم الإصدار. الترقية لاحقًا قد تُدخل تغييرات كسرية تؤثر على مسار الموارد غير المتصلة.

---

## الخطوة 2: إنشاء كائن محرك OCR  

الآن سنقوم فعليًا **بكيفية إنشاء OCR** عن طريق إنشاء كائن `OcrEngine`. هذا الكائن هو نقطة الدخول لجميع مهام التعرف.

```csharp
using OcrSdk;               // Namespace provided by the OCR library
using OcrSdk.Resources;    // Contains LocalResourceProvider

// ...

// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

لماذا نحتاج إلى محرك مخصص؟ الـ `OcrEngine` يحتفظ بالإعدادات، يخزن نماذج اللغة مؤقتًا، ويدير مجموعات الخيوط. إنشاءه مرة واحدة وإعادة استخدامه عبر عمليات مسح متعددة أكثر كفاءة بكثير من إنشاء كائن جديد لكل صورة.

---

## الخطوة 3: توجيه المحرك إلى مجلد موارد محلي  

إليك الجزء الحاسم الذي يتيح لك **كيفية تشغيل OCR** دون لمس الويب أبداً. نُعيّن `LocalResourceProvider` يقرأ بيانات اللغة من دليل على القرص.

```csharp
// Step 3: Configure the engine to use offline resources
string resourcePath = @"C:\MyApp\OcrResources";
ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);
```

**ما الذي يحدث خلف الكواليس؟** الـ `LocalResourceProvider` يطبق نفس الواجهة التي يستخدمها الموفر السحابي الافتراضي، لكنه يقرأ ملفات `.dat` من `resourcePath`. هذه الحيلة تضمن أن جميع استدعاءات OCR اللاحقة تبقى محلية.

> **احذر:** إذا كان المسار خاطئًا أو كان المجلد يفتقد الملفات المطلوبة (`eng.traineddata`, `ocr_config.xml`, إلخ)، سيُطلق المحرك استثناءً `ResourceNotFoundException`. تحقق دائمًا من صحة المجلد قبل تعيينه.

---

## الخطوة 4: التحقق من جاهزية المحرك  

تحقق سريع من الصحة يوفر عليك وقت التصحيح لاحقًا. استدعِ `IsReady` (أو الخاصية المكافئة) واطبع النتيجة.

```csharp
// Step 4: Verify the engine can locate its resources
if (ocrEngine.IsReady)
{
    Console.WriteLine("✅ OCR engine is ready – offline mode confirmed.");
}
else
{
    Console.WriteLine("❌ OCR engine failed to load resources. Check the path and files.");
    return;
}
```

يجب أن ترى علامة الاختبار الخضراء في وحدة التحكم. إذا ظهرت علامة الصليب الحمراء، تحقق مرة أخرى من أن `resourcePath` يشير إلى المجلد الذي يحتوي على حزم اللغات.

---

## الخطوة 5: تشغيل OCR على صورة نموذجية  

أخيرًا، لنقم فعليًا **بتشغيل OCR** على صورة. ضع صورة باسم `sample.png` في نفس مجلد الموارد (أو أي موقع يمكن الوصول إليه) ومرّرها إلى المحرك.

```csharp
// Step 5: Perform OCR on a local image
string imagePath = Path.Combine(resourcePath, "sample.png");

// Load the image (the SDK may provide its own Image class)
var ocrImage = OcrImage.FromFile(imagePath);

// Run recognition – this call is completely offline
OcrResult result = ocrEngine.Recognize(ocrImage);

// Output the recognized text
Console.WriteLine("🖋️ Recognized Text:");
Console.WriteLine(result.Text);
```

**الناتج المتوقع** (بافتراض أن `sample.png` يحتوي على العبارة “Hello OCR!”):

```
🖋️ Recognized Text:
Hello OCR!
```

إذا كان الناتج فارغًا، تحقق من وضوح الصورة ومن وجود نموذج اللغة الإنجليزية (`eng`) في `OcrResources`.

---

## الحالات الحدية والمشكلات الشائعة  

| الحالة | ما يحدث | كيفية الإصلاح |
|-----------|--------------|---------------|
| **ملف لغة مفقود** | `ResourceNotFoundException` في الخطوة 3 | تأكد من وجود `eng.traineddata` (أو اللغة المستهدفة) في المجلد. |
| **صورة تالفة** | `OcrException` مع “Unsupported format” | حوّل الصورة إلى PNG أو BMP قبل تمريرها إلى المحرك. |
| **عدة خيوط** | حالات سباق إذا أنشأت محركات متعددة | أعد استخدام كائن `OcrEngine` واحد؛ فهو آمن للاتصالات المتزامنة `Recognize`. |
| **المسار يحتوي على مسافات** | فشل المحرك في العثور على الموارد | استخدم سلسلة حرفية (`@"C:\Path With Spaces\OcrResources"`) أو هروب الشرطات المائلة. |

---

## مثال كامل يعمل  

فيما يلي برنامج وحدة تحكم جاهز للتنفيذ يجمع كل شيء معًا. انسخ الشيفرة إلى مشروع `.csproj` جديد واضغط **F5**.

```csharp
// File: Program.cs
using System;
using System.IO;
using OcrSdk;
using OcrSdk.Resources;

namespace OfflineOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Point to local resources (offline mode)
            string resourcePath = @"C:\MyApp\OcrResources";
            ocrEngine.ResourceProvider = new LocalResourceProvider(resourcePath);

            // 3️⃣ Verify the engine can load resources
            if (!ocrEngine.IsReady)
            {
                Console.WriteLine("❌ Engine failed to initialize. Check your resource folder.");
                return;
            }
            Console.WriteLine("✅ Engine initialized successfully.");

            // 4️⃣ Load a test image
            string imagePath = Path.Combine(resourcePath, "sample.png");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            var ocrImage = OcrImage.FromFile(imagePath);

            // 5️⃣ Run OCR – entirely offline
            OcrResult result = ocrEngine.Recognize(ocrImage);

            // 6️⃣ Show the result
            Console.WriteLine("\n🖋️ Recognized Text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

**تشغيل البرنامج** يجب أن يطبع رسائل التأكيد والنص المستخرج، مما يثبت أنك الآن تعرف **كيفية إنشاء OCR** و**كيفية تشغيل OCR** دون مغادرة الجهاز أبداً.

---

## الخاتمة  

لقد غطينا كل ما تحتاج معرفته حول **كيفية إنشاء OCR** في مشروع C# وأظهرنا **كيفية تشغيل OCR** بالكامل في وضع غير متصل. من خلال تكوين `LocalResourceProvider`، تُزيل زمن الاستجابة الشبكي، تحمي البيانات الحساسة، وتكتسب سيطرة كاملة على دورة حياة OCR.  

هل أنت مستعد للتحدي التالي؟ جرّب استبدال نموذج اللغة الإنجليزية بلغة أخرى، أو جرب خطوات تمهيدية مختلفة للصور (تحويل إلى تدرج الرمادي، تصحيح الميل) لتحسين الدقة. النمط نفسه ينطبق—فقط وجه المحرك إلى مجلد موارد مختلف.

إذا واجهت أي صعوبات، راجع جدول الحالات الحدية أعلاه أو اترك تعليقًا؛ برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}