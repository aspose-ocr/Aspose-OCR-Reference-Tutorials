---
category: general
date: 2026-03-17
description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) لصور PNG دفعيًا في C# بسرعة.
  تعلم استخراج النص من ملفات PNG، تحويل PNG إلى نص، وقراءة الصور من الدليل باستخدام
  سكريبت بسيط.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: ar
og_description: كيفية تنفيذ OCR دفعي لصور PNG في C# مع كود خطوة بخطوة. استخراج النص
  من ملفات PNG، تحويل PNG إلى نص، وقراءة الصور من الدليل بسهولة.
og_title: كيفية إجراء OCR دفعي لصور PNG في C# – دليل شامل
tags:
- OCR
- C#
- Image Processing
title: كيفية تنفيذ OCR لصور PNG على دفعات في C# – دليل كامل
url: /ar/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

All preserved.

Now produce final content with Arabic translation. Ensure code blocks placeholders unchanged.

Also need to translate the "Expected output:" blockquote label but keep formatting.

Let's assemble final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعي لصور PNG في C# – دليل كامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لمجلد مليء بلقطات الشاشة دون فتح كل ملف يدويًا؟ لست وحدك—فالمطورون يسألون باستمرار كيف يمكنهم عمل OCR دفعي لمجموعات كبيرة من ملفات PNG، خاصة عندما يكون الهدف هو استخراج نص من ملفات PNG للتحليل اللاحق.  

في هذا الدرس سنستعرض مثالًا جاهزًا للتنفيذ بلغة C# يقوم **باستخراج نص من PNG**، **تحويل PNG إلى نص**، ويظهر لك أفضل طريقة لـ **قراءة الصور من دليل**. في النهاية ستحصل على سكريبت واحد يضع ملف `.txt` بجوار كل صورة، مما يوفر لك ساعات من النسخ واللصق اليدوي.

## ما ستحققه

- تهيئة محرك OCR مرة واحدة وإعادة استخدامه للدفعة بأكملها.  
- مسح كل ملف `*.png` في مجلد معين دون كتابة حلقة بنفسك.  
- كتابة نتيجة OCR لكل صورة في ملف نصي منفصل، مع الحفاظ على اسم الملف الأصلي.  
- معالجة الحالات الشائعة مثل المجلدات الفارغة أو الملفات غير الصورية بشكل سلس.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضًا).  
- مكتبة OCR تُظهر الأنواع `OcrEngine` و `ImageStream` و `OcrResult` (مثال على ذلك SDK الخيالي **FastOCR** المستخدم في الأمثلة).  
- معرفة أساسية بـ C#—لا حاجة لأنماط متقدمة.

---

## كيفية تنفيذ OCR دفعي لصور PNG – نظرة عامة

فيما يلي **البرنامج الكامل القابل للتنفيذ**. لا تتردد في نسخه‑ولصقه في مشروع وحدة تحكم جديد، استبدل مسارات العنصر النائب، واضغط **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **الإخراج المتوقع:** لكل ملف `image01.png` ستجد ملف `image01.txt` يحتوي على الأحرف التي تم التعرف عليها. سيعرض الطرفية كل ملف عند كتابته.

![مخطط كيفية تنفيذ OCR دفعي](how-to-batch-ocr-diagram.png "مخطط يوضح كيفية تنفيذ OCR دفعي لصور PNG باستخدام C#")

---

## شرح خطوة بخطوة

### 1. تهيئة محرك OCR – قلب العملية  

السطر `var ocrEngine = new OcrEngine();` ينشئ نسخة واحدة من المحرك سيتم إعادة استخدامها للدفعة بأكملها. إعادة استخدام المحرك **ضرورية** لأن معظم مكتبات OCR تخصّص موارد ثقيلة (مثل نماذج اللغة) عند الإنشاء. التهيئة مرة واحدة تحسّن الأداء بشكل كبير—خاصة عندما يكون لديك عشرات أو مئات من ملفات PNG.  

**نصيحة احترافية:** إذا كنت بحاجة إلى لغة غير الإنجليزية، اضبط `ocrEngine.Config.Language = Language.Spanish;` (أو أي تعداد مدعوم).  

### 2. قراءة الصور من الدليل – تحديد كل PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` يفعل تمامًا ما توعد به الكلمة المفتاحية الثانوية *read images from directory*. يُعيد مصفوفة من المسارات المطلقة، والتي نُمرّرها لاحقًا إلى محرك OCR.  

**لماذا لا نستخدم `SearchOption.AllDirectories`؟** إذا كانت صورك متداخلة في مجلدات فرعية، يمكنك التحويل إلى `GetFiles(path, "*.png", SearchOption.AllDirectories)`. فقط تذكر أن الفحص الأعمق قد يجلب ملفات غير مرغوب فيها، لذا قم بالترشيح وفقًا لذلك.

