---
category: general
date: 2026-02-19
description: دروس C# OCR تُظهر كيفية استخراج النص من الصورة، التعرف على النص من ملف
  JPG، وتحويل الصورة إلى نص باستخدام مكتبة Aspose OCR.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from jpg
- convert image to text
- extract text from jpg
language: ar
og_description: دليل C# OCR يشرح لك استخراج النص من الصورة، والتعرف على النص من JPG،
  وتحويل الصورة إلى نص باستخدام Aspose OCR.
og_title: دليل c# OCR – استخراج النص من الصورة باستخدام Aspose OCR
tags:
- OCR
- C#
- Aspose
title: دورة C# OCR – استخراج النص من الصورة باستخدام Aspose OCR
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-image-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR Tutorial – استخراج النص من الصورة باستخدام Aspose OCR

هل تساءلت يومًا كيف **استخراج النص من صورة** دون أن تشعر بالإحباط؟ في العديد من التطبيقات الواقعية تحتاج إلى قراءة فاتورة ممسوحة ضوئيًا، استخراج رقم تسلسلي من صورة، أو ببساطة تحويل JPG إلى نص قابل للبحث. هذا **c# ocr tutorial** يوضح لك بالضبط كيفية القيام بذلك، باستخدام مكتبة Aspose OCR، ويغطي أيضًا الفروق الدقيقة بين *recognize text from jpg* و *convert image to text*.

في هذا الدليل ستتعلم كيفية إعداد حزمة Aspose OCR NuGet، كتابة برنامج كونسول صغير يقرأ صورة، ومعالجة أكثر المشكلات شيوعًا (مثل صيغ الصور غير المدعومة أو إعدادات اللغة). بنهاية الدليل ستحصل على مقتطف شيفرة يعمل يمكنك إدراجه في أي مشروع .NET والبدء في **استخراج النص من jpg** في ثوانٍ.

## ما ستحتاجه

| المتطلبات المسبقة | لماذا يهم |
|------------------|-----------|
| .NET 6 SDK (أو أحدث) | ميزات C# الحديثة وأداء أفضل |
| Visual Studio 2022 أو VS Code | تجربة تحرير مريحة |
| ملف صورة (`sample.jpg`) تريد معالجته | المصدر الفعلي لمحرك OCR الخاص بنا |
| اتصال بالإنترنت لتحميل حزمة Aspose.OCR NuGet | المكتبة ليست مدمجة، نحتاج إلى تنزيلها |

إذا كان أي من هذه غير مألوف لك، لا تقلق – الخطوات أدناه ستقودك عبر كل جزء، والشيفرة تعمل حتى على محرر نص عادي مع `dotnet` CLI.

## الخطوة 1: تثبيت حزمة Aspose.OCR NuGet

أولًا، علينا جلب محرك OCR إلى مشروعنا. افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، يمكنك أيضًا النقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن “Aspose.OCR” واضغط *Install*.

هذا الأمر يجلب أحدث نسخة مستقرة (اعتبارًا من فبراير 2026 هي 23.3) ويضيف الإشارة إلى ملف `.csproj` الخاص بك. لا حاجة لنسخ DLLs إضافية—كل شيء يُدار بواسطة وقت تشغيل .NET.

## الخطوة 2: إنشاء هيكل تطبيق كونسول بسيط

الآن لننشئ تطبيق كونسول بسيط سيستضيف منطق OCR. أنشئ ملفًا باسم `Program.cs` (أو استبدل الموجود) والصق الهيكل التالي:

```csharp
using System;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the OCR routine from here.
            Console.WriteLine("Starting c# OCR tutorial...");
        }
    }
}
```

لاحظ وجود `using System;` في الأعلى – سنحتاجه لإخراج النص إلى الكونسول وللتعامل مع الاستثناءات المحتملة لاحقًا.

## الخطوة 3: تهيئة محرك OCR وتحديد اللغة

