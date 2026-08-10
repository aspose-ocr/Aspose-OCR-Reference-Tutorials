---
category: general
date: 2026-06-19
description: Python'da OCR kullanarak PDF'den metin nasıl çıkarılır – PDF'den metin
  çıkarma, görüntüden metin tanıma ve bir OCR Python örneği kapsayan adım adım öğretici.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: tr
og_description: Python'da OCR kullanarak PDF nasıl çıkarılır. PDF'den metin çıkarmayı,
  görüntüden metin tanımayı öğrenin ve tam bir OCR Python örneğini görün.
og_title: Python’da OCR ile PDF Metni Nasıl Çıkarılır – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Python’da OCR ile PDF Metni Nasıl Çıkarılır – Tam Kılavuz
url: /tr/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF Metnini OCR ile Python’da Nasıl Çıkarılır – Tam Kılavuz

Sadece taranmış bir görüntü olduğunda **PDF içeriğini nasıl çıkaracağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—sözleşmeler, faturalar veya tarihi arşivler gibi—aldığınız PDF seçilebilir metin içermez. İyi haber? Birkaç Python satırı bu yalnızca görüntü sayfalarını aranabilir, düzenlenebilir metne dönüştürebilir.

Bu öğreticide, bir PDF okuyan, ilk sayfasını görüntü olarak işleyen ve ardından bir OCR motoru kullanarak **PDF'den metin çıkarır** pratik bir **OCR Python örneği** üzerinden ilerleyeceğiz. Sonunda **OCR ile PDF okuma** yöntemini tam olarak öğrenecek, her adımın neden önemli olduğunu anlayacak ve kodu çok sayfalı belgeler veya farklı diller için nasıl uyarlayacağınızı göreceksiniz.

## Öğrenecekleriniz

