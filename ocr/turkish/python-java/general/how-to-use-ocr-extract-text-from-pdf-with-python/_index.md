---
category: general
date: 2026-04-26
description: Tarama yapılan PDF'lerde OCR kullanma, PDF'den metin çıkarma, PDF'de
  OCR çalıştırma ve taranmış PDF'yi birkaç adımda aranabilir dosyalara dönüştürme.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: tr
og_description: 'Python''da OCR nasıl kullanılır: PDF''den metin çıkarmayı öğrenin,
  PDF üzerinde OCR çalıştırın ve taranmış PDF''leri aranabilir belgelere dönüştürün.'
og_title: OCR Nasıl Kullanılır – PDF'ten Metin Çıkarma Hızlı Rehberi
tags:
- OCR
- Python
- PDF
- Text Extraction
title: OCR nasıl kullanılır – PDF'den Python ile Metin Çıkarma
url: /tr/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Nasıl Kullanılır – PDF'den Metin Çıkarma Python ile

Hiç **OCR nasıl kullanılır** diye merak ettiniz mi ve taranmış bir sözleşme, fiş ya da e‑kitaptan metin çıkarmak istediniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede aldığınız PDF sadece bir görüntüdür ve OCR olmadan içeriğini arayamaz, indeksleyemez ya da analiz edemezsiniz.  

Bu öğreticide, **OCR nasıl kullanılır**, **PDF'den metin çıkarma** ve taranmış PDF dosyalarını **arama yapılabilir belgelere dönüştürme** konularını gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Ayrıca OCR motorunun her sayfayı net bir şekilde görebilmesi için **PDF'yi görüntü olarak yükleme** inceliklerine de değineceğiz.

> **Hızlı ön izleme:** Sonunda çok sayfalı bir PDF'i yükleyen, her sayfada OCR çalıştıran ve tanınan metni ekrana yazdıran bir betiğiniz olacak – harici hizmetlere ihtiyaç duymadan.

## Gereksinimler

- Python 3.9+ (herhangi bir yeni sürüm yeterli)
- `aocr` paketi (veya `OcrEngine` ve `Image.load` sağlayan uyumlu bir OCR kütüphanesi)
- İşlemek istediğiniz taranmış PDF dosyası (ör. `contract.pdf`)
- Makul bir RAM miktarı (≈ 200 MB / 100 sayfalık PDF genellikle yeterlidir)

OCR kütüphanesini henüz kurmadıysanız, şu komutu çalıştırın:

```bash
pip install aocr
```

> **İpucu:** Bağımlılıkları düzenli tutmak için bir sanal ortam (virtual environment) kullanın.

## Adım 1: PDF'yi Görüntü Olarak Yükle – Bulmacanın İlk Parçası

Herhangi bir OCR işlemi gerçekleşmeden önce PDF, bir görüntü olarak temsil edilmelidir. İşte burada ikincil anahtar kelime **load pdf as image** devreye girer.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Neden önemli?* `aocr.Image.load` her PDF sayfasını OCR motorunun anlayabileceği bir bitmap’e rasterleştirir. Bu adımı atlayıp ham PDF'i verirseniz, motor piksel verisi beklediği için bir hata fırlatır; vektör verisi almaz.

> **Not:** Yol mutlak ya da göreli olabilir. Dosyanın okunabilir olduğundan emin olun; aksi takdirde `FileNotFoundError` alırsınız.

## Adım 2: PDF Üzerinde OCR Çalıştır – Pikselleri Karaktere Dönüştürme

PDF artık bir görüntü olduğuna göre **run OCR on PDF** işlemini gerçekleştirebiliriz. Aşağıdaki kod parçacığı tüm sayfaları tek seferde işler:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Arka planda ne oluyor?* `process_all_pages` rasterleştirilmiş sayfalar üzerinde döner, OCR modelini uygular ve sayfa başına bir sonuç nesnesi içeren bir liste döndürür. Her sonuç, tanınan metin, güven skorları ve (isteğe bağlı) sınırlama kutularını (bounding boxes) içerir.

## Adım 3: PDF'den Metin Çıkarma – Metinleri Çekme