يدعم Aspose OCR عشرات اللغات، لكن لمعظم العروض التجريبية الإنجليزية كافية. المحرك خفيف الوزن، لذا يمكننا إنشاء كائنه مباشرة داخل `Main`. أضف الشيفرة التالية **بعد** سطر `Console.WriteLine` التمهيدي:

```csharp
using Aspose.OCR;   // <-- add this using directive at the top of the file

// ...

// Step 3: Create an OCR engine and configure it for English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // you can switch to Language.Spanish, etc.
};
```

لماذا نحدد اللغة صراحةً؟ لأن خوارزمية التعرف الأساسية تستخدم قواميس خاصة باللغة لتحسين الدقة. تخطي هذه الخطوة قد يعمل، لكنك غالبًا ستحصل على نتائج مشوشة للنص غير الإنجليزي.

## الخطوة 4: التعرف على النص من صورة JPG

هذا هو جوهر الدرس – تمرير ملف صورة إلى المحرك واستخراج النتيجة النصية. أدخل الشيفرة أدناه مباشرة بعد تهيئة المحرك:

```csharp
// Step 4: Define the path to the image you want to process
string imagePath = @"YOUR_DIRECTORY/sample.jpg";   // <-- replace with your actual path

try
{
    // Recognize the image. This method returns an OcrResult object.
    OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

    // Display the raw OCR output in the console
    Console.WriteLine("\n--- OCR Output ---");
    Console.WriteLine(ocrResult.Text);
}
catch (Exception ex)
{
    // If something goes wrong (file not found, unsupported format, etc.)
    Console.Error.WriteLine($"Error during OCR: {ex.Message}");
}
```

بعض النقاط التي يجب ملاحظتها:

* **`RecognizeImage`** يعمل مع معظم صيغ الصور النقطية الشائعة – JPEG، PNG، BMP، TIFF. لهذا السبب يمكن لهذا الدرس *recognize text from jpg* دون خطوات تحويل إضافية.
* تُعيد الطريقة كائن `OcrResult` يحتوي على `Text`، `Confidence`، وحتى `BoundingBoxes` إذا احتجت بيانات الموقع لاحقًا.
* تغليف الاستدعاء داخل `try/catch` يجعل البرنامج أكثر صلابة – ملف مفقود لن يتسبب بعد الآن في تعطل التطبيق بالكامل.

## الخطوة 5: تشغيل التطبيق والتحقق من المخرجات

احفظ الملف، عد إلى الطرفية، ونفّذ:

```bash
dotnet run
```

ستظهر لك نتيجة مشابهة لـ:

```
Starting c# OCR tutorial...

--- OCR Output ---
Hello, world!
This is a sample image containing text.
```

إذا طبع الكونسول النص الدقيق الموجود في `sample.jpg`، تهانينا! لقد قمت للتو **تحويل الصورة إلى نص** باستخدام بضع أسطر من C#.

### ماذا لو كان المخرجات غريبة؟

* **ثقة منخفضة:** حاول زيادة دقة الصورة أو تطبيق معالجة مسبقة (مثل الشحذ، التحويل إلى ثنائي). يحتوي Aspose OCR على طريقة `PreprocessImage` يمكنك استكشافها.
* **لغة خاطئة:** تأكد من أن `ocrEngine.Language` يطابق لغة الصورة المصدر.
* **صيغة غير مدعومة:** تأكد أن امتداد الملف هو JPEG فعليًا؛ أحيانًا ملف PNG محفوظ بامتداد `.jpg` يربك المحلل.

## الخطوة 6: تجميع المثال الكامل لإعادة الاستخدام

فيما يلي **البرنامج الكامل القابل للتنفيذ** الذي يمكنك نسخه ولصقه في أي مشروع كونسول جديد. يتضمن جميع جمل `using` الضرورية، معالجة الاستثناءات، وتعليقات توضح كل سطر.

