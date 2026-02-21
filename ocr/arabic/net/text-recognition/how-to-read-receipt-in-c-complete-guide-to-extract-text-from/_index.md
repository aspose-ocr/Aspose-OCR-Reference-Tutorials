---
category: general
date: 2026-02-20
description: تعلم كيفية قراءة الإيصال في C# عن طريق استخراج النص من الصورة وتحويله
  إلى JSON. كود خطوة بخطوة باستخدام Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: ar
og_description: اكتشف كيفية قراءة الإيصال في C# عن طريق تحميل ملف صورة، استخراج النص
  باستخدام Aspose OCR، وتحويل النتيجة إلى JSON. مثال كامل على الشيفرة.
og_title: كيفية قراءة إيصال في C# – استخراج النص، تحويله إلى JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: كيفية قراءة الإيصال في C# – دليل كامل لاستخراج النص من الصورة
url: /ar/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

"الإصلاح / التوصية". But need to preserve pipe formatting. Let's translate.

Also bullet lists.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية قراءة الإيصال في C# – دليل كامل

هل تساءلت يومًا **كيف تقرأ صور الإيصالات** برمجيًا؟ ربما تبني تطبيقًا لتتبع النفقات وتحتاج إلى استخراج بنود الفاتورة من صورة إيصال بقالة. في تجربتي، أكبر نقطة ألم هي تحويل صورة JPEG الضبابية إلى بيانات منظمة يمكنك استخدامها فعليًا. الخبر السار؟ ببضع أسطر من C# و Aspose OCR يمكنك **استخراج النص من الصورة**، ثم **تحويل الصورة إلى JSON** بطريقة تبدو تقريبًا سحرية.

في هذا الدرس ستحصل على حل جاهز للتنفيذ **يحمّل ملف صورة C#**، يشغل OCR، ويُخرج حمولة JSON مفصلة. لا خدمات خارجية، لا استدعاءات REST معقدة—فقط شفرة .NET صافية يمكنك إدراجها في أي مشروع Console أو ASP.NET. بنهاية الدرس ستفهم لماذا كل خطوة مهمة، وكيفية التعامل مع الحالات الطرفية الشائعة (مثل أحجام الإيصالات غير القياسية)، وما هو شكل مخرجات JSON فعليًا.

## ما الذي ستحتاجه

- **.NET 6.0 أو أحدث** – يستخدم الكود `System.Drawing.Common` المدعوم على Windows و Linux و macOS.  
- **Aspose.OCR for .NET** – يمكنك الحصول على حزمة NuGet التجريبية المجانية (`Aspose.OCR`) أو استخدام نسخة مرخصة إذا كانت لديك.  
- صورة **إيصال تجريبية** (`receipt.jpg`) موضوعة في مكان يمكن لتطبيقك قراءته.  
- أي بيئة تطوير تفضلها (Visual Studio، Rider، VS Code).  

هذا كل شيء. لا إعدادات إضافية، لا مفاتيح API.

---

## الخطوة 1 – تحميل ملف الصورة C# (الكلمة المفتاحية الأساسية في التنفيذ)

قبل أن يتمكن محرك OCR من القيام بسحره، عليك جلب الصورة إلى الذاكرة. هذه هي خطوة “تحميل ملف صورة C#” الكلاسيكية التي يغفل عنها الكثير من المطورين.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**لماذا هذه الخطوة مهمة:**  
`Image.FromFile` يقرأ الملف *مرة واحدة* ويبقي المقبض مفتوحًا، وهو مثالي لتمرير OCR سريع. إذا كنت تعالج العديد من الإيصالات في حلقة، فكر في استخدام `Image.FromStream` لتجنب قفل الملف.

> **نصيحة احترافية:** إذا واجهت *FileNotFoundException*، تحقق من المسار وتأكد من وجود الصورة فعليًا. المسارات النسبية تعمل أيضًا (`"./receipt.jpg"`)، لكن المسارات المطلقة أكثر أمانًا للوظائف الإنتاجية.

---

## الخطوة 2 – إنشاء وتكوين محرك OCR

يأتي Aspose OCR مع `OcrEngine` جاهز. لا تحتاج إلى تدريب نموذج؛ المكتبة تعرف بالفعل كيفية قراءة النص المطبوع، وهو ما تستخدمه معظم الإيصالات.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**لماذا نضبط هذه الخيارات:**  
`DetectOrientation` يخبر المحرك بتدوير الصورة تلقائيًا إذا تم مسح الإيصال رأسًا على عقب. ضبط اللغة يحد من مجموعة الأحرف، مما يمكن أن يحسن الدقة—خاصة عندما تحتاج فقط إلى بيانات أبجدية إنجليزية رقمية.

