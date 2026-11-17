---
category: general
date: 2026-03-18
description: Aspose OCR'i Python'da kullanarak görüntülerden metin çıkarmayı ve taranmış
  görüntülerin metnini düzenlenebilir dizelere dönüştürmeyi öğrenin. Adım adım kod
  dahil.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: tr
og_description: Aspose OCR'i Python'da kullanarak görüntülerden metin çıkarın. Bu
  öğreticide, taranmış görüntülerdeki metni sadece birkaç satır kodla nasıl dönüştüreceğinizi
  gösteriyoruz.
og_title: Aspose OCR ile Görsellerden Metin Çıkarma – Python Rehberi
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Aspose OCR ile Görsellerden Metin Çıkarma – Python Rehberi
url: /tr/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görsellerden Metin Çıkarma – Aspose OCR – Python Kılavuzu

Hiç **görsellerden metin çıkarmak** gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli taranmış PDF'leri, gürültülü ekran görüntülerini veya fotoğraflanmış fişleri aranabilir, düzenlenebilir string'lere dönüştürme zahmetiyle karşılaşıyor.  

İyi haber? Aspose OCR for Python ile **tarama görüntülerinin metnini** toplu olarak, IDE'nizden çıkmadan dönüştürebilirsiniz. Bu öğreticide, tam olarak nasıl yapılacağını, her adımın neden önemli olduğunu ve nelere dikkat etmeniz gerektiğini gösteren çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

## Öğrenecekleriniz

- Python ortamında Aspose OCR kütüphanesini kurma.  
- Görsel dosyalarının (PNG, JPG, TIFF vb.) bir listesini hazırlama.  
- Tek bir metod çağrısı ile toplu OCR çalıştırma.  
- Her dosya için çıkarılan metni erişme ve gösterme.  
- Desteklenmeyen formatlar ve büyük dosya bellek kullanımı gibi yaygın tuzakları ele alma.  

Sonunda, **görsellerden metin çıkarma** ihtiyacını karşılayacak yeniden kullanılabilir bir betiğe sahip olacaksınız—veri girişi otomasyonu, belge indeksleme veya sonraki NLP boru hatlarını besleme için mükemmel.

---

![Extract text from images example](/images/ocr-extract-text.png "görsellerden metin çıkarma")

*Image alt text: “Python’da Aspose OCR kullanarak görsellerden metin çıkarma”*

## Ön Koşullar

- Python 3.8 ve üzeri (kod f‑string kullanıyor).  
- Geçerli bir Aspose OCR for Python lisansı veya ücretsiz deneme anahtarı.  
- İşlemek istediğiniz görseller yerel olarak depolanmış (PNG, JPG veya TIFF karışık olabilir).  

Zaten bir sanal ortamınız varsa harika—yoksa şu komutla bir tane oluşturun:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Artık SDK'yı kurmaya hazırsınız.

## Adım 1: Aspose OCR SDK'yı Kurun

Aspose OCR motorunu PyPI üzerinden dağıtıyor, bu yüzden tek bir `pip` komutu yeterli:

```bash
pip install aspose-ocr
```

> **Pro ipucu:** Daha sonra beklenmedik kırılma değişikliklerinden kaçınmak için sürümü sabitleyin (ör. `aspose-ocr==22.12`).

## Adım 2: OCR Motoru Sınıfını İçe Aktarın

İle çalışacağınız temel sınıf `OcrEngine`. Betiğinizin en üstüne şu satırı ekleyin:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Neden önemli:* Sadece ihtiyacınız olanı içe aktarmak, özellikle betiği daha büyük bir uygulamaya entegre ettiğinizde başlangıç süresini düşük tutar.

## Adım 3: İşlenecek Görsel Dosyalarını Tanımlayın

Tarama yapmak istediğiniz her görselin tam yolunu içeren bir Python listesi oluşturun. `YOUR_DIRECTORY` kısmını gerçek klasör yolunuzla değiştirin.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Köşe durumu:** Yüzlerce dosyanız varsa, manuel düzenlemelerden kaçınmak için `glob.glob('*.png')` gibi bir yöntemle bu listeyi programlı olarak oluşturmayı düşünün.

## Adım 4: Tüm Görselleri Tek Seferde OCR'a Gönderin

Aspose OCR, `processMultiple` adlı kullanışlı bir metod sunar; bu metod, her giriş dosyası için bir `OcrResult` nesnesi içeren bir liste döndürür.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Neden toplu işleme?* Her görseli ayrı ayrı göndermek ekstra yük oluşturur (motorun başlatılması, yerel kütüphanelerin yüklenmesi). Toplu çağrı CPU kullanımını azaltır ve genel işi hızlandırır.

