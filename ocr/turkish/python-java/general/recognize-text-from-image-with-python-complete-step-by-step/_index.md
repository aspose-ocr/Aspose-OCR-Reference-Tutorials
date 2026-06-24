---
category: general
date: 2026-06-16
description: Python OCR kullanarak görüntüden metni tanıyın. OCR için görüntüyü nasıl
  yükleyeceğinizi, yüksek doğruluk modunu nasıl ayarlayacağınızı ve görüntüyü metne
  dönüştürmek için OCR tanımasını nasıl çalıştıracağınızı öğrenin.
draft: false
keywords:
- recognize text from image
- convert image to text
- load image for ocr
- run ocr recognition
- set high accuracy mode
language: tr
og_description: Python’da görüntüden metin tanıma. Bu kılavuz, OCR için görüntünün
  nasıl yükleneceğini, yüksek doğruluk modunun nasıl ayarlanacağını ve görüntüyü metne
  dönüştürmek için OCR tanımasının nasıl çalıştırılacağını gösterir.
og_title: görselden metin tanıma – Tam Python OCR Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  headline: recognize text from image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: recognize text from image using Python OCR. Learn how to load image
    for OCR, set high accuracy mode, and run OCR recognition to convert image to text.
  name: recognize text from image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Empty Result
    text: 'Sometimes the engine returns an empty string. This usually means the image
      is too blurry or the text color blends with the background. Try:'
  - name: 2. Non‑Latin Scripts
    text: 'If your picture contains Cyrillic, Chinese, or Arabic characters, you’ll
      need to tell the OCR engine which language pack to use:'
  - name: 3. Large Batches
    text: Processing a folder of images? Wrap the core logic in a loop and reuse the
      same engine instance to avoid repeated initialization overhead.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python ile görüntüden metin tanıma – Tam Adım Adım Kılavuz
url: /tr/python-java/general/recognize-text-from-image-with-python-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin tanıma – Tam Python OCR Eğitimi

Bulut hizmeti için ödeme yapmadan **görüntüden metin tanıma** nasıl yapılır hiç merak ettiniz mi? Tek başınıza değilsiniz. İster eski makbuzları dijitalleştiriyor olun, ister ekran görüntülerinden altyazı çıkarıyor olun, bir resmi düzenlenebilir metne dönüştürmek faydalı bir beceridir.

Bu öğreticide, **OCR için görüntü yükleme**, **yüksek doğruluk modunu ayarlama** ve **OCR tanıma çalıştırma** adımlarını gösteren **tam, çalıştırılabilir bir örnek** üzerinden ilerleyeceğiz, böylece sadece birkaç Python satırıyla **görüntüyü metne dönüştürebileceksiniz**. Gereksiz ayrıntı yok, sadece hemen kopyalayıp yapıştırabileceğiniz pratik bölümler.

## Ne Oluşturacaksınız

Bu rehberin sonunda, aşağıdaki özelliklere sahip küçük bir betiğiniz olacak:

1. Bir OCR motoru örneği oluşturur.
2. Düşük çözünürlüklü resimlerde daha iyi sonuçlar için **set high accuracy mode** bayrağını etkinleştirir.
3. Diskten **OCR için görüntü yükler**.
4. **OCR tanıma çalıştırır** ve **görüntüden metin tanır**.
5. Çıkarılan dizeyi yazdırır – etkili bir şekilde **görüntüyü metne dönüştürür**.

Python 3.8+ ve biraz merakınız varsa, hazırsınız.

## Önkoşullar

- **Python 3.8 veya daha yeni** – kod, eski sürümlerin anlayamadığı tip ipuçları kullanıyor.
- `ocr` modülünü sunan bir OCR kütüphanesi (örnek, genel bir sarmalayıcıyı taklit eder; `pytesseract`, `easyocr` veya tercih ettiğiniz herhangi bir satıcı‑özel SDK ile değiştirin).
- Kontrol ettiğiniz bir klasörde `low-res.jpg` adlı düşük çözünürlüklü bir JPEG.
- (İsteğe bağlı) Bağımlılıkları düzenli tutmak için bir sanal ortam: `python -m venv venv && source venv/bin/activate`.

