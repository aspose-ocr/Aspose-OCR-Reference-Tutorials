---
category: general
date: 2026-04-11
description: تحويل الصورة إلى JSON باستخدام Aspose OCR Cloud في C#. تعلّم كيفية التعرف
  على النص، استخراج النص من الصورة، ومعالجة الفاتورة باستخدام OCR في دقائق.
draft: false
keywords:
- convert image to json
- how to recognize text
- extract text from image
- c# ocr tutorial
- process receipt with ocr
language: ar
og_description: تحويل الصورة إلى JSON باستخدام Aspose OCR Cloud في C#. يوضح هذا الدليل
  كيفية التعرف على النص، استخراج النص من الصورة، ومعالجة الإيصال باستخدام OCR.
og_title: تحويل الصورة إلى JSON – دليل OCR بلغة C# للإيصالات
tags:
- OCR
- C#
- Aspose
- JSON
title: تحويل الصورة إلى JSON – درس OCR بلغة C# للإيصالات
url: /ar/net/text-recognition/convert-image-to-json-c-ocr-tutorial-for-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى JSON – دليل OCR بلغة C# للإيصالات

هل احتجت يوماً إلى **تحويل الصورة إلى JSON** لكن لم تكن متأكدًا من أين تبدأ؟ في هذا الدليل سنرشدك عبر دورة كاملة من البداية إلى النهاية لتقنية OCR بلغة C# التي تلتقط صورة لإيصال، تتعرف على النص، وتنتج حمولة JSON منظمة.  

إذا تساءلت يوماً *كيف يتم التعرف على النص* في مستند ممسوح ضوئياً، أو كنت تبحث عن طريقة سريعة لـ **استخراج النص من الصورة**، فأنت في المكان الصحيح. بنهاية هذا المقال ستتمكن من **معالجة الإيصال باستخدام OCR** وإرسال النتيجة مباشرة إلى واجهات برمجة التطبيقات (APIs) التابعة لك.

## ما ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل مع .NET Core أيضًا)  
- مفتاح Aspose Cloud API – يمكنك الحصول على تجربة مجانية من بوابة Aspose  
- صورة إيصال نموذجية (`receipt.jpg`) مخزنة محليًا  
- بيئة التطوير المفضلة لديك (Visual Studio، VS Code، Rider – أيًا كان)

لا تحتاج إلى أي حزم NuGet إضافية بخلاف عميل `Aspose.OCR.Cloud` الرسمي. إذا كان SDK مثبتًا لديك، فأنت جاهز للانطلاق.

## الخطوة 1 – تحويل الصورة إلى JSON: إعداد عميل OCR

أولاً، نحتاج إلى إنشاء نسخة من `CloudOcrClient`. هذا الكائن يتولى جميع عمليات التواصل مع خدمة OCR الخاصة بـ Aspose وسيعيد النتيجة بصيغة JSON.

```csharp
using Aspose.OCR.Cloud;
using System;
using System.Threading.Tasks;

class CloudDemo
{
    static async Task Main()
    {
        // 👉 Replace with your real API key – keep it secret!
        var ocrClient = new CloudOcrClient("YOUR_API_KEY");

        // The path to the receipt you want to process
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";

        // Send the image for recognition (English language in this example)
        var ocrResultJson = await ocrClient.RecognizeAsync(imagePath, Language.English);

        // Show the raw JSON response
        Console.WriteLine(ocrResultJson);
    }
}
```

**لماذا هذا مهم:** تهيئة العميل هو الجسر بين كود C# الخاص بك ومحرك OCR السحابي. طريقة `RecognizeAsync` تقوم بالعمل الشاق – ترفع الصورة، تشغل محرك OCR، وتعيد سلسلة JSON تحتوي على النص المعترف به، درجات الثقة، وإحداثيات الصناديق المحيطة.

> **نصيحة احترافية:** احفظ مفتاح API في متغير بيئي أو مدير أسرار بدلاً من تضمينه مباشرة في الكود. بهذه الطريقة تتجنب تسريبات غير مقصودة.

## الخطوة 2 – كيفية التعرف على النص من الإيصال

الآن بعد أن أصبح العميل جاهزًا، دعنا نستعرض *كيفية* التعرف على النص. يدعم Aspose OCR العديد من اللغات، لكن بالنسبة لمعظم الإيصالات اللغة الإنجليزية تكفي. إذا احتجت لغة أخرى، استبدل `Language.English` بالقيمة المناسبة من الـ enum.

```csharp
// Example: Recognize a Spanish receipt
var spanishResult = await ocrClient.RecognizeAsync(imagePath, Language.Spanish);
Console.WriteLine(spanishResult);
```

**ما الذي يحدث خلف الكواليس؟** الخدمة تشغل نموذج تعلم عميق يكتشف الأحرف، يجمعها إلى كلمات، ثم يكوّن سطورًا. الـ JSON المرتجع يبدو تقريبًا هكذا:

```json
{
  "text": "Total $12.34\nDate 04/10/2026\n...",
  "confidence": 0.97,
  "regions": [
    { "boundingBox": "10,20,200,30", "text": "Total $12.34" },
    { "boundingBox": "10,60,200,30", "text": "Date 04/10/2026" }
  ]
}
```

يمكنك تحليل هذا الـ JSON باستخدام `System.Text.Json` أو `Newtonsoft.Json` لاستخراج الحقول التي تهمك.

