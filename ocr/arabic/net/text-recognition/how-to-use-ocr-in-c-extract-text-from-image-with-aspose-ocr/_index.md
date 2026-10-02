---
category: general
date: 2026-02-24
description: كيفية استخدام OCR في C# لاستخراج النص من ملفات الصور. تعلم تحويل PNG
  إلى نص، قراءة الصور بشكل غير متزامن، ومعالجة المشكلات الشائعة.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من الصور. يوضح هذا الدليل خطوة
  بخطوة OCR غير المتزامن باستخدام Aspose، ويغطي التحويل، ومعالجة الأخطاء، وأفضل الممارسات.
og_title: كيفية استخدام OCR في C# – دليل شامل
tags:
- OCR
- C#
- Aspose
title: كيفية استخدام OCR في C# – استخراج النص من الصورة باستخدام Aspose OCR
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصورة

هل تساءلت يومًا **كيفية استخدام OCR** لاستخراج النص من صورة دون كتابته يدويًا؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى *استخراج النص من الصورة* مثل ملفات PNG، والطريقة التقليدية للنسخ‑اللصق لا تكفي.  

في هذا الدرس سنستعرض حلًا كاملًا وغير متزامن **يحوّل PNG إلى نص** باستخدام مكتبة Aspose.OCR. في النهاية ستعرف بالضبط كيفية قراءة ملفات الصور، معالجة الأخطاء، ودمج النتيجة في تطبيقاتك.  

سنتناول كل شيء من إعداد حزمة NuGet إلى تعديل محرك OCR لتحسين الدقة، وسنضيف نصائح حول ما يجب فعله عندما لا تكون الصورة واضحة تمامًا. لا حاجة للبحث عن روابط الوثائق—كل ما تحتاجه موجود هنا.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يعمل على .NET Core و .NET Framework أيضًا)  
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)  
- حزمة NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)  
- ملف صورة (PNG, JPG, BMP) تريد معالجته – سنسميه `input.png`

هذا كل شيء. إذا كان لديك هذه المتطلبات، فأنت جاهز للبدء.

![مخطط يوضح سير عمل OCR – كيفية استخدام OCR لاستخراج النص من صورة](/images/ocr-workflow.png)

## الخطوة 1: تثبيت Aspose.OCR وإضافة المساحات الاسمية

أولاً، أضف المكتبة إلى مشروعك. افتح وحدة تحكم مدير الحزم وشغّل:

```powershell
Install-Package Aspose.OCR
```

بعد ذلك، في أعلى ملف C# الخاص بك، أضف المساحات الاسمية اللازمة:

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **نصيحة احترافية:** إذا كنت تستخدم .NET 6 APIs الحد الأدنى، يمكنك وضع عبارات `using` هذه في ملف عالمي حتى لا تحتاج لتكرارها عبر عدة فئات.

### لماذا هذا مهم

توفر لك مساحة الاسم `Aspose.OCR` الوصول إلى `OcrEngine`، الفئة الأساسية التي تقرأ الصورة فعليًا. بدونها، سيتعين عليك كتابة كود تحليل البكسل بنفسك—وهو مسار معقد للغاية. إضافة المساحات الاسمية تجعل الكود منظمًا وتُعلم المُترجم أين يجد الأنواع التي ستستخدمها.

## الخطوة 2: إنشاء محرك OCR غير متزامن

سنغلف استدعاء OCR في طريقة `async` حتى يبقى واجهة المستخدم مستجيبة ويمكن لكود الخادم أن يتوسع. إليك هيكل تطبيق كونسول:

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### شرح

- `OcrEngine ocrEngine = new OcrEngine();` – ينشئ محركًا بالإعدادات الافتراضية. يمكنك لاحقًا تعديل اللغة أو وضع الكشف أو فلاتر ما قبل المعالجة.  
- `await ocrEngine.RecognizeImageAsync(...)` – الطريقة غير المتزامنة تُعيد `Task<OcrResult>`. الانتظار يحرّر الخيط بينما يعمل OCR في الخلفية.  
- `ocrResult.Text` – تمثيل النص العادي لكل ما استطاع المحرك قراءته. هذا هو جوهر *كيفية استخراج النص* من صورة.

## الخطوة 3: تحسين المحرك للحصول على دقة أفضل

يعمل OCR مباشرةً بشكل جيد على الصور النظيفة ذات التباين العالي، لكن الصور الواقعية غالبًا ما تحتاج إلى بعض المساعدة. يمكنك تعديل بعض الخصائص قبل استدعاء `RecognizeImageAsync`:

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### متى تستخدم هذه الإعدادات

- **مسحات منخفضة الجودة** – فعّل `ImagePreprocessingOptions.Auto` للسماح لـ Aspose بتنظيف الضوضاء.  
- **ملفات PDF متعددة اللغات** – غيّر `Language` إلى `OcrLanguage.French` أو اجمع اللغات باستخدام قناع بت.  
- **حقول النماذج** – قصر `Characters` على الأرقام أو الأحرف الكبيرة لتقليل الإيجابيات الزائفة.

