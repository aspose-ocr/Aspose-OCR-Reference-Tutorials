---
category: general
date: 2026-04-17
description: تعلم كيفية تنفيذ OCR في C# للتعرف على النص من الصورة، استخراج النص من
  JPG وتحويل الصورة إلى نص بسرعة.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- extract text from jpg
- convert image to text
- how to extract text
language: ar
og_description: كيف تقوم بتنفيذ OCR في C#؟ يوضح لك هذا الدليل كيفية التعرف على النص
  من الصورة، استخراج النص من ملف JPG وتحويل الصورة إلى نص في دقائق.
og_title: كيفية تنفيذ OCR في C# – التعرف على النص من الصورة
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR في C# – التعرف على النص من الصورة
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – التعرف على النص من الصورة

هل تساءلت يومًا **كيفية تنفيذ OCR** على صورة حصلت عليها من ماسح ضوئي أو هاتف؟ في العديد من المشاريع ستحتاج إلى **التعرف على النص من الصورة** — سواء كان إيصالًا، ملاحظة مكتوبة يدويًا، أو صفحة PDF تم تحويلها إلى JPEG. الخبر السار هو أنه باستخدام Aspose.OCR يمكنك **استخراج النص من jpg** وال**تحويل الصورة إلى نص** ببضع أسطر من C#.

في هذا الدرس سنستعرض العملية بالكامل، من تثبيت المكتبة إلى التعامل مع الحالات الحدية مثل اللغات المفقودة. بنهاية الدرس ستعرف بالضبط **كيفية تنفيذ OCR**، وستحصل على برنامج جاهز للتنفيذ يطبع السلسلة المستخرجة إلى وحدة التحكم. لا اختصارات غامضة مثل “انظر الوثائق” — مجرد حل كامل ومستقل.

## ما ستحتاجه

- **.NET 6+** (الكود يعمل على .NET Framework أيضًا، لكن .NET 6 هو الإصدار طويل الأمد الحالي)
- حزمة **Aspose.OCR for .NET** عبر NuGet – ثبّتها باستخدام `dotnet add package Aspose.OCR`
- ملف صورة (JPEG, PNG, BMP) تريد اختبارها – سنسميه `input.jpg`
- أي بيئة تطوير تفضلها (Visual Studio, Rider, VS Code)

هذا كل شيء. لا إعدادات إضافية، لا خدمات خارجية، ولا خطوات مخفية.

## الخطوة 1: تثبيت Aspose.OCR وإضافة مرجع

أولًا، احضر مكتبة OCR إلى مشروعك. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

الأمر يجلب أحدث نسخة مستقرة (اعتبارًا من أبريل 2026 هي **23.9.0**) ويحدّث ملف `.csproj` الخاص بك. بعد ذلك، أضف توجيه `using` في أعلى ملفك:

```csharp
using Aspose.OCR;
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فإن واجهة مدير الحزم NuGet تعمل بنفس الفعالية — فقط ابحث عن *Aspose.OCR*.

## الخطوة 2: تحميل الصورة التي تريد التعرف عليها

الآن نحتاج إلى إخبار محرك OCR أي صورة يقرأ. توفر Aspose طريقة مريحة `OcrImage.FromFile` تدعم معظم الصيغ الشائعة.

```csharp
// Step 2: Load the image you want to recognize
var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي أو احتفظ بالصورة بجوار الملف التنفيذي واستخدم مسارًا نسبيًا. إذا لم يكن الملف موجودًا، فإن الطريقة ترمي استثناء `FileNotFoundException`، يمكنك التقاطه لاحقًا.

## الخطوة 3: إنشاء محرك OCR (متوافق مع النظام الأساسي)

تختار Aspose.OCR تلقائيًا أفضل محرك أساسي لنظام التشغيل الذي تعمل عليه (Windows, Linux, macOS). إنشاءه داخل كتلة `using` يضمن التخلص السليم.

```csharp
// Step 3: Create the OCR engine (auto‑selects best engine for the platform)
using var ocrEngine = new OcrEngine();
```

لماذا `using`؟ يحتفظ المحرك بموارد أصلية (مثل الذاكرة غير المُدارة) تحتاج إلى تحريرها. نسيان التخلص قد يؤدي إلى تسرب الذاكرة، خاصةً عند معالجة العديد من الصور في حلقة.

## الخطوة 4: (اختياري) تعيين اللغة – الإنجليزية افتراضيًا

إذا كانت صورتك تحتوي على نص إنجليزي، يمكنك تخطي هذه الخطوة لأن `OcrLanguage.English` هو الافتراضي. للغات أخرى، عيّن ببساطة قيمة الـ enum المناسبة.

```csharp
// Step 4: (Optional) Specify the language – English is the default
ocrEngine.Language = OcrLanguage.English;
```

> **هل تعلم؟** يدعم Aspose.OCR أكثر من 30 لغة، بما فيها العربية، الصينية، والروسية. تبديل اللغة سهل كتغيير الـ enum.

## الخطوة 5: تشغيل عملية التعرف

استدعاء `Recognize` يقوم بالعمل الشاق — تحليل البكسل، تجزئة الأحرف، والبحث في القاموس يحدث خلف الكواليس.

```csharp
// Step 5: Run the recognition process on the loaded image
var ocrResult = ocrEngine.Recognize(ocrImage);
```

إذا لم يتمكن المحرك من العثور على أي نص، فإن `ocrResult.Text` سيكون سلسلة فارغة. قد ترغب في التحقق من `ocrResult.HasText` (قيمة Boolean) قبل المتابعة.

## الخطوة 6: استرجاع وعرض نتيجة النص العادي

