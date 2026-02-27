---
category: general
date: 2026-02-27
description: كيفية تمكين OCR في C# لتحويل PDF إلى نص. تعلم كيفية استخراج النص من ملفات
  PDF متعددة اللغات باستخدام Aspose OCR.
draft: false
keywords:
- how to enable ocr
- convert pdf to text
- how to extract text
- how to recognize pdf
- recognize pdf text c#
language: ar
og_description: كيفية تمكين OCR في C# وتحويل PDF إلى نص. دليل خطوة بخطوة لاستخراج
  النص من PDF والتعرف عليه باستخدام Aspose OCR.
og_title: كيفية تمكين OCR في C# – تحويل PDF إلى نص
tags:
- OCR
- C#
- PDF
- Aspose
title: كيفية تمكين OCR في C# – تحويل PDF إلى نص بسهولة
url: /ar/net/ocr-configuration/how-to-enable-ocr-in-c-convert-pdf-to-text-easily/
---

C#" translate to Arabic: "لقطة شاشة لتكوين محرك OCR تُظهر كيفية تمكين OCR في C#". Keep same path.

Table headers and cells translate.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين OCR في C# – تحويل PDF إلى نص بسهولة

كيفية تمكين OCR في C# هو سؤال يطرحه العديد من المطورين عندما يحتاجون إلى استخراج النص من ملفات PDF. إذا سبق لك وأن نظرت إلى فاتورة ممسوحة ضوئياً وتساءلت *“كيف يمكنني استخراج هذا النص دون إعادة كتابته بالكامل؟”* فأنت في المكان الصحيح. في هذا الدرس سنستعرض حلاً كاملاً جاهزاً للتنفيذ لا يوضح فقط **كيفية تمكين OCR** بل يوضح أيضاً **كيفية تحويل PDF إلى نص**، **كيفية استخراج النص** من مستندات متعددة اللغات، و**كيفية التعرف على محتوى PDF** باستخدام C#.

سنستخدم مكتبة Aspose.OCR، التي تدعم العشرات من اللغات مباشرةً، لذا لن تحتاج إلى التعامل مع محركات منفصلة للإنجليزية أو العربية أو اليابانية أو أي نص آخر. بنهاية هذا الدليل ستحصل على طريقة واحدة **تتعرف على نص PDF باستخدام C#**، تطبع النتيجة على وحدة التحكم، ويمكنك إدراجها في أي مشروع .NET.

## المتطلبات المسبقة – ما تحتاجه قبل البدء

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضاً)
- Visual Studio 2022 (أو أي محرر تفضله)
- ترخيص أو نسخة تجريبية مجانية من **Aspose.OCR for .NET** – يمكنك الحصول على مفتاح مؤقت من موقع Aspose.
- ملف PDF تجريبي يحتوي على عدة لغات (سنسميه `multilang.pdf`).

إذا كان أي من هذه العناصر مفقوداً، احصل على SDK من موقع مايكروسوفت وقم بتثبيت حزمة NuGet:

```bash
dotnet add package Aspose.OCR
```

هذا كل ما يلزم للإعداد. جاهز؟ لنبدأ.

## كيفية تمكين OCR في C# – الإعداد والتكوين

أول شيء عليك فعله هو إنشاء مثال (instance) من محرك OCR وتحديد اللغات التي تتوقعها. هذه هي خطوة **كيفية تمكين OCR** التي تشغل باقي سير العمل.

```csharp
using Aspose.OCR;
using System;

public class OcrDemo
{
    public static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Enable the languages you need (English, Arabic, Japanese)
        ocrEngine.Language = OcrLanguage.English |
                             OcrLanguage.Arabic |
                             OcrLanguage.Japanese;

        // Step 3: Recognize text from the PDF file
        string recognizedText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

        // Step 4: Output the extracted text
        Console.WriteLine(recognizedText);
    }
}
```

**لماذا هذا مهم:** من خلال ضبط خاصية `Language` صراحةً، توجه المحرك لاستخدام نماذج الأحرف المناسبة، مما يحسن الدقة بشكل كبير—خاصةً لملفات PDF ذات النصوص المختلطة. تخطي هذه الخطوة (أو تركها على الإعداد الافتراضي) سيجعل المحرك يخمن، وغالباً ما ينتج عنه مخرجات مشوشة.