OCR sonuçları elinizde olduğuna göre düz metni çıkarmak çok basit. Sayfalar üzerinde döngü kurup çıktıyı ekrana yazdıracağız ve ikincil anahtar kelime **extract text from pdf**'yi göstereceğiz.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Beklenen çıktı** (kısaltılmış):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Metni tek bir dize olarak istiyorsanız, sadece birleştirin:

```python
full_text = "\n".join(r.text for r in page_results)
```

Böylece **PDF'den metin çıkarma** işlemini OCR ile başarıyla tamamladınız.

## Adım 4: Taranmış PDF'yi Dönüştür – Arama Yapılabilir Hale Getirme

Birçok downstream araç (ör. Elasticsearch veya SharePoint) düz metin dökümü yerine arama yapılabilir bir PDF bekler. OCR çıktısını orijinal PDF'e gömerek **convert scanned PDF** işlemini gerçekleştirebilir, böylece arama yapılabilir bir sürüm elde edebilirsiniz.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Neden zahmet?* Arama yapılabilir bir PDF, orijinal düzeni ve görselleri korurken metin seçimi ve indekslemeye izin verir – insanlar ve makineler için kazan‑kazan bir durum.

## Yaygın Tuzaklar & Kenar Durumları

### Bellekten Daha Büyük Çok Sayfalı PDF'ler

PDF'iniz yüzlerce sayfa içeriyorsa, hepsini bir anda yüklemek RAM'i tüketebilir. `aocr` kütüphanesi tembel (lazy) yüklemeyi destekler:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Ardından sayfaları tek tek işleyin:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Düşük Kaliteli Taramalar

Bulanık ya da düşük kontrastlı taramalar OCR doğruluğunu ciddi şekilde düşürür. Görüntüyü motora vermeden önce ön işleme yapmayı düşünün:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Dil Desteği

Varsayılan olarak motor İngilizce varsayar. Başka bir dilde **run OCR on PDF** yapmak için dil kodunu ayarlayın:

```python
ocr_engine.language = "spa"  # Spanish
```

İlgili dil modelinin kurulu olduğundan emin olun.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `ocr_pdf.py` adlı bir dosyaya koyup hemen çalıştırabileceğiniz bağımsız bir betik:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Şöyle çalıştırın:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Metin konsola yazdırılacak ve `-o` parametresi verdiyseniz, orijinal dosyanın yanında arama yapılabilir bir PDF oluşacaktır.

## İpucu ve En İyi Uygulamalar

- **Toplu işleme:** Onlarca PDF ile çalışırken yukarıdaki mantığı bir döngüye sarın ve her dosyanın başarı/başarısızlık durumunu kaydedin.
- **Güven skorları filtresi:** Her `page_result` bir güven metriği içerir. Düşük güvenli sayfaları elden geçirme için atın ya da işaretleyin.
- **Paralellik:** CPU'nuz birden fazla çekirdek içeriyorsa, `concurrent.futures` kullanarak sayfaları paralel işleyin — ancak bellek kullanımına dikkat edin.
- **Sürüm kilidi:** `aocr` API'si zamanla değişebilir. `requirements.txt` içinde sürümü sabitleyin (ör. `aocr==2.3.1`) böylece kırılma riskini azaltırsınız.

## Sonuç

**OCR nasıl kullanılır**, **PDF'den metin çıkarma**, **PDF üzerinde OCR çalıştırma**, **PDF'yi görüntü olarak yükleme** ve hatta **taranmış PDF'yi arama yapılabilir formata dönüştürme** konularını adım adım ele aldık. Kod tamam, açıklamalar *ne* ve *neden* sorularını yanıtlıyor ve artık görüntü‑tabanlı PDF'lerle çalışan herhangi bir proje için yeniden kullanılabilir bir deseniniz var.

Sırada ne var? Çıkarılan metni bir doğal dil işleme hattına besleyin, arama yapılabilir PDF'leri Elasticsearch ile indeksleyin ya da Tesseract, Azure Computer Vision gibi farklı OCR arka planlarıyla deney yapın. Ufkunuz geniş, araçlar ise parmaklarınızın ucunda.

İyi kodlamalar, ve PDF'leriniz her zaman arama yapılabilir olsun! 

![how to use OCR example](/images/ocr_workflow.png "how to use OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}