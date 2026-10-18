---
category: general
date: 2026-03-26
description: Özel bir sözlük kullanarak OCR doğruluğunu artırmak için PNG dosyasında
  OCR çalıştırma ve görüntüden metin çıkarma. OCR için görüntüyü hızlıca yüklemeyi
  öğrenin.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: tr
og_description: PNG dosyasında OCR çalıştırma ve görüntüden metin çıkarma, geliştirilmiş
  OCR doğruluğu için özel sözlük kullanarak. Adım adım rehber.
og_title: OCR Nasıl Çalıştırılır – Python'da Görüntüden Metin Çıkarma
tags:
- OCR
- Python
- Image Processing
title: OCR Nasıl Çalıştırılır – Python'da Görüntüden Metin Çıkarma
url: /tr/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Nasıl Çalıştırılır – Görüntüden Metin Çıkarma Python'da

Hiç **OCR nasıl çalıştırılır** diye merak ettiniz mi, taranmış bir faturada ya da ekran görüntüsünde temiz, aranabilir metin elde etmek için? Yalnız değilsiniz. Birçok projede darboğaz sadece görüntüyü OCR için yüklemek ve ardından motoru alan‑özgü kelimeleri anlamaya ikna etmektir.  

Bu öğreticide, **görüntüden metin çıkarma** dosyalar, **PNG'den metin tanıma** varlıklarını nasıl yapacağınızı gösteren ve hatta özel sözlükler ve özel karakterlerle **OCR doğruluğunu artırma** ipuçlarını gösteren eksiksiz, doğrudan çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir Python kod tabanına ekleyebileceğiniz bağımsız bir betiğe sahip olacaksınız.

## Gereksinimler

- Python 3.8+ (kod tip ipuçları kullanıyor ancak daha eski 3.x sürümlerinde de çalışır)
- Hedeflediğiniz OCR motoru ile gelen `ocr` kütüphanesi (kurulum: `pip install ocr‑engine` – gerçek paket adıyla değiştirin)
- İşlemek istediğiniz bir görüntü dosyası (`input.png`)
- İsteğe bağlı: Alan‑özgü kelimeler içeren düz metin dosyası (`invoice_terms.txt`), satır başına bir kelime

Ağır dış bağımlılıklar yok, bulut API anahtarları yok, sadece yerel bir OCR motoru.

---

## Adım 1: OCR Kütüphanesini Kurun ve İçe Aktarın

İlk olarak, OCR paketinin kurulu olduğundan emin olun. Varsayımsal `ocr-engine` paketini kullanıyorsanız, şu komutu çalıştırın:

```bash
pip install ocr-engine
```

Şimdi ihtiyacınız olan sınıfları içe aktarın:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro ipucu:** Sanal bir ortamda çalışıyorsanız, kurulumdan önce onu etkinleştirin, böylece global Python ortamınız temiz kalır.

## Adım 2: Bir OCR Motoru Örneği Oluşturun

Bir motor nesnesi oluşturmak, her OCR görevinin giriş noktasıdır. Bunu, tarayıcı donanımını yazılım içinde açmak gibi düşünün.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Neden önemli: motor, dil paketleri, tanıma modları ve daha sonra ekleyeceğiniz özel kaynaklar gibi yapılandırmaları tutar. Onsuz **OCR için görüntü yükleme** yapamaz veya tanıma hattını çalıştıramazsınız.

## Adım 3: Tanımak İstediğiniz Görüntüyü Yükleyin

Burada gerçekten **OCR için görüntü yükleme** yapıyoruz. `Imaging.Image.load()` yöntemi dosyayı okur ve motorun beklediği iç bitmap formatına dönüştürür.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

JPEG veya TIFF dosyanız varsa, aynı yöntem çalışır—sadece uzantıyı değiştirin. Motor formatı otomatik olarak algılar.

> **Köşe durumu:** Çok büyük görüntüler (5 MP üzeri) bellek dalgalanmalarına neden olabilir. Performans sorunlarıyla karşılaşırsanız, yüklemeden önce Pillow ile ölçek küçültmeyi düşünün.

## Adım 4: Doğruluğu Artırmak İçin Özel Bir Sözlük Sağlayın

