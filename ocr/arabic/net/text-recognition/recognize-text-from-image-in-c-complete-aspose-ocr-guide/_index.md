---
category: general
date: 2026-03-07
description: التعرف على النص من الصورة بسرعة باستخدام Aspose OCR. تعلّم كيفية تحويل
  DjVu إلى نص، استخراج النص من الصورة، وتحميل الصورة للتعرف الضوئي على الأحرف في دليل
  خطوة‑بخطوة بلغة C#.
draft: false
keywords:
- recognize text from image
- convert djvu to text
- how to extract text from image
- extract text from djvu
- load image for OCR
language: ar
og_description: التعرف على النص من الصورة في C# باستخدام Aspose OCR. يوضح هذا الدليل
  كيفية تحويل djvu إلى نص، استخراج النص من الصورة، وتحميل الصورة للتعرف الضوئي على
  الأحرف مع نصائح عملية.
og_title: التعرف على النص من الصورة – دليل Aspose OCR الكامل بلغة C#
tags:
- C#
- Aspose OCR
- Document Processing
title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
url: /ar/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل كامل C# Aspose OCR

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج موثوقة؟ لست وحدك. سواء كنت تتعامل مع فواتير ممسوحة ضوئيًا، ملفات DJVU تاريخية، أو مجرد لقطة شاشة PNG، قد يشعر استخراج الأحرف الدقيقة وكأنه فك شفرة نص قديم.

الأمر ببساطة—Aspose OCR يجعل العملية كلها سهلة. في هذا الدليل سنستعرض كيفية **تحويل djvu إلى نص**، **استخراج النص من الصورة**، و**تحميل الصورة للتعرف الضوئي على الأحرف (OCR)** باستخدام برنامج C# مختصر. في النهاية ستحصل على تطبيق كونسول يعمل ويطبع السلسلة التي تم التعرف عليها في الكونسول، وستفهم “السبب” وراء كل سطر.

## ما ستتعلمه

- كيفية إعداد محرك Aspose OCR في مشروع .NET.  
- الكود الدقيق اللازم **لتحميل الصورة للتعرف الضوئي على الأحرف** من ملف DJVU.  
- لماذا يجب استدعاء `Recognize()` قبل قراءة `Text`.  
- الأخطاء الشائعة (DJVU متعدد الصفحات، صيغ غير مدعومة) وكيفية تجنبها.  
- طرق سريعة **لتحويل djvu إلى نص** للمعالجة الدفعة.

كل ما تحتاجه هو .NET SDK حديث (≥ 6.0) ورخصة Aspose OCR (الإصدار التجريبي المجاني يكفي للاختبار). لا خدمات خارجية، لا استدعاءات REST—فقط C# نقي.

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6 SDK أو أحدث | ميزات لغة حديثة وأداء أفضل. |
| حزمة Aspose.OCR من NuGet (`Install-Package Aspose.OCR`) | توفر الفئة `OcrEngine` التي سنستخدمها. |
| ملف DJVU (مثال: `sample.djvu`) | يوضح **تحويل djvu إلى نص**. |
| إلمام أساسي بتطبيقات كونسول C# | يجعل الخطوات تتدفق بصورة طبيعية. |

إذا كان أي من هذه غير موجود، توقف وقم بتثبيته الآن؛ وإلا لن يتم تجميع الكود.

## الخطوة 1 – تثبيت Aspose.OCR وإنشاء المشروع

أولاً، أنشئ مشروع كونسول جديد وأضف مكتبة OCR.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

*نصيحة محترف:* استخدم العلامة `--framework net6.0` إذا أردت تثبيت إطار العمل الهدف بشكل صريح.

## الخطوة 2 – تهيئة محرك OCR وتحميل صورة DJVU

المحرك يحتاج إلى مصدر صورة. Aspose.OCR يمكنه قراءة صيغ متعددة، بما فيها DJVU، لذا نوجهه ببساطة إلى مسار الملف.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

// Step 2: Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the DJVU file – the first page is used by default
// This demonstrates “load image for OCR” and also “convert djvu to text”
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.djvu");
```

**لماذا هذا مهم:**  
- `OcrEngine` هو نقطة الدخول؛ إنشاؤه مرة واحدة وإعادة استخدامه يقلل من استهلاك الذاكرة.  
- `ImageStream.FromFile` يخفف عنك تفاصيل الصيغة، بحيث يمكنك لاحقًا استبدال ملف DJVU بـ PNG أو TIFF دون تعديل أي كود آخر—مثالي لـ “كيفية استخراج النص من الصورة” في سيناريوهات مختلفة.

## الخطوة 3 – تشغيل عملية التعرف

استدعاء `Recognize()` يشغل العملية الثقيلة. تحت الغطاء، Aspose يستخدم مصنفًا قائمًا على الشبكات العصبية يعمل على النص المطبوع والمكتوب يدويًا.

```csharp
// Step 3: Perform OCR on the loaded image
ocrEngine.Recognize();
```

*ملاحظة حالة حافة:* إذا كان ملف DJVU يحتوي على صفحات متعددة، فإن `ImageStream.FromFile` لا يزال يحمل الصفحة الأولى فقط. لمعالجة جميع الصفحات تحتاج إلى حلقة حول `ImageStream.FromFile(...).Pages`. بالنسبة لمعظم المهام السريعة، تكون الصفحة الأولى كافية.

## الخطوة 4 – استرجاع وعرض النص المعترف به

بعد عملية التعرف، يملأ المحرك الخاصية `Text` بسلسلة نصية عادية. يمكنك الآن طباعتها على الكونسول، أو حفظها في ملف، أو تمريرها إلى نظام آخر.

```csharp
// Step 4: Get the OCR result
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