---

## الخطوة 3 – التعرف على الصورة وتحويلها إلى JSON

الآن يأتي الجزء الممتع: **استخراج النص من الصورة** و **تحويل الصورة إلى JSON** في استدعاء واحد.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

طريقة `RecognizeToJson` تُعيد بنية JSON غنية تشمل:

- `Text`: النص العادي المتسلسل.  
- `Lines`: مصفوفة كائنات السطر مع الإحداثيات.  
- `Words`: كل كلمة مع درجات الثقة.  
- `Regions`: مربعات الحد للكتل النصية المكتشفة.

يمكنك تحويل هذا الـ JSON إلى كائن C# إذا احتجت وصولًا مُعَرَّفًا، لكن في كثير من السيناريوهات يكون طباعة الـ JSON الخام كافية.

---

## الخطوة 4 – إخراج الـ JSON (أو تخزينه)

لنلق نظرة على المخرجات ونناقش ما يمكن فعله بها.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### مثال على المخرجات

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**ما الخطوة التالية؟**  
حلل مصفوفة `Lines` لاستخراج مبلغ `Total`، أو مرر الـ JSON إلى خدمة لاحقة تخزن قيود النفقات. لأن النتيجة بالفعل JSON، يمكنك ربطها مباشرة بأي قاعدة NoSQL، أو Azure Function، أو تدفق Power Automate.

---

## الخطوة 5 – التعامل مع الحالات الطرفية الشائعة

حتى أفضل محركات OCR تواجه بعض الصعوبات. إليك بعض السيناريوهات التي قد تصادفها أثناء تعلم **كيفية قراءة صور الإيصالات**.

| الحالة | الإصلاح / التوصية |
|-----------|----------------------|
| **إيصال منخفض الدقة (≤ 150 dpi)** | قم بتكبير الصورة أولًا باستخدام `Bitmap` و `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **إيصال مائل أو مدوَّر** | أبقِ `DetectOrientation = true`. إذا كان الميل شديدًا، عالج مسبقًا بـ `Image.RotateFlip` أو مكتبة طرف ثالث مثل OpenCV. |
| **خلفية ملونة (مثلاً إيصال على طاولة)** | حوّل إلى تدرج الرمادي وزد التباين قبل OCR (`ImageAttributes`). |
| **عدة إيصالات في صورة واحدة** | قص كل منطقة إيصال يدويًا أو استخدم `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **ملفات كبيرة تسبب OutOfMemory** | استخدم عبارات `using` لتصريف كائنات `Image` فورًا، أو عالجها على دفعات. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## الخطوة 6 – مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج *الكامل* الذي يمكنك تجميعه الآن. يتضمن جميع الخطوات، توجيهات `using` الصحيحة، ومعالجة الأخطاء بأناقة.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**لتشغيله:**  
`dotnet run` من مجلد المشروع. إذا تم إعداد كل شيء بشكل صحيح، سترى الـ JSON يُطبع في وحدة التحكم ويحفظ بجوار صورة الإيصال.

---

## الخلاصة

لقد غطينا للتو **كيفية قراءة صور الإيصالات** في C# من البداية إلى النهاية. من خلال تحميل الصورة، تكوين Aspose OCR، واستدعاء `RecognizeToJson`، يمكنك **استخراج النص من الصورة** و **تحويل الصورة إلى JSON** دون كتابة الكثير من الشيفرة. النهج قابل للتوسع—from عرض إيصـال واحد إلى معالج دفعات يتعامل مع مئات الإيصالات كل ليلة.

خطوات مستقبلية قد تستكشفها:

- **تحليل الـ JSON** لاستخراج التواريخ، المبالغ الإجمالية، وبنود الفاتورة (باستخدام `System.Text.Json` أو `Newtonsoft.Json`).  
- **دمجه مع قاعدة بيانات** (SQL، Cosmos DB) لتخزين سجلات النفقات تلقائيًا.  
- **إضافة واجهة مستخدم** (WinForms، WPF، أو Blazor) لتمكين السحب والإفلات للإيصالات.  
- **استبدال Aspose OCR** بمحرك آخر (Tesseract، Microsoft Azure OCR) إذا كانت الرخصة تشكل عائقًا—فقط حافظ على نمط “تحميل ملف صورة C#”.

لا تتردد في التجربة، وكسر الأشياء، ثم العودة إلى هنا لتحديث معلوماتك. إذا واجهت أي عائق، المجتمع (ومنتديات Aspose) مكان رائع لطرح الأسئلة. برمجة سعيدة، واستمتع بتحويل تلك الإيصالات الورقية إلى بيانات نظيفة قابلة للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}