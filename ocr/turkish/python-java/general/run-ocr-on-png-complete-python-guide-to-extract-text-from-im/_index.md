---
category: general
date: 2026-01-12
description: Python ile PNG dosyalarında OCR'ı hızlıca çalıştırın. Görüntü ve faturadan
  metin nasıl çıkarılır öğrenin ve Aspose.OCR kullanarak OCR için görüntüyü yükleyin.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: tr
og_description: PNG üzerinde OCR'ı anında çalıştırın. Bu kılavuz, görüntü ve faturadan
  metin nasıl çıkarılır, OCR için görüntü nasıl yüklenir ve sonuçların JSON ve CSV
  olarak nasıl kaydedileceğini gösterir.
og_title: PNG Üzerinde OCR Çalıştırma – Tam Python Öğreticisi
tags:
- OCR
- Python
- Image Processing
title: PNG'de OCR Çalıştır – Görsellerden Metin Çıkarma İçin Tam Python Rehberi
url: /tr/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG Üzerinde OCR Çalıştırma – Görüntülerden Metin Çıkarma İçin Tam Python Rehberi

Hiç **PNG üzerinde OCR çalıştırma** ihtiyacı duydunuz ama hangi kütüphanenin temiz, yapılandırılmış sonuçlar vereceğinden emin değildiniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—fatura otomasyonu veya makbuz tarama gibi—ilk adım **görüntüden metin çıkarma**dır ve PNG, kayıpsız kalitesini koruduğu için yaygın bir formattır.

Bu öğreticide Aspose.OCR Python paketini kullanarak uygulamalı bir örnek üzerinden ilerleyeceğiz. Rehberin sonunda **OCR için görüntü yükleme**, her satırdaki metni çıkarma, bu veriyi düzenli bir JSON nesnesine dönüştürme ve hatta CSV’ye dökme konularını öğreneceksiniz. Gereksiz ayrıntı yok, sadece pratik ve hemen çalıştırılabilir bir çözüm.

## Öğrenecekleriniz

- Aspose.OCR kütüphanesini nasıl kurup içe aktaracağınızı.  
- **PNG üzerinde OCR çalıştırma** ve sonuç nesnesini nasıl yöneteceğinizi.  
- **Faturalardan metin çıkarma** ve çıktıyı JSON veya CSV olarak biçimlendirme yolları.  
- Düşük kontrastlı görüntüler, çok dilli belgeler ve güven skorlarıyla başa çıkma ipuçları.  
- Bugün çalıştırabileceğiniz tam bir kopyala‑yapıştır kod örneği.

> **Önkoşul:** Python 3.8+ ve pip hakkında temel bir bilgi. Aspose ile hiç çalışmadıysanız endişelenmeyin—bu rehber başlamanız için ihtiyacınız olan her şeyi kapsıyor.

---

## Adım 1 – Aspose.OCR’ı Kurun ve Ortamınızı Hazırlayın

**PNG üzerinde OCR çalıştırma** öncesinde kütüphanenin sisteminizde bulunması gerekir.

```bash
pip install aspose-ocr
```

> **Pro ipucu:** Bağımlılıkları izole tutmak için bir sanal ortam (`python -m venv venv`) kullanın. Bu, birden fazla projeyle uğraşırken sürüm çakışmalarını önler.

Kurulum tamamlandıktan sonra ihtiyacımız olan modülleri içe aktarın:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Burada ağır işi yapan `asposeocr` ve daha sonra serileştirme için yerleşik `json` kütüphanesini getiriyoruz.

---

## Adım 2 – OCR Motorunu Oluşturun ve Dili Ayarlayın

OCR motoru, pikselleri gerçekten okuyan çekirdek bileşendir. Çoğu İngilizce fatura için İngilizce dil paketini kullanmak isteyeceksiniz:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Neden önemli:** Dili belirtmek karakter kümesini daraltır, bu da doğruluğu artırır ve işleme süresini kısaltır. Çok dilli faturalarla çalışmanız gerektiğinde sadece `ocr.Language.ENGLISH` yerine uygun enum değerini kullanın.

---

## Adım 3 – OCR İçin Görüntüyü Yükleyin

Şimdi **OCR için görüntü yükleme** işlemini yapacağız. `Image.load` yöntemi bir dosya yolu alır ve PNG, JPEG, BMP ve daha fazlasını destekler.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Köşe durumu:** PNG dosyanız olağanüstü büyükse (5 MB’ın üzerindeyse), bellek kullanımını makul tutmak için önce yeniden boyutlandırmayı düşünün. Pillow bunu tek bir satırda yapabilir:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Adım 4 – PNG Üzerinde OCR Çalıştırın ve Sonucu Yakalayın

