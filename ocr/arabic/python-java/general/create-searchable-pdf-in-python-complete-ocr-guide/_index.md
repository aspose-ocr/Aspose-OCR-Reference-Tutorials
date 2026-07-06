---
category: general
date: 2026-06-22
description: إنشاء ملف PDF قابل للبحث في بايثون باستخدام OCR – تعلم كيفية تحويل الصورة
  إلى PDF، التعرف على نص PDF، وأتمتة سير عملك.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث في بايثون باستخدام OCR. اتبع هذا الدليل خطوة
  بخطوة لتحويل الصورة إلى PDF، التعرف على نص PDF، وأتمتة معالجة المستندات.
og_title: إنشاء ملف PDF قابل للبحث في بايثون – دليل OCR كامل
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: إنشاء ملف PDF قابل للبحث في بايثون – دليل OCR الكامل
url: /ar/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث في بايثون – دليل OCR كامل

هل احتجت يوماً إلى **إنشاء PDF قابل للبحث** من عقد ممسوح ضوئياً لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون نفس المشكلة عندما يحاولون لأول مرة تحويل صورة bitmap إلى مستند يمكن البحث فيه نصيًا. الخبر السار هو أنه باستخدام سكريبت بايثون صغير يمكنك **تحويل الصورة إلى PDF**، والسماح لمحرك OCR بالتعرف على كل كلمة، والحصول في النهاية على ملف قابل للبحث بشكل كامل.

في هذا الدرس سنستعرض العملية بالكامل، من تثبيت المكتبة المناسبة إلى معالجة الحالات الخاصة مثل المستندات متعددة الصفحات. بحلول النهاية ستكون قادرًا على **ocr image to pdf**، **recognize text pdf**، ودمج سير العمل في خطوط أنابيب أتمتة أكبر.

## ما ستحتاجه

قبل أن نبدأ، تأكد من أن لديك ما يلي على جهازك:

| المتطلب | لماذا يهم |
|-------------|----------------|
| Python 3.8 أو أحدث | صياغة حديثة وتلميحات نوعية أفضل |
| `ocr` حزمة بايثون (أو أي SDK OCR متوافق) | توفر `OcrEngine`، `ImageStream`، وإخراج PDF |
| صورة ممسوحة ضوئياً (JPEG، PNG، أو TIFF) | المصدر الذي ستقوم بتحويله |
| صلاحية كتابة إلى مجلد لإخراج PDF | حتى تتمكن من حفظ الملف المُنتج |