Çoğu OCR motoru genel dil modelleriyle gelir. Faturalar, makbuzlar veya yasal belgelerde sık sık eksik kelimeler görürsünüz. Özel bir kelime listesi sağlamak, motora “bu terimler geçerli, doğru olarak ele al” demektir.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Tipik girişler şöyle olabilir:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Bunları eklemek, **OCR doğruluğunu artırma** ölçütünü büyük ölçüde iyileştirir—özellikle ASCII dışı semboller için.

## Adım 5: Varsayılan Küme Tarafından Kapsanmayan Özel Karakterleri Ekleyin

Alanınız Euro işareti (€) veya İskandinav Ø gibi semboller kullanıyorsa, bunları açıkça ekleyebilirsiniz:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Motor artık bu glifleri tanıma aşamasında geçerli olarak kabul edecek, “çöp” çıktısı olasılığını azaltacaktır.

## Adım 6: OCR İşlemine Başlayın ve Metni Alın

Son olarak, tanıyıcıyı çağırın ve düz metin sonucunu alın. `recognize()` çağrısı zengin bir nesne döndürür; çoğu kullanım senaryosu için yalnızca ham dizeye ihtiyacımız var.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Beklenen çıktı** (kısaltılmış):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Çıktı bozuk görünüyorsa, özel sözlüğünüzün ve özel karakterlerin doğru yüklendiğini iki kez kontrol edin.

---

## Görsel Genel Bakış

![how to run OCR diagram](ocr-workflow.png){alt="OCR nasıl çalıştırılır diyagramı"}

Yukarıdaki diyagram, bir görüntüyü yüklemekten temiz metin elde etmeye kadar olan akışı gösterir ve özel sözlükler ile karakter kümelerini nerede ekleyebileceğinizi vurgular.

---

## Sık Sorulan Sorular & Dikkat Edilmesi Gerekenler

### Bu çok sayfalı PDF'lerle çalışır mı?

Evet—her sayfayı bir PNG'ye dönüştürün (`pdf2image` gibi bir araçla) ve aynı `ocr_engine` örneğine sırasıyla besleyin. Motor her görüntüyü bağımsız olarak işler, böylece birleştirebileceğiniz bir dize listesi elde edersiniz.

### Görüntü döndürülmüş olsaydı ne olur?

Çoğu modern OCR motoru yönelimi otomatik algılar, ancak zorla döndürmek için şu komutu kullanabilirsiniz:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### İngilizce dışındaki diller nasıl ele alınır?

Görüntüyü yüklemeden önce dil modelini değiştirin:

```python
ocr_engine.set_language("de")  # German
```

İlgili dil paketinin kurulu olduğundan emin olun.

---

## Tam Betik – Kopyala & Yapıştır İçin Hazır

Aşağıda, yer tutucu yolları değiştirdikten sonra çalıştırmaya hazır tam program yer almaktadır.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Şu şekilde çalıştırın:

```bash
python run_ocr.py
```

Çıktı olarak konsola çıkarılan metni görmelisiniz. Buradan dosyaya yazabilir, bir veritabanına besleyebilir veya sonraki NLP işlem hatlarına aktarabilirsiniz.

---

## Özet & Sonraki Adımlar

**PNG üzerinde OCR nasıl çalıştırılır**, **görüntüden metin çıkarma** ve **PNG'den metin tanıma** konularını ele aldık; ayrıca sözlükler ve özel karakterlerle **OCR doğruluğunu artırma** yollarını gösterdik.  

Sonra, şunları düşünün:

- **Toplu işleme:** Görüntü dizini üzerinde döngü.
- **Son‑işleme:** Fatura numaralarını veya tarihleri çekmek için regex kullanın.
- **Entegrasyon:** Betiği, isteğe bağlı OCR hizmetleri için bir Flask API'ye bağlayın.

Daha ileri konularla ilgileniyorsanız, OpenCV ön işleme ile **OCR için görüntü yükleme** üzerine öğreticilere göz atın veya Tesseract 4+ gibi LSTM katmanlı derin öğrenme tabanlı OCR modellerine dalın.

---

### Denemeye Devam!

`invoice_terms.txt` dosyasını tıbbi terimler listesiyle değiştirin, Yunanca karakterler ekleyin veya motoru düşük çözünürlüklü bir fotoğrafla besleyerek doğruluğun ne kadar uzayabileceğini görün. Ne kadar çok denerseniz, ön işleme, özel sözlükler ve motor ayarları arasındaki dengeyi o kadar iyi anlarsınız.

Kodlamaktan keyif alın, ve OCR sonuçlarınız her zaman net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}