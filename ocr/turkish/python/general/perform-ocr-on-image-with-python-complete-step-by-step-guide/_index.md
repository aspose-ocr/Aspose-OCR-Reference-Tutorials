---
category: general
date: 2026-07-05
description: Python kullanarak görüntüde OCR gerçekleştirin. Görüntüyü metne dönüştürmeyi,
  OCR için görüntüyü yüklemeyi ve dakikalar içinde görüntüden Kiril alfabesi metni
  çıkarmayı öğrenin.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: tr
og_description: Python'da görüntü üzerinde OCR gerçekleştirin. Bu rehber, görüntüyü
  metne nasıl dönüştüreceğinizi, OCR için görüntüyü nasıl yükleyeceğinizi ve görüntüden
  Kiril alfabesi metnini hızlıca nasıl çıkaracağınızı gösterir.
og_title: Python ile Görüntüde OCR Yapma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Python ile Görüntüde OCR Yapın – Tam Adım Adım Kılavuz
url: /tr/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Görüntü Üzerinde OCR Gerçekleştirme – Tam Adım‑Adım Kılavuz

Üçüncü taraf bir hizmete göndermeden **görüntü üzerinde OCR gerçekleştirme** dosyalarını nasıl yapacağınızı hiç merak ettiniz mi? Yalnız değilsiniz. Pek çok projede—pasaport tarayıcıları, fiş dijitalleştiricileri veya arşivleme araçları—bir resimden ham metni elde etmek ilk engeldir.  

Bu öğreticide, **converts image to text python** tarzında bir pratik örnek üzerinden ilerleyecek, **load image for OCR** nasıl yapılacağını gösterecek ve sonunda açık kaynaklı `aocr` kütüphanesini kullanarak **extract Cyrillic text from image** işlemini yapacağız. Sonunda, ona yönelttiğiniz herhangi bir resimde **recognize Cyrillic text** yapabilecek durumda olacaksınız.

> **Ne kazanacaksınız:** çalıştırmaya hazır bir betik, her adımın net açıklamaları ve yaygın sorunlarla (bulanık taramalar veya beklenmedik yazı tipleri gibi) başa çıkma ipuçları. Harici API'ler yok, sadece saf Python.

---

## Önkoşullar

- Python 3.8 veya daha yeni bir sürüm kurulu.
- Kullanımına alışkın olduğunuz bir terminal veya komut istemcisi.
- `aocr` paketi (`pip install aocr` ile kurulabilir).
- Kiril alfabesi karakterleri içeren bir görüntü dosyası (ör. taranmış bir Rus pasaportu).  

Eğer bunlardan herhangi biri size yabancı geliyorsa panik yapmayın—her maddeye ilerledikçe kısaca değineceğiz.

---

## Adım 1: Görüntü Üzerinde OCR Gerçekleştirme – Ortamı Kurma

İlk olarak, OCR kütüphanesinin bulunduğu temiz bir Python ortamına ihtiyacımız var. Sanal ortam kullanmak bağımlılıkları izole eder ve sürüm çakışmalarını önler.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Neden?**  
Ayrı bir ortam, `aocr` paketinin ve yerel ikili dosyalarının diğer projelerle çakışmamasını sağlar. Ayrıca tekrarlanabilirliği çok kolaylaştırır—başkası reposunu klonlayıp aynı `pip install -r requirements.txt` komutunu çalıştırabilir.

> **Pro ipucu:** Bağımlılıkları `pip freeze > requirements.txt` ile dondurun, böylece hangi sürümlerin kullanıldığını her zaman tam olarak bilirsiniz.

---

## Adım 2: OCR İçin Görüntüyü Yükleme – Dosyayı İçe Aktarma ve Hazırlama

Kütüphane hazır olduğuna göre, **load image for OCR** yapmamız gerekiyor. `aocr.Image.from_file` metodu, yaygın formatların çoğunu (PNG, JPEG, TIFF) işler. İşte nasıl yapacağınız:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Burada ne oluyor?**  
`aocr.Image.from_file` ikili veriyi okur, çözer ve OCR motorunun anlayabileceği bir nesneye depolar. Dosya bulunamazsa, Python bir `FileNotFoundError` hatası fırlatır; bu hatayı daha sonra nazik bir hata yönetimi için yakalayabilirsiniz.

> **Köşe durum:** Bazı tarayıcılar çok sayfalı TIFF'ler üretir. Bu durumda, önce sayfaları bölmeniz gerekir—`aocr` bunun için `Image.from_tiff_pages()` sağlar.

---

## Adım 3: OCR Motorunu Yapılandırma – Kiril Tanımasını Zorlamak

Varsayılan olarak, birçok OCR motoru dili tahmin etmeye çalışır ve bu, Latin dışı betikler için bozuk çıktıya yol açabilir. **recognize Cyrillic text** güvenilir bir şekilde yapmak için dili açıkça “cyrillic” olarak ayarlarız.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Neden dili zorlayalım?**  
Kiril karakterleri, Latin harflerle görsel benzerlikler taşır (ör. “A” vs “А”). Motora Kiril bekleyeceğini söylemek, özellikle düşük çözünürlüklü taramalarda yanlış tanıma oranını büyük ölçüde azaltır.

