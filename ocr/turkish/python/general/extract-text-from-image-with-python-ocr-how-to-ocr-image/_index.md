---
category: general
date: 2026-05-31
description: Python'ın aocr kütüphanesini kullanarak görüntüden metin çıkarın. Görüntüyü
  OCR ile nasıl işleyebileceğinizi, OCR için görüntüyü nasıl yükleyeceğinizi ve sadece
  birkaç satırda özel karakterleri nasıl tanıyacağınızı öğrenin.
draft: false
keywords:
- extract text from image
- recognize special characters
- convert image to text
- how to ocr image
- load image for ocr
language: tr
og_description: Python'ın aocr kütüphanesini kullanarak görüntüden metin çıkarın.
  Bu kılavuz, görüntüyü OCR ile işleme, OCR için görüntü yükleme ve özel karakterleri
  hızlıca tanıma yöntemlerini gösterir.
og_title: Python OCR ile Görüntüden Metin Çıkarma – Görüntüyü OCR Nasıl Yapılır
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  headline: Extract Text from Image with Python OCR – How to OCR Image
  type: TechArticle
- description: Extract text from image using Python's aocr library. Learn how to OCR
    image, load image for OCR, and recognize special characters in just a few lines.
  name: Extract Text from Image with Python OCR – How to OCR Image
  steps:
  - name: 5.1 Low‑Resolution Images
    text: 'If the image is under 150 dpi, the OCR accuracy can drop dramatically.
      A quick fix is to upscale before feeding it to aocr:'
  - name: 5.2 Incorrect Language Detection
    text: 'aocr auto‑detects language, but you can force a specific script for better
      results:'
  - name: 5.3 Noise and Background Patterns
    text: 'A noisy background can confuse the model. Pre‑process with OpenCV to binarize:'
  type: HowTo
- questions:
  - answer: Not directly. Convert PDF pages to images first (e.g., using `pdf2image`)
      and then feed each image to aocr.
    question: Does this work on PDFs?
  - answer: For typical 300 dpi scans, aocr processes a page in ~0.3 s on a modern
      laptop—roughly twice as fast as vanilla Tesseract with default settings.
    question: How fast is aocr compared to Tesseract?
  - answer: 'Absolutely. Wrap the `main` function in a loop over `Path(folder).glob("*.png")`
      and collect results in a CSV. --- ## Conclusion You now have a solid, end‑to‑end
      workflow to **extract text from image** using Python’s aocr library. From loading
      the file to printing Unicode output, every step is expla'
    question: Can I batch‑process a folder of images?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Python OCR ile Görüntüden Metin Çıkarma – Görüntüyü OCR Nasıl Yapılır
url: /tr/python/general/extract-text-from-image-with-python-ocr-how-to-ocr-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR ile Görüntüden Metin Çıkarma – OCR Nasıl Yapılır

Görselden **metin çıkarmak** istediğinizde, “Ł”, “Ž” veya “ß” gibi tuhaf sembolleri işleyebilecek kütüphaneyi bulamadıysanız yalnız değilsiniz. Gerçek dünyadaki birçok projede—tarama fişleri, çok dilli tabelalar veya tarihi belgeler gibi—**özel karakterleri tanıma** yeteneği, kullanılabilir bir veri seti ile çıkmaza giren bir veri seti arasındaki fark olabilir.

İyi haber? Birkaç Python satırı ve hafif **aocr** paketiyle, herhangi bir resmi aranabilir metne dönüştürebilirsiniz. Aşağıda tamamen çalıştırılabilir bir betik ve her adımın *neden* olduğu açıklanıyor, böylece sadece kopyala‑yapıştırmak yerine ne olduğunu gerçekten anlayacaksınız.

## Bu Eğitimde Neler Kapsanıyor

- **aocr** kütüphanesini kurma ve içe aktarma
- OCR için bir resmi yükleme (yaygın tuzaklar dahil)
- Motoru **görseli metne dönüştürmek** için çalıştırma
- Sonucu yazdırma ve özel‑karakter çıktısını işleme
- Temel akışı çok‑dilli destek ve hata yönetimi için genişletme

Bu rehberin sonunda, herhangi bir dildeki **görselden metin çıkarma** dosyalarını yapabilecek ve varsayılan ayarlar yetersiz kaldığında süreci nasıl ayarlayacağınızı bileceksiniz.

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.8+ | aocr modern tip özelliklerine dayanır |
| `pip` erişimi | Kütüphaneyi kurmak için |
| Örnek bir görüntü (ör. `multilingual.png`) | Özel karakterleri göstermek için bunu kullanacağız |
| Sanal ortamlarla temel aşinalık (isteğe bağlı) | Bağımlılıkları düzenli tutar |

