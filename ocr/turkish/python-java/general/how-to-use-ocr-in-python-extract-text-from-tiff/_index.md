---
category: general
date: 2026-07-05
description: Python’da OCR’ı kullanarak TIFF dosyalarını hızlıca metne dönüştürme.
  TIFF görüntülerinden metin çıkarmak ve bir Python OCR motoru oluşturmak için ocr
  kütüphanesi Python adımlarını öğrenin.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: tr
og_description: Python'da OCR nasıl kullanılır? Bu rehber, bir Python OCR motoru ve
  ocr kütüphanesi python kullanarak TIFF'i metne nasıl dönüştüreceğinizi adım adım
  gösterir.
og_title: Python'da OCR Nasıl Kullanılır – Tam TIFF Metin Çıkarma
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Python'da OCR Nasıl Kullanılır – TIFF'ten Metin Çıkarma
url: /tr/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Nasıl Kullanılır – TIFF'ten Metin Çıkarma

Hiç **Python'da OCR nasıl kullanılır** diye merak ettiniz mi ve taranmış bir kitabı düzenlenebilir metne dönüştürmek istediniz mi? Tek başınıza değilsiniz—geliştiriciler, araştırmacılar ve hobi meraklıları, çok sayfalı TIFF görüntüleriyle çalışırken aynı engelle karşılaşıyor. İyi haber? **ocr library python** sayesinde küçük bir OCR motoru başlatabilir, bir TIFF dosyasına yönlendirebilir ve saniyeler içinde temiz, aranabilir metin elde edebilirsiniz.

Bu öğreticide ihtiyacınız olan her şeyi adım adım göstereceğiz: doğru paketi kurmak, çok sayfalı bir TIFF dosyasını yüklemek, OCR motorunu çalıştırmak ve sonunda her sayfanın içeriğini yazdırmak. Sonuna geldiğinizde **TIFF'i metne dönüştürme** ve **TIFF'ten metin çıkarma** işlemlerini Python ortamınızdan çıkmadan yapabilecek duruma geleceksiniz.