---

## Adım 4: Görüntü Üzerinde OCR Gerçekleştirme – Tanıma Çalıştırma

Görüntü yüklendi ve motor ayarlandıktan sonra nihayet **perform OCR on image** yapıyoruz. `recognize` metodu, çıkarılan metin ve güven skorlarını içeren bir `OcrResult` nesnesi döndürür.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**`ocr_result` size ne sağlıyor?**  
- `text`: tanınan karakterlerin düz metin dizesi.  
- `confidence`: genel kesinliği gösteren bir float (0‑1).  
- `lines`: daha ayrıntılı kontrol gerektiğinde satır nesnelerinin listesi.  

> **Sık sorulan soru:** *Metin baş aşağı olursa ne olur?*  
> `aocr` görüntüleri otomatik döndürebilir; `recognize` çağırmadan önce sadece `ocr_engine.auto_rotate = True` ayarlayın.

---

## Adım 5: Görüntüyü Metne Dönüştürme Python – Çıktıyı Son İşleme

Ham dize, gereksiz boşluklar veya satır sonu artefaktları içerebilir. **convert image to text python** tarzında temizlemek için birkaç basit adım uygulayacağız:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Neden zahmet?**  
Temizlenmiş çıktı, sonraki işlem hatlarına beslemek için daha kolaydır—veritabanına kaydediyor olun, bir çeviri API'sine gönderiyor olun ya da pasaport numaraları için regex aramaları yapıyor olun.

---

## Adım 6: Görüntüden Kiril Metni Çıkarma – Hepsini Bir Araya Getirme

Her şeyi tek, yeniden kullanılabilir bir fonksiyonda toplayalım. Bu, **extract Cyrillic text from image** işlemini projelerinizde tek satır hâline getirir.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Görmeniz gereken sonuç (örnek):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Görüntü net ve yazı tipi OCR modeline uyuyorsa, neredeyse kusursuz bir transkripsiyon elde edersiniz.

## Sorun Giderme & İpuçları

| Sorun | Muhtemel Neden | Çözüm |
|-------|----------------|-------|
| Bozuk karakterler | Yanlış dil ayarı | `ocr_engine.language = "cyrillic"` ayarlandığından emin olun |
| Boş çıktı | Görüntü çok karanlık veya düşük çözünürlüklü | Kontrastı artırmak için `opencv` ile ön işleme yapın |
| Yanlış yönlendirme | Görüntü 90° döndürülmüş | `ocr_engine.auto_rotate = True` ayarlayın |
| Yavaş performans | Büyük görüntü ( >5 MP ) | Tanımadan önce `aocr.Image.resize(width=1024)` ile yeniden boyutlandırın |

![görüntü üzerinde OCR örneği](ocr_example.png "görüntü üzerinde OCR örneği")

*Alt metin: “görüntü üzerinde OCR örneği, bir pasaport taramasından Kiril metni çıkaran Python kodunu gösteriyor.”*

## Sonuç

Sadece saf Python kullanarak **perform OCR on image** dosyalarını gerçekleştirdik, **load image for OCR** nasıl yapılacağını öğrendik, motoru **recognize Cyrillic text** yapacak şekilde zorladık ve sonunda **extract Cyrillic text from image** işlemini düzenli bir yardımcı fonksiyonla yaptık. `aocr` kurulumundan sonucu temizlemeye kadar tüm işlem hattı, birkaç düzine satır kod içinde sığar ve **convert image to text python** tarzında bir işleme ihtiyacı olan herhangi bir projeye eklenebilir.

## Sıradaki Adımlar

- **Batch processing:** Taramaların bulunduğu bir klasörü döngüye alıp sonuçları SQLite'da saklayın.  
- **Language detection:** `langdetect` ile `aocr`'yi birleştirerek Kiril ve Latin arasında otomatik geçiş yapın.  
- **Advanced preprocessing:** Daha yüksek doğruluk için görüntüleri eğriltmekten, gürültüyü azaltmaktan veya ikili hale getirmekten `opencv` kullanın.  
- **Integrate with FastAPI:** `extract_cyrillic_text` fonksiyonunu web uygulamaları için bir REST uç noktası olarak açın.  

Denemekten çekinmeyin—İngiliz pasaportları için dili “latin” olarak değiştirin ya da tamamen farklı bir OCR arka ucunu deneyin. Kavramlar aynı kalır ve kod, uyum sağlayacak kadar esnektir.

Kodlamaktan keyif alın, ve görüntüleriniz her zaman okunaklı olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüyü Metne Dönüştür – URL'den Görüntü Üzerinde OCR Gerçekleştirme](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Aspose.OCR Kullanarak Dil Seçimiyle Görüntü Metni Çıkarma (C#)](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}