---
category: general
date: 2026-04-11
description: تعلم كيفية التعرف على النص من ملفات PNG واستخراج النص من الصورة باستخدام
  C# و Aspose OCR. يتضمن خطوات تحميل ملف الصورة في C#، التدقيق الإملائي والكود الكامل.
draft: false
keywords:
- recognize text from png
- extract text from image c#
- load image file c#
language: ar
og_description: تعرّف على النص من ملف PNG بسهولة باستخدام C#. اتبع هذا الدليل خطوة
  بخطوة لتحميل ملف الصورة باستخدام C#، استخراج النص من الصورة باستخدام C#، وإجراء
  التدقيق الإملائي.
og_title: التعرف على النص من ملف PNG في C# – دليل OCR كامل
tags:
- OCR
- C#
- Aspose
title: التعرف على النص من PNG في C# – دليل شامل للتعرف الضوئي على الأحرف وتدقيق الإملاء
url: /ar/net/text-recognition/recognize-text-from-png-in-c-full-ocr-spell-check-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG – دليل كامل لـ C# OCR وتدقيق الإملاء

هل احتجت يومًا إلى **التعرف على النص من PNG** لكنك لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك؛ العديد من المطورين يواجهون هذه المشكلة عندما يبدأون باستخراج البيانات من الصور. الخبر السار؟ مع Aspose OCR يمكنك تحميل ملف صورة في C#، استخراج النص، وحتى تشغيل مدقق إملائي مدمج — كل ذلك في بضع أسطر.

في هذا الدليل سنستعرض العملية بالكامل: تحميل ملف PNG، استدعاء محرك OCR، وأخيرًا فحص الكلمات غير الصحيحة إملائيًا. بنهاية القراءة ستكون قادرًا على **استخراج النص من صورة C#** في مشاريعك دون الحاجة للبحث في وثائق متفرقة. لا تحتاج إلى خبرة سابقة في OCR، فقط بيئة تطوير .NET.

## ما ستحتاجه

- **.NET 6.0** (أو أي نسخة حديثة من .NET) – الواجهة البرمجية تعمل بنفس الطريقة عبر .NET Core و .NET Framework.
- **Aspose.OCR for .NET** حزمة NuGet – قم بتثبيتها عبر الأمر `dotnet add package Aspose.OCR`.
- صورة **PNG** تحتوي على نص قابل للقراءة (مثال: `letter.png` موجودة في مجلد تتحكم فيه).
- محرر شفرة أو بيئة تطوير متكاملة (IDE) (Visual Studio, VS Code, Rider—اختر ما تفضله).

هذا كل شيء. لا محركات OCR إضافية، لا ملفات DLL أصلية، فقط حزمة مُدارة نظيفة.

---

## الخطوة 1: تحميل ملف صورة PNG في C#

قبل أن يتمكن محرك OCR من أي شيء، يحتاج إلى تدفق (stream) يشير إلى الصورة. توفر Aspose الدالة `ImageStream.FromFile` التي تُجرد تفاصيل نظام الملفات.

```csharp
using System;
using System.Linq;
using Aspose.OCR;

class SpellCheckDemo
{
    static void Main()
    {
        // ✅ Load the PNG image from disk
        var imagePath = @"C:\Images\letter.png";          // <-- adjust to your folder
        var image = ImageStream.FromFile(imagePath);
```

> **نصيحة احترافية:** إذا كانت صورتك مضمنة كموارد أو جاءت من طلب ويب، يمكنك استخدام `ImageStream.FromBytes(byte[])` بدلاً من ذلك — دون الحاجة للتعامل مع نظام الملفات.

### لماذا التحميل مهم

تحميل الصورة بشكل صحيح يضمن أن محرك OCR يتلقى بيانات البكسل الدقيقة التي يتوقعها. إذا كان التدفق تالفًا سيتسبب ذلك في حدوث استثناء في `Recognize`، وستضيع وقتًا في تصحيح الأخطاء لاحقًا.

---

## الخطوة 2: تهيئة محرك OCR

إنشاء كائن `OcrEngine` أمر بسيط، لكن قد ترغب في تعديل إعدادات اللغة أو الدقة لحالات استخدام محددة (مثل المستندات متعددة اللغات). المُنشئ الافتراضي يعمل جيدًا للنص الإنجليزي.

```csharp
        // ✅ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // Optional: set language to English explicitly
        // ocrEngine.Language = Language.English;
```

### لماذا كائن محرك؟

المحرك يحتفظ بالإعدادات (اللغة، فلاتر ما قبل المعالجة، إلخ). من خلال فصل الإعدادات عن الصورة، يمكنك إعادة استخدام نفس المحرك لعدة ملفات — مفيد للمعالجة الدفعة.

---

## الخطوة 3: التعرف على النص من PNG

الآن يحدث السحر. تُعيد الدالة `Recognize` كائن `OcrResult` يحتوي على السلسلة الخام، درجات الثقة، وأكثر.

```csharp
        // ✅ Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Grab the plain text
        string recognizedText = ocrResult.Text;
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);
```

**الناتج المتوقع** (بافتراض أن `letter.png` يحتوي على “Hello World!”):

```
=== OCR Output ===
Hello World!
```

إذا احتوت الصورة على عدة أسطر، فإن النتيجة تحتفظ بفواصل الأسطر، مما يجعل المعالجة اللاحقة سهلة.

### حالة خاصة: PNG منخفض الدقة

إذا كان ناتج OCR مشوشًا، فكر في تكبير الصورة أو تعديل `ocrEngine.PreprocessingOptions`. غالبًا ما تفقد الصور ذات الدقة المنخفضة (DPI) التفاصيل التي يعتمد عليها المحرك.