```bash
# Example installation for a hypothetical `ocr` package
pip install ocr-lib
```

> **Pro tip:** `pytesseract` kullanıyorsanız, Tesseract motorunu ayrı olarak kurun (`sudo apt-get install tesseract-ocr` Linux'ta, macOS'ta Homebrew).

---

## Adım 1: Görüntüden Metin Tanıma – OCR Motorunu Başlatma

İlk olarak, ağır işi üstlenecek yeni bir OCR motoru nesnesine ihtiyacımız var.

```python
# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Neden önemli:* `OcrEngine` sınıfı sonraki tüm işlemler için giriş noktasıdır. Ona beslediğiniz pikselleri yorumlayacak bir beyin gibi düşünün. Her çalıştırmada yeni bir örnek oluşturmak temiz bir durum sağlar, özellikle daha sonra **set high accuracy mode** gibi ayarları değiştirirken.

---

## Adım 2: Yüksek Doğruluk Modunu Ayarla – Düşük Çözünürlüklü Sonuçları Artır

Düşük çözünürlüklü görüntüler OCR motorlarını karıştırmasıyla ünlüdür. Yüksek doğruluk bayrağını etkinleştirmek, motorun karakterleri okumadan önce ekstra ön işleme (yukarı ölçekleme, gürültü azaltma vb.) uygulamasını sağlar.

```python
# Step 2: Enable high‑accuracy mode for better results
engine.high_accuracy = True   # <-- activates advanced preprocessing
```

> **Neden etkinleştirilmeli?** Kaynak resim grenli ya da çok küçük olduğunda, varsayılan mod harfleri kaçırabilir veya kelimeleri birleştirebilir. Yüksek doğruluk yolu, biraz hız kaybını kabul ederek doğrulukta belirgin bir artış sağlar—gecikmenin kritik olmadığı tek seferlik betikler için mükemmeldir.

---

## Adım 3: OCR için Görüntü Yükle – Dosyayı Hazırlama

Şimdi gerçekten **OCR için görüntü yükle**yoruz. `ocr.Image.load_from_file` yardımcı işlevi dosya‑g/ç ve görüntü kod çözme adımlarını soyutlar.

```python
# Step 3: Load the low‑resolution image to be processed
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/low-res.jpg")
```

*Arka planda ne oluyor?* Kütüphane JPEG'i okur, bitmap'e dönüştürür ve motor örneği içinde saklar. Bellekte zaten bir görüntünüz varsa (ör. bir web isteğinden), çoğu kütüphane ayrıca bir `from_bytes` yöntemi sunar—sadece çağrıyı değiştirin.

---

## Adım 4: OCR Tanıma Çalıştır – Çekirdek Eylem

Motor hazır ve resim yerinde olduğunda, nihayet **OCR tanıma çalıştırıyoruz**. Bu adım gerçek metin çıkarımını gerçekleştirir.

```python
# Step 4: Perform OCR recognition on the image
high_res_result = engine.recognize()
```

`recognize()` yöntemi, ham dize, güven puanları ve bazen sınırlama kutusu meta verileri içeren bir sonuç nesnesi döndürür. **görüntüyü metne dönüştürme** amacıyla, `text` özniteliğine odaklanacağız.

---

## Adım 5: Tanınan Metni Çıktıla – Görüntüyü Metne Dönüştür

İşlemin doruk noktası: çıkarılan dizeyi yazdırmak. İşte bu noktada görüntü nihayet düzenlenebilir metne dönüşür.

```python
# Step 5: Output the recognized text
print(high_res_result.text)
```

**Beklenen çıktı** (gerçek metniniz görüntüye bağlı olarak değişecektir):

```
Invoice #12345
Date: 2024‑03‑15
Total: $256.78
Thank you for your business!
```

Eğer bozuk karakterler görürseniz, **set high accuracy mode**'un gerçekten `True` olduğundan ve görüntünün aşırı sıkıştırılmadığından emin olun.

---

## Yaygın Kenar Durumlarını Ele Alma

### 1. Boş Sonuç

Bazen motor boş bir dize döndürür. Bu genellikle görüntünün çok bulanık olduğu ya da metin renginin arka planla karıştığı anlamına gelir. Şunları deneyin:

- Yüklemeden önce görüntü çözünürlüğünü artırın (`PIL.Image.resize`).
- Kontrastı ayarlayın (`ImageEnhance.Contrast`).

### 2. Latin Olmayan Yazı Sistemleri

Resminiz Kiril, Çince veya Arapça karakterler içeriyorsa, OCR motoruna hangi dil paketini kullanacağını söylemeniz gerekir:

```python
engine.language = "eng+rus"   # Example for English + Russian
```

### 3. Büyük Toplu İşlem

Bir klasördeki birden çok görüntüyü işliyor musunuz? Çekirdek mantığı bir döngüye sarın ve aynı motor örneğini yeniden kullanarak tekrar tekrar başlatma yükünden kaçının.

```python
import pathlib

