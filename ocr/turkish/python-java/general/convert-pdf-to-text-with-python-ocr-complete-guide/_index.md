---
category: general
date: 2026-07-05
description: Python OCR kullanarak PDF'yi metne dönüştürün. PDF'den metin çıkarmayı,
  toplu OCR işleme yapmayı ve birkaç kolay adımda OCR için PDF yüklemeyi öğrenin.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: tr
og_description: PDF'yi hızlıca metne dönüştürün. Bu öğretici, PDF'den metin çıkarmayı,
  toplu OCR işleme çalıştırmayı ve Python kullanarak taranmış PDF dosyalarını tanımayı
  gösterir.
og_title: Python OCR ile PDF'yi Metne Dönüştür – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Python OCR ile PDF'yi Metne Dönüştür – Tam Kılavuz
url: /tr/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'yi Python OCR ile Metne Dönüştür – Tam Kılavuz

Hiç **convert PDF to text** yaparken zorlanmadan merak ettiniz mi? Belki taranmış sözleşmeler, faturalar veya araştırma makaleleri yığınına sahipsiniz ve indeksleme ya da analiz için düz‑metin sürümüne ihtiyacınız var. İyi haber şu ki, birkaç satır Python kodu bu işi sizin için halledebilir.

Bu öğreticide, sadece **convert pdf to text** yapmakla kalmayıp, aynı zamanda **extract text from pdf** nasıl yapılır, **batch OCR processing** nasıl kurulur ve **load pdf for OCR** doğru şekilde nasıl yapılır gösteren pratik bir çözüm üzerinden ilerleyeceğiz. Sonunda, **recognize scanned pdf** sayfalarını tek seferde tanıyabilen, çalıştırmaya hazır bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

- Python OCR kütüphanesini kurun ve yapılandırın (örnek olarak genel bir `ocr` paketini kullanacağız).  
- Çok sayfalı bir PDF yükleyin ve OCR motoruna besleyin.  
- Sonuçlar üzerinde döngü kurarak çıkarılan metni yazdırın veya kaydedin.  
- Büyük dosyalar, şifreli PDF'ler ve karışık dil belgeleri gibi yaygın kenar durumlarını ele alın.  

Ağır GUI araçları yok, manuel kopyalama yok—sadece CI boru hattına veya bir masaüstü yardımcı programına ekleyebileceğiniz saf kod.

