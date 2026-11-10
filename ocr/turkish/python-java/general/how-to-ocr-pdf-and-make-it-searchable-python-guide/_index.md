---
category: general
date: 2026-01-12
description: Python'da PDF'yi OCR'lamayı ve PDF'yi hızlıca aranabilir hâle getirmeyi
  öğrenin. Tarama yapılan PDF'yi dönüştürün, metin PDF'sini çıkarın ve Aspose OCR
  kullanarak Python'da taranmış PDF'yi OCR'layın.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: tr
og_description: Python'da PDF'yi OCR nasıl yapılır? Bu adım adım öğretici, taranmış
  PDF dosyalarını aranabilir PDF'lere dönüştürmeyi ve Aspose OCR ile metin çıkarmayı
  gösterir.
og_title: PDF'yi OCR'leyerek Aranabilir Hale Getirme – Python Rehberi
tags:
- OCR
- Python
- PDF processing
title: PDF'yi OCR'layarak Aranabilir Hale Getirme – Python Rehberi
url: /tr/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'yi OCR'leyin ve Aranabilir Hale Getirin – Python Rehberi

Ticari yazılımlara büyük bir bütçe harcamadan **PDF'yi OCR'leme** yollarını hiç merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, taranmış bir sözleşme, fatura ya da herhangi bir görüntü‑tabanlı PDF'yi aranabilir bir belgeye dönüştürmek zorunda kaldığında bir duvara çarpar. İyi haber? Birkaç satır Python ve Aspose OCR ile taranmış PDF'yi dönüştürebilir, metin PDF'si çıkarabilir ve sonunda PDF'yi dakikalar içinde aranabilir hâle getirebilirsiniz.

Bu öğreticide ihtiyacınız olan her şeyi adım adım göstereceğiz: kütüphaneyi kurmaktan, dili yapılandırmaya, taranmış bir PDF'yi işlemeye ve sonucun hem orijinal görüntüyü hem de gizli bir metin katmanını içeren aranabilir bir PDF olarak kaydedilmesine kadar. Sonunda, herhangi bir projeye ekleyebileceğiniz, manuel kopyala‑yapıştırma gerektirmeyen yeniden kullanılabilir bir betiğiniz olacak.

---

## Gereksinimler

- **Python 3.8+** (kod 3.9, 3.10 ve daha yeni sürümlerde çalışır)
- Aktif bir **Aspose OCR for Python** lisansı (deneme sürümü deneyler için yeterlidir)
- Aranabilir hâle getirmek istediğiniz taranmış bir PDF dosyası (ör. `scanned_contract.pdf`)
- Komut satırı ve sanal ortamlarla temel aşinalık (isteğe bağlı ancak önerilir)

> **Pro ipucu:** Henüz bir lisansınız yoksa, Aspose web sitesinde 30‑günlük bir deneme kaydı oluşturun; deneme sürümü geliştirme amaçları için tam işlevseldir.

## Aspose OCR ile PDF'yi OCR'leme (H2'de Birincil Anahtar Kelime)

İlk adım doğru paketi edinmek. Aspose OCR, düşük seviyeli görüntü işleme detaylarını soyutlayan temiz, yüksek‑seviyeli bir API sunar.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

Paket kurulduktan sonra betiği yazmaya başlayabilirsiniz.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Dili neden ayarlamalısınız?**  
> OCR doğruluğu büyük ölçüde dil modeline bağlıdır. Motoru açıkça İngilizce metin bekleyecek şekilde ayarlayarak yanlış pozitifleri azaltır ve işleme süresini hızlandırırsınız.

## Adım 2: Taran PDF'yi Aranabilir PDF'ye Dönüştürme

Motor hazır olduğuna göre, onu taranmış belgenize yönlendirin. `process_pdf` yöntemi, hem orijinal görüntü verisini hem de tanınan metni içeren bir `PdfResult` nesnesi döndürür.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

Eğer **taran PDF** dosyalarını toplu olarak **dönüştürmeniz** gerekiyorsa, bir dizin üzerinde döngü kurup her dosya için `process_pdf` çağırmanız yeterlidir. Motor, çok sayfalı PDF'leri kutudan çıkar çıkmaz destekler.

