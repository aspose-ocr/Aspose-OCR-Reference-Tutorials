---
category: general
date: 2026-06-06
description: Python ile PNG görüntü OCR – görüntüden metin çıkarmayı öğrenin, bir
  Python OCR örneği çalıştırın ve hatta antik Yunan metinlerini kolayca okuyun.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: tr
og_description: Python'da OCR PNG görüntüsü açıklaması. Bu kılavuz, görüntüden metin
  nasıl çıkarılır, bir Python OCR örneği nasıl çalıştırılır ve antik Yunanca nasıl
  kolayca okunur gösterir.
og_title: Python'da PNG Görüntüsü OCR – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python'da PNG Görüntü OCR – Tam Adım Adım Rehber
url: /tr/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR PNG Görüntüsü – Tam Adım‑Adım Kılavuz

Ever wondered how to **OCR PNG image** files straight from a Python script? Maybe you have a folder full of scanned ancient manuscripts and you need to **extract text from image** files without manually typing everything. The good news is you don’t need a PhD in computer vision—just a few lines of code and the right library, and you’ll be reading ancient greek in seconds.

Bu öğreticide **python OCR example**'ı adım adım inceleyeceğiz; PNG'den metni tanır, dili Yunan polytonik olarak ayarlar ve sonucu yazdırır. Sonuna geldiğinizde **recognize image text**'i tam olarak nasıl yapacağınızı, yaygın sorunları nasıl yöneteceğinizi ve betiği diğer diller veya görüntü formatları için nasıl uyarlayacağınızı öğreneceksiniz.

## Öğrenecekleriniz

- Python OCR kütüphanesini (pytesseract + Tesseract OCR) kurun ve yapılandırın
- Bir OCR motoru örneği oluşturun ve PNG dosyasını yükleyin
- Tanıma dilini Yunan polytonik olarak ayarlayın, böylece **read ancient greek** yapabilirsiniz
- Tanınan metni çıktıya alın ve tipik sorunları giderin
- Betik'i birden fazla PNG'yi toplu işleyebilecek veya başka bir dile geçebilecek şekilde genişletin

### Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.8+ | Modern syntax and type hints |
| `pytesseract` package | Thin wrapper around the Tesseract engine |
| Tesseract OCR binaries (≥ 5.0) | The actual engine that does the heavy lifting |
| Greek language data (`grc.traineddata`) | Needed for **read ancient greek** correctly |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Our target for the **ocr png image** demo |

Python tarafını şu şekilde kurabilirsiniz:

```bash
pip install pytesseract Pillow
```

Ubuntu/macOS üzerinde motoru şu şekilde ekleyebilirsiniz:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Yunan polytonik eğitim verisini indirmeyi unutmayın:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Yol farklı olabilir; gerekirse `TESSDATA_PREFIX`'i ayarlayın.)*

---

## OCR PNG Görüntüsü: Motor Örneğini Oluşturma

İlk olarak Tesseract ile iletişim kuran bir nesneye ihtiyacımız var. `pytesseract` içinde motor, modül‑seviyesindeki fonksiyonlarla erişilir, ancak açıklık için bunu küçük bir sınıfa sarmalayacağız. Bu, orijinal kod parçacığında gördüğünüz “engine” kavramını yansıtır.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Neden sarmalansın?**  
- Kamu API'sını, başladığınız kod parçacığıyla aynı tutar, geçişi sorunsuz hâle getirir.  
- Ana akışı etkilemeden daha sonra günlükleme veya hata yönetimi eklememizi sağlar.  
- İyi OOP uygulamasını gösterir—kıdemli geliştiricilerin takdir ettiği bir şey.

---

## Görüntüden Metin Çıkarma: Dili Yunan Polytonik Olarak Ayarlama

Artık bir motorumuz olduğuna göre, hangi dili bekleyeceğini ona söylememiz gerekiyor. Yunan polytonik, standart “greek” verisiyle kapsanmayan diakritik işaretler kullanır, bu yüzden Tesseract'i `grc` eğitim dosyasına yönlendiririz.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Başka bir dilde **extract text from image** dosyaları çıkarmak isterseniz, sadece `"grc"` yerine İngilizce için `"eng"`, Fransızca için `"fra"` gibi bir değer koyun. Aynı satır, yüklü olan herhangi bir dil için çalışır.

---

## Görüntü Metnini Tanıma: PNG Üzerinde OCR Çalıştırma

