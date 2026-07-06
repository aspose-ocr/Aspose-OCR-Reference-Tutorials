---
category: general
date: 2026-03-05
description: كيفية استخدام OCR في C# لاستخراج النص من صور الإيصالات. تعلم كيفية تحميل
  الصورة لـ OCR والتعرف على صورة الإيصال في دقائق.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من الإيصالات. اتبع هذا الدليل
  خطوة بخطوة لتحميل صورة للـ OCR والتعرف على صورة الإيصال بكفاءة.
og_title: كيفية استخدام OCR في C# – استخراج نص الفاتورة بسرعة
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: كيفية استخدام OCR في C# – استخراج النص من الإيصالات بسرعة
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الإيصالات بسرعة

هل تساءلت يومًا **كيفية استخدام OCR** لاستخراج البيانات مباشرةً من صورة إيصال بقالة؟ لست وحدك. في العديد من تطبيقات الأعمال الصغيرة، تكون العقبة هي تحويل صورة PNG غير واضحة إلى نص منظم يمكنك العمل به فعليًا.  

الخبر السار؟ ببضع أسطر من C# و Aspose.OCR يمكنك **تحميل الصورة للـ OCR**، تشغيل المحرك، و **التعرف على صورة الإيصال** في أقل من دقيقة. أدناه ستجد مثالًا كاملًا جاهزًا للتنفيذ، بالإضافة إلى نصائح للأجزاء الصعبة التي يتجاوزها معظم الدروس.

## ما يغطيه هذا الدليل

سنستعرض كل ما تحتاج إلى معرفته:

* تثبيت حزمة NuGet الخاصة بـ Aspose.OCR.  
* إعداد محرك OCR – جوهر **كيفية استخدام OCR** بشكل صحيح.  
* تحميل ملف الإيصال (هذه هي خطوة **تحميل الصورة للـ OCR**).  
* تشغيل عملية التعرف واستخراج كل من بيانات التخطيط بصيغة JSON و XML.  
* معالجة المشكلات الشائعة مثل فقدان الترخيص أو صيغ الصور غير المدعومة.  

في النهاية ستحصل على برنامج مستقل يستخرج النص من أي إيصال تضعه في مجلد. لا خدمات خارجية، لا سحر مخفي.

## المتطلبات المسبقة

* .NET 6 SDK أو أحدث (الكود يتوافق أيضًا مع .NET Core).  
* ملف ترخيص Aspose.OCR صالح (`Aspose.OCR.lic`). يمكنك الحصول على نسخة تجريبية مجانية من Aspose إذا لم يكن لديك أحد بعد.  
* صورة إيصال نموذجية – `receipt.png` تعمل جيدًا، لكن أي صيغة نقطية شائعة ستفي بالغرض.  

إذا كان لديك كل ذلك، رائع – لنبدأ.