## Önkoşullar

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.9 veya daha yeni (örnek 3.11 üzerinde test edilmiştir)
- `ocr` kütüphanesinin (veya tercih ettiğiniz herhangi bir uyumlu **python ocr engine**'in) güncel bir sürümü
- İşlemek istediğiniz çok sayfalı TIFF dosyası (biz buna `scanned_book.tif` diyeceğiz)
- Python betikleri ve sanal ortamlar konusunda temel bilgi

Ağır dış araçlar gerekmez—sadece pip ve birkaç satır kod yeterli.

## OCR Library Python'ı Kurun

İlk adım: sağlam bir OCR arka ucuna ihtiyacınız var. Bu rehberde, basit bir yüksek‑seviye API sunan hayali `ocr` paketini kullanacağız, ancak aynı desen `pytesseract` gibi Tesseract tabanlı sarmalayıcılarla ya da ticari SDK'larla da çalışır.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Windows kullanıyorsanız ve paket yerel ikili dosyalara dayanıyorsa, uygun Visual C++ yeniden dağıtılabilir paketinin kurulu olduğundan emin olun. Kurulum sırasında eksik bir şey varsa genellikle uyarı verir.

## Python'da OCR Motoru Nasıl Kullanılır

Kütüphane hazır olduğuna göre, bir OCR motoru başlatıp TIFF dosyamıza yönlendirelim. Aşağıdaki kod parçacığı bir motor örneği oluşturur, dili İngilizce olarak ayarlar ve çok sayfalı işleme hazırlar.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Neden dili ayarlamalıyız?**  
Çoğu OCR motoru doğruluğu artırmak için dil modelleri kullanır. Bu adımı atlayarsanız motor, noktalama işaretlerini veya özel karakterleri yanlış tanıyabilecek genel bir modele geri döner.

## Çok Sayfalı TIFF Görüntüsünü Yükleyin

Sıradaki adım taranmış belgeyi yüklemek. `ocr.Image.load` yardımcı fonksiyonu, TIFF yığınlarını kutudan çıkar çıkmaz anlar ve her sayfayı dahili olarak temsil eden bir nesne döndürür.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Köşe durumu:** TIFF dosyanız sıkıştırma (CCITT Group 4, LZW vb.) kullanıyorsa ve kütüphane bir hata veriyorsa, önce ImageMagick ile sıkıştırılmamış bir sürüme dönüştürmeyi deneyin:  
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Tüm Sayfalarda OCR Çalıştırın – TIFF'i Metne Dönüştürün

Görüntü nesnesi elinizde olduğuna göre, motor artık tüm sayfaları bir kerede işleyebilir. Bu yöntem, her bir sayfa için OCR sonucunu tutan bir liste döndürür.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Arka planda ne oluyor?**  
`recognize_multi_page` fonksiyonu, rasterleştirilmiş her sayfayı dolaşır, sinir‑ağ tanıma motorunu çalıştırır ve düz metin çıktısını güven puanlarıyla birlikte paketler. Temelde, manuel bir döngü yazmaktan sizi kurtaran toplu bir işlemdir.

## Sonuçları Döngüyle İşleyin – TIFF'ten Metin Çıkarma

Son olarak tanınan metni gösteriyoruz. Çıktıyı ayrı `.txt` dosyalarına yazabilir, bir veritabanına itebilir ya da bir arama indeksine besleyebilirsiniz—iş akışınıza uygun olanı seçin.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Beklenen Çıktı

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Her `result.text` dizesi, o sayfa için ham OCR çıktısını içerir. Satır sonu korunumu gerekiyorsa, çoğu motor `result.lines` listesini dize olarak sunar.

## Büyük TIFF Dosyalarıyla Çalışma – İpuçları & Püf Noktaları

500 sayfalık bir TIFF işlemek bellek yoğun olabilir. İşlerin sorunsuz gitmesi için birkaç strateji:

1. **Sayfaları parçalar halinde işleyin** – `recognize_multi_page` yerine, bir jeneratör içinde `engine.recognize(page)` çağrısı yaparak bir seferde bir sayfa işleyin.
2. **DPI'yı ayarlayın** – Görüntü çözünürlüğünü (ör. 300 DPI'dan 200 DPI'a) düşürmek CPU yükünü azaltır ve çoğu basılı metin için doğruluğu çok az etkiler.
3. **Paralelleştirin** – OCR motorunuz thread‑safe ise, `concurrent.futures.ThreadPoolExecutor` kullanarak tanıma işlemini birden çok sayfada aynı anda çalıştırın.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Çıkarılan Metni Dosyalara Kaydedin

Gerçek dünya akışları genellikle kalıcı depolama ister. Aşağıdaki kısa kod, her sayfanın metnini kendi dosyasına dökerek sayfa sırasını korur.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Artık indeksleme veya daha ileri NLP işleme için hazır `.txt` dosyalarından oluşan temiz bir dizininiz var.

## Görsel Önizleme – OCR Sonuçlarını Görsel Olarak Kullanma

OCR katmanını orijinal görüntü üzerinde görmek isterseniz (hata ayıklama için kullanışlı), birçok kütüphane sınırlayıcı kutular çizmeye izin verir. Pillow kullanarak hızlı bir örnek:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Python'da OCR Kullanımı – TIFF sayfası üzerinde OCR katmanı](ocr_overlay_example.png)

*Alt metin:* Python'da OCR Kullanımı – tanınan metnin TIFF sayfası üzerindeki görsel katmanı.

## Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| Bozuk karakterler | Yanlış dil modeli | `engine.language` değerini doğru enum ile ayarlayın |
| Eksik sayfalar | TIFF sıkıştırması desteklenmiyor | Önce sıkıştırılmamış TIFF'e dönüştürün |
| Yavaş performans | Yüksek DPI + tek‑iş parçacıklı işleme | DPI'ı düşürün veya çok‑iş parçacıklı çalışmayı etkinleştirin |
| Boş çıktı | Görüntü çok karanlık/düşük kontrast | Kontrast artırma (`opencv` veya `Pillow`) ile ön‑işlem yapın |

Bu sorunları erken aşamada ele almak, ileride saatler süren hata ayıklamayı önler.

## Sonraki Adımlar – Temel Çıkarma Ötesine Geçmek

Artık **Python'da OCR nasıl kullanılır** temellerini kavradığınıza göre, aşağıdaki konuları keşfetmeyi düşünün:

- **PDF oluşturma** – Çıkarılan metni `reportlab` ile birleştirerek aranabilir PDF'ler oluşturun.
- **Dil tespiti** – `langdetect` kullanarak `engine.language` ayarını otomatik değiştirin.
- **Yapısal veri çıkarma** – Ham metinden tarih, isim veya tablo gibi bilgileri çekmek için düzenli ifadeler veya spaCy kullanın.
- **Alternatif OCR arka uçları** – Çok dilli desteğe ihtiyacınız varsa `ocr` yerine `pytesseract` ya da `easyocr` gibi paketleri deneyin.

Bu konular, ikincil anahtar kelimeler **ocr library python**, **convert tiff to text**, **extract text from tiff**, ve **python ocr engine** ile doğal olarak bağlantılıdır ve daha ileri projeler için sağlam bir temel sunar.

---

### Sonuç

Kurulumdan çok sayfalı işleme kadar **Python'da OCR nasıl kullanılır** konusunu ele aldık ve **TIFF'i metne dönüştürme** ile **TIFF'ten metin çıkarma** işlemlerini basit bir **python OCR engine** ile nasıl yapacağınızı gösterdik. Yukarıdaki tam çalışan örnek, çoğu standart TIFF dosyası için kutudan çıkar çıkmaz çalışmalı; verilen ipuçları ise daha büyük belgelerle ölçeklendirme ya da OCR'ı daha geniş akışlara entegre etme konusunda yardımcı olacaktır.

Kendi taranmış kitaplarınız, makbuzlarınız veya arşiv görüntülerinizle deneyin—sonra “Sonraki Adımlar” bölümünde listelenen ileri seviye fikirleri keşfedin. İyi kodlamalar, OCR sonuçlarınız her daim doğru olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, tam çalışan kod örnekleri ve adım adım açıklamalar içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR for Java ile tiff'ten metin çıkarma](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Aspose OCR Kullanarak Akıştan Görüntü Metni Çıkarma](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}