Motor hazır ve görüntü yüklendi, şimdi **PNG üzerinde OCR çalıştırma** ve yapılandırılmış sonucu alma zamanı.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

`ocr_result` nesnesi, tanınan metin ve güven skoru (0‑100) içeren bir `OcrRegion` koleksiyonu barındırır. Bu, **faturalardan metin çıkarma** satırları için gereken ayrıntılı veriyi elde ettiğiniz yerdir.

---

## Adım 5 – Sonucu JSON’a Dönüştürün ve Güzel Bir Şekilde Yazdırın

Çoğu downstream sistem JSON’u sever, bu yüzden OCR çıktısını güzel biçimlendirilmiş bir dizeye dönüştüreceğiz.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Örnek Çıktı

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Her satırın bir güven metriği içerdiğine dikkat edin—bu, **faturalardan metin çıkarma** işlemini otomatikleştirirken düşük güvenli girdileri filtrelemek için mükemmeldir.

---

## Adım 6 – OCR Verisini CSV Olarak Kaydedin (Metin + Güven İçin Bir Satır)

CSV, elektronik tablolar veya hızlı veri içe aktarmaları için idealdir. Aspose, her şeyi bir CSV dosyasına dökmek için tek satırlık bir yöntem sunar.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Oluşturulan CSV şu şekilde görünecek:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Artık Excel, Google Sheets’te açabilir ya da bir veritabanına besleyebilirsiniz.

---

## Bonus – Düşük‑Güven Metin ve Çok‑Sayfalı PDF’lerle Baş Etme

### Güven’e Göre Filtreleme

Yalnızca yüksek güvenli satırları istiyorsanız, JSON’u dosyaya yazmadan önce filtreleyin:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Çok‑Sayfalı Belgeler

Aspose.OCR, çok‑sayfalı PNG veya PDF’de her sayfa için otomatik olarak yeni bir `page` girdisi oluşturur. Tüm sayfaları işlemek için `ocr_data["pages"]` üzerinden döngü kurmanız yeterlidir—ekstra kod gerekmez.

---

## Tam Çalışan Örnek

Aşağıda **tam script** yer alıyor; kopyalayıp yapıştırarak hemen çalıştırabilirsiniz. `YOUR_DIRECTORY` kısmını PNG dosyanızın bulunduğu klasörle değiştirin.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Script’i `python run_ocr.py` ile çalıştırın; konsolda JSON dökümünü, diskte bir CSV dosyasını ve yüksek güvenli girdilerin filtrelenmiş listesini göreceksiniz.

---

## Sıkça Sorulan Sorular

**S: Bu yöntemi bir fatura yerine taranmış bir makbuzdan metin çıkarmak için kullanabilir miyim?**  
C: Kesinlikle. Aynı iş akışı geçerli—tek yapmanız gereken `image_path`i makbuz PNG’nize yönlendirmek. Makbuz farklı bir dildeyse, `engine.language`ı ona göre değiştirin.

**S: PNG’mde döndürülmüş (rotated) metin varsa ne olur?**  
C: Aspose.OCR otomatik olarak yönü algılar, ancak inatçı durumlarda Pillow ile görüntüyü manuel olarak döndürüp motorun önüne verebilirsiniz.

**S: Aspose.OCR için ücretli bir lisansa ihtiyacım var mı?**  
C: Kütüphane, çıktıya bir filigran ekleyen ücretsiz bir değerlendirme moduna sahiptir. Üretim ortamında kullanmak için Aspose web sitesinden bir lisans almanız gerekir.

---

## Sonuç

Python kullanarak **PNG üzerinde OCR çalıştırma** için ihtiyacınız olan her şeyi ele aldık: SDK’yı kurma, görüntüyü yükleme, yapılandırılmış metin çıkarma ve sonucu JSON ya da CSV olarak kaydetme. İster basit bir script için **görüntüden metin çıkarma**, ister otomatik bir muhasebe hattı için **faturalardan metin çıkarma** yapıyor olun, yukarıdaki adımlar sağlam, üretim‑hazır bir temel sunar.

İleride şunları keşfedebilirsiniz:

- CSV çıktısını bir veritabanına entegre ederek toplu fatura depolama.  
- Tarih, tutar veya vergi kimlik numarası gibi bilgileri çekmek için düzenli ifadelerle post‑processing.  
- Faturalarınızda QR kodları varsa `ocr_engine.recognize_barcode` özelliğini kullanma.

Deneyin, güven eşiğini ayarlayın ve belge‑işleme akışınızın ne kadar kolaylaştığını izleyin. Daha fazla sorunuz veya paylaşmak istediğiniz bir kullanım senaryonuz varsa aşağıya yorum bırakın—iyi OCRlamalar!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}