- Python için güvenilir bir OCR kütüphanesini kurun ve yapılandırın.  
- PDF sayfalarını OCR için uygun görüntülere dönüştürün.  
- **Görüntüden metin tanıma** ve temiz Unicode dizgileri alın.  
- Ortak tuzaklar (düşük çözünürlüklü PDF'ler, döndürülmüş sayfalar) ve bunlardan nasıl kaçınılır.  
- Betik genişletilerek birden çok sayfa veya toplu işleme desteklenir.

**Önkoşullar**: Python 3.8+, pip ve sanal ortamlar hakkında temel bir anlayış. Önceden OCR deneyimi gerekmez—sadece takip edin.

---

## ## OCR ile Python’da PDF Metni Nasıl Çıkarılır

Bu H2 başlığı, anahtar kelimemizi arama motorlarının sevdiği yerde içerir. Hadi doğrudan koda dalalım.

### Adım 1 – Gerekli Paketleri Kurun

İlk olarak bir OCR motoruna ihtiyacımız var. Aşağıdaki örnek popüler **ocr** paketini (Tesseract'ın ince bir sarmalayıcısı) kullanıyor. Farklı bir arka uç tercih ederseniz, kavramlar aynı kalır.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro ipucu:** Linux'ta ayrıca Tesseract ikili dosyasına ihtiyacınız olacak: `sudo apt-get install tesseract-ocr`. macOS kullanıcıları Homebrew üzerinden alabilir: `brew install tesseract`.

### Adım 2 – OCR Motorunu Başlatın ve Dili Ayarlayın

Şimdi motoru çalıştırıp İngilizce karakterleri aramasını söylüyoruz. `ocr.Language.English` ifadesini desteklenen herhangi bir dil kodu ile değiştirebilirsiniz.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Neden önemli:** Dili belirtmek, motorun dil‑spesifik sözlükler ve karakter modelleri uygulayabilmesi sayesinde doğruluğu büyük ölçüde artırır.

### Adım 3 – PDF Sayfasını Görüntü Olarak Yükleyin

OCR, PDF nesneleri yerine raster görüntüler üzerinde çalışır. `ocr.Image.from_pdf` yardımcı işlevi seçilen sayfayı bitmap olarak işler. Diğer sayfalar için `page_number` değerini ayarlayın (0‑tabanlı indeksleme).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Köşe durumu:** PDF taranmış görüntüler yerine vektör grafikler içeriyorsa, net bir işleme alabilirsiniz. Düşük çözünürlüklü taramalar için DPI'yi artırmayı düşünün: `ocr.Image.from_pdf(..., dpi=300)`.

### Adım 4 – İşlenen Görüntüden Metin Tanıma

İşte **ocr python örneği**nin kalbi. Motor bitmap'i işler ve çıkarılan dizeyi içeren bir nesne döndürür.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

`ocr_result.text` özniteliği, mümkün olduğunda satır sonlarını koruyan düz metin çıktısını tutar.

### Adım 5 – Çıkarılan Metni Yazdırın veya Saklayın

Son olarak sonucu çıktılarız. Gerçek bir uygulamada muhtemelen bir dosyaya veya veritabanına yazarsınız.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Betik çalıştırıldığında aşağıdakine benzer bir şey göstermelidir:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Bu, OCR kullanarak tam bir **extract text from pdf** iş akışıdır.

---

## ## Görüntüden Metin Tanıma – Doğruluğu Ayarlama

Sadece **recognize text from image** (örneğin bir makbuzun JPEG'i) ile ilgileniyorsanız, PDF dönüştürme adımını atlayabilirsiniz:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Daha iyi sonuçlar için ipuçları:**

- **Ön‑işleme**: görüntüyü gri tonlamaya dönüştürün, eşikleme uygulayın veya eğikliği düzeltin. Pillow bunu kolaylaştırır.
- PDF işleme sırasında **DPI'yi artırın**: daha yüksek çözünürlük OCR motoruna daha fazla detay sağlar.
- Sayfa segmentasyonu için OCR motorunun **konfigürasyonunu etkinleştirin** (`ocr_engine.config = "--psm 6"` tek tip bloklar için).

## ## OCR ile PDF Okuma – Çoklu Sayfaları İşleme

Çoğu sözleşme birkaç sayfadan oluşur. Her sayfayı döngüyle işlemek basittir:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Bu fonksiyon **OCR ile PDF okur**, çıktıyı birleştirir ve net bir sayfa sonu işareti ekler. Ardından `full_text`'i bir arama indeksine besleyebilir veya `.txt` dosyası olarak saklayabilirsiniz.

## ## Yaygın Tuzaklar ve Çözümleri

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| Bozuk karakterler, çok sayıda `?` | Yanlış dil veya eksik dil veri dosyaları | Doğru Tesseract dil paketini (`tesseract-ocr-<lang>`) kurun ve `ocr_engine.language` ayarlayın. |
| Eksik satırlar veya kesik kelimeler | Düşük DPI (150'nin altında) | PDF'i 300 DPI veya daha yüksek (`dpi=300`) renderlayın. |
| Metin döndürülmüş veya ters | Taran sayfa dikey değil | Tanımadan önce `ocr.Image.deskew(page_image)` kullanın. |
| Büyük PDF'lerde yavaş işleme | Sayfalar tek bir iş parçacığında sırayla işleniyor | `concurrent.futures.ThreadPoolExecutor` ile paralelleştirin. |

## ## OCR Python Örneğini Genişletme

- **PDF/A'ya dışa aktar**: Çıkarma sonrası metni `reportlab` veya `pypdf2` kullanarak aranabilir bir PDF'e gömebilirsiniz.
- **Dil algılama**: OCR çıktısında `langdetect` kullanarak `ocr_engine.language`'ı dinamik olarak değiştirebilirsiniz.
- **Toplu işleme**: `os.listdir` ile bir dizini dolaşın ve `extract_all_pages` fonksiyonunu her dosyaya uygulayın.

## ## Beklenen Çıktı ve Doğrulama

Betik, net bir İngilizce tarama üzerinde çalıştırıldığında, uygun noktalama işaretleriyle temiz bir metin bloğu görmelisiniz. Doğrulamak için:

1. Birkaç satırı orijinal taranmış görüntüyle karşılaştırmak.  
2. Çıktının boş olmadığını kontrol etmek için basit bir kelime sayımı çalıştırmak (`len(ocr_result.text.split())`).  
3. İsteğe bağlı olarak, sonucu `pyspellchecker` gibi bir yazım denetleyicisine besleyerek OCR hatalarını tespit etmek.

## Sonuç

Geleneksel ayrıştırmanın başarısız olduğu durumlarda **PDF içeriğini nasıl çıkaracağınızı** ele aldık, tam bir **ocr python örneği** gösterdik ve hem tek sayfalı hem çok sayfalı senaryolar için **görüntüden metin tanıma** ve **OCR ile PDF okuma** yöntemlerini açıkladık. Yukarıdaki kod parçacıklarıyla artık herhangi bir taranmış PDF'yi aranabilir, düzenlenebilir metne dönüştürebilirsiniz—artık manuel yeniden yazma yok.

Sonraki adımlar? Dili İspanyolcaya (`ocr.Language.Spanish`) değiştirin veya doğruluğu artırmak için görüntü ön‑işleme teknikleriyle deney yapın. Bir belge‑yönetim sistemi oluşturuyorsanız, çıkarılan metni Elasticsearch ile indekslemeyi düşünün, böylece ışık hızında arama elde edersiniz.

Sorularınız mı var ya da tuhaf bir PDF ile mi karşılaştınız? Yorum bırakın, iyi kodlamalar!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [PDF Metnini Tanıma – Aspose.OCR ile Java için OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Aspose.OCR kullanarak C# ile görüntü metni çıkarma ve dil seçimi](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}