Tesseract gibi ağır harici araçlara gerek yok—**aocr**, kutudan çıkar çıkmaz çalışan hızlı bir sinir ağı motoru içerir.

---

## Adım 1: aocr Kütüphanesini Kurun

İlk olarak, bir terminal (veya IDE’nizin konsolu) açın ve şu komutu çalıştırın:

```bash
pip install aocr
```

*İpucu:* Birden fazla projeyle çalışıyorsanız, önce bir sanal ortam oluşturun:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # macOS/Linux
.\ocr-env\Scripts\activate    # Windows
pip install aocr
```

Bu, OCR bağımlılıklarını sisteminizin geri kalanından izole eder—sonradan çok fazla baş ağrısını önlediğini gördüm.

---

## Adım 2: OCR için Görüntüyü Yükleyin

Paket hazır olduğuna göre, **OCR için görüntüyü yüklememiz** gerekiyor. `OcrEngine` sınıfı bir dosya yolunu bekler, bu yüzden görüntünün mevcut ve okunabilir olduğundan emin olun.

```python
import aocr

# Step 2: Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Step 2b: Point to your image file (adjust the path as needed)
image_path = r"YOUR_DIRECTORY/multilingual.png"
ocr_engine.load_image(image_path)
```

> **Neden önemli:**  
> - `load_image` hızlı bir tutarlılık kontrolü yapar (dosya varlığı, desteklenen format).  
> - Ham bir dize (`r"..."`) kullanmak, Windows yollarında istenmeyen kaçış karakteri hatalarını önler.  
> - Görüntü çok büyükse, aocr belleği makul tutmak için otomatik olarak ölçek küçültür.  

`FileNotFoundError` alırsanız, yolu iki kez kontrol edin ve dosya uzantısının PNG, JPEG veya BMP olduğundan emin olun.

---

## Adım 3: OCR Gerçekleştir – Görüntüyü Metne Dönüştür

Görüntü bellekteyken, sonraki çağrı aslında **özel karakterleri tanır** ve bir Unicode dizesi üretir.

```python
# Step 3: Run the OCR engine
recognized_text = ocr_engine.recognize()
```

Arka planda, aocr çok dilli veri setleriyle eğitilmiş hafif bir konvolüsyon‑rekürent ağ çalıştırır. Bu yüzden Kiril, Latin‑genişletilmiş ve hatta bazı nadir gliflerin karakterlerini doğru şekilde göreceksiniz.

---

## Adım 4: Çıkarılan Metni Görüntüle

Son olarak, sonucu yazdıralım. Çıktı, motorun çözebildiği her karakteri, o sinir bozucu diakritik işaretler de dahil olmak üzere içerecek.

```python
# Step 4: Show what we extracted
print("=== OCR RESULT ===")
print(recognized_text)
```

**Örnek çıktı** (gerçek sonucunuz görüntü içeriğine bağlı olacaktır):

```
=== OCR RESULT ===
Łąka žužuҖß – multilingual test string
```

*Görsel örneği:*  
![Görselden metin çıkarma örnek çıktısı](https://example.com/ocr-output.png "Görselden metin çıkarma örnek çıktısı")

> **Not:** `print` çağrısı modern Python’da varsayılan olarak UTF‑8 kodlamasını kullanır, bu yüzden çoğu terminalde özel karakterleri doğru şekilde görmelisiniz. Eğer bozuk çıktı alırsanız, konsolunuzu UTF‑8’e ayarlayın veya dizeyi `encoding='utf-8'` ile bir dosyaya yazın.

---

## Adım 5: Kenar Durumlarını ve Yaygın Tuzakları Ele Alma

### 5.1 Düşük Çözünürlüklü Görüntüler

Görüntü 150 dpi’nin altında ise OCR doğruluğu büyük ölçüde düşebilir. Hızlı bir çözüm, aocr’a vermeden önce ölçeği artırmaktır:

```python
from PIL import Image

