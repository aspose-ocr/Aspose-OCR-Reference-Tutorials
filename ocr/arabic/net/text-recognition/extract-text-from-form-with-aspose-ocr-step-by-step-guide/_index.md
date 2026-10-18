---
category: general
date: 2026-03-23
description: استخراج النص من النموذج بسرعة باستخدام Aspose OCR. تعلّم كيفية التعرف
  على النص في المنطقة ومعالجة جزء OCR من الصورة مع مثال كامل بلغة C#.
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: ar
og_description: استخراج النص من النموذج باستخدام Aspose OCR. يوضح هذا الدرس كيفية
  التعرف على النص في المنطقة ومعالجة جزء OCR من الصورة باستخدام C#.
og_title: استخراج النص من النموذج باستخدام Aspose OCR – دليل كامل
tags:
- C#
- OCR
- Aspose
- Image Processing
title: استخراج النص من النموذج باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من نموذج باستخدام Aspose OCR – دليل خطوة بخطوة

هل احتجت يومًا إلى **استخراج النص من نموذج** لكن الصفحة بأكملها كانت فوضى صاخبة؟ لست وحدك—المطورون يتعاملون باستمرار مع ملفات PDF، الفواتير الممسوحة، أو الاستطلاعات المكتوبة يدويًا حيث يهم حقل واحد فقط. الخبر السار؟ يمكنك إخبار Aspose OCR بالتركيز فقط على الجزء الذي يهمك، متجاهلًا البقية.  

في هذا الدليل سنوضح لك بالضبط كيفية **التعرف على النص في منطقة** من نموذج ممسوح، استخراج القيمة المطلوبة، والحفاظ على باقي الصورة دون تعديل. في النهاية ستحصل على برنامج C# جاهز للتشغيل يتعامل مع **جزء OCR من الصورة** الذي يهمك، دون الحاجة إلى أي خدمات خارجية.

## ما ستحصل عليه من هذا الدرس

- تطبيق C# كامل وقابل للتنفيذ في سطر الأوامر يستخراج حقلًا من صورة نموذج.  
- شرح واضح لماذا استهداف مستطيل أسرع وأكثر دقة.  
- نصائح للتعامل مع النتائج الفارغة، إعدادات DPI المختلفة، والنماذج متعددة الصفحات.  
- قائمة مراجعة سريعة لتتمكن من تعديل الكود لمشاريعك الخاصة في دقائق.

**المتطلبات المسبقة** – ستحتاج إلى .NET 6 أو أحدث، Visual Studio 2022 (أو أي بيئة تطوير تفضلها)، واتصال بالإنترنت للمرة الأولى لجلب حزمة Aspose.OCR من NuGet. لا توجد مكتبات أخرى مطلوبة.

---

## استخراج النص من نموذج – إعداد المشروع

قبل أن نغوص في الكود، دعنا نتأكد من أن البيئة جاهزة. الخطوات بسيطة عمدًا، لأن السحر الحقيقي يحدث بمجرد إنشاء محرك OCR.

1. **إنشاء مشروع وحدة تحكم جديد**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **إضافة Aspose.OCR عبر NuGet**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **نسخ النموذج الممسوح** إلى مجلد المشروع وإعادة تسميته إلى `form.png`.  
   (إذا كان ملفك PDF، قم بتصدير الصفحة المطلوبة كـ PNG أولاً—Aspose OCR يعمل بشكل أفضل مع الصور النقطية.)

هذا كل شيء. باقي الدرس يفترض أن هذه الخطوات الثلاث قد أُنجزت.

![مثال على استخراج النص من نموذج](form-region.png "مثال على استخراج النص من نموذج")

*نص بديل للصورة: مثال على استخراج النص من نموذج يُظهر منطقة مميزة على مستند ممسوح.*

## التعرف على النص في منطقة – تعريف منطقة الاهتمام

لماذا نهتم بالمستطيل أصلاً؟ تخيل أن لديك مسحًا بحجم 2 ميغابايت لإقرار ضريبي كامل. تشغيل OCR على كل شيء يضيع دورات المعالج وقد ينتج إيجابيات كاذبة من حقول غير ذات صلة. من خلال تضييق النطاق إلى الإحداثيات الدقيقة التي تحتوي على القيمة المستهدفة، ستحصل على:

- **تقليل وقت المعالجة** حتى 80 % للصور الكبيرة.  
- **زيادة الدقة** لأن المحرك يتجاهل الرسومات المشتتة.  
- **تبسيط ما بعد المعالجة**—أنت تعرف بالضبط النص المتوقع.

يتم تعريف المستطيل بأربعة أرقام: `x`، `y`، `width`، و `height`. تُقاس هذه القيم بالبكسل من الزاوية العلوية اليسرى للصورة. إذا لم تكن متأكدًا من موقع الحقل، افتح الصورة في برنامج Paint، مرر فوق الزاوية العلوية اليسرى لقراءة قيم X/Y، ثم اسحب لقياس العرض والارتفاع.

