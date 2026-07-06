---
category: general
date: 2026-06-25
description: Python OCR kullanarak görüntüden metin çıkarın. OCR için görüntüyü nasıl
  yükleyeceğinizi, Python’da OCR nasıl yapılacağını ve fişi birkaç basit adımda JSON’a
  nasıl dönüştüreceğinizi öğrenin.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: tr
og_description: Python OCR kullanarak görüntüden metin çıkarın. Bu öğretici, OCR için
  bir görüntü yüklemeyi, Python’da OCR gerçekleştirmeyi ve bir fişi JSON’a dönüştürmeyi
  adım adım gösterir.
og_title: Python'da Görüntüden Metin Çıkarma – Tam OCR Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Python'da Görüntüden Metin Çıkarma – Tam OCR Rehberi
url: /tr/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Görüntüden Metin Çıkarma – Tam OCR Rehberi

Görüntüden **metin çıkarmak** gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Bu öğreticide **OCR için görüntü yükleme**, **Python'da OCR gerçekleştirme** ve **fişi JSON'a dönüştürme** konularını adım adım göstereceğiz — sadece birkaç satır kodla.

Eğer bir fatura tarama uygulaması, harcama takibi ya da sadece veri girişini otomatikleştirmek istiyorsanız, bu akışı öğrenmenin neden bir oyun değiştirici olduğunu göreceksiniz. Sonunda, bir fatura resmini okuyup, sonraki hizmetler için hazır temiz bir JSON yükü üreten çalışan bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

`aocr` kütüphanesinin kurulumundan ham sonucun işlenmesine kadar her adımı ele alacağız. Özellikle şunları öğreneceksiniz:

1. **Create an OCR engine instance** – tüm tanıma işlemlerinin giriş noktası.  
2. **Load an image for OCR** – motorun hangi dosyayı okuyacağını belirtin.  
3. **Choose the export format** – JSON veya XML, biz JSON'u seçeceğiz çünkü tüketmesi daha kolay.  
4. **Run the recognition** – Python'da gerçekten OCR gerçekleştirin.  
5. **Print or store the result** – fişi JSON'a dönüştürün ve çıktıyı görün.

OCR konusunda önceden deneyim gerekmez; sadece temel bir Python kurulumu ve bir görüntü dosyası (fatura, broşür, ihtiyacınız olan herhangi bir şey) yeterlidir.  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="Python OCR kullanarak görüntüden metin çıkarma akışını gösteren diyagram"}

## Görüntüden Metin Çıkarma – Adım Adım Python OCR

Aşağıda tamamen hazır, çalıştırılabilir betik bulunuyor. `receipt_ocr.py` adlı bir dosyaya kopyalayıp yapıştırabilir ve `python receipt_ocr.py` komutuyla çalıştırabilirsiniz.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Neden Bu Çalışıyor

- **Engine instance** – `aocr.OcrEngine()` tüm ağır işleri (model yükleme, ön işleme vb.) kapsüller.  
- **Loading the image** – `engine.load_image()` kütüphaneye hangi bitmap'i analiz edeceğini söyler; JPEG, PNG ya da çok sayfalı PDF'leri de besleyebilirsiniz.  
- **Export format** – `engine.export_format`'ı `aocr.ExportFormat.JSON` olarak ayarlamak, sonucu yapılandırılmış bir dize haline getirir, JSON bekleyen API'ler için mükemmeldir.  
- **Recognition call** – `engine.recognize()` sahne arkasında sinir ağı çıkarımını çalıştırır; algılanan metin blokları, güven skorları ve düzen bilgilerini içeren bir JSON dizesi döndürür.  

---

## aocr ile OCR için Görüntü Yükleme

Görüntünün özel bir ön işleme ihtiyacı olup merak ediyorsanız, kısa cevap **hayır**—`aocr` çoğu yaygın durumu (kontrast ayarı, eğikliği düzeltme) otomatik olarak halleder. Ancak doğruluğu şu şekilde artırabilirsiniz:

- Görüntünün en az 300 dpi olduğundan emin olmak.  
- İlgisiz kenarları kırpmak.  
- Beslemeden önce gri tonlamaya dönüştürmek (isteğe bağlı, `engine.load_image()` sizin için yapar).  

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro ipucu:* Fatura çok fazla gürültü içeriyorsa, yukarıdaki ekstra adım **Python'da OCR gerçekleştirme** doğruluğunu belirgin bir şekilde artırabilir.

---

## Dışa Aktarım Biçimini Seçin ve Fişi JSON'a Dönüştürün

Şöyle sorabilirsiniz: “Neden sadece düz metin almıyoruz?” Çünkü JSON, hiyerarşik yapıyı (satırlar, kelimeler, sınırlama kutuları) korur. Bu, *toplam tutar* veya *tarih* gibi alanları daha sonra eşleştirmeyi çok kolaylaştırır.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Betik çalıştırıldığında, `json_result` aşağıdaki gibi görünecek (kısaltılmış olarak):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Artık **fişi JSON'a dönüştürme** yükünüz var; bunu doğrudan bir veritabanına, bir REST uç noktasına ya da bir makine‑öğrenme modeline besleyebilirsiniz.

---

## Tanıma Çalıştırma ve Sonuçları Alma

Son adım—gerçekten OCR'i çalıştırmak—`recognize()` çağrısı kadar basittir. Sahne arkasında kütüphane:

1. Görüntüyü önceden eğitilmiş bir konvolüsyonel ağdan geçirir.  
2. Ağ çıktısını okunabilir karakterlere çözer.  
3. Her şeyi seçilen formata paketler (bizim örneğimizde JSON).  

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Çıktıyı yazdırmak yerine saklamanız gerekiyorsa, sadece bir dosyaya yazın:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Köşe durum:* Bazı faturalar ASCII olmayan karakterler içerir (ör. “€” ). Yukarıda gösterildiği gibi dosyayı UTF‑8 kodlamasıyla açtığınızdan emin olun, aksi takdirde bozuk metin oluşur.

---

## Tam Çalışan Örnek (Tüm Adımlar Tek Betikte)

Her şeyi bir araya getirerek, uçtan uca çalıştırabileceğiniz son betik burada:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Şu komutla çalıştırın:

```bash
python receipt_ocr.py
```

Bir onay satırı görmeli ve aynı klasörde yapılandırılmış veriyi içeren bir `receipt_output.json` dosyası bulunmalı.

---

## Sonuç

Artık Python kullanarak **görüntüden metin nasıl çıkarılır**, **OCR için görüntü nasıl yüklenir**, **Python'da OCR nasıl gerçekleştirilir** ve **fiş nasıl JSON'a dönüştürülür** konularını biliyorsunuz. Bu uçtan uca akış hafiftir, sadece `aocr` paketine ihtiyaç duyar ve herhangi bir otomasyon hattına eklenebilir.

Sırada ne var? Dışa aktarım biçimini XML'e değiştirmeyi deneyin, farklı görüntü ön işleme teknikleriyle oynayın ya da yüklenen bir fişi kabul edip anında JSON yükü dönen küçük bir Flask API'si oluşturun. Temelleri kavradığınızda sınır yok.

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR for .NET ile Görüntüden Metin – OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR for .NET kullanarak görüntüden tablo nasıl çıkarılır](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}