```csharp
// Program.cs
using System;
using Aspose.OCR;   // Aspose OCR library

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("=== c# OCR Tutorial – Extract Text from Image ===");

            // 1️⃣ Create OCR engine and set language (English by default)
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Path to the image you want to process
            string imagePath = @"YOUR_DIRECTORY/sample.jpg"; // <-- update this

            try
            {
                // 3️⃣ Perform OCR – this both *recognizes text from jpg* and *extracts text from image*
                OcrResult result = ocrEngine.RecognizeImage(imagePath);

                // 4️⃣ Output the recognized string – you’ve now *converted image to text*
                Console.WriteLine("\n--- OCR Result ---");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Friendly error message – helps when the file is missing or corrupted
                Console.Error.WriteLine($"Oops! Something went wrong: {ex.Message}");
            }

            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

احفظه كـ `Program.cs`، شغّل `dotnet run`، وستحصل على عرض حي لـ **استخراج النص من jpg** في العمل.

## إضافي: استخراج النص من صور متعددة في مجلد

غالبًا ما تحتاج إلى معالجة مجموعة من المسح الضوئي دفعة واحدة. إليك امتداد سريع يمر على كل ملف `.jpg` في مجلد، ينفّذ OCR، ويكتب كل نتيجة إلى ملف `.txt` يحمل نفس الاسم الأساسي.

```csharp
using System.IO;

// ...

string folderPath = @"YOUR_DIRECTORY"; // folder containing many jpg files

foreach (string file in Directory.GetFiles(folderPath, "*.jpg"))
{
    try
    {
        OcrResult batchResult = ocrEngine.RecognizeImage(file);
        string txtPath = Path.ChangeExtension(file, ".txt");
        File.WriteAllText(txtPath, batchResult.Text);
        Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {Path.GetFileName(file)}: {ex.Message}");
    }
}
```

هذا المقتطف يوضح سيناريو واقعي حيث *استخراج النص من صورة* على نطاق واسع، وهو طلب شائع لأنظمة إدارة المستندات.

## توضيح صورة (اختياري)

إذا رغبت في إضافة إشارة بصرية في المقال، يمكنك تضمين لقطة شاشة لمخرجات الكونسول:

![مخرجات وحدة التحكم في درس c# OCR تُظهر النص المستخرج](/images/ocr-console.png)

*يتضمن النص البديل الكلمة المفتاحية الأساسية لتلبية متطلبات تحسين محركات البحث.*

## أسئلة شائعة وحالات خاصة

**س: هل يعمل هذا على ملفات PDF؟**  
ج: ليس مباشرة. ستحتاج أولاً إلى تحويل كل صفحة PDF إلى صورة (مثلاً باستخدام Aspose.PDF) ثم تمرير تلك الصور إلى محرك OCR.

**س: ماذا عن الخط اليدوي؟**  
ج: يركز Aspose OCR على النص المطبوع. للخطوط المتصلة أو الملاحظات المكتوبة يدويًا ستحتاج إلى نموذج متخصص (مثل Azure Cognitive Services أو Google Vision).

**س: هل يمكنني تغيير ترميز الإخراج؟**  
ج: `OcrResult.Text` هو `string` في .NET، وهو UTF‑16 بشكل افتراضي، لذا يمكنك كتابته بأي ترميز ملف تفضله باستخدام `File.WriteAllText(path, text, Encoding.UTF8)`.

**س: هل المكتبة مجانية؟**  
ج: تقدم Aspose وضع تقييم كامل مع علامة مائية. للإنتاج ستحتاج إلى ترخيص، لكن استخدام الـ API يبقى نفسه.

## الخلاصة

لقد أكملت للتو **c# OCR tutorial** الذي يرشّحك عبر تثبيت Aspose OCR، تهيئة المحرك، و**استخراج النص من صورة** — بما في ذلك JPEGs — حتى تتمكن من *convert

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}