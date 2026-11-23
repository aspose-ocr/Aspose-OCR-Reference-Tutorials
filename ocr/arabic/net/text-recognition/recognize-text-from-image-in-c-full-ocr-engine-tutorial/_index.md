---
category: general
date: 2026-06-06
description: التعرف على النص من الصورة باستخدام محرك OCR بلغة C#. تعلم كيفية تحويل
  الصورة إلى JSON، وتحويل الصورة إلى XML، وتحميل الصورة للتعرف الضوئي على الأحرف في
  دقائق.
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: ar
og_description: التعرف على النص من الصورة باستخدام محرك OCR بلغة C#. تصدير النتائج
  إلى JSON وXML، وإتقان تحميل الصور للتعرف الضوئي على الأحرف.
og_title: التعرف على النص من الصورة في C# – دليل كامل لمحرك OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: التعرف على النص من الصورة في C# – دليل كامل لمحرك OCR
url: /ar/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة في C# – دليل كامل لمحرك OCR

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكن لم تكن متأكدًا أي مكتبة C# تختار؟ لست وحدك—المطورون يواجهون باستمرار تحويل الإيصالات الممسوحة، لقطات الشاشة، أو الملاحظات المكتوبة يدويًا إلى نص قابل للبحث. الخبر السار؟ باستخدام **محرك OCR حديث لـ C#** يمكنك القيام بذلك ببضع أسطر فقط، ثم **تحويل الصورة إلى JSON** أو **تحويل الصورة إلى XML** للمعالجة اللاحقة.

في هذا الدليل سنستعرض كل خطوة: تثبيت حزمة OCR، تحميل صورة للـ OCR، استخراج النص، وأخيرًا تصدير النتائج إلى كل من JSON و XML. بنهاية الدليل ستحصل على تطبيق كونسول مكتمل يمكنك إدراجه في أي مشروع .NET. لا مراجع غامضة، مجرد حل كامل قابل للتنفيذ.

## ما ستحصل عليه بعد القراءة

- صورة واضحة لكيفية **تحميل صورة للـ OCR** باستخدام محرك OCR شائع في C#.  
- كود يعمل **يتعرف على النص من الصورة** ويعيد كائن نتيجة غني.  
- مقتطفات بسيطة **تحول الصورة إلى JSON** و **تحول الصورة إلى XML** دون مكتبات إضافية.  
- نصائح للتعامل مع ملفات PDF متعددة الصفحات، صيغ الصور المختلفة، ومشكلات شائعة مثل المسحات منخفضة التباين.

### المتطلبات المسبقة

- .NET 6 SDK أو أحدث (يمكنك أيضًا استهداف .NET Framework 4.8 إذا رغبت).  
- معرفة أساسية بـ C#—لا شيء معقد، فقط فهم للصفوف و `async`/`await`.  
- ملف صورة (`structured.png` في الأمثلة) تريد تطبيق OCR عليه.  

إذا كان لديك كل ذلك، لنبدأ.

---

## التعرف على النص من الصورة – إعداد محرك OCR

أولاً وقبل كل شيء. نحتاج إلى مكتبة OCR موثوقة. في هذا الدرس سنستخدم **IronOcr**، محرك تجاري المستوى يأتي بإصدار مجتمع مجاني على NuGet. يدعم اللغة الإنجليزية مباشرةً ويزودنا بفئة `OcrEngine` كما هو موضح في المقتطف الأصلي.

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **نصيحة احترافية:** إذا كان ميزانيتك ضيقًا، استبدل `IronOcr` بـ `Tesseract`—واجهة البرمجة تختلف قليلًا لكن المفاهيم تبقى هي نفسها.

الآن أنشئ مشروع كونسول جديد وأضف بيانات `using` المطلوبة:

```csharp
using IronOcr;
using System.IO;
```

### تكوين المحرك خطوة بخطوة

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*لماذا هذا مهم:* تهيئة المحرك مرة واحدة وإعادة استخدامه عبر صور متعددة يقلل من الحمل الزائد. كما أن تحديد اللغة صراحةً يتجنب روتين الكشف التلقائي للمحرك، والذي قد يكون أبطأ وأقل دقة.

---

## تحميل صورة للـ OCR – تزويد المحرك بالبيانات الصحيحة

المحرك يتوقع كائن `OcrInput`. يمكنك توجيهه إلى مسار ملف، تدفق، أو حتى `Bitmap`. إليك أبسط طريقة:

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **حالة حافة:** إذا كان المصدر ملف PDF متعدد الصفحات، استدعِ `input.AddPdf("file.pdf")` بدلاً من PNG. سيعامل محرك OCR كل صفحة كصورة منفصلة تلقائيًا.

---

## التعرف على النص من الصورة – تشغيل عملية OCR

