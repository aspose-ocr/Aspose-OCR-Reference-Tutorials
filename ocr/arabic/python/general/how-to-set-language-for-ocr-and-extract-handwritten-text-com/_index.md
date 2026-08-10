---
category: general
date: 2026-03-26
description: كيفية ضبط اللغة في محرك OCR واستخراج النص المكتوب يدوياً من الصور – دليل
  خطوة بخطوة لتحويل الصورة إلى نص.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: ar
og_description: كيفية ضبط اللغة في محرك التعرف الضوئي على الحروف واستخراج الملاحظات
  المكتوبة بخط اليد من الصور. تعلم تحويل الصورة إلى نص في دقائق.
og_title: كيفية ضبط اللغة للتعرف الضوئي على الأحرف – استخراج النص المكتوب بخط اليد
  بسهولة
tags:
- OCR
- Python
- Image Processing
title: كيفية ضبط اللغة للتعرف الضوئي على الأحرف واستخراج النص المكتوب بخط اليد – دليل
  شامل
url: /ar/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ضبط اللغة لمحرك OCR واستخراج النص المكتوب يدوياً – دليل شامل

هل تساءلت يوماً **كيف تضبط اللغة** على محرك OCR الخاص بك حتى يفهم فعلاً الأحرف التي تحتاجها؟ ربما لديك صورة لقائمة بقالة، ملاحظة اجتماع، أو مخطط غير واضح ولا تستطيع استخراج النص منها. الخبر السار؟ لا تحتاج إلى دكتوراه في رؤية الحاسوب—فقط بضع أسطر من بايثون والعلامات الصحيحة.

في هذا الدرس سنستعرض الخطوات الدقيقة **لاستخراج النص المكتوب يدوياً** من ملف PNG، تحويل تلك الصورة إلى نص عادي، وسنشرح “السبب” وراء كل إعداد. بنهاية الدرس ستكون قادرًا على التعرف على الملاحظات المكتوبة يدوياً في أي مشروع، سواء كان تطبيقًا لتدوين الملاحظات أو خط أنابيب معالجة دفعات.

> **ما ستحتاجه**  
> • بايثون 3.8+ (الكود يعمل مع 3.10 أيضًا)  
> • مكتبة `ocr` (أو أي غلاف متوافق يتيح الوصول إلى `OcrEngine`)  
> • صورة نموذجية مثل `note_handwritten.png` – أي صورة تحتوي على أحرف لاتينية موسعة ستكفي.

هيا نبدأ.

---

## كيفية ضبط اللغة وتمكين التعرف على الكتابة اليدوية

أول شيء يجب القيام به هو إخبار محرك OCR بأي أبجدية يجب أن يتوقعها. إذا تخطيت هذه الخطوة، سيعود المحرك إلى مجموعة عامة غالبًا ما تُخطئ في التعرف على الأحرف ذات اللكنات أو الرموز الخاصة.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**لماذا هذا مهم:**  
- **ExtendedLatin** يغطي أحرفًا مثل “ñ”، “ø”، و “ç”، وهي شائعة في العديد من الملاحظات الأوروبية.  
- العلامة `recognize_handwritten` تُحوّل النموذج الأساسي من OCR النص المطبوع إلى شبكة عصبية مدربة على الخطوط المتصلة. بدونها، يعتبر المحرك خربشاتك ضوضاء.

> **نصيحة احترافية:** إذا كنت تعالج مستندات بعدة لغات، أنشئ محركًا منفصلًا لكل لغة أو غيّر `ocr_engine.language` ديناميكيًا قبل كل استدعاء. هذا يُجنبك تحميل مجموعات أحرف غير مستخدمة.

![لقطة شاشة لتكوين محرك OCR تُظهر كيفية ضبط اللغة](/images/ocr-set-language.png "كيفية ضبط اللغة على محرك OCR")

*نص بديل للصورة: “كيفية ضبط اللغة على شاشة تكوين محرك OCR.”*

---

## استخراج النص المكتوب يدوياً من صورة PNG

الآن بعد أن علم المحرك ما يبحث عنه، حان الوقت لتزويده بصورة. طريقة `recognize_image` تُعيد كائن نتيجة غني؛ الخاصية `text` تحتوي على السلسلة النصية التي تهمك.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

عند تشغيل السكريبت، يجب أن ترى شيئًا مشابهًا لـ:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

هذا الإخراج يثبت أنك نجحت في **تحويل الصورة إلى نص** وأن المحرك احترم إعداد اللغة الذي قدمته.

