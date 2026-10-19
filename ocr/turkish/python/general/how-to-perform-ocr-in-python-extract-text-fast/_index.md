---
category: general
date: 2026-03-26
description: Python'da OCR nasıl yapılır öğrenin ve görüntüden metni kolayca çıkarın,
  taramadan metni okuyun veya basit bir OcrEngine kullanarak faturadan metin çıkarın.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: tr
og_description: Python'da OCR nasıl yapılır? Bu rehber, dakikalar içinde görüntüden
  metin çıkarmayı, taramadan metin okumayı ve faturadan metin çıkarmayı gösterir.
og_title: Python'da OCR Nasıl Yapılır – Metni Hızlıca Çıkar
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR Nasıl Yapılır – Metni Hızlıca Çıkar
url: /tr/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Nasıl Yapılır – Metni Hızlı Çıkar

Tarayıcıdan alınmış bir makbuzda ya da bulanık bir PDF'de **OCR nasıl yapılır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede **görüntüden metin çıkarma** ihtiyacı erken ortaya çıkar ve her şeyi “elle yazma” yaklaşımı ölçeklenebilir değildir.  

Bu öğreticide, **OCR nasıl kullanılır** gösteren, taramadan metin okuyan, bir faturadan veri çeken ve hatta otomatik eğim düzeltmesini bile yöneten, sadece birkaç Python satırıyla çalışan eksiksiz, hazır bir örnek göreceksiniz.

## Öğrenecekleriniz

* Gerekli tam bağımlılıklar ve import'lar.
* Bir `OcrEngine` örneği oluşturma ve yapılandırma.
* Aynı motoru kullanarak **görüntüden metin çıkarma**, **tarama üzerinden metin okuma** ve **faturadan metin çıkarma** yolları.
* Yaygın tuzaklar (yanlış dil, eksik dosyalar, büyük görüntüler) ve bunlardan nasıl kaçınılır.
* OCR'un başarılı olduğunu doğrulamak için beklenen çıktı.

Harici dokümantasyon bağlantılarına gerek yok—her şey kendi içinde, böylece kodu kopyala‑yapıştırıp sonuçları hemen görebilirsiniz.

## Önkoşullar

Before we dive in, make sure you have:

* Python 3.8+ yüklü ( `ocr` paketi herhangi bir yeni sürümle çalışır).
* `ocr` kütüphanesi mevcut (`pip install ocr‑engine` – farklı bir paket adı ise değiştirin).
* İşlemek istediğiniz bir görüntü dosyası – demo için `invoice.png` dosyasını `YOUR_DIRECTORY` adlı klasörde kullanacağız.

Hepsi bu. Eğer bunlar zaten varsa, hazırsınız.

## Adım 1: OCR Modülünü Kurun ve İçe Aktarın

İlk olarak: OCR kütüphanesine ihtiyacımız var. Henüz kurmadıysanız, terminalinizde aşağıdaki komutu çalıştırın:

```bash
pip install ocr-engine
```

Şimdi modülü script'imizde içe aktaralım.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro ipucu:** Sanal ortamınızı düzenli tutun; daha sonra başka görüntü‑işleme paketleri eklediğinizde sürüm çakışmalarını önler.

## Adım 2: OCR Motorunu Oluşturun ve Yapılandırın

Motoru oluşturmak, yapıcı metodunu çağırmak kadar basittir, ancak gerçek güç doğru yapılandırmada yatar. Dili İngilizce olarak ayarlayacağız ve otomatik eğim düzeltmesini açacağız; bu, tam hizalanmamış taranmış faturalarla çalışırken çok önemlidir.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

`auto_skew` neden etkinleştirilmeli? Birçok tarayıcı görüntüleri birkaç derece kaydırır. Düzeltme olmadan motor karakterleri kaçırabilir ve tamamen okunabilir bir faturayı anlamsız bir metne dönüştürebilir.

## Adım 3: Hedef Görüntünüzde OCR Yapın

