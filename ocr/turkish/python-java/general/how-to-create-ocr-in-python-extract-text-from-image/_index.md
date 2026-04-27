---
category: general
date: 2026-04-26
description: OCR'yi hızlı ve güvenilir bir şekilde nasıl oluşturacağınızı öğrenin.
  Görüntüden metin çıkarmayı, OCR için görüntüyü yüklemeyi ve özel bir sözlükle PNG
  üzerinde OCR çalıştırmayı öğrenin.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: tr
og_description: Python'da OCR nasıl oluşturulur ve görüntüden metin nasıl çıkarılır.
  Bu rehber, OCR için görüntünün nasıl yükleneceğini, PNG üzerinde OCR çalıştırmayı
  ve özel bir sözlük kullanmayı gösterir.
og_title: Python'da OCR Nasıl Oluşturulur – Hızlı Metin Çıkarma
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR Nasıl Oluşturulur – Görüntüden Metin Çıkarma
url: /tr/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Nasıl Oluşturulur – Adım Adım Kılavuz

Hiç **OCR nasıl oluşturulur** diye merak ettiniz mi ve taranmış PDF'lerinizi, ekran görüntülerinizi ya da el yazısı notlarınızı okuyabilen bir OCR? Tek başınıza değilsiniz. Birçok gerçek dünya projesinde *görüntüden metin çıkarma* dosyalarına ihtiyacımız var, ancak kutudan çıkan motorlar genellikle alan‑özel kelimelerde zorlanıyor.  

Bu öğreticide, OCR için bir görüntü yükleyen, özel bir sözlük uygulayan ve sonunda **PNG dosyalarında OCR çalıştıran** eksiksiz, çalıştırılabilir bir örnek göreceksiniz. Sonuna kadar herhangi bir görüntüden metin çıkarabilecek ve motoru kendi terminolojinize uyarlayabileceksiniz.

## Bu Öğreticide Neler Kapsanıyor

* Küçük ama güçlü `aocr` paketini (veya uyumlu herhangi bir kütüphaneyi) kurmak.  
* **Özel bir sözlük** yapılandırarak `aspocorp` veya `licensekey` gibi terimlerin tanınmasını sağlamak.  
* **OCR için bir görüntü yükleme**, ister PNG, JPEG ya da taranmış bir PDF sayfası olsun.  
* OCR sürecini çalıştırmak ve sonucu yazdırmak.  

Harici dokümantasyon bağlantıları yok, sadece bugün kopyala‑yapıştır yapıp çalıştırabileceğiniz bağımsız bir çözüm.

### Önkoşullar