img = Image.open(image_path)
img = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
img.save("upscaled.png")
ocr_engine.load_image("upscaled.png")
```

### 5.2 Yanlış Dil Algılama

aocr dili otomatik algılar, ancak daha iyi sonuçlar için belirli bir betiği zorlayabilirsiniz:

```python
ocr_engine.set_language("rus")   # forces Cyrillic detection
```

Desteklenen dil kodları `eng`, `deu`, `fra`, `rus`, `spa` vb. içerir.

### 5.3 Gürültü ve Arka Plan Desenleri

Gürültülü bir arka plan modeli şaşırtabilir. OpenCV ile ön işleme yaparak ikiliye dönüştürün:

```python
import cv2

raw = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
_, thresh = cv2.threshold(raw, 127, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
cv2.imwrite("clean.png", thresh)
ocr_engine.load_image("clean.png")
```

---

## Tam Betik – Tek‑Tık Çözüm

Aşağıda **tam, çalıştırılabilir örnek** yer alıyor ve tüm parçaları birleştiriyor. `ocr_demo.py` olarak kaydedin ve `python ocr_demo.py` komutunu çalıştırın.

```python
# ocr_demo.py
# -------------------------------------------------
# Complete example: extract text from image using aocr
# -------------------------------------------------

import aocr
from pathlib import Path
import sys

def main(image_path: str):
    # Verify the file exists early – gives a nicer error message
    if not Path(image_path).is_file():
        sys.exit(f"❌ File not found: {image_path}")

    # 1️⃣ Create OCR engine
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Load the image (you can also call preprocess_image() here)
    ocr_engine.load_image(image_path)

    # Optional: force language if you know it (uncomment)
    # ocr_engine.set_language("eng")

    # 3️⃣ Run OCR – this is where we **convert image to text**
    recognized_text = ocr_engine.recognize()

    # 4️⃣ Output – includes special characters like Ł, Ž, Җ, ß
    print("\n=== OCR RESULT ===")
    print(recognized_text)

if __name__ == "__main__":
    # Example usage: python ocr_demo.py multilingual.png
    if len(sys.argv) != 2:
        sys.exit("Usage: python ocr_demo.py <path-to-image>")
    main(sys.argv[1])
```

Şöyle çalıştırın:

```bash
python ocr_demo.py YOUR_DIRECTORY/multilingual.png
```

Çıkarılan karakterlerin konsola yazdırıldığını görmelisiniz, bu da **görselden metin çıkarma** ve **özel karakterleri tanıma** işlemini başarıyla tamamladığınızı doğrular.

---

## Sıkça Sorulan Sorular

**S: Bu PDF'lerde çalışır mı?**  
C: Doğrudan değil. PDF sayfalarını önce görüntülere dönüştürün (ör. `pdf2image` kullanarak) ve ardından her görüntüyü aocr'a verin.

**S: aocr, Tesseract ile karşılaştırıldığında ne kadar hızlı?**  
C: Tipik 300 dpi taramalarda, aocr bir sayfayı modern bir dizüstü bilgisayarda ~0.3 s içinde işler—varsayılan ayarlarla saf Tesseract'tan yaklaşık iki kat daha hızlı.

**S: Görüntü klasörünü toplu işleyebilir miyim?**  
C: Kesinlikle. `main` fonksiyonunu `Path(folder).glob("*.png")` üzerinden bir döngüye sarın ve sonuçları bir CSV dosyasında toplayın.

---

## Sonuç

Artık Python’un aocr kütüphanesini kullanarak **görselden metin çıkarma** için sağlam, uçtan uca bir iş akışına sahipsiniz. Dosyayı yüklemekten Unicode çıktıyı yazdırmaya kadar her adım açıklanmıştır, böylece kendi projelerinize uyarlayabilirsiniz—ister bir fiş tarama hizmeti, ister çok dilli bir belge arşivi oluşturuyor olun.

Sonra, aşağıdaki ilgili konuları keşfetmeyi düşünün:

- **convert image to text** PDF'ler için (`pdf2image` + OCR kullanın)  
- **recognize special characters** el yazısı notlarda (`ocr_engine.set_dpi(600)` ile deneyin)  
- **load image for OCR** bir web API'de (Flask + aocr)  

Deneyin, dil ayarlarını değiştirin ve verilerinizin anında aranabilir hale geldiğini izleyin. Sorularınız veya ilginç bir kullanım senaryonuz mu var? Aşağıya yorum bırakın—mutlu kodlamalar!

## Sonra Ne Öğrenmelisiniz?

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR kullanarak C# ile görüntü metni çıkarma ve dil seçimi](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Görselden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}