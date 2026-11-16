---
category: general
date: 2026-03-18
description: Aspose OCR kullanarak taradığınız dosyalardan aranabilir PDF oluşturun.
  Tarama PDF'sini nasıl dönüştüreceğinizi, PDF'den metin çıkartmayı ve metni hızlıca
  tanımayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: tr
og_description: Arama yapılabilir PDF'yi anında oluşturun. Tarama yapılmış PDF'yi
  dönüştürmek, PDF'den metin çıkarmak ve Aspose OCR kullanarak PDF'deki metni tanımak
  için bu kılavuzu izleyin.
og_title: Aranabilir PDF Oluşturma – Aspose OCR ile Adım Adım
tags:
- OCR
- PDF
- Aspose
- Python
title: Aranabilir PDF Oluştur – Taralı PDF'yi Aspose OCR ile Dönüştür
url: /tr/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aranabilir PDF Oluşturma – Adım Adım Kılavuz  

Bir yığın taranmış sayfadan **create searchable PDF** oluşturmanız gerektiğinde, nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz—çoğu geliştirici, ilk tarama sunucularına geldiğinde bu duvara çarpar.  

İyi haber şu ki, Aspose OCR ile sadece birkaç satırda **convert scanned pdf** yapabilir, doğrulama için **extract text from pdf** alabilir ve hatta anında **recognize text pdf** yapabilirsiniz. Bu öğreticide, kütüphaneyi kurmaktan tam bir aranabilir belge kaydetmeye kadar tüm süreci adım adım gösterecek ve **convert image pdf** gibi kenar durumlarıyla başa çıkmak için birkaç ipucu ekleyeceğiz.

## Neler Başaracaksınız  

Bu rehberin sonunda şunları yapabilecek:

* Bir taranmış PDF'yi (veya yalnızca görüntü içeren PDF'yi) Aspose OCR'e yükleyin.  
* Motorun hangi sayfaları işleyeceğini belirtin – yalnızca bir alt küme gerektiğinde kullanışlı.  
* OCR sonuçlarını orijinal dosyaya gömerek çıktının gerçek bir **searchable PDF** olmasını sağlayın.  
* Sayfa sayısını yazdırarak ve isterseniz çıkarılan metni dökerek işlemi doğrulayın.  

Harici hizmetler yok, gizli bir sihir yok—sadece saf Python ve Aspose'un kendi API'si.

## Önkoşullar  

* Python 3.8 ve üzeri.  
* `aspose-ocr` paketi – `pip install aspose-ocr` ile kurun.  
* Taranmış bir PDF dosyası (veya yalnızca görüntüler içeren bir PDF).  
* Python betikleme konusunda temel bilgi.  

Eğer bunlara sahipseniz, harika—hadi başlayalım.

<img src="searchable-pdf-workflow.png" alt="Aranabilir PDF oluşturma iş akışı">  

*(OCR işlem hattının illüstrasyonu – kod için gerekli değil ancak görsel öğrenenlere yardımcı olur.)*

## Adım 1 – OCR Motorunu Başlatma  

İlk iş olarak, bir `OcrEngine` örneğine ihtiyacınız var. Bunu, her pikseli okuyup Unicode karakterlerine dönüştürecek bir beyin olarak düşünün.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Neden önemli:** Motor olmadan seçenekleri ayarlayamaz veya tanıma çalıştıramazsınız. Erken başlatmak, daha sonra özel sözlükler ekleyebileceğiniz bir yer de sağlar.

## Adım 2 – Kaynak PDF'nizi Yükleyin  

Aspose OCR doğrudan PDF'leri okuyabilir, bu da her sayfayı kendiniz rasterleştirmenize gerek olmadığı anlamına gelir. Sadece motoru dosyaya yönlendirin.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Pro ipucu:* PDF büyükse, dosyanın diskte kilitlenmesini önlemek için bir akıştan yüklemeyi düşünün.

## Adım 3 – PDF Tanıma Seçeneklerini Yapılandırma  

İşte ikincil anahtar kelimelerin parlamaya başladığı yer. Motoru sadece belirli sayfalarda **convert scanned pdf** yapacak şekilde, tanınan metni gömecek ya da orijinal görüntüleri dokunulmaz tutacak şekilde söyleyebilirsiniz.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Neden önemli:**  
* `setEmbedRecognisedText(True)` raster PDF'yi **searchable PDF**'ye dönüştürmenin anahtarıdır.  
* `setPageRange` **convert image pdf** işlemini seçici olarak yapmanıza yardımcı olur—sadece birkaç sayfayı OCR'lamak istediğiniz büyük belgeler için faydalıdır.  
* Metin çıkarımını etkinleştirmek, daha sonra **extract text from pdf** işlemini bir görüntüleyici açmadan yapmanızı sağlar.