![Python OCR ile PDF'yi Metne Dönüştür](https://example.com/images/convert-pdf-to-text.png "Python OCR ile PDF'yi Metne Dönüştür")

## Önkoşullar

İlerlemeye başlamadan önce, şunların olduğundan emin olun:

| Gereksinim | Neden Önemli |
|------------|--------------|
| Python 3.9+ | Modern sözdizimi, tip ipuçları ve daha iyi performans. |
| `ocr` library (or a wrapper around Tesseract) | Örnekte kullanılan `OcrEngine`, `Language` ve `Image` sınıflarını sağlar. |
| A multi‑page scanned PDF (e.g., `contract.pdf`) | Bu, **load pdf for OCR** yapacağınız kaynaktır. |
| Basic command‑line familiarity | Paketleri kurmak ve betiği çalıştırmak için. |

Eğer Tesseract'ı altyapı olarak kullanıyorsanız, işletim sisteminizin paket yöneticisiyle kurun (`apt-get install tesseract-ocr` Linux'ta, `brew install tesseract` macOS'ta). Ardından Python sarmalayıcısını ekleyin:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## Adım 1: OCR Motorunu Oluşturun ve Tanıma Dilini Ayarlayın

İlk olarak bir OCR motoru örneğine ihtiyacımız var. Dili İngilizce olarak ayarlamak yaygın bir varsayılandır, ancak daha sonra diğer desteklenen dillere geçebilirsiniz.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**Neden önemli:** Motor, piksel verisini yorumlayan beyin gibidir. `engine.language`'i açıkça tanımlayarak, her sayfada dil algılamanın getirdiği ek yükten kaçınır ve **batch OCR processing**'i önemli ölçüde hızlandırırsınız.

## Adım 2: PDF Belgesini OCR için Yükleyin

Şimdi PDF'yi belleğe alıyoruz. `ocr.Image.load` yöntemi bir dosya yolunu kabul eder ve motorun anlayabileceği bir nesne döndürür.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**İpucu:** PDF'niz şifre korumalıysa, çoğu kütüphane bir `password` argümanı almanıza izin verir. Bunu erken ele almak, daha sonra karşılaşabileceğiniz belirsiz “cannot open file” hatasını önler.

## Adım 3: Tüm Sayfalarda OCR Çalıştırın – Tek Çağrıda Taranmış PDF'yi Tanıyın

OCR'yi sayfa sayfa çalıştırmak büyük belgelerde yavaş olabilir. `recognize_multi_page` yöntemi, mümkün olduğunda birden çok iş parçacığı kullanarak, dahili olarak **batch OCR processing** gerçekleştirir.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**Arka planda ne oluyor?** Motor, her sayfayı temel OCR motoruna (örneğin Tesseract) akıtır, metni toplar ve bir `OcrResult` içinde paketler. Bu yaklaşım I/O yükünü azaltır ve daha sonra **extract text from pdf** için temiz bir yol sunar.

## Adım 4: Sonuçlar Üzerinde Döngü Kurun ve Tanınan Metni Çıktılayın

Son olarak, her `OcrResult` üzerinde döngü kurar ve metni yazdırırız. Ayrıca her sayfayı ayrı bir `.txt` dosyasına yazabilir veya tek bir belgeye birleştirebilirsiniz.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**Neden enumerate?** `enumerate(..., start=1)` kullanmak, insan tarafından okunabilir bir sayfa numarası sağlar; bu, daha sonra orijinal PDF'nin belirli bir bölümüne referans vermeniz gerektiğinde kullanışlıdır.

### Beklenen Çıktı

Betik, 3 sayfalı bir sözleşme üzerinde çalıştırıldığında şu çıktıyı üretebilir:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

Bir sayfada tanınabilir metin yoksa, ilgili `result.text` boş bir dize olacaktır—boş veya sadece görüntü içeren sayfaları tespit etmek için mükemmeldir.

## Büyük PDF'leri ve Bellek Kısıtlamalarını Ele Alma

500 sayfalık bir PDF'yi işlemek, her şeyi bir anda yüklerseniz RAM'i tüketebilir. İşte iki strateji:

1. **Chunked Loading** – Bazı kütüphaneler bir sayfa aralığını yüklemenize izin verir:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **Streaming to Disk** – Tüm listeyi bellekte tutmak yerine, her sayfanın metnini doğrudan bir dosyaya yazın.

Her iki teknik de **convert pdf to text** iş akışınızı ölçeklenebilir tutar.

## Hatalar ve Kenar Durumlarıyla Baş Etme

- **Encrypted PDFs** – `Image.load`'a şifreyi geçirin:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **Mixed Languages** – Farklı bir betik tespit ederseniz, sayfa başına dili değiştirin:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **Low‑Resolution Scans** – OCR'den önce kontrastı artırmak için `Pillow` gibi bir kütüphane ile görüntüleri ön işleme tabi tutun. Bu, **recognize scanned pdf** adımının kalitesini büyük ölçüde artırabilir.

## Tam Betik: PDF'yi Tek Çalışmada Metne Dönüştür

Aşağıda, her şeyi bir araya getiren tam, çalıştırmaya hazır betik yer alıyor. `pdf_to_text.py` olarak kaydedin ve `python pdf_to_text.py` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**Betik çalıştırıldığında**, `page_1.txt`, `page_2.txt` vb. dosyaları içeren bir `output` klasörü oluşturulur ve **extract text from pdf** işlemini yapılandırılmış bir şekilde gerçekleştirir.

## Çözümü Test Etme

1. **Sanity Check** – Oluşturulan bir `.txt` dosyasını açın ve ilk birkaç satırın orijinal belgenin başlığıyla eşleştiğini doğrulayın.
2. **Performance Test** – `time` komutunu kullanarak 100 sayfalık bir PDF üzerinde betiğin süresini ölçün. Beklenenden uzun sürerse, kütüphanenin çoklu iş parçacığı bayrağını (genellikle `engine.set_threads(4)`) etkinleştirmeyi düşünün.
3. **Quality Assurance** – OCR çıktısını, elle yazılmış bir alıntı ile diff aracıyla karşılaştırın. Temiz taramalar için %95'in üzerinde karakter doğruluğu hedefleyin.

## Sonraki Adımlar ve İlgili Konular

- **Improve Accuracy**: `engine.dpi = 300` ile deney yapın veya OCR'den önce görüntü ön işleme (düzleştirme, gürültü azaltma) uygulayın.  
- **Searchable PDFs**: Çıkarılan metni orijinal PDF'ye gömmek için bir PDF kütüphanesi (örneğin `PyPDF2` veya `pdfplumber`) kullanın, böylece aranabilir hale gelir.  
- **Natural Language Processing**: Çıkarılan metni spaCy veya NLTK'ye besleyerek varlık çıkarımı, duygu analizi veya anahtar kelime etiketleme yapın.  
- **Automation Pipelines**: Bu betiği `watchdog` ile birleştirerek bir klasörü izleyin ve yeni bir dosya ortaya çıktığında otomatik olarak **convert pdf to text** yapın.

Bu kalıpları ustalaşarak, şunları yapabileceksiniz

## Sonra Ne Öğrenmelisiniz?

Bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}