Şimdi görüntü dosyasını motora veriyoruz. `recognize_image` metodu, ham metni ve (kütüphane sağlıyorsa) güven puanlarını içeren bir nesne döndürür.

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Eğer **tarama üzerinden metin okuma** senaryosuyla çalışıyorsanız, yolu taranmış PDF'nin PNG veya JPEG'e dönüştürülmüş haliyle değiştirmeniz yeterlidir. Aynı çağrı, temel kütüphanenin desteklediği herhangi bir görüntü formatı için çalışır.

## Adım 4: Çıkarılan Metni İnceleyin ve Kullanın

Ham OCR çıktısını yazdıralım. Gerçek bir fatura‑işleme hattında muhtemelen bu dizeyi ayrıştırıp satır öğelerini, toplamları ve tarihleri çıkarırsınız, ancak şimdilik hızlı bir bakış OCR'un başarılı olduğunu doğrular.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Beklenen çıktı (kısaltılmış):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Çıktı bozuk görünüyorsa, görüntünün net olduğundan ve `engine.language` değerinin belgenin diliyle eşleştiğinden emin olun.

## Adım 5: Yaygın Kenar Durumlarını Ele Alma

### Büyük Görüntüler

5000 × 5000 piksel bir taramayı işlemek bellek açısından yoğun olabilir. Bunu hafifletmenin hızlı bir yolu, görüntüyü motora göndermeden önce ölçeklendirmektir:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Çoklu Diller

Eğer hem İngilizce hem de İspanyolca içeren bir **görüntüden metin çıkarma** ihtiyacınız varsa, bir dil listesi ayarlayabilirsiniz:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Motor, her iki dilin karakterlerini tanımaya çalışacaktır.

### Hata Yönetimi

Dosyanın var olduğunu asla varsaymayın. Kullanıcı dostu bir mesaj vermek için çağırmayı try‑except bloğuna alın:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Görsel Referans

Aşağıda demoda kullandığımız örnek faturanın ekran görüntüsü var. Hafif eğimi fark edin—tam da `auto_skew`'in düzelttiği şey.

![otomatik eğim düzeltmesi gösteren bir fatura görüntüsü üzerinde OCR nasıl yapılır](/images/ocr-example.png)

*Alt metin:* otomatik eğim düzeltmesi gösteren bir fatura görüntüsü üzerinde OCR nasıl yapılır.

## Tam, Çalıştırılabilir Örnek

Her şeyi bir araya getirerek, komut satırından çalıştırabileceğiniz tek bir script burada. Kurulum, yapılandırma, hata yönetimi ve çıkarılan metni `output.txt` adlı bir dosyaya yazan basit bir son‑işlem adımını kapsar.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

`python full_ocr_demo.py` komutunu çalıştırmak, çıkarılan metni konsola yazdıracak ve `output.txt` dosyasına kaydedecek. Buradan, **faturadan metin çıkarma** otomasyonu için ihtiyacınız olan düzenli ifadeler, CSV yazarları veya başka herhangi bir mantığı uygulayabilirsiniz.

## Sonuç

Artık Python'da **OCR nasıl yapılır** sorusuna sağlam, uçtan uca bir yanıtınız var. Bir `OcrEngine` oluşturarak, dili ve eğim düzeltmesini yapılandırarak ve birkaç pratik kenar durumunu ele alarak, dağınık dokümantasyon arasında dolaşmadan güvenilir bir şekilde **görüntüden metin çıkarma**, **tarama üzerinden metin okuma** ve **faturadan metin çıkarma** yapabilirsiniz.

Sırada ne var? Dosyaları bir döngüye besleyin, farklı dillerle deney yapın veya çıktıyı bir PDF oluşturma kütüphanesine bağlayarak aranabilir PDF'ler oluşturun. Gökyüzü sınırdır ve az önce gördüğünüz kod sağlam bir başlangıç platformudur.

Belirli bir dosya formatı hakkında sorularınız mı var ya da güven eşiğini ayarlamakta yardıma mı ihtiyacınız var? Aşağıya bir yorum bırakın—OCR hattınızı ince ayar yapmanızda memnuniyetle yardımcı oluruz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}