---
category: general
date: 2026-04-26
description: Python kullanarak görüntülerden OCR nasıl çıkarılır – OCR için görüntüyü
  nasıl yükleyeceğinizi ve bir makbuzdan metin çıkaracağınızı gösteren bir Python
  OCR örneği.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: tr
og_description: Python kullanarak görüntülerden OCR nasıl çıkarılır. Bir Python OCR
  örneği öğrenin, OCR için görüntüyü yükleyin ve dakikalar içinde makbuzdan metni
  çıkarın.
og_title: Python'da OCR Nasıl Çıkarılır – Tam Kılavuz
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR nasıl çıkarılır – Adım adım öğretici
url: /tr/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Nasıl Çıkarılır – Tam Kılavuz

Hiç **how to extract ocr** ifadesini bulanık bir makbuz ya da taranmış bir faturadan merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler, temiz, makine‑okunabilir metne ihtiyaç duyduklarında sık sık bir engelle karşılaşıyorlar. İyi haber? Sadece birkaç Python satırıyla bir makbuzun resmini yüksek‑güvenilir, aranabilir metne dönüştürebilirsiniz.

Bu öğreticide **python ocr example** gösteren bir **how to load image for ocr** örneği üzerinden ilerleyecek, motoru çalıştıracak ve %85 % güven eşiğini karşılayan karakterleri tutacağız. Sonunda **extract text from receipt** görüntülerinden belgeyi taramaya ya da API parametrelerini tahmin etmeye gerek kalmadan metin çıkarabileceksiniz.

## İhtiyacınız Olanlar

- Python 3.9 veya daha yeni (kullandığımız sözdizimi 3.8+ ile çalışır)
- `aocr` paketi (veya bir `OcrEngine` sınıfı sağlayan herhangi bir OCR kütüphanesi). Şöyle kurun:

```bash
pip install aocr
```

- `receipt.png` adlı örnek makbuz görüntüsü, referans alabileceğiniz bir klasörde bulunmalı.
- Bir metin editörü ya da IDE—VS Code, PyCharm ya da basit bir notebook yeterli.

Hepsi bu. Ağır çerçeveler yok, harici hizmetler yok, sadece saf Python.

