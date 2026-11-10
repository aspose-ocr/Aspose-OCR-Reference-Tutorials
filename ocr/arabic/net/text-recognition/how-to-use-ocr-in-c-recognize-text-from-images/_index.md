---
category: general
date: 2026-02-09
description: كيفية استخدام OCR في C# للتعرف على النص من الصورة، استخراج النص، وتحويل
  الصورة إلى نص باستخدام Aspose OCR. دليل كامل خطوة بخطوة.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: ar
og_description: كيفية استخدام OCR في C# للتعرف على النص من الصورة، استخراج النص، وتحويل
  الصورة إلى نص باستخدام Aspose OCR. دليل كامل مع الشيفرة.
og_title: كيفية استخدام OCR في C# – التعرف على النص من الصور
tags:
- C#
- Aspose OCR
- Image Processing
title: كيفية استخدام OCR في C# – التعرف على النص من الصور
url: /ar/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – التعرف على النص من الصور

هل تساءلت يومًا **كيف تستخدم OCR** لتحويل لقطة شاشة إلى نص قابل للتحرير؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى *recognize text from image* لكن لا يتوفر لديهم مثال واضح جاهز للتنفيذ.  

في هذا الدرس سنستعرض العملية بالكامل — تحميل الترخيص، إنشاء المحرك، تغذية تدفق الصورة، وأخيرًا استخراج النص العادي. بنهاية الدرس ستكون قادرًا على **extract text from image**، **convert image to text**، وحتى فهم تفاصيل التعامل مع **load image stream**.

> **ما ستحصل عليه:** برنامج C# كامل قابل للتنفيذ يستخدم Aspose.OCR، شرح لكل خطوة، ونصائح لتجنب الأخطاء الشائعة.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (API يعمل أيضًا مع .NET Framework 4.6+)  
- حزمة NuGet لـ Aspose.OCR للـ .NET (`Aspose.OCR`) مثبتة  
- ملف ترخيص Aspose OCR صالح (`Aspose.OCR.lic`) – النسخة التجريبية مجانية لكنها تضيف علامة مائية.  
- صورة (`sample.jpg`) تحتوي على نص واضح قابل للقراءة آليًا.

> **نصيحة:** إذا كنت تستخدم Visual Studio، فإن أمر وحدة التحكم في NuGet هو  
> `Install-Package Aspose.OCR -Version 23.10` (استبدل بأحدث نسخة).

---

## كيفية استخدام OCR: تحميل الترخيص وتهيئة المحرك

أول شيء يجب عليك فعله هو إبلاغ Aspose أنك تمتلك ترخيصًا. إذا تخطيت هذه الخطوة سيستمر البرنامج في العمل، لكن ستظهر علامة مائية في الناتج وستضيع وقتًا ثمينًا في فحوصات وضع التجربة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**لماذا هذا مهم:** كائن `License` يعطل علامة الماء التجريبية ويفتح مجموعة الميزات الكاملة، والتي تشمل نماذج بدقة أعلى ودعم متعدد اللغات.  

> **نصيحة احترافية:** احفظ ملف الترخيص خارج مستودع التحكم في المصدر. استخدم متغيرات البيئة أو مخزنًا آمنًا لإدخال المسار أثناء وقت التشغيل.

---

## الخطوة 2 – تحميل تدفق الصورة (ولماذا هو أفضل من مسار الملف)

عند *load image stream* بدلاً من تمرير مسار ملف مباشر، تحصل على مرونة: يمكن أن تأتي الصورة من قاعدة بيانات، طلب ويب، أو مصفوفة بايت في الذاكرة.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**شرح:** `ImageStream` يج abstracts المصدر الأساسي، مما يسمح لمحرك OCR بمعالجة كل شيء بشكل موحد. إذا قمت لاحقًا بالتبديل إلى دلو تخزين سحابي، فستحتاج فقط إلى تعديل طريقة إنشاء `ImageStream`؛ باقي الكود يبقى دون تغيير.

---

## الخطوة 3 – التعرف على النص من الصورة

الآن يأتي جوهر الموضوع: **recognize text from image**. طريقة `OcrEngine.Recognize` تشغل نماذج الشبكات العصبية المدمجة مع Aspose وتعيد كائن `OcrResult` يحتوي على عدة خصائص مفيدة.

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**ما يحتويه `OcrResult`؟**  
- `PlainText` – سلسلة واحدة تحتوي على جميع الأحرف المكتشفة.  
- `Words` – مجموعة من كائنات الكلمات مع مربعات الحد (مفيدة للتظليل).  
- `Lines` – تجميع على مستوى السطر، مفيد للحفاظ على فواصل الفقرات.

