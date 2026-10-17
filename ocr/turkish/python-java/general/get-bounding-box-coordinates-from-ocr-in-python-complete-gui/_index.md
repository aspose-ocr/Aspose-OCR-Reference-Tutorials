---
category: general
date: 2026-06-22
description: Python kullanarak görüntülerden sınırlayıcı kutu koordinatlarını alın.
  Aspose OCR ve JSON ayrıştırmasıyla dakikalar içinde Python’da görüntüden metin çıkarmayı
  öğrenin.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: tr
og_description: Python kullanarak görüntülerden sınırlama kutusu koordinatlarını alın.
  Bu rehber, Aspose OCR ile Python’da görüntüden metin çıkarmayı ve düzen verilerini
  ayrıştırmayı gösterir.
og_title: Python'da OCR'dan Sınır Kutusu Koordinatlarını Alın – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Python'da OCR'den Sınırlama Kutusu Koordinatlarını Alın – Tam Rehber
url: /tr/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR’dan Sınır Kutusu Koordinatlarını Al – Tam Kılavuz

Tar scanned bir faturadaki her kelime için **sınır kutusu koordinatlarını** almanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz. Birçok otomasyon projesinde, metni bir görüntü üzerinde vurgulamak, gizlemek ya da sonraki analizlere beslemek için konumunu bulmanız gerekir. İyi haber? Birkaç satır Python ve Aspose.OCR ile metni **ve** tam konumunu tek bir geçişte elde edebilirsiniz.

Bu öğreticide, **extract text from image python**‑stilinde metin çıkarımını gösteren uygulamalı bir örnek üzerinden ilerleyecek, ardından JSON düzen verisine dalarak bu sınır kutularını çekeceğiz. Gereksiz ayrıntı yok, sadece çalışan bir betik, her adımın neden önemli olduğuna dair açıklamalar ve yaygın tuzaklardan kaçınma ipuçları.

---

## Ne Oluşturacaksınız

Bu kılavuzun sonunda, aşağıdaki özelliklere sahip çalıştırılabilir bir Python betiğiniz olacak:

1. Bir görüntüyü (ör. bir fatura PNG’si) Aspose OCR’a yükler.
2. Motoru JSON düzen bilgisi üretmesi için yapılandırır.
3. JSON’u bir Python sözlüğüne ayrıştırır.
4. Tanınan her kelimeyi dolaşarak metnini **ve** sınır kutusu koordinatlarını yazdırır.

Ayrıca kodu çok sayfalı PDF’ler, farklı görüntü formatları ve özel koordinat sistemleri için nasıl uyarlayabileceğinizi de göreceksiniz.

### Önkoşullar

- Makinenizde Python 3.8+ yüklü olmalı.  
- Aktif bir Aspose.OCR for Python lisansı ya da ücretsiz deneme (kütüphane lisanssız da çalışır ancak filigran ekler).  
- `pip install aspose-ocr` (PyPI üzerindeki paket adı).  
- `invoice.png` adlı örnek bir görüntünün, başvurabileceğiniz bir klasörde bulunması.

Hepsi bu—ağır çerçeveler, dış hizmetler yok. Hadi başlayalım.

---

## Adım 1: Gerekli Kütüphaneleri Kurun ve İçe Aktarın

İlk olarak Aspose OCR paketinin ve yerleşik `json` modülünün kullanılabilir olduğundan emin olun. `json` modülü Python ile birlikte gelir, bu yüzden sadece Aspose’u kurmamız yeterli.

```bash
pip install aspose-ocr
```

Şimdi bunları betiğinizde içe aktarın:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Neden önemli:** `aspose.ocr`’yi içe aktarmak yüksek performanslı OCR motoruna erişim sağlar, `json` ise ham düzen dizesini yerel bir Python sözlüğüne dönüştürerek kolay gezinme imkanı verir.

## Adım 2: OCR Motorunu Oluşturun ve Görüntünüzü Yükleyin

Motor, sürecin kalbidir. Onu örnekleyip taramak istediğiniz görüntüyü işaretlersiniz.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **İpucu:** `"YOUR_DIRECTORY/invoice.png"` ifadesini gerçek dosyanıza işaret eden mutlak ya da göreli bir yol ile değiştirin. Dosya bulunamazsa Aspose `FileNotFoundError` fırlatır, bu yüzden yazımını iki kez kontrol edin.

## Adım 3: Motoru JSON Düzen Verisi Üretmesi İçin Yapılandırın