مع المحرك والمدخل جاهزين، عملية التعرف هي سطر واحد:

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` هو كائن `OcrResult` يحتوي على:

- `Text` – السلسلة المستخرجة الخام.  
- `Lines` – مجموعة كائنات `OcrLine` مع درجات الثقة.  
- `Words` – مجموعة الكلمات الفردية، أيضًا مع درجة الثقة.  

يمكنك فحصه مباشرةً في المصحح، لكن غالبًا ما ستحتاج إلى تسلسل البيانات.

---

## تحويل الصورة إلى JSON – تصدير نتائج OCR

IronOcr يأتي مع تسلسل JSON مدمج عبر `System.Text.Json`. المقتطف التالي يكتب ملف JSON منسق بجوار صورة المصدر:

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**ما ستراه:** مستند JSON منسق يحتوي على النص الخام، درجات الثقة، ومربعات الإحاطة لكل سطر وكلمة. هذا الهيكل مثالي لتغذيته إلى خدمات لاحقة مثل ElasticSearch أو Azure Cognitive Search.

---

## تحويل الصورة إلى XML – إخراج بيانات منظم

بعض الأنظمة القديمة لا تزال تتوقع XML. طريقة `ToXml()` في IronOcr توفر لك تحويلًا سريعًا:

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

الـ XML يعكس هيكلية JSON، مع عناصر `<Line>` و `<Word>` التي تحمل سمة `Confidence`. إذا احتجت مخططًا مخصصًا، يمكنك تحويل `result` يدويًا إلى `XDocument`—الواجهة متوافقة تمامًا مع LINQ.

---

## مثال كامل من البداية إلى النهاية

بدمج كل ما سبق، إليك ملف `Program.cs` جاهز للتنفيذ:

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**الناتج المتوقع** (مقتطع للوضوح):

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

شغّل البرنامج باستخدام `dotnet run`. إذا تم توصيل كل شيء بشكل صحيح، سترى مخرجات الكونسول وتظهر ملفان في `YOUR_DIRECTORY`.

---

## أسئلة شائعة ومشكلات محتملة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كانت الصورة JPEG مع دوران EXIF؟* | استخدم `input.AutoRotate()` قبل `Deskew()`. سيقرأ IronOcr وسم EXIF ويصحح الاتجاه. |
| *هل يمكنني تطبيق OCR على مجلد من الصور دفعة واحدة؟* | بالطبع. غلف المنطق السابق داخل حلقة `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |
| *كيف أحسن الدقة في المسحات الضوضائية؟* | زد من `input.Denoise()` وفكر في `input.BlackWhiteThreshold(120)`. أيضًا، قدم حزمة لغة تتطابق مع لغة المستند. |
| *هل تنسيق JSON متوافق مع مكتبات OCR أخرى؟* | المخطط عام بما فيه الكفاية—`Text`، `Lines`، `Words`—لذا يمكنك تحويله إلى مخرجات Tesseract بأقل تعديل. |

---

## نصائح الأداء (مستوى محترف)

- **إعادة استخدام المحرك**: إنشاء `IronTesseract` داخل حلقة ضيقة قد يقلل الإنتاجية حتى 30 %. احتفظ بـ singleton لكل نطاق تطبيق.  
- **توازي I/O**: إذا كنت تعالج عشرات الصور، اقرأها إلى الذاكرة بشكل متزامن (`Task.WhenAll`) ومرّر كل `OcrInput` إلى نفس المحرك—IronOcr آمن للخطوط المتعددة.  
- **تصدير دفعي**: بدلاً من كتابة كل ملف JSON/XML على حدة، اجمع النتائج في مجموعة واحدة وسلسل مرة واحدة. هذا يقلل من عمليات القراءة/الكتابة على القرص.

---

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أصبحت قادرًا على **التعرف على النص من الصورة**، فكر في توسيع خط الأنابيب:

- **تكامل البحث** – ادفع الـ JSON إلى Elasticsearch للبحث النصي الكامل.  
- **تصنيف المستندات** – مرّر مخرجات OCR إلى نموذج تعلم آلي خفيف لتصنيف الفواتير، العقود، أو الإيصالات تلقائيًا.  
- **النص المكتوب يدويًا** – غيّر حزمة اللغة إلى `OcrLanguage.EnglishHandwritten` (متوفرة في الطبقة المتميزة من IronOcr).  

كل من هذه النقاط يبني على الأساس الذي أنشأته للتو، وستبقيك مشغولًا لأسابيع.

---

## الخلاصة

لقد استعرضنا كيفية **التعرف على النص من الصورة** باستخدام **محرك OCR حديث لـ C#**، ثم **تحويل الصورة إلى JSON** و **تحويل الصورة إلى XML**، وأخيرًا كيفية **تحميل صورة للـ OCR** بطريقة قوية. المثال الكامل يعمل في أقل من دقيقة، والملفات المصدرة جاهزة لأي نظام لاحق.

جرّب الكود، عدّل الإعدادات، واستمتع بالنتائج.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}