### 3. تحويل مسارات الملفات إلى كائنات ImageStream  

معظم SDKs الخاصة بـ OCR تتوقع تدفقًا (stream) بدلاً من مسار خام. تعبير LINQ `Select(path => ImageStream.FromFile(path)).ToList()` يُنشئ **قائمة من التدفقات** التي يمكن لمُعَرِّف الدفعة استهلاكها في استدعاء واحد. هذه الخطوة تضمن أيضًا أن مقابض الملفات تُفتح مرة واحدة فقط، مما يقلل من عبء الإدخال/الإخراج.  

**حالة حدية:** إذا كان الملف تالفًا، قد يرمي `ImageStream.FromFile` استثناء. غلف التحويل بـ `try/catch` إذا كنت تحتاج إلى مرونة.

### 4. التعرف على النص في الدفعة بأكملها  

`ocrEngine.RecognizeBatch(imageStreams)` هو النقطة المثالية لـ *how to batch OCR*. بدلاً من التكرار على كل صورة واستدعاء طريقة صورة واحدة، نمرّر المجموعة بالكامل إلى المحرك. داخليًا قد تقوم المكتبة بتوازي العمل، مما يمنحك زيادة سرعة على الأجهزة متعددة النوى.  

**نصيحة:** إذا لم تُظهر مكتبة OCR طريقة دفعية، يمكنك تحقيق أداء مماثل باستخدام `Parallel.ForEach` حول استدعاء `Recognize` للصور الفردية.

### 5. كتابة كل نتيجة OCR – تحويل PNG إلى نص  

حلقة `for` النهائية تكتب `ocrResults[i].Text` إلى ملف `.txt` يحمل اسمًا يطابق PNG الأصلي. هذا هو بالضبط ما تصفه الكلمة المفتاحية الثانوية *convert PNG to text*. استدعاء `Path.Combine` يضمن وجود مجلد الإخراج ويمنع أخطاء عبور المسار.  

**مشكلة شائعة:** نسيان إنشاء مجلد الإخراج أولًا سيسبّب استثناء `DirectoryNotFoundException`. السطر `Directory.CreateDirectory(outputFolder);` يحل ذلك مسبقًا.

---

## التعامل مع التغيّرات في العالم الحقيقي

| الحالة | ما الذي يجب تغييره | السبب |
|-----------|----------------|-----|
| **مجلد الإدخال فارغ** | احتفظ بالحارس `if (imagePaths.Length == 0)` في البداية | يمنع استدعاء OCR غير ضروري ويعطي رسالة ودية |
| **أنواع ملفات مختلطة** | استخدم `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | يضمن معالجة PNG فقط، مما يحقق *extract text png* دون أخطاء |
| **صور ضخمة (> 5 MB)** | قلل الحجم قبل إرساله إلى OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (إذا كان API يدعم) | يقلل من ضغط الذاكرة وغالبًا ما يحسن دقة التعرف |
| **لغة OCR مختلفة** | اضبط `ocrEngine.Config.Language = Language.French;` | يطابق المحرك لغة الصور المصدرية |

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات JPEG أو TIFF؟**  
ج: يبقى المنطق الأساسي كما هو؛ فقط غيّر نمط البحث إلى `"*.jpg"` أو `"*.tif"` وتأكد من أن مكتبة OCR يمكنها فك تشفير تلك الصيغ.

**س: كيف يمكنني معالجة آلاف الصور دون نفاد الذاكرة؟**  
ج: استبدل استدعاء الدفعة بنهج تدفقي—عالج مجموعة، مثلاً 50 صورة في كل مرة، ثم حرّر التدفقات قبل تحميل المجموعة التالية.

**س: أحتاج إلى درجة ثقة OCR. أين يمكنني العثور عليها؟**  
ج: معظم كائنات `OcrResult` تعرض خاصية `Confidence`. يمكنك توسيع خطوة الكتابة:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## الخلاصة

لقد غطينا للتو **كيفية تنفيذ OCR دفعي** لصور PNG في C# من البداية إلى النهاية. من خلال تهيئة محرك واحد، قراءة الصور من الدليل، تحويلها إلى تدفقات، التعرف على الدفعة بأكملها، وأخيرًا كتابة كل نتيجة إلى ملف نصي، لديك الآن نمط قوي وجاهز للإنتاج لمهام **extract text PNG**، **convert PNG to text**، و **read images from directory**.  

ما التالي؟ جرّب استبدال موفر OCR، أضف معالجة ما بعد متعددة الخيوط (مثل التدقيق الإملائي)، أو أدخل ملفات `.txt` في فهرس بحث. السماء هي الحد عندما تتقن سير عمل الدفعة.  

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}