> **نصيحة محترف:** إذا كنت تعلم أن مستنداتك تحتوي على لغة واحدة فقط، قصر العلامة (flag) على تلك اللغة. سيُسرّع المعالجة حتى 30 ٪.

### صورة – نظرة بصرية على تمكين OCR  
![لقطة شاشة لتكوين محرك OCR تُظهر كيفية تمكين OCR في C#](/images/enable-ocr-csharp.png)

*نص بديل: مخطط يوضح كيفية تمكين OCR في C# باستخدام Aspose.OCR.*

## تحويل PDF إلى نص باستخدام Aspose OCR

الآن بعد أن تم توضيح **كيفية تمكين OCR**، دعنا نتحدث عن عملية التحويل الفعلية. طريقة `RecognizeFromFile` تقوم بالعمل الشاق: تفتح ملف PDF، تشغل محرك OCR على كل صفحة، وتعيد سلسلة نصية واحدة تحتوي على جميع الأحرف المستخرجة.

### ما الذي يحدث خلف الكواليس؟

1. **تحويل الصفحة إلى صورة نقطية** – يتم تحويل كل صفحة PDF إلى صورة bitmap، لأن OCR يعمل على الصور.
2. **اختيار نموذج اللغة** – بناءً على العلامات التي ضبطتها مسبقاً، يختار المحرك الشبكة العصبية المناسبة.
3. **اكتشاف خطوط النص** – يجد المحرك خطوط النص حتى وإن كانت مائلة.
4. **فك تشفير الأحرف** – أخيراً، يطابق نمط البكسل مع أحرف Unicode.

نظرًا لأن الطريقة تُعيد سلسلة نصية عادية، يمكنك **تحويل PDF إلى نص** بسطر واحد من الكود. إذا احتجت إلى نهج أكثر تفصيلاً (مثلاً معالجة صفحة بصفحة)، يمكنك استدعاء `RecognizeFromStream` داخل حلقة.

## كيفية استخراج النص من ملفات PDF متعددة اللغات

لنفترض أن ملف PDF يحتوي على عناوين إنجليزية، نص عربي في المتن، وملاحظات يابانية في الهوامش. الكود الذي عرضناه سابقاً يتعامل مع هذا السيناريو، لكن قد تتساءل **كيف يمكن استخراج النص** فقط من جزء لغة معينة.

يمكنك تصفية النتيجة باستخدام عمليات سلسلة بسيطة أو تعبيرات نمطية (regex). إليك مثال سريع يقتطع الأجزاء الإنجليزية فقط:

```csharp
using System.Text.RegularExpressions;

// After recognizing the whole document...
string allText = ocrEngine.RecognizeFromFile("YOUR_DIRECTORY/multilang.pdf");

// Regex to keep only ASCII characters (roughly English)
string englishOnly = Regex.Replace(allText, @"[^\u0000-\u007F]+", string.Empty);

Console.WriteLine("English extracted:");
Console.WriteLine(englishOnly);
```

**لماذا التصفية؟** في العديد من سير عمل الأعمال تحتاج فقط إلى الجزء المكتوب بالحروف اللاتينية للفهرسة، بينما يُخزن الباقي في مكان آخر. هذا النمط يوضح **كيفية استخراج النص** بفعالية دون الحاجة إلى تشغيل OCR مرة ثانية.

## كيفية التعرف على PDF – التعامل مع الحالات الخاصة

حتى أفضل محركات OCR قد تواجه صعوبات مع بعض ملفات PDF. إليك بعض المشكلات الشائعة وكيفية معالجتها:

| المشكلة | العرض | الحل |
|--------|-------|------|
| مسح ضوئي منخفض الدقة (<150 dpi) | أحرف مفقودة، كلمات مشوشة | عالج PDF مسبقاً بـ `ocrEngine.ImageProcessingOptions.Dpi = 300;` |
| صفحات مائلة | النص يظهر بشكل جانبي | اضبط `ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;` |
| ملفات PDF محمية بكلمة مرور | `RecognizeFromFile` يرفع استثناء | مرّر كلمة المرور: `ocrEngine.RecognizeFromFile(path, "myPassword");` |
| ملفات ضخمة (>100 صفحة) | تعطل بسبب نفاد الذاكرة | عالجها على دفعات: حمّل 10 صفحات في كل مرة وادمج النتائج. |

تطبيق هذه التعديلات يضمن أن حلّك **يتعرف على محتوى PDF** بثقة، بغض النظر عن العيوب.

```csharp
// Example of handling low‑resolution and rotation
ocrEngine.ImageProcessingOptions.Dpi = 300;
ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;
```

## التعرف على نص PDF باستخدام C# – مثال كامل يعمل

بدمج كل ما سبق، إليك برنامج مستقل يمكنك نسخه ولصقه في تطبيق Console. يوضح **كيفية تمكين OCR**، **تحويل PDF إلى نص**، **استخراج أجزاء لغة محددة**، و**معالجة الحالات الخاصة**.

```csharp
using Aspose.OCR;
using System;
using System.Text.RegularExpressions;

namespace PdfOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable languages (English, Arabic, Japanese)
            ocrEngine.Language = OcrLanguage.English |
                                 OcrLanguage.Arabic |
                                 OcrLanguage.Japanese;

            // Optional: improve accuracy for low‑res PDFs
            ocrEngine.ImageProcessingOptions.Dpi = 300;
            ocrEngine.PageSegmentationMode = PageSegmentationMode.AutoRotate;

            // 3️⃣ Path to your multi‑language PDF
            string pdfPath = @"C:\Docs\multilang.pdf";

            // 4️⃣ Recognize all text
            string fullText = ocrEngine.RecognizeFromFile(pdfPath);
            Console.WriteLine("=== Full extracted text ===");
            Console.WriteLine(fullText);
            Console.WriteLine();

            // 5️⃣ Extract only English (as an example of how to extract text)
            string englishOnly = Regex.Replace(fullText, @"[^\u0000-\u007F]+", string.Empty);
            Console.WriteLine("=== English‑only excerpt ===");
            Console.WriteLine(englishOnly);
        }
    }
}
```

**الناتج المتوقع** (مقتطع للتوفير):

```
=== Full extracted text ===
Welcome to our report…
مرحبا بكم في تقريرنا…
ようこそ、私たちのレポートへ…

=== English‑only excerpt ===
Welcome to our report...
```

شغّل البرنامج، ووجهه إلى ملف PDF الخاص بك، وسترى وحدة التحكم تطبع النص المتعدد اللغات بالكامل والجزء الإنجليزي المصفى.

## أسئلة شائعة (وإجابات سريعة)

- **هل يعمل هذا مع .NET Framework 4.7؟**  
  نعم. حزمة Aspose.OCR NuGet تستهدف .NET Standard 2.0، المتوافقة مع كل من .NET Core و .NET Framework.

- **ماذا لو أردت تشغيل OCR على صور بدلاً من PDF؟**  
  استخدم `ocrEngine.RecognizeFromImage("image.png")`. نفس علامات اللغة تُطبق، لذا لا يزال عليك **كيفية تمكين OCR** مرة واحدة.

- **هل يمكنني كتابة المخرجات إلى ملف .txt؟**  
  بالتأكيد. استبدل `Console.WriteLine(fullText);` بـ `File.WriteAllText("output.txt", fullText);`.

- **هل هناك طريقة للحصول على درجات الثقة؟**  
  Aspose.OCR يُظهر كائنات `OcrResult` حيث يمكنك قراءة `Confidence` لكل كلمة. راجع وثائق API لـ `RecognizeFromFile(..., out OcrResult result)`.

## الخلاصة

غطّينا **كيفية تمكين OCR** في C#، وأظهرنا لك **كيفية تحويل PDF إلى نص**، وشرحنا **كيفية استخراج النص** من أقسام لغوية محددة، وأثبتنا **كيفية التعرف على PDF** بشكل موثوق باستخدام Aspose OCR. الكود القابل للتنفيذ أعلاه يمنحك أساساً صلباً لدمج OCR في أي تطبيق .NET—سواءً كنت تبني نظام إدارة مستندات، أو معالج فواتير آلي، أو فهرس بحث متعدد اللغات.

الخطوات التالية؟ جرّب تغيير علامات اللغة لتشمل الصينية أو الكورية، جرب `ImageProcessingOptions` للماسحات الضوضائية، أو مرّر النص المستخرج إلى خط أنابيب معالجة لغة طبيعية. كل هذه الإضافات لا تزال تعتمد على المبدأ الأساسي نفسه: **كيفية تمكين OCR** بشكل صحيح في البداية.

برمجة سعيدة، ولتكن ملفات PDF الخاصة بك قابلة للبحث دائماً!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}