الناتج النموذجي يكون كالتالي:

```
=== Recognized Text ===
This is a sample DJVU page.
It contains several lines of text,
including numbers like 12345.
```

إذا كان الناتج مشوشًا، تحقق من أن صورة المصدر ليست منخفضة الدقة؛ توصيّة Aspose هي 300 dpi أو أعلى للحصول على أفضل دقة.

## مثال كامل يعمل

بدمج كل ما سبق، إليك ملف واحد (`Program.cs`) يمكنك لصقه في المشروع الذي أنشأته مسبقًا.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load the DJVU file (first page only)
            // Replace the path with your actual file location
            ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.djvu");

            // 3️⃣ Run the recognition
            ocrEngine.Recognize();

            // 4️⃣ Retrieve and print the text
            string recognizedText = ocrEngine.Text;

            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

شغّله باستخدام:

```bash
dotnet run
```

يجب أن ترى السلسلة المستخرجة مطبوعة في الطرفية. هذه أبسط طريقة **للتعرف على النص من الصورة** باستخدام Aspose OCR.

## الخطوة 5 – متقدم: تحويل صفحات DJVU متعددة إلى ملفات نصية

إذا كنت بحاجة إلى **تحويل djvu إلى نص** بشكل جماعي، وسّع الكود السابق بحلقة:

```csharp
var djvuPath = @"YOUR_DIRECTORY/multi_page.djvu";
var stream = ImageStream.FromFile(djvuPath);

for (int i = 0; i < stream.PageCount; i++)
{
    ocrEngine.Image = stream.GetPage(i);
    ocrEngine.Recognize();

    var pageText = ocrEngine.Text;
    System.IO.File.WriteAllText(
        $"page_{i + 1}.txt",
        pageText);
}
```

*لماذا يعمل هذا:* `GetPage(i)` تُعيد كائن `Image` للصفحة المطلوبة، مما يتيح لك إعادة استخدام نفس نسخة `OcrEngine`. نص كل صفحة يُحفظ في ملف `.txt` خاص به، مما يمنحك خط أنابيب **تحويل djvu إلى نص** نظيف.

## أسئلة شائعة ومشكلات محتملة

- **هل يمكنني استخراج النص من JPEG بدلًا من DJVU؟**  
  بالتأكيد. فقط غيّر امتداد الملف في `FromFile`. نفس الكود **كيفية استخراج النص من الصورة** ينطبق لأن Aspose يخفف عنك الصيغة.

- **ماذا أفعل إذا احتوى ناتج OCR على فواصل أسطر زائدة؟**  
  استخدم `String.Replace("\r\n", " ")` أو تعبيرًا نمطيًا لتطبيع الفراغات.

- **هل أحتاج رخصة للاستخدام في الإنتاج؟**  
  النسخة التجريبية مجانية حتى 100 صفحة. للاستخدام غير المحدود، اشترِ رخصة واستدعِ `License license = new License(); license.SetLicense("Aspose.OCR.lic");` قبل إنشاء المحرك.

- **هل المحرك آمن للاستخدام متعدد الخيوط؟**  
  لا. أنشئ نسخة منفصلة من `OcrEngine` لكل خيط أو احمِ الوصول بقفل.

## نصائح لتحسين الدقة

1. **زيادة DPI** – إذا كنت تتحكم في تحويل المصدر، احرص على إخراج الصور بدقة 300 dpi أو أعلى.  
2. **معالجة مسبقة للصورة** – البينارايزيشن البسيط (`ocrEngine.Image = ImageProcessing.Binarize(ocrEngine.Image)`) يمكن أن يحسّن النتائج على المسحات الضوضائية.  
3. **تحديد اللغة** – `ocrEngine.Language = Language.English;` يحد من مجموعة الأحرف ويسرّع عملية التعرف.

## الخلاصة

أصبح لديك الآن مثال كامل وجاهز للتنفيذ **للتعرف على النص من الصورة** باستخدام Aspose OCR، وقد رأيت كيف **تحويل djvu إلى نص**، **كيفية استخراج النص من الصورة**، والطريقة الصحيحة **لتحميل الصورة للتعرف الضوئي على الأحرف**. الكود مستقل، يعمل على أي بيئة تشغيل .NET 6+، ويمكن توسيعه لمعالجة دفعات من مستندات DJVU متعددة الصفحات.

الخطوات التالية قد تشمل:

- إضافة **اكتشاف اللغة** لملفات DJVU متعددة اللغات.  
- دمج ناتج OCR مع فهرس بحث (مثال: Elasticsearch).  
- استخدام تحويل Aspose إلى PDF لتحويل النص المستخرج إلى ملفات PDF قابلة للبحث.

جرّبه، عدّل الـ DPI، جرب صيغ صور مختلفة، ودع محرك OCR يقوم بالعمل الشاق نيابةً عنك. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}