Dil ayarlandıktan sonra PNG'yi motorun içine besliyoruz. Orijinal örnek sabit bir yol kullandı; biz `Path` nesneleriyle biraz daha esnek hâle getireceğiz.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**İpuçları & Kenar Durumları**

- **File not found** – çağrıyı `try/except FileNotFoundError` içinde sarmalayarak dostça bir mesaj verin.  
- **Low‑resolution PNG** – OCR'den önce Pillow ile ön işleme (ör. yeniden boyutlandırma, ikilileştirme) yapmayı düşünün.  
- **Non‑Greek text** – Tesseract yine de çözümlemeye çalışır, ancak doğruluk büyük ölçüde düşer. Her zaman dili eşleştirin.

---

## Tanınan Metni Çıktılamak

Son olarak sonucu yazdırıyoruz. Gerçek bir projede bunu bir veritabanına, CSV'ye ya da hatta bir çeviri hattına aktarabilirsiniz.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Betik'i antik Yunan bir yazıtın net taraması üzerinde çalıştırdığınızda, aşağıdakine benzer bir çıktı görmelisiniz:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Çıktı bozuk görünüyorsa, **greek.traineddata** dosyasının doğru klasörde olduğundan ve PNG'nin çok gürültülü olmadığından emin olun.

---

## Tam Çalışan Örnek (Tüm Adımlar Tek Betikte)

Aşağıda eksiksiz, çalıştırmaya hazır program yer alıyor. `ocr_greek.py` olarak kaydedin ve `python ocr_greek.py` komutuyla çalıştırın.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Beklenen çıktı** (kısaltılmış olarak):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Doğru Yunan karakterlerini görürseniz, tebrikler—Python’da başarılı bir **ocr png image** işlemi gerçekleştirdiniz!

---

## Yaygın Sorular & Profesyonel İpuçları

### Gürültülü bir PNG'de doğruluğu nasıl artırırım?

- Görüntüyü gri tonlamaya dönüştürün: `img = img.convert('L')`
- İkili eşik uygulayın: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Yeniden ölçeklendirin: `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Bu adımlar genellikle bir **recognize image text** kabusunu temiz bir sonuca dönüştürür.

### Tüm bir PNG klasörünü işleyebilir miyim?

Kesinlikle. `recognize_image` çağrısını `Path.glob("*.png")` üzerinden bir `for` döngüsüyle sarın. Her sonucu bir sözlükte saklayın veya daha sonra analiz için bir CSV'ye yazın.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Sadece sayıları çıkarmam gerekirse ne yapmalıyım?

`image_to_string`'e özel bir **config** dizesi gönderin:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Bu şekilde tablolar, seri numaraları veya zaman damgaları içeren **extract text from image** dosyalarından metin çıkarabilirsiniz.

### Güven skorlarını elde etmenin bir yolu var mı?

Evet—her kelime için güven skorunu içeren bir TSV döndüren `pytesseract.image_to_data`'yı kullanın. Son dizeyi birleştirmeden önce düşük güvenilirlikli tokenları filtreleyebilirsiniz.

---

## Öğreticiyi Genişletme

Temelleri kavradığınıza göre, aşağıdaki ilgili konuları keşfetmeyi düşünün:

- **Batch OCR with multiprocessing** – büyük PNG koleksiyonlarını hızlandırın.  
- **Hybrid OCR + NLP pipelines** – çıkarılan antik Yunan'ı otomatik olarak modern İngilizceye çevirin.  
- **Alternative engines** – belirli kullanım durumları için `easyocr` veya `opencv`‑tabanlı yöntemleri deneyin.  
- **Cloud OCR services** – sunucusuz ölçeklendirme için Google Vision, Azure Computer Vision veya AWS Textract.

Bunların her biri, az önce ele aldığımız temel **python ocr example** üzerine inşa edildiği için, daha derine dalarken rahat hissedeceksiniz.

## Sonuç

Basit bir kod parçacığını Python’da sağlam bir **ocr png image** iş akışına dönüştürdük. Bir `OcrEngine` oluşturarak, dili Yunan polytonik olarak ayarlayarak, bir PNG besleyerek ve sonucu yazdırarak, artık **extract text from image** dosyalarını, **recognize image text**'i ve hatta **read ancient greek** nasıl yapacağınızı biliyorsunuz.

## Sonra Ne Öğrenmelisin?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}