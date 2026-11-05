---
category: general
date: 2026-03-18
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية استخراج
  النص، تشغيل التعرف الضوئي على الأحرف، والتعرف على النص السيريلي دون الحاجة إلى الإنترنت.
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR. دليل خطوة بخطوة لتشغيل
  التعرف الضوئي على الأحرف، كيفية استخراج النص، والتعرف على النص السيريلي دون اتصال.
og_title: استخراج النص من الصورة في C# – دليل OCR دون اتصال
tags:
- C#
- OCR
- Aspose
- Image Processing
title: استخراج النص من الصورة في C# – دليل OCR كامل دون اتصال
url: /ar/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – دليل OCR كامل دون اتصال

هل احتجت يومًا إلى **استخراج النص من الصورة** لكنك كنت قلقًا من تأخر الشبكة أو قيود الترخيص؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يجب أن يعمل تطبيقهم في بيئة معزولة، ومع ذلك يحتاج إلى OCR موثوق. الخبر السار؟ مع Aspose OCR يمكنك تشغيل كامل سير العمل محليًا، **استخراج النص من الصورة** دون الحاجة إلى الإنترنت مطلقًا.

في هذا البرنامج التعليمي سنستعرض مثالًا عمليًا يوضح **كيفية استخراج النص**، إعداد محرك غير متصل، **تشغيل التعرف على OCR**، وحتى **التعرف على النص السيريلي**. في النهاية ستحصل على تطبيق C# Console جاهز للتنفيذ يطبع السلسلة المكتشفة مباشرةً في وحدة التحكم.

## ما الذي ستحتاجه

- .NET 6.0 SDK (أو أي نسخة حديثة من .NET)  
- Visual Studio 2022 أو VS Code – حسب ما تفضله  
- حزمة NuGet Aspose.OCR for .NET  
- مجلد يحتوي على ملفات نموذج Aspose OCR (قم بتنزيلها مرة واحدة من بوابة Aspose)  
- ملف صورة يتضمن أحرف إنجليزية وسيريليّة (مثال: `cyrillic_doc.jpg`)

لا خدمات خارجية، لا تنزيلات مخفية أثناء التشغيل – كل شيء موجود على قرصك.

## الخطوة 1: تثبيت Aspose.OCR وتحضير الموارد

أولاً، أضف حزمة NuGet Aspose.OCR إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

بعد ذلك، أنشئ مجلدًا باسم `AsposeOCRResources` في أي مكان على جهازك وانسخ ملفات النموذج التي حمّلتها من Aspose إليه. سيبحث محرك OCR عن حزم اللغات في هذا الدليل، لذا تأكد من صحة المسار.

> **نصيحة احترافية:** احتفظ بمجلد الموارد بجوار ملف `.csproj` الخاص بك؛ فهذا يبسط التعامل مع المسارات أثناء التطوير.

## الخطوة 2: بناء محرك OCR غير المتصل

الآن سنقوم بإنشاء كائن المحرك وتوجيهه إلى مجلد الموارد. هذه هي الخطوة الحاسمة التي تسمح لنا **بتشغيل التعرف على OCR** بالكامل دون اتصال.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

لماذا نحمل اللغات صراحةً؟ لأننا أخبرنا المحرك بالبقاء غير متصل؛ لن يتصل بخوادم Aspose لجلب الحزم المفقودة. إذا نسيت تحميل لغة ما، سيتجاهل أي أحرف من تلك الكتابة.

## الخطوة 3: تمرير الصورة إلى المحرك

مع جاهزية المحرك، نُعطيه الآن الصورة التي نريد معالجتها. تساعد الدالة `ImageStream.FromFile` في قراءة الملف إلى صيغة يفهمها محرك OCR.

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

إذا كانت صورتك كبيرة، فكر في تصغير حجمها مسبقًا لتحسين السرعة والدقة. يعمل محرك OCR بأفضل شكل مع DPI يقارب 300.

## الخطوة 4: تنفيذ عملية التعرف

استدعاء `Recognize` يقوم بالعمل الشاق. تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة المستخرجة، درجات الثقة، والمزيد.

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