![Yüksek‑güvenilir OCR sonucu – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*Görsel alt metni: how to extract ocr from a receipt using Python OCR*

## 1. Adım – OCR Motoru Örneğini Oluşturma (how to extract ocr)

İlk yaptığımız şey bir OCR motoru başlatmak. Bunu, pikselleri bizim için okuyacak bir beyin olarak düşünün.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Why?** `OcrEngine` örneği oluşturmak size yeni bir yapılandırma nesnesi verir. Daha sonra dil modellerini, DPI ayarlarını ya da ön işleme adımlarını—ana işleme döngüsüne dokunmadan—ayarlayabilirsiniz.

## 2. Adım – OCR için Görüntüyü Yükleme

Sonra motoru analiz etmek istediğimiz görüntüye yönlendiririz. İşte **load image for ocr** anahtar kelimesinin devreye girdiği yer.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** Görüntünüz farklı bir dizinde bulunuyorsa, platform‑bağımsız bir yol oluşturmak için `os.path.join` kullanın.

**Why load the image this way?** `Image.load` yardımcı işlevi dosyayı motorun anlayabileceği bir formata okur, yaygın formatları (PNG, JPEG, TIFF) otomatik olarak işler. Bu adımı atlamak ya da ham baytları beslemek bir `ValueError` oluşturur.

## 3. Adım – OCR İşlemini Çalıştırma

Şimdi OCR'ı gerçekten çalıştırıyoruz. `process` metodu, tanınan semboller, güven skorları ve sınırlayıcı kutular içeren zengin bir sonuç nesnesi döndürür.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**What does `ocr_result` contain?** Çoğu kütüphanede şunlar bulunur:

- `text`: ham birleştirilmiş dize.
- `symbol_confidences`: `(char, confidence)` ikililerinden oluşan bir liste.
- `boxes`: her karakter için koordinatlar (görsel hata ayıklama için faydalı).

Karakter bazında güvene erişim bir sonraki adım için hayati önem taşır.

## 4. Adım – Yalnızca Yüksek‑Güvenilir Sembolleri Tut (≥ 85 %)

Bir makbuz genellikle lekeler, soluk baskı ya da arka plan gürültüsü içerir. Düşük‑güvenilir sembolleri filtreleyerek sonraki ayrıştırmayı büyük ölçüde iyileştiririz.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Why 85 %?** Deneysel olarak, %0.85 civarında bir eşik çoğu basılı makbuz için geri çağırma ve kesinliği dengeler. Sayılar eksikse eşik değerini düşürün; anlamsız karakterler görürseniz yükseltin.

## 5. Adım – Yüksek‑Güvenilir Çıkarılan Metni Çıktılamak

Son olarak, temizlenmiş dizeyi yazdırır (ya da saklarız). Bu, **extract text from receipt** iş akışımızın çekirdeğidir.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Tipik çıktı şöyle görünür:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Artık bu dizeyi bir CSV yazıcıya, bir veritabanına ya da herhangi bir sonraki analiz boru hattına besleyebilirsiniz.

## Tam, Çalıştırmaya Hazır Script

Aşağıda `ocr_receipt.py` dosyasına kopyalayıp hemen çalıştırabileceğiniz tam kod parçacığı yer alıyor.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Dosyayı kaydedin, `receipt.png` dosyasının mevcut olduğundan emin olun ve çalıştırın:

```bash
python ocr_receipt.py
```

Temizlenmiş makbuz metninin konsola yazdırıldığını göreceksiniz.

## Kenar Durumları ve Ne‑Olur Senaryoları

| Durum | Önerilen Çözüm |
|-----------|----------------|
| **Very low confidence across the board** | Görüntüyü ön‑işleme tabi tutun: kontrastı artırın, gri tonlamaya dönüştürün veya bir gürültü azaltma filtresi (`cv2.GaussianBlur`) uygulayın. |
| **Non‑Latin characters** | `OcrEngine`'e bir dil modeli geçin (ör. `ocr_engine.language = "spa"` İspanyolca için). |
| **Multiple receipts in one image** | Tüm görüntüde OCR çalıştırın, ardından `\n\n+` (çift satır sonu) tespit eden düzenli ifadelerle sonucu bölün. |
| **Need the raw OCR text as well** | Hata ayıklama için filtrelenmiş sürümün yanında `ocr_result.text`'i tutun. |

Bu varyasyonlar, **how to use OCR** bilginizin en basit durumu aşarak ölçeklenmesini sağlar.

## Yaygın Tuzaklar (Ve Nasıl Kaçınılır)

- **Forgetting to install the library** – `pip install aocr` komutunun başarılı olması gerekir, ardından içe aktarım yapılabilir.
- **Using the wrong path separator** on Windows (`\` vs `/`). Use `os.path.join`.
- **Hard‑coding the confidence threshold** without testing – always run a quick visual check on a few receipts first.
- **Ignoring Unicode normalisation** – bazı makbuzlar özel tire karakterleri içerir; çıktıyı saklamayı planlıyorsanız `unicodedata.normalize('NFKC', text)` çalıştırın.

## Sonraki Adımlar – Temelin Ötesine Geçmek

Şimdi **how to extract ocr** verisini tek bir makbuzdan çıkarabildiğinize göre, şunları yapmak isteyebilirsiniz:

1. **Batch process a folder of receipts** – tüm PNG/JPG dosyaları üzerinde döngü kurup her sonucu bir CSV'ye yazın.
2. **Integrate with a database** – `high_confidence_text`'i hızlı aramalar için SQLite'ta saklayın.
3. **Apply natural‑language parsing** – tarih, toplam ve vergi tutarlarını çekmek için regex ya da `dateutil` kullanın.
4. **Experiment with alternative libraries** – `pytesseract`, `easyocr` ya da bulut hizmetleri (Google Vision, Azure OCR) çok dilli destek ya da daha yüksek doğruluk gerektiğinde tercih edin.

Bu konular doğal olarak ikincil anahtar kelimelerimizi içerir: *python ocr example*, *extract text from receipt*, *load image for ocr*, ve *how to use OCR*.

## Sonuç

Tam bir **python ocr example** üzerinden **how to extract ocr** metninin bir makbuz görüntüsünden nasıl çıkarılacağını, düşük‑güvenilir sembollerin nasıl filtreleneceğini ve temiz sonuçların nasıl çıktılanacağını gösterdik. Adımlar basit, kod bağımsız ve yaklaşım daha büyük projelere uyacak kadar esnek.

Kendi makbuzlarınızla deneyin, güven eşiğini ayarlayın ve ardından toplu işleme geçin. Eğer ince bir logo ya da alışılmadık bir font gibi tuhaflıklarla karşılaşırsanız, yukarıdaki kenar‑durum ipuçlarını hatırlayın. İyi kodlamalar, OCR boru hatlarınız her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}