أخيرًا، استخرج السلسلة واكتبها إلى وحدة التحكم. هنا حيث تقوم فعليًا **تحويل الصورة إلى نص**.

```csharp
// Step 6: Retrieve the plain‑text result and display it
string recognizedText = ocrResult.Text;
Console.WriteLine("Recognized text:");
Console.WriteLine(recognizedText);
```

سيظهر الناتج شيئًا مثل:

```
Recognized text:
Invoice #12345
Date: 04/15/2026
Total: $256.78
```

إذا كنت تحتاج النص لمعالجة إضافية (مثل حفظه إلى ملف، إدخاله في قاعدة بيانات، أو تشغيل تعبير نمطي)، فأنت بالفعل تملك النص في المتغير `recognizedText`.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في تطبيق وحدة تحكم جديد (`dotnet new console`). يتضمن معالجة الأخطاء لأكثر المشكلات شيوعًا.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the image you want to recognize
            var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.jpg");

            // 2️⃣ Create the OCR engine (auto‑selects best engine for the platform)
            using var ocrEngine = new OcrEngine();

            // 3️⃣ (Optional) Set language – English is default
            ocrEngine.Language = OcrLanguage.English;

            // 4️⃣ Run the recognition process
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // 5️⃣ Check if any text was found
            if (!ocrResult.HasText || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be extracted from the image.");
                return;
            }

            // 6️⃣ Retrieve and display the plain‑text result
            string recognizedText = ocrResult.Text;
            Console.WriteLine("Recognized text:");
            Console.WriteLine(recognizedText);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine("The specified image file was not found. Double‑check the path.");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"An unexpected error occurred: {ex.Message}");
        }
    }
}
```

> **الناتج المتوقع:** تقوم وحدة التحكم بطباعة الأحرف الدقيقة التي اكتشفها محرك OCR. إذا كانت الصورة المصدر واضحة وعالية الدقة، عادةً ما تتجاوز الدقة 95 %.

## معالجة الحالات الحدية الشائعة

### 1️⃣ الصور متعددة اللغات  
إذا كان لديك إيصال ثنائي اللغة، عيّن `ocrEngine.Language` إلى `OcrLanguage.Multilingual`. سيحاول المحرك اكتشاف كل لغة تلقائيًا.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### 2️⃣ صور منخفضة الدقة أو مائلة  
قم بمعالجة الصورة مسبقًا (تدوير، تغيير الحجم، زيادة التباين) قبل تمريرها إلى Aspose. المكتبة توفر طرق `OcrImage` مثل `Resize` و `Rotate`.

```csharp
ocrImage = ocrImage.Rotate(0.0); // placeholder – replace with actual angle if needed
```

### 3️⃣ دفعات كبيرة  
عند معالجة عشرات الملفات، أعد استخدام نفس كائن `OcrEngine` بدلاً من إنشاء كائن جديد في كل حلقة. فقط تذكر التخلص منه بعد انتهاء الدفعة.

```csharp
using var batchEngine = new OcrEngine();
foreach (var file in Directory.GetFiles(@"images", "*.jpg"))
{
    var img = OcrImage.FromFile(file);
    var result = batchEngine.Recognize(img);
    // handle result…
}
```

### 4️⃣ قيود الذاكرة على حاويات Linux  
إذا كنت تعمل داخل حاوية Docker بذاكرة RAM محدودة، عيّن `ocrEngine.MaxMemoryUsage` (إذا كانت الـ API توفر هذه الخاصية) لتجنب تعطل OOM.

## نصائح احترافية وملاحظات

- **ترميز الملف:** السلسلة المرجعة هي UTF‑16 (`string` في .NET). إذا كنت تحتاج UTF‑8 للكتابة إلى ملف، استخدم `Encoding.UTF8.GetBytes(recognizedText)`.
- **الأداء:** بالنسبة لصورة واحدة، تكلفة تهيئة المحرك لا تكاد تُذكر. بالنسبة للوظائف الضخمة، قم بالتهيئة مرة واحدة (انظر مثال الدفعة) لتقليل وقت المعالجة بحوالي ~30 %.
- **التصحيح:** إذا كان ناتج OCR مشوشًا، افحص `ocrResult.Words` (مجموعة من كائنات الكلمات الفردية) لترى درجات الثقة. الثقة المنخفضة غالبًا ما تعني أن الصورة غير واضحة.
- **الرخصة:** يعمل Aspose.OCR في وضع التقييم بدون رخصة، لكنه يضيف علامة مائية إلى النص الناتج. سجّل ملف رخصة (`Aspose.OCR.lic`) للاستخدام الإنتاجي.

## نظرة بصرية

![مثال على كيفية تنفيذ OCR في C#](ocr-example.png "مثال على كيفية تنفيذ OCR في C#")

*تُظهر لقطة الشاشة الناتج الكامل لوحدة التحكم بعد تشغيل الكود النموذجي.*

## الخلاصة

الآن لديك فهم قوي **كيفية تنفيذ OCR** في C# باستخدام Aspose.OCR، ويمكنك بثقة **التعرف على النص من الصورة**، **استخراج النص من jpg**، و**تحويل الصورة إلى نص** لأي معالجة لاحقة. يغطي المثال الخطوات الأساسية، يوضح لماذا كل جزء مهم، ويشير إلى سيناريوهات متقدمة مثل دعم متعدد اللغات ومعالجة الدفعات.

ما الخطوة التالية؟ جرّب استبدال JPEG بـ PNG، جرب `OcrLanguage.Multilingual`، أو مرّر النص المستخرج إلى خط أنابيب معالجة اللغة الطبيعية. السماء هي الحد عندما يمكنك تحويل الصور إلى سلاسل قابلة للبحث والتحرير.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}