إذا لم تقم بتثبيت الـ SDK بعد، نفّذ:

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv .venv`) للحفاظ على نظافة الاعتمادات.

## نظرة عامة على سير العمل

1. **إنشاء مثيل لمحرك OCR** – الدماغ وراء التعرف.  
2. **تحميل الصورة** التي تريد معالجتها.  
3. **تهيئة المحرك** لإنتاج PDF قابل للبحث بدلاً من نص عادي.  
4. **تحضير تدفق في الذاكرة** سيحمل بايتات PDF.  
5. **تشغيل التعرف** – يقرأ المحرك الصورة، يستخرج النص، ويكتب PDF.  
6. **حفظ PDF على القرص** حتى يمكنك فتحه بأي عارض.

هذه هي القصة الكاملة في ستة أسطر من الشيفرة. لنفصِّل كل خطوة.

---

## إنشاء PDF قابل للبحث – دليل OCR بايثون خطوة بخطوة

### الخطوة 1: تهيئة محرك OCR

أول شيء تقوم به هو إنشاء كائن `OcrEngine`. فكر فيه كتشغيل ماسح ضوئي جاهز لقراءة صورتك.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **لماذا هذا مهم:** إنشاء المثيل للمحرك يخصص مخازن داخلية ويحمل بيانات اللغة. تخطي هذه الخطوة سيتسبب في حدوث خطأ `NoneType` لاحقًا عندما تحاول تعيين الصورة.

### الخطوة 2: تحميل الصورة التي تريد تحويلها

بعد ذلك نزود المحرك بتدفق صورة. المساعد `ImageStream.from_file` يقرأ الملف ويغلفه بصيغة يفهمها محرك OCR.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **حالة خاصة:** إذا كان المصدر لديك ملف TIFF متعدد الصفحات، استخدم `ocr.MultiPageImageStream.from_file` بدلاً من ذلك. سيعامل المحرك كل صفحة كصفحة PDF منفصلة تلقائيًا.

### الخطوة 3: إخبار المحرك بإنتاج PDF قابل للبحث

بشكل افتراضي، العديد من SDKs الخاصة بـ OCR تُنتج نصًا عاديًا. نحتاج إلى تغيير صيغة الإخراج إلى PDF بحيث يكون الملف الناتج بصريًا وقابلًا للبحث.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **ما الذي يحدث خلف الكواليس؟** الآن يدمج المحرك طبقة نصية غير مرئية خلف الصورة النقطية، مما يتيح لك البحث عن الكلمات كما في PDF أصلي.

### الخطوة 4: تحضير تدفق في الذاكرة لبيانات PDF

بدلاً من الكتابة مباشرة إلى القرص، نلتقط PDF في `MemoryStream`. هذا يحافظ على سرعة الإدخال/الإخراج ويسمح لك بتمرير البايتات إلى مكان آخر (مثل رفعها إلى S3) إذا رغبت.

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### الخطوة 5: تشغيل التعرف وكتابة PDF

الآن يحدث العمل الشاق. استدعاء `recognize` يقرأ الصورة، ينفذ OCR، ويُرسل PDF القابل للبحث إلى `pdf_stream`.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **مشكلة شائعة:** نسيان استدعاء `engine.recognize` سيترك `pdf_stream` فارغًا، ومحاولة حفظه ستثير خطأ `ValueError`. تحقق دائمًا من `pdf_stream.length` إذا كنت بحاجة للتأكد من إنتاج البيانات.

### الخطوة 6: حفظ PDF المُنتج إلى ملف

أخيرًا، نقوم بتفريغ البايتات من تدفق الذاكرة إلى القرص. يمكن فتح الملف الناتج في Adobe Reader أو Preview أو أي عارض PDF يدعم البحث النصي الكامل.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **النتيجة التي ستراها:** افتح PDF، اضغط `Ctrl+F`، اكتب كلمة تظهر في المسح الأصلي، وستلاحظ أن العارض يبرزها فورًا. هذا هو ما يميز **PDF قابل للبحث**.

## تحويل الصورة إلى PDF – تعديل الإعدادات للحصول على أفضل النتائج

إذا كان هدفك الأساسي هو مجرد **تحويل الصورة إلى PDF** دون OCR، يمكنك تخطي الخطوة 3 وتعيين صيغة الإخراج إلى `ocr.OutputFormat.IMAGE_PDF`. سيضمّن المحرك الصورة النقطية كصفحة PDF دون طبقة نصية مخفية.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

استخدم هذا الوضع عندما تحتاج إلى نسخة بصرية دقيقة ولكن لا تهتم بالبحث—ربما لأغراض الأرشفة حيث لا يلزم OCR.

## التعرف على نص PDF – إضافة حزم اللغة والتحكم في DPI

للحصول على تجربة **recognize text PDF** قوية، ضع في اعتبارك التعديلات الاختيارية التالية:

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **لماذا تعديل DPI؟** الدقة الأعلى توفر للمحرك المزيد من البكسلات للتحليل، مما يقلل الأخطاء في التعرف على المسحات منخفضة الجودة.

## PDF OCR بايثون – دمجه في خطوط أنابيب أكبر

الآن بعد أن يمكنك **python ocr pdf** في بضع أسطر، تخيل دمج هذه المنطق في API باستخدام Flask:

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

هذه النقطة النهاية الصغيرة تسمح للعميل بإرسال صورة عبر POST وتلقي **PDF قابل للبحث** فورًا—مثالية لخدمات معالجة المستندات كخدمة SaaS.

## مشاكل شائعة عند **ocr image to pdf**

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| صفحات PDF فارغة | الصورة غير محمَّلة (`engine.set_image` تم استدعاؤه بمسار خاطئ) | تحقق من المسار واستخدم `os.path.abspath` |
| لا نص قابل للبحث | صيغة الإخراج لا تزال مضبوطة على `IMAGE_PDF` | استدعِ صراحةً `set_output_format(ocr.OutputFormat.PDF)` |
| حروف مشوشة | حزمة لغة خاطئة | حمّل اللغة الصحيحة باستخدام `settings.set_language("eng")` |
| معالجة بطيئة على ملفات كبيرة | استخدام DPI الافتراضي (72) على صور عالية الدقة | زيادة DPI إلى 300 أو معالجة الصفحات دفعةً واحدةً بشكل منفصل |

## مثال كامل قابل للتنفيذ (جاهز للنسخ واللصق)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

شغّل السكريبت، افتح PDF المُنتج، وحاول البحث عن كلمة تعرف أنها موجودة في المسح الأصلي. إذا سارت الأمور بسلاسة، فقد أتقنت الآن **create searchable pdf** باستخدام بايثون.

## الخلاصة

لقد غطينا كل ما تحتاجه لإنشاء ملفات **PDF قابلة للبحث** باستخدام مكتبة OCR بايثون: تهيئة المحرك، تحميل صورة، ضبط إخراج PDF، تدفق النتيجة، وأخيرًا حفظها على القرص. كما رأيت كيفية **convert image to PDF**، وضبط **

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [التعرف على نص PDF – عمليات OCR باستخدام Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/)
- [كيفية OCR PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}