خلف الكواليس، يقوم Aspose بتحليل البت ماب، تشغيل الشبكات العصبية الخاصة بكل لغة، وربط الأحرف معًا. لأننا حمّلنا كلًا من الإنجليزية والسيريليّة، يتم التعامل مع المستندات المختلطة بسلاسة.

## الخطوة 5: عرض النص المستخرج

أخيرًا، نطبع النتيجة. في تطبيق حقيقي قد تخزنها في قاعدة بيانات أو تُرسلها إلى خدمة أخرى، لكن لهذا العرض سنكتفي بطباعتها.

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

تشغيل البرنامج يجب أن يعطيك شيئًا مثل:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى من أن حزمة اللغة السيريليّة موجودة في مجلد الموارد بشكل صحيح وأن الصورة ليست غير واضحة.

![extract text from image example](extract_text_image.png "extract text from image")

*نص بديل للصورة: استخراج النص من الصورة – نتيجة OCR تُظهر سطورًا إنجليزية وسيريليّة.*

## معالجة المشكلات الشائعة

### حزم اللغات المفقودة

إذا حصلت على استثناء يقول “Language data not found”، فهذا يعني أن المحرك لم يتمكن من العثور على ملفات النموذج. تحقق من `ResourcesPath` وتأكد أن المجلد يحتوي على `english.dat` و `cyrillic.dat` (أو ملفات ذات أسماء مشابهة).

### درجات ثقة منخفضة

أحيانًا يُعيد محرك OCR درجات ثقة منخفضة لبعض الأحرف، خاصةً إذا كان هناك ضوضاء في الصورة. يمكنك تحسين الدقة عبر:

- تحويل الصورة إلى تدرج رمادي قبل تمريرها إلى المحرك  
- تطبيق مرشح متوسط لتقليل البقع  
- التأكد من أن النص أفقيًا (قم بتدويره إذا لزم الأمر)

### الصور الكبيرة

معالجة صورة بدقة 10 MP قد تكون بطيئة. قلل الحجم إلى عرض أقصى 2000 px مع الحفاظ على نسبة الأبعاد؛ سيظل المحرك يلتقط معظم الأحرف بدقة.

## توسيع المثال

- **معالجة دفعات:** ضع منطق التعرف داخل حلقة تتكرر على جميع الملفات في دليل ما.  
- **تنسيقات الإخراج:** يوفر `OcrResult` أيضًا مجموعة `TextLines` التي تشمل المربعات المحيطة—مفيدة لتسليط الضوء على النص في تطبيقات الواجهة.  
- **لغات إضافية:** ما عليك سوى استدعاء `LoadLanguage` مع أي قيمة enum مدعومة أخرى (مثال: `Language.French`).  

كل هذه الإضافات لا تزال تتبع مبدأ **كيفية استخراج النص**—فقط حمّل حزم اللغات المناسبة ودع المحرك يتولى البقية.

## ملخص الكود الكامل

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

احفظه كملف `Program.cs`، نفّذ الأمر `dotnet run`، وسترى وحدة التحكم تطبع النص الذي استخرجه المحرك من صورتك. هذا كل شيء—لقد نجحت في **استخراج النص من الصورة** دون اتصال.

## الخلاصة

غطّينا كل ما تحتاجه لـ **استخراج النص من الصورة** باستخدام Aspose OCR في سيناريو كامل غير متصل. أظهر الدليل **كيفية استخراج النص**، وبيّن **تشغيل التعرف على OCR**، وأثبت أنه يمكنك **التعرف على النص السيريلي** جنبًا إلى جنب مع الإنجليزية دون أي استدعاءات شبكة.

من إعداد حزمة NuGet إلى معالجة الحالات الطرفية مثل حزم اللغات المفقودة، لديك الآن أساس قوي لبناء ميزات مدعومة بـ OCR في أي تطبيق .NET.

ما الخطوة التالية؟ جرّب معالجة ملفات PDF، مسح صفحات متعددة، أو دمج الناتج مع فهرس بحث. السماء هي الحد عندما تتقن OCR غير المتصل.

برمجة سعيدة، ولتكون صورك دائمًا واضحة كالبلور!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}