---

## الخطوة 4: تشغيل مدقق الإملاء المدمج

يأتي Aspose OCR مع وحدة تدقيق إملائي خفيفة تعمل مباشرة على نتيجة OCR. تساعدك هذه الخطوة على التقاط الأخطاء مثل “H3llo” بدلاً من “Hello”.

```csharp
        // ✅ Spell‑check the OCR result
        var misspellings = ocrResult.SpellCheck();

        if (misspellings.Any())
        {
            Console.WriteLine("\nPossible misspellings:");
            foreach (var entry in misspellings)
            {
                Console.WriteLine($"{entry.Word} → {string.Join(", ", entry.Suggestions)}");
            }
        }
        else
        {
            Console.WriteLine("\nNo spelling issues detected.");
        }
    }
}
```

**نموذج الناتج** (إذا قرأ OCR كلمة “World” بشكل خاطئ كـ “W0rld”):

```
Possible misspellings:
W0rld → World, Word, Would
```

### لماذا تدقيق الإملاء؟

OCR لا يكون مثاليًا بنسبة 100 %، خاصةً مع الخلفيات المزعجة. يمكن لتدقيق إملائي سريع أن يزيل الأخطاء الواضحة قبل إدخال النص إلى التحليلات أو قواعد البيانات اللاحقة.

---

## الخطوة 5: جمع كل شيء معًا – مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى مشروع وحدة تحكم جديد، عدل مسار الصورة، واضغط **F5**.

```csharp
using System;
using System.Linq;
using Aspose.OCR;

class SpellCheckDemo
{
    static void Main()
    {
        // 1️⃣ Load the PNG image
        var imagePath = @"C:\Images\letter.png"; // <-- change this path
        var image = ImageStream.FromFile(imagePath);

        // 2️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine();
        // ocrEngine.Language = Language.English; // optional

        // 3️⃣ Recognize text
        var ocrResult = ocrEngine.Recognize(image);
        string recognizedText = ocrResult.Text;
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(recognizedText);

        // 4️⃣ Spell check
        var misspellings = ocrResult.SpellCheck();

        if (misspellings.Any())
        {
            Console.WriteLine("\nPossible misspellings:");
            foreach (var entry in misspellings)
                Console.WriteLine($"{entry.Word} → {string.Join(", ", entry.Suggestions)}");
        }
        else
        {
            Console.WriteLine("\nNo spelling issues detected.");
        }
    }
}
```

**تشغيل العرض** يطبع نص OCR متبوعًا بأي اقتراحات إملائية. يعمل على أي PNG يحتوي على نص إنجليزي واضح ومطبع. للغات أخرى، قم ببساطة بتعيين `ocrEngine.Language` وفقًا لذلك.

---

## أسئلة شائعة وملاحظات

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني معالجة ملفات JPEG أو BMP؟* | بالتأكيد—`ImageStream.FromFile` يقبل أي صيغة يدعمها Aspose (PNG, JPEG, BMP, TIFF). |
| *ماذا لو كانت الصورة في تدفق ذاكرة (memory stream)؟* | استخدم `ImageStream.FromBytes(byteArray)` أو `ImageStream.FromStream(stream)`. |
| *هل مدقق الإملاء يدعم اللغة؟* | نعم، فهو يحترم اللغة المحددة في محرك OCR. |
| *كيف أحسن الدقة في الصور المائلة؟* | فعّل `ocrEngine.PreprocessingOptions.Deskew = true;` قبل استدعاء `Recognize`. |
| *هل أحتاج إلى ترخيص لـ Aspose.OCR؟* | النسخة التجريبية المجانية تعمل حتى 100 صفحة. للإنتاج، احصل على ترخيص لإزالة العلامات المائية. |

---

## الخطوات التالية – ما بعد OCR الأساسي

الآن بعد أن أصبحت قادرًا على **التعرف على النص من PNG** و **استخراج النص من صورة C#**، فكر في هذه الإضافات:

1. معالجة دفعة – تكرار عبر مجلد يحتوي على PNGs وكتابة نتيجة OCR لكل صورة في ملف `.txt` منفصل.
2. التكامل مع Azure Cognitive Services – دمج Aspose OCR مع واجهات برمجة تطبيقات الترجمة السحابية لإنشاء خطوط عمل متعددة اللغات.
3. استخراج بيانات منظمة – استخدم التعبيرات النمطية على `recognizedText` لاستخراج التواريخ، أرقام الفواتير، أو العناوين.
4. تحسين الأداء – للأحجام الكبيرة، أعد استخدام كائن `OcrEngine` واحد وتمكين المعالجة المتعددة الخيوط.

كل من هذه الخطوات يبني على الأساسيات التي غطيناها، مما يتيح لك تحويل صورة بسيطة إلى بيانات قابلة للاستخدام.

---

## الخلاصة

لقد استعرضنا مثالًا كاملاً من البداية إلى النهاية يوضح كيفية **التعرف على النص من PNG** في C#، **تحميل ملف صورة C#** بشكل صحيح، ثم **استخراج النص من صورة C#** مع التقاط الأخطاء الإملائية. الشيفرة مستقلة، والتوضيحات تغطي كلًا من “كيف” و “لماذا”، والآن لديك أساس قوي لأي ميزة تعتمد على OCR قد تحتاجها.

جرّبه، عدّل خيارات ما قبل المعالجة، وشاهد مدى نظافة النص المستخرج. إذا واجهت أي مشاكل، اترك تعليقًا أدناه — برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}