## الخطوة 4: معالجة الأخطاء بلطف

OCR ليس سحريًا؛ قد يفشل إذا كان الملف مفقودًا أو معطوبًا أو بصيغة غير مدعومة. غلف الاستدعاء غير المتزامن بكتلة try/catch:

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### لماذا هذا مفيد

توفير رسائل خطأ واضحة يسرّع عملية التصحيح ويحسّن تجربة المستخدم النهائي. بدلاً من تعطل عام، ستحصل على موجه مفيد يخبرك بما إذا كان عليك فحص المسار أو صيغة الملف أو إعدادات محرك OCR.

## الخطوة 5: جمع كل شيء معًا – مثال كامل يعمل

فيما يلي برنامج كونسول كامل وجاهز للتنفيذ يوضح **كيفية استخدام OCR**، يطبق ما قبل المعالجة، ويتعامل مع الأخطاء. انسخه إلى مشروع `.csproj` جديد واضغط F5.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع** (بافتراض أن `input.png` يحتوي على العبارة “Hello World”):

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

إذا كانت الصورة غير واضحة، قد ترى أحرفًا إضافية أو كلمات مفقودة—وهنا تصبح خيارات ما قبل المعالجة من الخطوة 3 حاسمة.

## الخطوة 6: توسيع الحل – من PNG إلى PDF أو ملفات نصية

أحيانًا تحتاج إلى **تحويل PNG إلى نص** ثم تخزين النتيجة في ملف `.txt` أو تضمينها في تقرير PDF. إليك مقتطف سريع يكتب ناتج OCR إلى ملف:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

أو، إذا كنت تنشئ PDF باستخدام Aspose.PDF:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

توضح هذه الإضافات كيف يمكن لـ **كيفية قراءة بيانات الصورة** تغذية العمليات اللاحقة—إنشاء تقارير، فهرسة بحث، أو حتى إمداد نموذج لغة.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ما هي صيغ الصور المدعومة؟* | Aspose.OCR يدعم PNG, JPEG, BMP, TIFF, و GIF. إذا كان لديك PDF، استخرج صفحاته كصور أولاً. |
| *هل يمكنني معالجة صور متعددة بالتوازي؟* | نعم—غلف كل استدعاء `RecognizeImageAsync` في مهمة منفصلة واستخدم `Task.WhenAll`. فقط احرص على استهلاك الذاكرة. |
| *ماذا يحدث إذا أعاد OCR نصًا فارغًا؟* | تحقق من جودة الصورة: انخفاض التباين أو النص المدور غالبًا ما يفشل. فعّل `ImagePreprocessingOptions.Deskew` أو قم بتدوير الصورة يدويًا قبل OCR. |
| *هل هناك حد لحجم الصورة؟* | الصور الكبيرة (>10 MP) قد تتسبب في `OutOfMemoryException`. قلل حجمها إلى دقة معقولة (مثلاً 300 DPI) قبل التعرف. |
| *هل أحتاج إلى ترخيص لـ Aspose.OCR؟* | وضع التطوير يعمل بترخيص مؤقت، لكن للإنتاج ستحتاج إلى ترخيص مدفوع لإزالة علامات التقييم. |

## نصائح الأداء

- **أعد استخدام كائن `OcrEngine`** للمعالجة على دفعات؛ إنشاء محرك جديد لكل صورة يضيف عبئًا.  
- **أوقف اللغات غير المستخدمة** لتسريع الكشف—كل لغة إضافية تضيف تكلفة معالجة صغيرة.  
- **شغّل OCR على خيط خلفي** (كما هو موضح) للحفاظ على استجابة خيوط الواجهة في تطبيقات سطح المكتب أو الويب.

## الخلاصة

لقد غطينا **كيفية استخدام OCR** في C# من البداية حتى النهاية: تثبيت Aspose.OCR، كتابة طريقة غير متزامنة، تعديل الإعدادات للصور الضوضائية، معالجة الأخطاء، وحفظ النتائج. الآن لديك طريقة موثوقة *لاستخراج النص من ملفات الصورة*، *تحويل PNG إلى نص*، وحتى إمداد هذا النص إلى عمليات أخرى مثل إنشاء PDF.  

هل أنت مستعد للتحدي التالي؟ جرّب إمداد ناتج OCR إلى فهرس Azure Cognitive Search القابل للبحث، أو جرب OCR متعدد اللغات بإضافة `OcrLanguage.Spanish | OcrLanguage.French` إلى المحرك. السماء هي الحد عندما تعرف **كيفية قراءة بيانات الصورة** برمجيًا.

*إذا وجدت هذا الدليل مفيدًا، أعطه نجمة على GitHub، شاركه مع زملائك، أو اترك تعليقًا أدناه بأفكارك الخاصة حول OCR. برمجة سعيدة!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}