إذا كنت تحتاج فقط إلى النص الخام، فإن `PlainText` هو أسرع مسار. للسيناريوهات المتقدمة (مثل وضع النتائج فوق الصورة الأصلية)، استكشف `Words` و `Lines`.

---

## الخطوة 4 – عرض أو حفظ النص المستخرج

أخيرًا، دعنا نطبع النص المعترف به إلى وحدة التحكم. في تطبيق حقيقي قد تكتب إلى قاعدة بيانات، ملف، أو ترسله عبر API.

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**الناتج المتوقع:**  
إذا كان `sample.jpg` يحتوي على الجملة *“Hello World!”*، ستظهر لك:

```
=== OCR Output ===
Hello World!
==================
```

عند استخدام ترخيص تجريبي، سيحتوي الناتج على علامة مائية صغيرة “Aspose OCR Demo” في نهاية النص. مع ترخيص كامل، تختفي تمامًا.

---

## مثال كامل جاهز للتنفيذ (انسخ‑الصق)

فيما يلي البرنامج بالكامل، جاهز للترجمة. استبدل المسارات بمواقعك الخاصة وستكون جاهزًا للبدء.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **تذكر:** الكود أعلاه **extracts text from image** و **converts image to text** في استدعاء واحد. لا حلقات إضافية، ولا معالجة يدوية للبكسل — Aspose يتولى العمل الشاق.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو كانت صورتي غير واضحة أو منخفضة التباين؟

Aspose OCR يتضمن خيارات ما قبل المعالجة (مثل `ocrEngine.ImagePreprocessor`). يمكنك تمكين التثنث أو تصحيح الميل قبل التعرف:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### كيف أتعامل مع لغات متعددة؟

قم بتعيين خاصية `Language` على المحرك:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

سوف يحاول المحرك بعد ذلك اكتشاف اللغتين تلقائيًا.

### هل يمكنني معالجة ملفات PDF بدلاً من JPEGs؟

نعم — Aspose OCR يمكنه قراءة ملفات PDF مباشرة، لكن ستحتاج إلى مكتبة Aspose.PDF لاستخراج كل صفحة كصورة أولاً، ثم تغذية تدفق الصورة إلى محرك OCR.

### ماذا عن الدفعات الكبيرة؟

ضع منطق التعرف داخل حلقة وأعد استخدام نفس كائن `OcrEngine`. إنشاء محرك جديد لكل صورة يضيف عبئًا غير ضروري.

---

## نصائح احترافية لـ OCR جاهز للإنتاج

- **Cache the license object**: حمّله مرة واحدة عند بدء التطبيق، لا في كل طلب.  
- **Reuse `OcrEngine`**: المحرك يحتفظ بذاكرات داخلية؛ إعادة الاستخدام يقلل من ضغط الـ GC.  
- **Limit image size**: الصور الكبيرة جدًا (>5 MP) تزيد من وقت المعالجة بشكل كبير. قلل الدقة إلى 150‑300 DPI إذا لم تكن الدقة العالية مطلوبة.  
- **Validate output**: OCR ليس مثاليًا؛ نفّذ فحص ثقة بسيط (`ocrResult.Words.Average(w => w.Confidence)`) وضع علامة على النتائج ذات الثقة المنخفضة للمراجعة اليدوية.  
- **Thread safety**: `OcrEngine` غير آمن للـ threading. أنشئ كائنات منفصلة لكل خيط أو استخدم نمط التجمع.

---

## الخلاصة

لقد غطينا **how to use OCR** في C# من تحميل الترخيص إلى استخراج نص نظيف قابل للبحث. باتباع الخطوات أعلاه يمكنك **recognize text from image**، **extract text from image**، وتحويل الصورة إلى نص بسهولة **convert image to text** مع إتقان نمط **load image stream** الذي يجعل شفرتك مرنة لمصادر البيانات المستقبلية.

هل أنت مستعد للتحدي التالي؟ جرّب إضافة قصّ مناطق الاهتمام، دمج مع Azure Blob storage، أو تغذية مخرجات OCR في خط أنابيب معالجة اللغة الطبيعية. السماء هي الحد، والآن لديك أساس قوي للبناء عليه.

---

![Diagram showing the OCR flow: load license → create engine → load image stream → recognize → output text](image-placeholder.png "how to use OCR to recognize text from image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}