### Hataları Zarifçe Ele Alma

Bir görsel okunamazsa (bozuk dosya, desteklenmeyen format), `processMultiple` bir istisna fırlatır. Betiğin çalışmaya devam etmesi için çağrıyı `try/except` bloğuna alın:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Adım 5: Her Dosya İçin Çıkarılan Metni Görüntüleyin

Sonuçlar üzerinde döngü kurun, her `OcrResult` nesnesini orijinal dosya adıyla eşleştirin. `getText()` metodu tanınan string'i döndürür.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Beklenen Çıktı

Tam betiği üç basit ekran görüntüsü üzerinde çalıştırdığınızda aşağıdaki gibi bir çıktı alabilirsiniz:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Bir görsel tanınabilir karakter içermiyorsa boş bir string görürsünüz—hiçbir şey kırılmaz ve bu dosyayı manuel inceleme için işaretleyip işaretlemeyeceğinize karar verebilirsiniz.

## Bonus: OCR Doğruluğunu İnce Ayar Yapma

Aspose OCR, denemek isteyebileceğiniz birkaç isteğe bağlı ayar sunar:

| Ayar | Ne İşe Yarar | Ne Zaman Kullanılır |
|------|--------------|---------------------|
| `ocr_engine.setLanguage('eng')` | İngilizce dil modelini zorlar (yanlış pozitifleri azaltır). | Çoğunlukla İngilizce belgeler. |
| `ocr_engine.setResolution(300)` | Düşük dpi taramalarda doğruluğu artırır. | 200 dpi’nin altındaki taramalar. |
| `ocr_engine.setPageSegMode('single_block')` | Tüm görseli tek bir metin bloğu olarak işler. | Basit fişler veya kimlik kartları. |

Bu satırları `ocr_engine` oluşturduktan hemen sonra ekleyebilirsiniz:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Yaygın Tuzaklar ve Önleme Yöntemleri

1. **Büyük TIFF yığınları** – Çok sayfalı bir TIFF, tüm sayfalar aynı anda yüklendiğinde gigabaytlarca RAM tüketebilir. `processMultiple`'a göndermeden önce dosyayı tek‑sayfalı görsellere bölün.  
2. **Latin dışı yazı sistemleri** – **görsellerden metin çıkarma** işlemi sırasında Kiril, Arapça veya Çince karakterler varsa dil kodunu uygun şekilde değiştirin (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Dosya yolu boşlukları** – Boşluk içeren Windows yolları `FileNotFoundError` oluşturabilir. Her yolu raw string olarak sarın (`r"C:\My Folder\image.png"`) veya `os.path.abspath` kullanın.  

Bu sorunları önceden ele almak, ileride karşılaşabileceğiniz belirsiz çalışma zamanı hatalarını önler.

---

## Tam Çalışan Örnek

Aşağıda `batch_ocr.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz eksiksiz betik yer alıyor. Yukarıda tartıştığımız en iyi uygulama ayarlarını içeriyor.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Kaydedin, sanal ortamınızı etkinleştirin ve çalıştırın:

```bash
python batch_ocr.py
```

Çıkarılan string'lerin konsola yazdırıldığını göreceksiniz; bunları veritabanına kaydetmek veya bir doğal dil modeli beslemek gibi sonraki adımlara hazır hale getirebilirsiniz.

---

## Sonuç

Bu rehberde, Aspose OCR for Python kullanarak **görsellerden metin çıkarma** sürecini, kurulumdan toplu işleme ve hata yönetimine kadar tüm adımlarla gösterdik. Betik kompakt, tamamen işlevsel ve genişletmesi kolay—ister taranmış görüntü metnini CSV dosyalarına dönüştürmek, bir arama indeksine beslemek, ister sadece veri girişini otomatikleştirmek için kullanın.

Bir sonraki adım için hazır mısınız? Bu OCR boru hattını bir PDF birleştiriciyle eşleştirerek aranabilir PDF'ler oluşturabilir veya bir bulut depolama tetikleyicisine bağlayarak her yüklenen taramayı anında işleyebilirsiniz. Ufkunuz geniş, ve artık üzerine inşa edebileceğiniz sağlam bir temeliniz var.

Sorularınız veya geliştirme önerileriniz mi var? Aşağıya yorum bırakın, mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}