* Python 3.8 ve üzeri (kod f‑string'ler kullanıyor).  
* Komut satırıyla temel aşinalık – birkaç `pip install` komutu yazacaksınız.  
* Örnekteki (`technical_doc.png`) bir görüntü dosyası, referans alabileceğiniz bir yerde konumlandırılmış.  

Bu üç öğeyi karşılıyorsanız, hazırsınız.  

---

## Adım 1: OCR Kütüphanesini Kurun

İlk olarak, programlanabilir bir yapılandırma nesnesini destekleyen bir OCR motoruna ihtiyacımız var. `aocr` paketi, yerel bir OCR motoru etrafında hafif bir sarmalayıcıdır ve demolar için iyi çalışır.

```bash
# Install the library (run once)
pip install aocr
```

> **Pro ipucu:** Windows kullanıyorsanız ve bir derleme hatası alıyorsanız, önceden derlenmiş tekerlekleri içeren `pip install aocr‑binary` komutunu deneyin.

### Neden Bu Kütüphane Kurulmalı?

`aocr`, **özel bir sözlük** ekleyebileceğimiz bir `config` nesnesine doğrudan erişim sağlar. Bu, niş kelime dağarcıklarında doğruluğu artıran gizli sosdur.

---

## Adım 2: OCR Motoru Örneğini Oluşturun ve Özel Bir Sözlük Ekleyin

Şimdi motoru başlatıyoruz ve hangi kelimeleri bilinen olarak ele alması gerektiğini söylüyoruz.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Neden Özel Bir Sözlük Önemlidir

Standart OCR modelleri genel korpuslar üzerinde eğitilmiştir. Model “aspocorp” gördüğünde, bunu “aspo corp” olarak bölüp harfleri tamamen atabilir. Özel bir liste sağlayarak tanıyıcıyı ihtiyacımız olan tam yazımına yönlendiririz ve son‑işlem çabasını büyük ölçüde azaltırız.

---

## Adım 3: İşlemek İstediğiniz Görüntüyü Yükleyin

İşte **OCR için görüntü yükleme** kısmı. `Image.load` yöntemi bir yol dizesi alır ve dosya tipini otomatik olarak belirler.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Köşe durumu:** Kaynağınız çok sayfalı bir PDF ise, önce her sayfayı PNG'ye dönüştürün (ör. `pdf2image` ile) ve motorun içine tek tek besleyin.

### Daha İyi Görüntü Kalitesi İçin İpuçları

* Çözünürlüğü en az 300 dpi tutun.  
* Görüntünün dik olduğundan emin olun; gerekirse `Pillow` ile döndürün.  
* Renkli taramaları gürültüyü azaltmak için gri tonlamaya çevirin.

---

## Adım 4: PNG Dosyasında OCR İşlemini Çalıştırın

Motor yapılandırıldı ve görüntü yüklendiğinde, sonunda **PNG üzerinde OCR çalıştırıyoruz**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

`process()` çağrısı, tanınan metni, güven skorlarını ve her kelime için sınırlayıcı kutuları içeren bir nesne döndürür.

---

## Adım 5: Tanınan Metni Çıktı Alın

Motorun ne bulduğunu görmenin en basit yolu `text` özelliğini yazdırmaktır.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Beklenen Çıktı

`technical_doc.png` dosyası *“The Aspocorp licensekey expires on 2025‑12‑31.”* cümlesini içeriyorsa, konsol şu şekilde görüntülenmelidir:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Özel sözlüğün marka adını olduğu gibi koruduğuna dikkat edin—sıradan bir OCR bunu bozmuş olabilirdi.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, `run_ocr.py` olarak kaydedilebilecek tam script yer alıyor. Yer tutucu yolu, görüntünüzün konumuyla değiştirmeniz yeterli.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Terminalden çalıştırın:

```bash
python run_ocr.py
```

Daha önceki örnekte gösterildiği gibi, çıkarılan metnin konsola yazdırıldığını görmelisiniz.

---

## Sıkça Sorulan Sorular (SSS)

| Soru | Cevap |
|----------|--------|
| **Tarama PDF'den metin çıkarabilir miyim?** | Evet. Önce her sayfayı PNG (veya TIFF) formatına dönüştürün, ardından görüntüleri aynı script'e besleyin. |
| **Görüntüm PNG yerine JPEG olursa ne olur?** | `Image.load` yöntemi JPEG, BMP, TIFF ve PNG'yi kutudan çıkar çıkmaz destekler. Sadece dosya uzantısını değiştirin. |
| **Düşük kontrastlı taramalarda doğruluğu nasıl artırırım?** | `Pillow` ile ön‑işlem yapın – kontrastı artırın, ikilileştirme uygulayın veya `opencv` ile eğikliği düzeltin. |
| **Her kelime için güven skorlarını almak mümkün mü?** | `ocr_result` içinde `words` bulunur – her kelimenin bir `confidence` özelliği vardır ve bu üzerinden döngü kurabilirsiniz. |
| **Bunu başsız (headless) bir sunucuda çalıştırabilir miyim?** | Kesinlikle. `aocr` GUI bağımlılıkları içermez, CI pipeline'ları için mükemmeldir. |

---

## Sonraki Adımlar ve İlgili Konular

Artık **OCR nasıl oluşturulur** ve **görüntü dosyalarından metin çıkarma** konularını bildiğinize göre, şunları keşfetmeyi düşünün:

* **Ön‑işleme teknikleri** – `load image for OCR` sadece ilk adımdır; gürültüyü azaltmak veya keskinleştirmek için `opencv` kullanın.  
* **Toplu işleme** – aranabilir bir arşiv oluşturmak için PNG'lerin bulunduğu bir dizinin üzerinden döngü yapın.  
* **Çok‑dilli destek** – Fransızca veya Almanca belgeleri okumak istiyorsanız motorun dil paketlerini ekleyin.  
* **Elasticsearch ile entegrasyon** – çıkarılan metni taranmış varlıklar üzerinde tam metin araması için indeksleyin.  

Bu uzantıların her biri, az önce ele aldığımız temel desene dayanır, bu yüzden geçiş sorunsuz olacaktır.

---

## Özet

Birkaç dakikada, özellikle PNG dosyalarında güvenilir bir şekilde **görüntü dosyalarından metin çıkaran OCR nasıl oluşturulur** sorusunu yanıtladık ve size **OCR için görüntü yükleme**, **özel bir sözlük uygulama** ve **PNG üzerinde OCR çalıştırma** işlemlerini harici hizmetler olmadan nasıl yapacağınızı gösterdik.  

Script'i çalıştırın, sözlüğü kendi jargonunuza göre ayarlayın ve herhangi bir belge‑dijitalleştirme projesi için sağlam bir temel elde edin.  

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—yardımcı olmaktan mutluluk duyarız. Ve başarı hikayelerinizi paylaşmayı unutmayın; topluluk gerçek‑dünya örneklerinden en iyi şekilde öğrenir.  

**Belgelerinizi otomatikleştirmeye hazır mısınız?** Kodu alın, uyarlayın ve bugün pikselleri aranabilir metne dönüştürmeye başlayın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}