## Adım 4 – Seçenekleri Motora Bağlama  

Şimdi seçenekleri motora bağlayın. Bu adım gözden kaçması kolaydır, ancak atlanırsa motor varsayılan ayarlarla (aranabilir metin olmadan) çalışır.

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Adım 5 – Seçilen Sayfalarda OCR Çalıştırma  

Her şey bağlandıktan sonra, gerçek tanıma tek bir metod çağrısıdır.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Eğer çok megabaytlık bir belge işliyorsanız, bunu bir try/except bloğuna sararak `OcrException` yakalamak ve sorunlu sayfayı kaydetmek isteyebilirsiniz.

## Adım 6 – Sonucu Doğrulama  

Hızlı bir mantık kontrolü, motorun kaç sayfa işlediğini yazdırmaktır. Ayrıca, daha fazla analiz için **extract text from pdf** yapmanız gerekiyorsa ham metni de alabilirsiniz.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Neden önemsiyorsunuz:** Sayfa sayısını görmek, `setPageRange`'in çalıştığını doğrular ve çıkarılan metin parçacığı OCR'un gerçekten karakterleri tanıdığını kanıtlar.

## Adım 7 – Aranabilir PDF'yi Kaydetme  

Son olarak, çıktıyı diske geri yazın. `ImageFormats.PDF` sabiti, Aspose'a dosyayı PDF olarak tutmasını söyler; artık aranabilir metinle zenginleştirilmiş.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Ortaya çıkan dosyayı herhangi bir PDF okuyucusunda açın ve metin araması deneyin—voilà, **created searchable pdf** yaptınız!

## Yaygın Kenar Durumlarını Ele Alma  

### Kaynak *yalnızca görüntü* PDF olduğunda  

Eğer giriş PDF'niz yalnızca görüntüler içeriyorsa (metin katmanı yok), aynı kod çalışır—sadece `setEmbedRecognisedText(True)`'in etkin olduğundan emin olun. Daha iyi doğruluk için DPI'yi artırmak isteyebilirsiniz:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Birden Çok Dil ile Çalışma  

Aspose OCR dil paketlerini destekler. `recognize()`'i çağırmadan önce bir dil yükleyin:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Büyük Belgeler  

500 sayfalık bir taranmış PDF işlemek bellek yoğun olabilir. İşi bölün:

1. Sayfa aralıkları üzerinde döngü yapın (`setPageRange(start, end)`).  
2. Her parçayı geçici bir aranabilir PDF olarak kaydedin.  
3. Parçaları `PdfMerger` ile birleştirin (başka bir Aspose bileşeni).

## Tam Çalışan Örnek (Tüm Adımlar Birlikte)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Bu betiği çalıştırmak, Adobe Reader, Chrome veya herhangi bir PDF görüntüleyicide açabileceğiniz ve kelimeleri anında arayabileceğiniz bir **searchable PDF** sağlar.

## Sonuç  

Artık Aspose OCR kullanarak **create searchable PDF** dosyaları oluşturmak için eksiksiz, uçtan uca bir çözümünüz var. Kaynağı yüklemekten, **convert scanned pdf** seçeneklerini yapılandırmaya, metni çıkarmaya ve doğrulamaya, son olarak aranabilir sonucu kaydetmeye kadar her adım kapsandı.  

Sonraki adımda, kaynağın PDF'ye paketlenmiş bir dizi JPEG olduğu **convert image pdf** senaryolarını keşfetmek ya da çok dilli belgeler için doğruluğu artırmak amacıyla dil‑spesifik OCR'a daha derinlemesine dalmak isteyebilirsiniz. Her iki durumda da desen aynı kalır: seçenekleri ayarlayın, `recognize()`'i çalıştırın ve kaydedin.  

Deney yapmaktan çekinmeyin—sayfa aralığını değiştirin, DPI'yi ayarlayın veya özel bir sözlük ekleyin. Sorunla karşılaşırsanız, aşağıya yorum bırakın ya da en son API detayları için Aspose'un resmi belgelerine bakın. İyi OCR'lar

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}