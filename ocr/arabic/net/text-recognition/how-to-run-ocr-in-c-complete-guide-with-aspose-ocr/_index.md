---
category: general
date: 2026-01-10
description: كيفية تشغيل OCR على صورة باستخدام Aspose OCR في C#. تعلم استخراج النص
  من الصورة، تشغيل OCR على الصورة، وتحميل الصورة لـ OCR مع تسريع GPU.
draft: false
keywords:
- how to run OCR
- extract text from image
- run OCR on image
- load image for OCR
- Aspose OCR tutorial
language: ar
og_description: كيفية تشغيل OCR على صورة باستخدام Aspose OCR. يوضح هذا الدرس كيفية
  استخراج النص من الصورة، تشغيل OCR على الصورة، وتحميل الصورة لـ OCR بكفاءة.
og_title: كيفية تشغيل OCR في C# – دليل كامل خطوة بخطوة
tags:
- OCR
- C#
- Aspose
title: كيفية تشغيل OCR في C# – دليل كامل مع Aspose OCR
url: /ar/net/text-recognition/how-to-run-ocr-in-c-complete-guide-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR في C# – دليل كامل مع Aspose OCR

هل تساءلت يومًا **كيف تشغّل OCR** على صورة وتستخرج النص دون أن تفقد أعصابك؟ لست وحدك. سواءً كنت تقوم برقمنة الفواتير، أو مسح الإيصالات، أو مجرد محاولة لإنشاء ملف PDF قابل للبحث، فإن القدرة على استخراج النص من الصورة هي حاجة يومية للعديد من المطورين.  

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يُظهر **كيف تشغّل OCR على ملفات الصور** باستخدام مكتبة Aspose OCR، مع تسريع باستخدام GPU للسرعة. بنهاية الدرس ستعرف بالضبط كيف تُحمّل الصورة لـ OCR، وتضبط استخدام الذاكرة، وتحصل على نصوص نظيفة—كل ذلك في بضع دقائق من الشيفرة.

## ما ستتعلمه

- كيفية تهيئة محرك Aspose OCR في C#  
- كيفية **load image for OCR** من القرص أو من تدفق  
- كيفية تمكين تسريع GPU وتحديد حد ذاكرة GPU  
- كيفية **extract text from image** والتحقق من النتيجة  
- المشكلات الشائعة (غياب وحدة GPU، حدود الذاكرة) وحلول سريعة  

لا تحتاج إلى أي خبرة سابقة مع Aspose OCR؛ فقط بيئة .NET جاهزة وصورة نموذجية.

---

## How to Run OCR on an Image with Aspose OCR

الخطوة الأولى التي تحتاجها هي مقطع شفرة واضح وقابل للتنفيذ يقوم بكل المهمة. إليك البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله فورًا.