![مثال على كيفية استخدام OCR](https://example.com/ocr-receipt.png "مثال على كيفية استخدام OCR")

## الخطوة 1: تثبيت Aspose.OCR وإنشاء مشروع جديد

أولًا: تحتاج إلى المكتبة التي تقوم بالعمل الشاق فعليًا. افتح طرفية في مجلد مشروعك وشغّل الأمر التالي:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

هذا الأمر يُنشئ تطبيقًا من نوع console ويضيف أحدث حزمة Aspose.OCR. في تجربتي، جعل اسم المشروع قصيرًا يجعل المسارات المُولدة أسهل للقراءة، خاصةً عندما تبدأ في التعامل مع عدة تطبيقات تجريبية.

## الخطوة 2: تهيئة محرك OCR – قلب **كيفية استخدام OCR**

الآن سنكتب الكود الذي يجيب على سؤال “**كيفية استخدام OCR** في C#”. افتح `Program.cs` واستبدل محتوياته بالمقتطف أدناه. لاحظ التعليقات – فهي تشرح *السبب* وراء كل سطر، وليس فقط *ما* يفعله.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### لماذا يعمل هذا

* **`OcrEngine`** هو نقطة الدخول؛ يحتفظ بكل الإعدادات التي قد تحتاج لتعديلها لاحقًا (اللغة، DPI، إلخ).  
* **`SetLicense`** يزيل علامة الماء التجريبية – خطوة حاسمة عندما تخطط لنشر الكود.  
* **`ImageStream.FromFile`** يقوم بعمل **تحميل الصورة للـ OCR**، مع معالجة PNG، JPEG، BMP، TIFF، وأكثر.  
* **`Recognize()`** هي الطريقة التي فعليًا **تتعرف على صورة الإيصال**. تحت الغطاء تقوم بالتحويل إلى ثنائي، التجزئة، وتصنيف الأحرف.  
* تصدير النتائج إلى JSON و XML يمنحك كلًا من نسخة قابلة للقراءة للإنسان وبنية صديقة للآلة يمكنك تمريرها إلى معالجات لاحقة.

## الخطوة 3: تشغيل العرض والتحقق من الناتج

قم بالترجمة والتنفيذ:

```bash
dotnet run
```

إذا تم ربط كل شيء بشكل صحيح، سترى شيئًا مشابهًا لـ:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

تطبع وحدة التحكم النص العادي، بينما يحتوي `receipt.json` و `receipt.xml` على معلومات تخطيط مفصلة (الإحداثيات، درجات الثقة، إلخ). هذه الملفات مفيدة إذا احتجت إلى ربط كل سطر بحقل قاعدة بيانات لاحقًا.

## الحالات الخاصة والنصائح المتقدمة

### 1️⃣ الترخيص مفقود أو غير صالح
إذا فشل `SetLicense`، يعود المحرك إلى وضع التجربة وستظهر علامة ماء في الناتج. غلف الاستدعاء بـ try/catch وسجّل رسالة ودية:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ صيغ الصور غير المدعومة
يدعم Aspose.OCR معظم الصيغ النقطية، لكن إذا قمت بتمرير PDF أو TIFF متعدد الصفحات ستحتاج أولًا إلى تحويل الصفحة المطلوبة إلى صورة. يمكن لمكتبة `Aspose.PDF` التعامل مع هذا التحويل.

### 3️⃣ إيصالات كبيرة وأداء
معالجة صورة بحجم 10 ميغابايت قد تكون بطيئة. قلل الدقة قبل تمريرها إلى المحرك:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

طريقة `Resize` تحافظ على نسبة الأبعاد (`0` للارتفاع) وتقلل حجم الملف بشكل كبير دون التضحية بدقة OCR للإيصالات النموذجية.

### 4️⃣ مشاكل اللغة والخط
قد تحتوي الإيصالات على أحرف خاصة (€, ¥، إلخ). عيّن اللغة صراحة إذا كنت تعرف الإعداد المحلي:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

لإيصالات متعددة اللغات، يمكنك تمكين وضع متعدد اللغات:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ استخراج البيانات المهيكلة
النص الخام مفيد، لكن معظم التطبيقات تحتاج إلى حقول مهيكلة (التاريخ، الإجمالي، العناصر). يتضمن تخطيط JSON إحداثيات `BoundingBox` لكل كلمة. يمكنك معالجته لاحقًا هكذا:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

هذا المقتطف يوضح الفكرة؛ في بيئة الإنتاج ربما تستخدم تعبيرًا نمطيًا أو محرك قواعد صغير.

## الأسئلة المتكررة

**س: هل يمكن تشغيل هذا على Linux؟**  
ج: بالتأكيد. Aspose.OCR متعدد المنصات؛ فقط قم بتثبيت بيئة تشغيل .NET على جهاز Linux وستعمل الشيفرة نفسها.

**س: ماذا لو احتجت لمعالجة عشرات الإيصالات في الدقيقة؟**  
ج: استخدم حلقة `Parallel.ForEach` وأعد استخدام نسخة واحدة من `OcrEngine` – فهو آمن للقراءة في بيئات متعددة الخيوط. تذكر التعامل مع حدود تراخيص الاستخدام المتزامن.

**س: هل يعمل هذا مع صور هاتفية مأخوذة بزاوية؟**  
ج: المحرك يتضمن تصحيحًا بسيطًا للانحراف، لكن للصور المائلة بشدة قد تحتاج إلى معالجة مسبقة باستخدام مكتبة معالجة صور (مثل OpenCV) لتصحيح الإيصال أولًا.

## مثال كامل يعمل (انسخه‑الصقه)

فيما يلي البرنامج *الكامل* الذي يمكنك وضعه في `Program.cs`. لا تحتاج إلى ملفات أخرى سوى الترخيص وصورة إيصال.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}