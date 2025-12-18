---
date: 2025-12-09
description: تعلم مثال Aspose OCR للغة Java لاستخراج النص من الصور في مشاريع Java.
  تكامل سهل، ودقة عالية في OCR لتطبيقات Java.
linktitle: Aspose OCR Java Example – Recognizing Lines in Images
second_title: Aspose.OCR Java API
title: مثال Aspose OCR بلغة Java – التعرف على الخطوط في الصور
url: /ar/java/advanced-ocr-techniques/recognize-lines/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مثال Aspose OCR Java – التعرف على الأسطر في الصور

## المقدمة

إذا كنت بحاجة إلى **aspose ocr java example** يستخراج النص بسرعة من الصور، فقد وصلت إلى المكان الصحيح. في هذا الدرس سنستعرض برنامج Java كامل جاهز للتنفيذ يتعرف على الأسطر الفردية من النص باستخدام Aspose.OCR for Java. في النهاية ستفهم لماذا يُعد Aspose OCR خيارًا موثوقًا لمطوري Java وكيفية دمج التعرف على مستوى السطر في أي تطبيق.

## إجابات سريعة
- **ماذا يفعل المثال؟** يتعرف على سطر واحد من النص في صورة مُعطاة.  
- **ما المكتبة المطلوبة؟** Aspose.OCR for Java (أحدث نسخة).  
- **هل أحتاج إلى ترخيص؟** النسخة التجريبية المجانية تكفي للتطوير؛ يلزم ترخيص تجاري للإنتاج.  
- **هل يمكن استخراج النص من أي صيغة صورة؟** نعم – تدعم JPEG، PNG، TIFF، BMP وغيرها.  
- **كم يستغرق التنفيذ؟** حوالي 10‑15 دقيقة للنسخ، تعديل المسار، والتشغيل.

## ما هو مثال Aspose OCR Java؟
**aspose ocr java example** هو مقطع شفرة مختصر يوضح كيفية استدعاء Aspose.OCR API من Java. يُظهر الخطوات الأساسية — إعداد البيئة، تكوين إعدادات التعرف، واسترجاع النص المُتعرف عليه — لتتمكن من تكييفه في مشاريعك الخاصة.

## لماذا نستخدم Aspose OCR for Java لـ *extract text image java*؟
- **دقة عالية** – خوارزميات متقدمة تتعامل مع الصور الضوضائية أو منخفضة الدقة.  
- **دعم صيغ متعددة** – يعمل مع JPEG، PNG، TIFF، BMP، GIF، إلخ.  
- **API بسيط** – القليل من الشفرة يكفي للحصول على نتائج موثوقة.  
- **قابل للتوسع** – مناسب لأدوات سطح المكتب، الخدمات الجانبية على الخادم، أو الخلفيات المحمولة.  

## المتطلبات المسبقة
قبل البدء، تأكد من وجود ما يلي:

1. **Java Development Kit (JDK)** – الإصدار 8 أو أحدث مثبت ومُعد.  
2. **Aspose.OCR for Java library** – حمّل أحدث ملف JAR من الصفحة الرسمية [here](https://releases.aspose.com/ocr/java/).  
3. **ملف صورة** يحتوي على النص الذي تريد التعرف عليه. حدّث المتغيّر `imagePath` في الشفرة للإشارة إلى هذا الملف.

## دليل خطوة بخطوة

### الخطوة 1: استيراد الحزم
أولاً، استورد فئات Aspose.OCR المطلوبة وأدوات Java القياسية.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

### الخطوة 2: تعيين دليل المستند
عرّف المجلد الذي يحتوي على ملفات الصور الخاصة بك.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

استبدل `"Your Document Directory"` بالمسار المطلق حيث توجد صورة الاختبار الخاصة بك.

### الخطوة 3: تعيين مسار الصورة
وجه محرك OCR إلى الصورة المحددة التي تريد معالجتها.

```java
// The image path
String imagePath = dataDir + "0001460985.Jpeg";
```

يمكنك تغيير اسم الملف ليتطابق مع صورتك الخاصة.

### الخطوة 4: إنشاء مثيل API
أنشئ كائن الفئة الرئيسية OCR – هذا الكائن سيُظهر طرق التعرف.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### الخطوة 5: تكوين إعدادات التعرف
أخبر Aspose.OCR بما تتوقعه. في هذا المثال نفعّل التعرف على **سطر واحد**.

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setRecognizeSingleLine(true);
```

إذا كنت بحاجة لاكتشاف أسطر متعددة، اضبط `setRecognizeSingleLine(false)` بدلاً من ذلك.

### الخطوة 6: تنفيذ التعرف OCR
شغّل محرك OCR واطبع السطر المُتعرف عليه في وحدة التحكم.

```java
RecognitionResult result = api.RecognizePage(imagePath, settings);
System.out.println("File: " + imagePath);
System.out.println("Result line: " + result.recognitionText);
```

عند تشغيل البرنامج، يجب أن ترى مسار الملف متبوعًا بالسطر المستخرج من النص.

## المشكلات الشائعة والحلول
| المشكلة | الحل |
|-------|----------|
| **`java.lang.NoClassDefFoundError`** | تأكد من إضافة ملف JAR الخاص بـ Aspose.OCR إلى مسار الـ classpath في مشروعك. |
| **إخراج فارغ** | تحقق من أن الصورة تحتوي على سطر نص واضح وأفقي وأن `setRecognizeSingleLine(true)` يتطابق مع حالتك. |
| **صيغة صورة غير مدعومة** | حوّل الصورة إلى صيغة مدعومة (مثل JPEG أو PNG) قبل المعالجة. |
| **بطء الأداء على صور كبيرة** | قلّص أو ضغط الصورة إلى دقة معقولة (≤ 1500 px عرض) قبل تشغيل OCR. |

## الأسئلة المتكررة

**س: هل يمكن لـ Aspose.OCR التعرف على أسطر متعددة في صورة؟**  
ج: نعم. اضبط `settings.setRecognizeSingleLine(false)` لتمكين اكتشاف الأسطر المتعددة.

**س: ما صيغ الصور المدعومة؟**  
ج: JPEG، PNG، TIFF، BMP، GIF، والعديد من الصيغ الأخرى مدعومة بالكامل.

**س: ما مدى دقة استخراج النص؟**  
ج: يقدم Aspose.OCR دقة عالية بفضل محرك التعرف المملوك له، خاصةً على الصور الواضحة وعالية الدقة.

**س: هل يمكنني استخدام هذه المكتبة في تطبيق ويب؟**  
ج: بالتأكيد. نفس شفرة Java تعمل في بيئات الخادم مثل Spring Boot، Tomcat، أو أي حاوية servlet.

**س: هل تتوفر نسخة تجريبية؟**  
ج: نعم. حمّل نسخة تجريبية مجانية من موقع Aspose [here](https://releases.aspose.com/). النسخة التجريبية تشمل جميع الميزات لكنها تضيف علامة مائية صغيرة إلى الناتج.

---

**آخر تحديث:** 2025-12-09  
**تم الاختبار مع:** Aspose.OCR for Java 24.11 (أحدث نسخة وقت الكتابة)  
**المؤلف:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}