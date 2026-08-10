---
category: general
date: 2026-06-22
description: Python’da PDF dosyalarını OCR ile nasıl okuyacağınızı, PDF’den metin
  çıkartmayı ve akış‑tabanlı bir yöntemle PDF’yi metne dönüştürmeyi öğrenin. Tarama
  yapılmış PDF’leri işlemek için basit adımlar.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: tr
og_description: Python'da PDF dosyalarını OCR ile nasıl işleyebilirsiniz? PDF'den
  metin çıkarmak, PDF'yi metne dönüştürmek ve taranmış PDF'yi bir akış kullanarak
  işlemek için bu rehberi izleyin.
og_title: Python'da PDF'yi OCR ile İşlemek – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Python'da PDF'yi OCR ile İşlemek – PDF'lerden Metin Çıkarma İçin Tam Kılavuz
url: /tr/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da PDF OCR Nasıl Yapılır – PDF'lerden Metin Çıkarma İçin Tam Kılavuz

Hiç **PDF OCR nasıl yapılır** diye merak ettiniz mi, ağır masaüstü araçlarıyla uğraşmadan? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—örneğin fatura otomasyonu ya da arşiv taramaları dijitalleştirirken—taratılmış bir PDF'i aranabilir, düzenlenebilir metne dönüştürmenin güvenilir bir yoluna ihtiyacınız olur.

Bu öğreticide, hafif bir Python OCR motoru kullanarak **PDF'den metin çıkarma** işlemini baştan sona gösteren temiz bir örnek üzerinden ilerleyeceğiz. Sonunda **PDF'yi metne dönüştürme**, **akıştan PDF yükleme** ve **taratılmış PDF işleme** konularını tam olarak öğreneceksiniz. Sihir yok, sadece bugün projenize ekleyebileceğiniz sade Python kodu.

## Öğrenecekleriniz

- PDF girişi anlayan bir Python OCR kütüphanesini kurma ve yapılandırma.  
- PDF‑tanıma modunu etkinleştirme ve çıktı formatını düz metin olarak ayarlama.  
- Çok sayfalı bir PDF'i dosya akışından (klasik “akıştan pdf yükleme” deseni) yükleme.  
- OCR'ı tüm sayfalara uygulama ve metinsel içeriği elde etme.  
- Sonuçları yazdırma veya sonraki işlemler için saklama.

**Önkoşullar**  
- Makinenizde Python 3.8+ yüklü.  
- pip ve sanal ortamlar hakkında temel bilgi.  
- Bilinen bir dizinde bulunan bir taratılmış PDF dosyası (örnekte `multipage.pdf` olarak adlandırılmış).

Bu konular size yabancı geliyorsa endişelenmeyin—her adım sade bir dille açıklanıyor ve ihtiyacınız olan tam komutları sağlıyoruz.

---

## Adım 1: OCR Motorunu Kurun (how to OCR PDF)

