---
category: general
date: 2026-01-15
description: تحويل الصورة إلى JSON باستخدام Aspose OCR في C#. تعلم كيفية استخراج النص
  من الصورة، الحصول على مربعات الإحاطة بصيغة JSON، والتعرف على صورة الإيصال.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: ar
og_description: تحويل الصورة إلى JSON باستخدام Aspose OCR في C#. دليل خطوة بخطوة لاستخراج
  النص من الصورة، التعرف على صورة الفاتورة، والحصول على إطارات JSON.
og_title: تحويل الصورة إلى JSON باستخدام دليل Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: تحويل الصورة إلى JSON باستخدام دليل Aspose OCR C#
url: /ar/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى JSON باستخدام دليل Aspose OCR C#

هل احتجت يومًا إلى **تحويل الصورة إلى JSON** لكنك لم تكن متأكدًا أي مكتبة يمكنها أن تزودك بالنص الخام وإحداثيات كل كلمة بدقة؟ لست وحدك. يواجه العديد من المطورين هذا العائق عندما يحاولون استخراج النص من ملفات الصور—خاصة الإيصالات—مع الحاجة أيضًا إلى حمولة JSON قابلة للقراءة آليًا للمعالجة اللاحقة.

في هذا الدرس سنستعرض مثالًا كاملًا **Aspose OCR C#** يوضح لك كيفية استخراج النص من الصورة، التعرف على صورة الإيصال، وإنتاج **مربعات إحداثيات JSON** لكل كلمة. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع سلسلة JSON منسقة يمكنك تمريرها إلى أي API أو قاعدة بيانات أو خط أنابيب تحليلي.

> **ما ستحصل عليه**  
> • مشروع C# كامل الوظائف **يحول الصورة إلى JSON**  
> • فهم لماذا نفعّل `IncludeBoundingBoxes` (إنه المفتاح لـ `json bounding boxes`)  
> • نصائح للتعامل مع صيغ صور ولغات مختلفة  

لنبدأ.

---

## ما الذي ستحتاجه

قبل أن نغوص في الكود، تأكد من تثبيت المتطلبات التالية:

- **.NET 6.0 SDK** (أو أي إصدار أحدث) – يستهدف الكود .NET 6 لكنه يعمل أيضًا على .NET Framework 4.7+.  
- **Aspose.OCR for .NET** حزمة NuGet – يمكنك إضافتها عبر `dotnet add package Aspose.OCR`.  
- صورة إيصال تجريبية (`receipt.jpg`) موجودة في مجلد يمكنك الإشارة إليه من مشروعك.  
- Visual Studio 2022، VS Code، أو أي بيئة تطوير تفضّلها.

لا توجد خدمات خارجية أخرى مطلوبة؛ كل شيء يعمل محليًا.

## نظرة عامة على تحويل الصورة إلى JSON

الفكرة الأساسية بسيطة: تحميل صورة، إخبار Aspose OCR بالتعرف على اللغة الإنجليزية (أو أي لغة مدعومة)، طلب تضمين مربعات الإحداثيات، وأخيرًا طلب النتيجة بصيغة **JSON**. المكتبة تتولى كل الأعمال الثقيلة—OCR، تحليل التخطيط، وتسلسل JSON.

إليك مخططًا عالي المستوى للتدفق (تخيل صورة صغيرة):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

هذا المخطط الصغير يلتقط كامل خط الأنابيب الذي سننفذه.

## الخطوة 1: إعداد المشروع وتثبيت Aspose OCR

أولًا، أنشئ مشروع كونسول جديد وأضف حزمة Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن **Aspose.OCR** وثبّت أحدث نسخة مستقرة (حاليًا 23.12).

## الخطوة 2: تحميل الصورة التي تريد التعرف عليها

سنستخدم الطريقة `OcrImage.FromFile` لقراءة صورة الإيصال. تأكد أن المسار يشير إلى ملف موجود؛ وإلا ستحصل على استثناء `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

إذا كانت صورتك موجودة بجانب ملف `.csproj`، يمكنك ببساطة استخدام `"receipt.jpg"`.

## الخطوة 3: تكوين خيارات OCR لمربعات إحداثيات JSON

السحر يحدث عندما نفعل `OutputFormat = OutputFormat.Json` **و** `IncludeBoundingBoxes = true`. الأول يطلب من Aspose تسلسل النتيجة كـ JSON، والثاني يضيف `x`، `y`، `width`، و`height` لكل كلمة—بالضبط ما تحتاجه لـ `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