## الخطوة 3 – استخراج النص من الصورة وبناء JSON يدويًا (اختياري)

أحيانًا لا تريد الـ JSON الخام الذي تقدمه Aspose؛ ربما تحتاج هيكلًا مخصصًا لخدمتك اللاحقة. المثال التالي يوضح كيفية تحويل الاستجابة إلى كائن أنظف.

```csharp
using System.Text.Json;

// Define a lightweight model for the data you actually need
public class ReceiptData
{
    public string Total { get; set; }
    public string Date { get; set; }
}

// Helper method to parse the Aspose JSON
static ReceiptData ParseReceipt(string rawJson)
{
    using JsonDocument doc = JsonDocument.Parse(rawJson);
    string text = doc.RootElement.GetProperty("text").GetString();

    // Very naive parsing – just for demo purposes
    var lines = text.Split('\n', StringSplitOptions.RemoveEmptyEntries);
    var data = new ReceiptData();

    foreach (var line in lines)
    {
        if (line.Contains("Total"))
            data.Total = line.Split(' ')[1];
        else if (line.Contains("Date"))
            data.Date = line.Split(' ')[1];
    }

    return data;
}

// Inside Main after getting ocrResultJson
var receipt = ParseReceipt(ocrResultJson);
string finalJson = JsonSerializer.Serialize(receipt, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine("Custom JSON output:");
Console.WriteLine(finalJson);
```

**لماذا نعيد الصياغة؟** العديد من الـ APIs تتوقع مخططًا محددًا (مثال: `{ "total": "12.34", "date": "2026-04-10" }`). باستخلاص الحقول المطلوبة فقط، تحافظ على خفة الحمولة وتجنب تسريب بيانات OCR غير ضرورية.

## الخطوة 4 – اختبار دليل OCR بلغة C# باستخدام إيصال نموذجي

شغّل البرنامج من الطرفية:

```bash
dotnet run
```

ستظهر لك كتلتان من المخرجات:

1. الـ JSON الخام الذي أرجعته Aspose (نتيجة **تحويل الصورة إلى JSON** مباشرة من السحابة).  
2. الـ JSON المخصص الذي بنيته في الخطوة السابقة.

المخرجات النموذجية تكون كالتالي:

```
{
  "text":"Total $12.34\nDate 04/10/2026\n...",
  "confidence":0.97,
  ...
}
Custom JSON output:
{
  "Total": "$12.34",
  "Date": "04/10/2026"
}
```

إذا صادفت خطأ مثل *401 Unauthorized*، تحقق من صحة مفتاح API ومسار الصورة.

## حالات الحافة والمشكلات الشائعة

| الحالة | ما الذي يجب مراقبته | الحل المقترح |
|-----------|------------------|---------------|
| **إيصال منخفض الدقة** | انخفاض ثقة OCR إلى أقل من 0.8 | عالج الصورة مسبقًا (زيادة DPI، تحسين الحدة) قبل الإرسال |
| **حروف غير إنجليزية** | اختيار لغة غير صحيحة | استخدم `Language.AutoDetect` أو حدد اللغة الصحيحة |
| **دفعة كبيرة من الإيصالات** | أخطاء حد المعدل (Rate‑limit) | نفّذ آلية back‑off أُسِي أو اطلب حصة أعلى من Aspose |
| **حقول مفقودة** | المحلل المخصص يُعيد `null` | أضف منطق احتياطي أو أنماط regex لاستخراج أكثر موثوقية |

## نظرة بصرية

![مخطط يوضح تدفق العملية من ملف الصورة → عميل OCR → استجابة JSON → التحليل المخصص → المخرجات النهائية بصيغة JSON](https://example.com/ocr-flow-diagram.png "تحويل الصورة إلى JSON")

*نص بديل:* *مخطط تدفق تحويل الصورة إلى JSON يوضح الخطوات التي تم تغطيتها في هذا الدليل.*

## ملخص

أظهرنا لك كيفية **تحويل الصورة إلى JSON** باستخدام Aspose OCR Cloud، وشرحنا *كيفية التعرف على النص* في إيصال، وعرضنا طرقًا لـ **استخراج النص من الصورة**، ودمجنا كل ذلك في **دليل OCR بلغة C#** يمكنك إدراجه في أي مشروع .NET.  

النقاط الأساسية هي:

- إعداد `CloudOcrClient` باستخدام مفتاح API الخاص بك.  
- استدعاء `RecognizeAsync` للحصول على حمولة JSON مباشرة من الخدمة.  
- (اختياري) إعادة تشكيل تلك الحمولة لتتناسب مع عقد البيانات الخاصة بك.  

## ما التالي؟

- **المعالجة الدفعة:** كرر العملية على مجلد من الإيصالات واجمع النتائج في مصفوفة JSON واحدة.  
- **التحليل المتقدم:** استخدم تعبيرات regex أو نموذج NLP صغير لاستخراج بنود الفاتورة، الضرائب، والخصومات.  
- **التكامل:** ادفع الـ JSON النهائي إلى قاعدة بيانات، طابور رسائل، أو Azure Function لمزيد من الأتمتة.  

لا تتردد في تجربة صيغ صور مختلفة (PNG، TIFF) أو تجربة تدفق **معالجة الإيصال باستخدام OCR** على صور تم التقاطها من الهاتف. السماء هي الحد عندما يكون لديك طريقة موثوقة لـ **تحويل الصورة إلى JSON**.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}