İlk olarak PDF girişi işleyebilen bir OCR motoruna ihtiyacınız var. Bu kılavuzda hayali `ocr` paketini kullanacağız (API popüler ticari SDK'ları taklit ediyor, aynı desen Tesseract‑OCR, ABBYY veya Google Vision ile de uygun bir sarmalayıcıyla çalışır).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **İpucu:** Windows'ta izin hataları alıyorsanız `pip install --user ocr` komutunu deneyin.

Paket kurulduktan sonra script'inizde içe aktarabilir ve bir motor örneği oluşturabilirsiniz—bu, **how to OCR PDF** konusunun kalbidir.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

`OcrEngine` nesnesi, daha sonra ayarlayacağımız dil, DPI ve özellikle PDF modu gibi tüm ayarları tutar.

---

## Adım 2: PDF Tanımayı Etkinleştirin ve Çıktıyı Seçin (extract text from PDF)

Varsayılan olarak birçok OCR SDK'sı sadece görüntü alır. Motorun gelen akışı PDF olarak algılamasını sağlamak için PDF tanıma bayrağını açar ve düz‑metin çıktısını isteriz.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Neden çıktı formatını belirtmeliyiz? Çünkü bazı motorlar gizli metin katmanlı PDF'ler, aranabilir PDF'ler ya da sınırlama kutuları ile JSON döndürebilir. Çoğu veri‑çıkarma hattı için **extract text from PDF** olarak düz string'ler en temiz downstream formatıdır.

---

## Adım 3: PDF'i Dosya Akışından Yükleyin (load PDF from stream)

PDF'i bir akıştan yüklemek bellek‑verimli bir desendir—dosyanın tamamını RAM'e yüklemekten kaçınırsınız. Bu, büyük çok‑sayfalı belgelerle çalışırken özellikle kullanışlıdır.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **Dosya S3'te ya da başka bir bulut kovasında ise ne olur?**  
> `from_file` ifadesini bir bayt tamponu kabul eden bir yöntemle (ör. `ImageStream.from_bytes(s3_object.read())`) değiştirin. Pipeline'ın geri kalanı aynı kalır.

---

## Adım 4: Tüm Sayfalarda OCR Çalıştırın (process scanned PDF)

Şimdi asıl iş başlıyor. Motor her sayfayı döngüye alacak, tanıma motorunu çalıştıracak ve sayfa nesnelerinin bir listesini döndürecek—her biri metinsel içeriğini sunar.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Arka planda OCR kütüphanesi her PDF sayfasını sıkıştırmadan çıkarır, yapılandırılmış DPI'da rasterleştirir ve bitmap'i sinir‑ağ modeli üzerinden geçirir. Sonuç? `Page` nesnelerinden oluşan bir koleksiyon, çıkarım için hazır.

---

## Adım 5: Tanınan Metni Alın ve Görüntüleyin (convert PDF to text)

Son olarak dönen sayfalar üzerinde döngü kurar ve tanınan metni yazdırırız. İşte **convert PDF to text** işleminin gerçekleştiği an.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Beklenen Çıktı

`multipage.pdf` üç taratılmış sayfa içeriyorsa, aşağıdakine benzer bir çıktı görürsünüz:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Sayfalar arasındaki temiz ayrımı fark edin—her sayfanın metnini bir veritabanına kaydetmeniz ya da bir NLP modeline beslemeniz gerektiğinde faydalıdır.

---

## Yaygın Kenar Durumlarını Ele Alma

### 1. Görüntü ve Metin Katmanları Karışık PDF'ler
Bazı PDF'ler zaten gizli bir metin katmanı içerir (ör. Word'den dışa aktarılmış). OCR motorunun **mevcut metni yok sayıp** görüntüyü yeniden işlemesini istiyorsanız şu ayarı yapın:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Bellek Sınırlarını Aşan Büyük Dosyalar
Gigabayt‑boyutundaki PDF'lerle çalışırken parçalar halinde işlemeyi düşünün:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Dil ve Yazı Tipi Desteği
Taradığınız belgeler Fransızca ya da özel karakterler içeriyorsa, motorun hangi dil modelini kullanacağını belirtin:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

---

## Tam Script – Çalıştırmaya Hazır

Aşağıda tüm parçaları bir araya getiren, çalıştırılabilir örnek bulunuyor. `ocr_pdf.py` olarak kaydedin ve `python ocr_pdf.py` komutuyla çalıştırın.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Script'i çalıştırmak** her sayfanın metnini konsola yazdırır, “Beklenen Çıktı” bölümünde gösterildiği gibi. Buradan çıktıyı bir dosyaya yönlendirebilirsiniz:

```bash
python ocr_pdf.py > extracted_text.txt
```

---

## Sonuç

Python'da **how to OCR PDF** dosyalarını baştan sona nasıl yapacağınızı ele aldık. Motoru yapılandırarak, belgeyi bir akıştan yükleyerek ve her tanınan sayfayı döngüyle işleyerek **extract text from PDF**, **convert PDF to text** ve **process scanned PDF** işlemlerini sadece birkaç satır kodla gerçekleştirebilirsiniz. Yaklaşım, iki‑sayfalık küçük faturadan yüzlerce sayfalık dev arşivlere kadar ölçeklenebilir.

Sırada ne var? Çıkarılan string'leri bir arama indeksine, bir dil‑modeli özetleyicisine ya da bir veri‑doğrulama hattına besleyin. Ayrıca konumsal meta verileri korumak için JSON gibi çıktı formatlarıyla da deneyler yapabilirsiniz.

Şifreli PDF'lerle nasıl başa çıkılacağı ya da bulut depolama entegrasyonu hakkında sorularınız mı var? Aşağıya yorum bırakın—mutlu kodlamalar! 

![PDF OCR iş akışını gösteren diyagram – how to OCR PDF, akıştan PDF yükleme, sayfaları tanıma ve metin çıkarma](ocr-pdf-workflow.png "how to OCR PDF iş akışı diyagramı")


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}