```csharp
// ------------------------------------------------------------
// Complete C# program: How to Run OCR with Aspose OCR
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Config;
using System.Drawing;          // For Image handling (optional)

// 1️⃣ Initialize the OCR engine
var ocrEngine = new OcrEngine();

// 2️⃣ Enable GPU acceleration (requires the Aspose OCR GPU module)
//    This speeds up recognition dramatically on supported hardware.
ocrEngine.Config.EnableGpuAcceleration = true;

// 3️⃣ (Optional) Limit GPU memory usage to 1024 MB to avoid OOM errors
ocrEngine.Config.GpuMemoryLimit = 1024;

// 4️⃣ Load the image you want to process
//    Replace the path with your own image file.
string imagePath = "YOUR_DIRECTORY/sample_skewed.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

// 5️⃣ Run the OCR recognition
ocrEngine.Recognize();

// 6️⃣ Retrieve the plain‑text result and display it
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**الناتج المتوقع** (بافتراض أن الصورة النموذجية تحتوي على العبارة “Hello World”):

```
=== OCR Result ===
Hello World
```

> **Pro tip:** إذا لم ترى أي نص، تحقق مرة أخرى من أن وحدة GPU مثبتة وأن مسار الصورة صحيح. طريقة `ImageStream.FromFile` تُطلق استثناء واضح إذا تعذر العثور على الملف.

---

## Extract Text from Image Using GPU Acceleration

لماذا نحتاج إلى GPU أصلاً؟ OCR على المعالج فقط يعمل، لكنه قد يكون بطيئًا جدًا على الصور الكبيرة أو عالية الدقة. تمكين تسريع GPU (الخطوة 2 أعلاه) ينقل العبء الثقيل إلى بطاقة الرسوميات، التي يمكنها معالجة آلاف البكسلات في الثانية.

### متى تستخدم GPU

- **معالجة دفعات** – مسح عشرات الفواتير مرة واحدة.  
- **مسحات عالية الدقة** – أي شيء فوق 300 dpi.  
- **تطبيقات الوقت الحقيقي** – مثل ماسح هاتف محمول يحتاج إلى رد فعل فوري.

إذا لم يكن لديك GPU متوافق، ما عليك سوى ضبط `EnableGpuAcceleration = false;` وسيتحول المحرك تلقائيًا إلى وضع المعالج.

---

## Run OCR on Image – Loading the Image Correctly

تحميل الصورة هو خطوة **load image for OCR** التي تُربك الكثيرين. Aspose OCR يتوقع `ImageStream`، يمكن إنشاؤه من ملف، أو تدفق ذاكرة، أو حتى URL. إليك بعض الأنماط:

```csharp
// Load from file (as shown earlier)
ocrEngine.Image = ImageStream.FromFile("path/to/file.jpg");

// Load from a byte array (useful for web uploads)
byte[] imageBytes = File.ReadAllBytes("uploaded_image.png");
ocrEngine.Image = ImageStream.FromBytes(imageBytes);