## Adım 3: Sonucu Aranabilir PDF Olarak Kaydetme (PDF'yi Aranabilir Hale Getirme)

Bulmacanın son parçası, aranabilir sürümü kalıcı hâle getirmektir. Aspose OCR bunu tek satırda yapar:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

`contract_searchable.pdf` dosyasını herhangi bir PDF görüntüleyicide açtığınızda, orijinal taranmış görüntüyü göreceksiniz, ancak artık **OCR motorunun tanıdığı herhangi bir kelimeyi** arayabilirsiniz. Gizli metin katmanı göze görünmez ancak tamamen indekslenebilir.

### Tam Script – Çalıştırmaya Hazır

Aşağıda eksiksiz, çalıştırılabilir bir örnek bulacaksınız. `make_searchable.py` adlı bir dosyaya kopyalayıp yapıştırın ve ortamınıza uygun yolları ayarlayın.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**Beklenen çıktı:**  
Betik çalıştırıldığında bir onay satırı yazdırır ve `contract_searchable.pdf` oluşturur. Dosyayı açın, `Ctrl + F` tuşlarına basın ve orijinal taranmış görüntüde yer alan herhangi bir kelimeyi yazın—ankâra anında eşleşmeler görmelisiniz.

## Yaygın Sorular ve Kenar Durumları

### 1. PDF birden fazla dil içeriyorsa ne olur?

Motora bir dil listesi geçirebilirsiniz:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR, aynı sayfadaki iki dili de tanımaya çalışacaktır.

### 2. Düşük çözünürlüklü taramaları nasıl ele alırım?

Kaynak görüntüler 150 dpi’nin altında ise OCR doğruluğu azalabilir. PDF'yi `pdfimages` gibi bir araçla sayfalara ayırın, Pillow ile ölçeklendirin ve daha yüksek çözünürlüklü görüntüleri `process_pdf`'a geri besleyin.

### 3. Aranabilir PDF oluşturmadan düz metni çıkarabilir miyim?

Kesinlikle. `PdfResult` nesnesi bir `text` özelliği sunar:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

Bu, yalnızca ham karakterlere ihtiyacınız olduğunda **extract text pdf** kullanım senaryosunu karşılar.

### 4. PDF klasörünü toplu işleme yapmanın bir yolu var mı?

Evet—`ocr_to_searchable` fonksiyonunu basit bir döngü içinde sarın:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

Artık tek bir komutla **taran pdf** dosyalarını toplu olarak **dönüştürebilirsiniz**.

## Performans İpuçları

- **Motoru yeniden kullanın**: Her dosya için yeni bir `OcrEngine` oluşturmak ek yük getirir. Bir kez örnekleyin ve birden çok çağrıda yeniden kullanın.
- **Paralel işleme**: Büyük toplular için Python’un `concurrent.futures.ThreadPoolExecutor`’ını düşünün—Aspose OCR, yalnızca okuma işlemleri için iş parçacığı‑güvenlidir.
- **Bellek yönetimi**: Çok sayfalı (yüzlerce sayfa) PDF'leri işliyorsanız, her dosyadan sonra `gc.collect()` çağırarak belleği boşaltın.

## Sonuç

Python’da **PDF'yi OCR'leme** yollarını ele aldık, bu taramaları **aranabilir PDF'lere** dönüştürdük ve hatta **extract text PDF**'yi doğrudan nasıl çıkaracağınızı gösterdik. Aspose OCR ile çok sayfalı belgeler, birden fazla dil ve yüksek doğruluklu tanıma gibi görevleri sadece birkaç satır kodla halledebileceğiniz güvenilir bir motor elde edersiniz.

Kendi sözleşmeleriniz, faturalarınız veya arşivlenmiş araştırma makaleleriniz üzerinde deneyin. Temelleri kavradıktan sonra, özel sözlükler, görüntü ön işleme veya çıktıyı Elasticsearch gibi tam metin arama indeksine entegre etme gibi gelişmiş özelliklerle denemeler yapın.

**ocr scanned pdf python** hakkında daha fazla sorunuz mu var ya da zor bir tarama için yardım mı gerekiyor? Aşağıya yorum bırakın, iyi kodlamalar!

--- 

![ocr pdf örneği](image-placeholder.png){alt="ocr pdf örneği"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}