## جزء OCR من الصورة – تحميل النموذج وتكوين المحرك

الآن بعد أن أصبحت المنطقة واضحة، دعنا نتحدث عن المحرك نفسه. `OcrEngine` هو قلب Aspose OCR. يكتشف اللغة تلقائيًا، يتعامل مع تصحيح الانحراف، ويعيد سلسلة نصية عادية. يمكنك أيضًا تعديل خصائصه—مثل `Resolution` أو `Language`—إذا كان نموذجك يستخدم نصًا غير لاتيني. بالنسبة لمعظم النماذج الإنجليزية، الإعدادات الافتراضية تعمل بشكل جيد.

فيما يلي **البرنامج الكامل المستقل** الذي يجمع كل شيء معًا. لا تتردد في نسخه ولصقه في `Program.cs` ثم الضغط على **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### النتيجة المتوقعة

إذا كان المستطيل يحيط بشكل صحيح بحقل يحتوي على النص “Invoice # 12345”، سيطبع وحدة التحكم:

```
Field value: Invoice # 12345
```

إذا كانت المنطقة فارغة أو فشل OCR، سترى:

```
Field value: [No text detected]
```

## شرح الكود خطوة بخطوة

فيما يلي نقسم البرنامج إلى أجزاء صغيرة، نشرح **السبب** وراء كل سطر، ونشير إلى الأماكن التي قد تحتاج فيها إلى تعديل الكود.

### الخطوة 1: تثبيت Aspose.OCR عبر NuGet *(H3)*

```bash
dotnet add package Aspose.OCR
```

*لماذا؟* حزمة NuGet تجمع محرك OCR الأصلي، ملفات بيانات اللغة، وملف تغليف .NET خفيف. بدونها، لا وجود لفئة `OcrEngine`.

### الخطوة 2: تهيئة OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*لماذا نستخدم `using`؟* `OcrEngine` يحتفظ بموارد غير مُدارة (ملفات DLL الأصلية، مخازن الصور). يضمن بيان `using` تحريرها، مما يمنع تسرب الذاكرة في الخدمات طويلة التشغيل.

### الخطوة 3: تحميل صورة النموذج *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*لماذا `ImageStream`؟* فهو يُجرد عملية إدخال/إخراج الملفات ويحول تلقائيًا الصيغ الشائعة (PNG، JPEG، TIFF) إلى تمثيل البت ماب الداخلي المطلوب من قبل Aspose OCR.

### الخطوة 4: تحديد المنطقة لاستخراج النص *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*لماذا `Rectangle`؟* محرك OCR يقبل `System.Drawing.Rectangle`. تسمح لك الأربعة معلمات بتحديد الحقل بدقة، مع قص باقي الصفحة.

*نصيحة:* إذا كنت بحاجة لدعم حقول متعددة، احفظ كل مستطيل في `Dictionary<string, Rectangle>` وتكرّر عبرها.

### الخطوة 5: تشغيل التعرف واسترجاع النتيجة *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*لماذا فحص `success`؟* قد يفشل OCR لأسباب مختلفة—صورة غير واضحة، لغة غير مدعومة، أو منطقة فارغة. فحص القيمة المنطقية يمنعك من العمل ببيانات غير صالحة.

### الخطوة 6: التعامل مع الحالات الحدية والمشكلات الشائعة *(H3)*

- **DPI مختلف:** إذا كان المسح بدقة منخفضة (< 150 DPI)، قم بزيادة `ocrEngine.Image.DpiX` و `ocrEngine.Image.DpiY` قبل استدعاء `Recognize`.  
- **صفحات متعددة:** بالنسبة لملفات PDF متعددة الصفحات، استخرج كل صفحة كملف PNG منفصل وكرر منطق المستطيل لكل صفحة.  
- **نص غير إنجليزي:** اضبط `ocrEngine.Language = Language.Thai;` (أو أي لغة مدعومة) قبل التعرف.  
- **تقليل الضوضاء:** `ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` يمكن أن يحسن النتائج على المسحات ذات الحبيبات.

## المضي قدمًا – تنوعات العالم الحقيقي

### استخراج حقول متعددة من نفس النموذج

إذا كنت بحاجة لاستخراج “Name”، “Date”، و “Amount” من مستند واحد، أنشئ مجموعة:

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### التكامل مع قاعدة بيانات

بعد الاستخراج، قد ترغب في تخزين النتيجة في SQL Server:

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### الأتمتة على الخادم

إذا كنت تخطط لتشغيل هذا كخدمة خلفية، غلف المنطق في طريقة `async` واستخدم `Task.Run` للحفاظ على استجابة واجهة المستخدم. تذكر ضبط `ocrEngine.ParallelProcessing = true;` لتسريع المعالجة على الأنوية المتعددة.

## الخلاصة

أصبح لديك الآن طريقة قوية وجاهزة للإنتاج **لاستخراج النص من نموذج** باستخدام Aspose OCR. من خلال التركيز على مستطيل محدد

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}