// Load from a remote URL (requires internet)
ocrEngine.Image = ImageStream.FromUrl("https://example.com/image.tif");
```

**Edge case:** بعض الصور تحتوي على قناة ألفا (شفافية) تُربك محرك OCR. إزالة الشفافية سهل:

```csharp
using (var bitmap = new Bitmap(imagePath))
{
    var nonAlpha = new Bitmap(bitmap.Width, bitmap.Height, System.Drawing.Imaging.PixelFormat.Format24bppRgb);
    using (var g = Graphics.FromImage(nonAlpha))
    {
        g.DrawImage(bitmap, 0, 0, bitmap.Width, bitmap.Height);
    }
    ocrEngine.Image = ImageStream.FromBitmap(nonAlpha);
}
```

الآن غطيت أكثر الطرق شيوعًا لـ **load image for OCR**، مما يضمن أن المحرك يتلقى تنسيقًا نظيفًا ومدعومًا في كل مرة.

---

## Tips for Loading Image for OCR Efficiently

1. **Resize large images** – OCR لا يحتاج إلى صورة بدقة 4 K؛ تقليل العرض إلى ~1500 px يسرّع العملية دون الإضرار بالدقة.  
2. **Convert to grayscale** – يقلل الضوضاء ويمكن أن يحسّن التعرف على المسحات منخفضة التباين.  
3. **Pre‑process with deskew** – إذا كانت الصورة مائلة، يمكن تمكين تصحيح الميل المدمج في Aspose OCR عبر `ocrEngine.Config.EnableDeskew = true;`.  

هذه التعديلات مفيدة خاصةً عندما تقوم بـ **extract text from image** على نطاق واسع.

---

## Common Pitfalls & How to Fix Them

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| `System.DllNotFoundException: Aspose.OCR.Gpu.dll` | وحدة GPU غير مثبتة | قم بتثبيت حزمة Aspose OCR GPU أو عطل GPU (`EnableGpuAcceleration = false`). |
| ناتج فارغ | مسار الصورة غير صحيح أو تنسيق غير مدعوم | تحقق من مسار `ImageStream.FromFile`؛ جرّب التحميل من بايتات للتأكد من قراءة الملف بشكل صحيح. |
| خطأ نفاد الذاكرة | حد ذاكرة GPU منخفض جدًا للدفعة الكبيرة | زيادة `GpuMemoryLimit` (مثلاً 2048) أو معالجة الصور على دفعات أصغر. |
| حروف مشوشة | الصورة تحتوي على ضوضاء شديدة أو تباين منخفض | معالجة مسبقة: تحويل إلى ثنائي، إزالة البقع، أو زيادة DPI قبل OCR. |

---

## Full Working Example – Put It All Together

فيما يلي تطبيق Console مختصر يجمع أفضل الممارسات التي ناقشناها: تسريع GPU، تحديد حد الذاكرة، معالجة مسبقة للصور، ومعالجة الأخطاء.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Config;

class Program
{
    static void Main()
    {
        try
        {
            // Initialize OCR engine
            var ocr = new OcrEngine();

            // Enable GPU (set false if no GPU)
            ocr.Config.EnableGpuAcceleration = true;
            ocr.Config.GpuMemoryLimit = 1024;          // 1 GB limit
            ocr.Config.EnableDeskew = true;            // Auto‑deskew

            // Load and optionally preprocess image
            string path = "YOUR_DIRECTORY/sample_skewed.jpg";
            using (var original = new Bitmap(path))
            {
                // Resize if too large
                const int maxWidth = 1500;
                Bitmap processed = original.Width > maxWidth
                    ? new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width))
                    : new Bitmap(original);

                // Convert to grayscale (optional but often helpful)
                var gray = new Bitmap(processed.Width, processed.Height, System.Drawing.Imaging.PixelFormat.Format24bppRgb);
                using (var g = Graphics.FromImage(gray))
                {
                    var cm = new System.Drawing.Imaging.ColorMatrix(
                        new float[][]{
                            new float[]{0.3f,0.3f,0.3f,0,0},
                            new float[]{0.59f,0.59f,0.59f,0,0},
                            new float[]{0.11f,0.11f,0.11f,0,0},
                            new float[]{0,0,0,1,0},
                            new float[]{0,0,0,0,1}});
                    var ia = new System.Drawing.Imaging.ImageAttributes();
                    ia.SetColorMatrix(cm);
                    g.DrawImage(processed, new Rectangle(0,0,processed.Width,processed.Height),
                                0,0,processed.Width,processed.Height, GraphicsUnit.Pixel, ia);
                }

                // Feed the processed bitmap into OCR
                ocr.Image = ImageStream.FromBitmap(gray);
            }

            // Run recognition
            ocr.Recognize();

            // Output result
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocr.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR: {ex.Message}");
        }
    }
}
```

تشغيل هذا البرنامج يطبع النص النظيف المستخرج من صورتك، موضح طريقة قوية لـ **extract text from image** حتى عندما لا تكون الصورة مثالية.

---

## Conclusion

لقد غطينا **how to run OCR** على صورة باستخدام Aspose OCR، من تهيئة المحرك إلى تحميل الصورة، تمكين تسريع GPU، ومعالجة الحالات الخاصة. الآن لديك مرجع موثوق يمكنك نسخه‑لصقه في أي مشروع .NET والبدء فورًا في **extracting text from image**.

ما الخطوة التالية؟ جرّب معالجة صفحات PDF، جرب لغات مختلفة (اضبط `ocrEngine.Config.Language = "spa"` للإسبانية)، أو دمج هذا التدفق في واجهة ويب API تعالج التحميلات مباشرة. السماء هي الحد، ومع الأدوات التي ناقشناها، أنت مجهز تمامًا لمواجهة أي تحدي OCR.

برمجة سعيدة، ولتكن نصوصك دائمًا نظيفة وOCR سريعًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}