**أخطاء شائعة**  
- **مسار غير صحيح** – تحقق مرة أخرى من موقع الملف؛ فقد يؤدي ملف مفقود إلى رفع استثناء `FileNotFoundError`.  
- **صورة منخفضة الدقة** – OCR للكتابة اليدوية يواجه صعوبة تحت 300 dpi. قم بزيادة الدقة أو أعد المسح إذا كان الإخراج مشوشًا.  
- **عكس الألوان** – إذا كان الخلفية داكنة والحبر فاتح، عكس الألوان أولًا (`Pillow` يمكنه المساعدة).

---

## تحويل الصورة إلى نص باستخدام دالة مساعدة

إذا كنت تخطط لتشغيل OCR على عشرات الملفات، غلف المنطق داخل دالة قابلة لإعادة الاستخدام. هذا يجعل الكود أسهل للاختبار وللتكامل مع خطوط أنابيب أخرى.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

الدالة المساعدة تعزل منطق **كيفية استخراج النص المكتوب يدوياً**، بحيث يمكنك استدعاؤها من نقطة نهاية Flask، أداة سطر أوامر، أو مهمة دفعة دون إعادة كتابة الإعدادات في كل مرة.

---

## التعرف على الملاحظات المكتوبة يدوياً في سيناريوهات واقعية

فيما يلي بعض الحالات التي قد تحتاج فيها إلى **التعرف على الملاحظات المكتوبة يدوياً** وكيف يتكيف هذا الإعداد:

| السيناريو | لماذا اللغة مهمة | تعديل مقترح |
|----------|-------------------|------------|
| **قوائم البقالة متعددة اللغات** | قد تحتوي العناصر على لهجات (مثال: “crème”) | غيّر `ocr_engine.language` لكل قائمة أو استخدم `ocr.Language.AutoDetect` إذا كان مدعومًا |
| **صور السبورة الصفية** | الطباشير قد ينتج خطوطًا باهتة | زد تباين الصورة قبل تمريرها إلى المحرك |
| **الوصفات الطبية** | الخط اليدوي فوضوي جدًا | اجمع OCR مع قاموس تصحيح إملائي لأسماء الأدوية |

في كل حالة، الخطوات الأساسية—**كيفية ضبط اللغة**، تمكين وضع الكتابة اليدوية، واستدعاء `recognize_image`—تبقى هي نفسها. هذه الثباتية هي ما يجعل النهج قويًا وسهل الصيانة.

---

## الحالات الحدية والتعديلات المتقدمة

1. **معالجة دفعات** – حمّل المحرك مرة واحدة، كرّر عبر الملفات، وغيّر خاصية `language` فقط عند الحاجة. هذا يقلل من عبء التهيئة.  
2. **الخطوط غير اللاتينية** – إذا احتجت معالجة سيريالية أو عربية، استبدل `ExtendedLatin` بالعدد المناسب (مثال: `ocr.Language.Cyrillic`). النمط نفسه يُطبق.  
3. **التعرف الجزئي** – أحيانًا يُعيد المحرك سلاسل فارغة لخطوط قصيرة جدًا. فحص سريع (`if not result.text.strip(): …`) يتيح لك الانتقال إلى نموذج ثانوي أو طلب إعادة المسح من المستخدم.  
4. **تحليل الأداء** – للمجموعات الكبيرة، قس زمن استدعاء `recognize_image`. إذا أصبح عنق زجاجة، فكر في التوازي باستخدام `concurrent.futures.ThreadPoolExecutor`.

---

## مثال كامل يعمل

فيما يلي السكريبت الكامل الذي يمكنك نسخه‑لصقه في ملف باسم `handwritten_ocr.py`. يتضمن تحليلًا للوسائط بحيث يمكنك توجيهه إلى أي صورة من سطر الأوامر.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

شغّله هكذا:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

يجب أن ترى نفس الإخراج كما في المقتطف السابق، مؤكدًا أنك نجحت في **تحويل الصورة إلى نص** و**التعرف على الملاحظات المكتوبة يدوياً**.

---

## الخلاصة

غطّينا **كيفية ضبط اللغة** على محرك OCR، فعلنا علامة النص المكتوب يدوياً، وبنينا دالة قابلة لإعادة الاستخدام **لاستخراج النص المكتوب يدوياً** من أي صورة. باتباع الخطوات أعلاه يمكنك بثقة **تحويل الصورة إلى نص**، سواء كنت تتعامل مع ملاحظة واحدة أو أرشيف ضخم من المستندات الممسوحة.

الخطوة التالية، جرّب تجربة حزم لغات مختلفة، عالج مجلدًا من الصور دفعةً، أو دمج هذا المنطق في خدمة ويب تُعيد نتائج JSON. الأساسيات تبقى نفسها، ومرونة مكتبة `ocr` تسمح لك بالتكيف مع أي حالة استخدام تقريبًا.

هل لديك أسئلة حول الحالات الحدية، الأداء، أو توسيع السكريبت إلى لغات أخرى؟ اترك تعليقًا أو راسلني على GitHub – برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}