يمكنك أيضًا تعديل `ocrOptions.Dpi` أو `ocrOptions.Language` إذا كنت بحاجة إلى دقة أعلى أو لغة مختلفة.

## الخطوة 4: تنفيذ التعرف – استخراج النص من الصورة

الآن نستدعي `Recognize`. تُعيد الطريقة كائن `OcrResult` يحتوي على سلسلة JSON، النص الخام، وأكثر.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

إذا احتجت إلى التعامل مع لغات أخرى، استبدل `Language.English` بـ `Language.Spanish` أو `Language.French` وغيرها. تدعم Aspose أكثر من 30 لغة جاهزة.

## الخطوة 5: إخراج النتيجة – حمولة JSON الخاصة بك

أخيرًا، نطبع JSON إلى الكونسول. في تطبيق حقيقي قد تكتبها إلى ملف أو ترسلها إلى خدمة.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

تشغيل البرنامج يجب أن ينتج مستند JSON مشابه للمقتطف أدناه.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

لاحظ كيف أن كل كلمة الآن تحمل **مربع إحداثيات JSON**—مثالي لتغذيته إلى واجهة مستخدم أو محلل لاحق.

## مثال عملي كامل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. لا أجزاء مخفية، لا استدعاءات خارجية—فقط C# نقي.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **احذر من:**  
> • **أخطاء مسار الملف** – تحقق مرة أخرى من موقع الصورة.  
> • **غياب حزمة NuGet** – تأكد من الإشارة إلى `Aspose.OCR`.  
> • **صيغ صور غير مدعومة** – استخدم JPEG، PNG، BMP، أو TIFF للحصول على أفضل النتائج.

## أسئلة شائعة وحالات خاصة

### هل يمكنني تحويل **صفحة PDF** إلى JSON بدلاً من JPEG؟

نعم. حوّل صفحة PDF إلى صورة أولًا (مثلاً باستخدام `Aspose.PDF`)، ثم مرّر تلك الصورة إلى نفس خط أنابيب OCR. سيكون إخراج JSON متطابقًا لأن خطوة OCR تهتم فقط بالبيانات النقطية.

### ماذا لو كان الإيصال غير واضح؟

زد قيمة DPI في `ocrOptions`. مثال:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

قد يزيد DPI العالي من استهلاك الذاكرة، لذا عليك موازنة الجودة مع الأداء.

### أحتاج إلى **عدة لغات** في نفس الإيصال (مثلاً الإنجليزية + الإسبانية).

يمكنك تمرير مصفوفة من اللغات:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

ستحاول Aspose التعرف على كل لغة بالترتيب المحدد.

### كيف أكتب JSON إلى ملف؟

ما عليك سوى استبدال سطر `Console.WriteLine` بـ:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

بهذا ستحصل على ملف دائم يمكنك إرساله إلى خدمات أخرى.

## ملخص بصري

![مثال تحويل الصورة إلى JSON](convert-image-to-json.png "مثال تحويل الصورة إلى JSON")

*تظهر لقطة الشاشة مخرجات الكونسول لسلسلة JSON بعد تشغيل النموذج.*

## الخلاصة

لقد أظهرنا لك كيف **تحول الصورة إلى JSON** باستخدام Aspose OCR في C#. من خلال تكوين `OutputFormat` و`IncludeBoundingBoxes`، يمكنك **استخراج النص من الصورة**، **التعرف على صورة الإيصال**، والحصول على **مربعات إحداثيات JSON** دقيقة لكل كلمة. الكود القابل للتنفيذ بالكامل موجود في المقتطف أعلاه، لذا يمكنك إدراجه في أي مشروع .NET الآن.

ما الخطوة التالية؟ جرّب تغذية JSON إلى عارض أمامي يبرز كل كلمة، أو أرسل البيانات إلى نموذج تعلم آلي يصنف بنود الإيصال. يمكنك أيضًا تجربة لغات أخرى، إعدادات DPI أعلى، أو معالجة دفعات من الصور في حلقة.

إذا واجهت أي صعوبات، تذكر النصائح المتعلقة بمسارات الملفات، DPI، ومصفوفات اللغات. لا تتردد في ترك تعليق أو فتح قضية في مستودع GitHub الذي تنشئه لهذا العرض. برمجة سعيدة، واستمتع بتحويل الصور إلى JSON منظم!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}