engine = ocr.OcrEngine()
engine.high_accuracy = True
engine.language = "eng"

for img_path in pathlib.Path("batch/").glob("*.jpg"):
    engine.image = ocr.Image.load_from_file(str(img_path))
    result = engine.recognize()
    print(f"{img_path.name}: {result.text[:50]}...")
```

---

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `ocr_demo.py` adlı bir dosyaya koyup hemen çalıştırabileceğiniz bir betik burada.

```python
#!/usr/bin/env python3
"""
ocr_demo.py – Recognize text from image using a generic OCR library.
"""

import ocr  # Replace with the actual OCR package you installed

def main():
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.high_accuracy = True          # set high accuracy mode
    engine.language = "eng"              # optional: specify language pack

    # Load image – change the path to your own file
    image_path = "YOUR_DIRECTORY/low-res.jpg"
    engine.image = ocr.Image.load_from_file(image_path)

    # Perform recognition
    result = engine.recognize()

    # Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Kaydedin, çalıştırılabilir yapın (`chmod +x ocr_demo.py`), ve çalıştırın:

```bash
./ocr_demo.py
```

Konsolda **görüntüyü metne dönüştür** çıktısını görmelisiniz.

---

## Saha İpuçları ve Püf Noktaları

- Birçok görüntü işliyorsanız **motoru önbelleğe alın**; her dosya için yeni bir örnek oluşturmak çalışma süresini iki katına çıkarabilir.
- Yerleşik yüksek doğruluk modu yeterli değilse **kendiniz ön işleme yapın**: OpenCV'yi gürültüyü azaltmak için (`cv2.fastNlMeansDenoisingColored`) veya ikiliye dönüştürmek için (`cv2.threshold`) kullanın.
- Düşük kaliteli sonuçları otomatik olarak filtrelemeniz gerekiyorsa **güveni kaydedin** (`result.confidence`).
- **Yolları sabit kodlamaktan kaçının**; çapraz platform uyumluluğu için `pathlib.Path` kullanın.

---

## Sonuç

Şimdi **görüntüden metin tanıma** işlemini basit bir Python iş akışıyla yaptık: **OCR için görüntü yükleme**, **yüksek doğruluk modunu ayarlama**, **OCR tanıma çalıştırma** ve sonunda **görüntüyü metne dönüştürme**. Tüm pipeline yirmi satırın altında bir kodla sığar, ancak toplu işler, çok dilli belgeler ve gürültülü girişlerle başa çıkacak kadar esnektir.

Bir sonraki meydan okumaya hazır mısınız? Genel `ocr` kütüphanesini `pytesseract` veya `easyocr` ile değiştirin, ek ön işleme adımları deneyin veya betiği bir Flask API'ye entegre edin; böylece bir web sayfasından resim yükleyebilir ve anlık transkripsiyonlar alabilirsiniz.

Sorularınız veya ilginç bir kullanım senaryonuz mu var? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla birlikte tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR Görüntü Tanıma’da Eşik Değerini Nasıl Ayarlarsınız](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Görüntüyü Metne Dönüştür – URL'den Görüntü Üzerinde OCR Yapma](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}