Aspose OCR, düz metin, yalnızca OCR‑JSON veya kelimeler, satırlar ve hatta tek tek karakterler için koordinatları içeren tam bir düzen JSON’u döndürebilir. **Sınır kutusu koordinatlarını** almak için düzen JSON’una ihtiyacımız var.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Neden JSON?** JSON, dil bağımsız, insan tarafından okunabilir ve Python sözlüklerine sorunsuz bir şekilde eşlenir. Düzen JSON’u, her girişin metni ve sekiz sayıdan oluşan bir `boundingBox` dizisi (dört köşe noktası) tuttuğu bir `"words"` dizisi içerir.

## Adım 4: Tanıma Çalıştırın ve Ham JSON Dizesini Alın

Şimdi OCR’ı gerçekten çalıştırıyoruz. `recognize()` metodu bir `OcrResult` nesnesi döndürür; bu nesneden JSON dizesini çıkarabiliriz.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

`layout_json`’i yazdırırsanız şöyle bir şey görürsünüz:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Köşe durum:** Bazı görüntüler OCR motoru metin algılayamazsa `"words"` dizisi boş olabilir. Bu durumda ilerlemeden önce görüntü kalitesini (kontrast, çözünürlük) kontrol edin.

## Adım 5: JSON’u Python Sözlüğüne Ayrıştırın

Yerel Python yapılarıyla çalışmak, dize manipülasyonundan çok daha kolaydır. Dizeyi dönüştürmek için `json.loads()` fonksiyonunu kullanın.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Artık `layout_data["words"]` her bir kelimeyi ve onun sınır kutusunu temsil eden sözlüklerin bir listesi.

## Adım 6: Kelimeler Üzerinde Döngü Kurun ve **Sınır Kutusu Koordinatlarını** Alın

İşte öğreticimizin çekirdeği: her kelimeyi dolaşmak, metni çıkarmak ve koordinatları yazdırmak. Bu, **sınır kutusu koordinatlarını** tam olarak aldığınız yerdir.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Örnek çıktı** (sayılar görüntünüze göre değişecektir):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Neden sekiz noktalı format?** Dört köşe (sol‑üst, sağ‑üst, sağ‑alt, sol‑alt) kelimenin etrafına bir çokgen çizebilmenizi sağlar, metin eğimli olsa bile. Sadece basit bir dikdörtgen ihtiyacınız varsa `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min` ve `height = max(y…) - y_min` hesaplayabilirsiniz.

## İsteğe Bağlı Geliştirmeler

### 1. Sınır Kutularını Basit Dikdörtgenlere Dönüştürün

Eğer sonraki aracınız sekiz nokta yerine `(x, y, width, height)` bekliyorsa, yardımcı bir fonksiyon ekleyin:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Çok Sayfalı PDF’leri İşleyin

Aspose OCR PDF akışlarını kabul edebilir. Görüntü yükleme satırını şu şekilde değiştirin:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Her sayfa için `set_page_number` metodunu döndürerek sayfa başına koordinatları toplayın.

### 3. Sınır Kutularını Görselleştirin

Orijinal görüntü üzerinde kutuları görmek istiyorsanız Pillow kullanın:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Şimdi tanınan her kelimenin etrafında kırmızı hatlar göreceksiniz—hata ayıklama ya da UI katmanları için mükemmel.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

- **JSON çok büyük olursa ne olur?** Büyük belgeler için JSON’u akış olarak işlemek ya da sayfa‑sayfa işleyerek bellek kullanımını düşük tutmayı düşünün.
- **Bazı kelimeler neden eksik?** Düşük kontrast veya el yazısı metinler OCR motorlarını zorlayabilir. Aspose’a göndermeden önce görüntüyü (kontrast artırma, ikilileştirme) ön‑işlemden geçirin.
- **Karakter‑seviyesi koordinatlar alabilir miyim?** Evet—`engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` ayarlayarak her bir karakterin kendi `boundingBox` dizisini içeren bir `"characters"` dizisi alabilirsiniz.
- **Koordinat sistemi sıfır‑tabanlı mı?** Kesinlikle. (0, 0) görüntünün sol‑üst köşesidir.

## Tam Betik – Kopyala & Çalıştır Hazır

Aşağıda, tüm adımları birleştiren eksiksiz, çalıştırılabilir bir örnek bulunuyor. `extract_bboxes.py` olarak kaydedin ve `python extract_bboxes.py` komutuyla çalıştırın.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}