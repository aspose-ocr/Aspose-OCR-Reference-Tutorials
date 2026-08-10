---
category: general
date: 2026-06-06
description: Python OCR kullanarak görüntü PDF'lerinden metin çıkarın. Tarama belgelerini,
  asenkron toplu tanıma ile hızlıca metne dönüştürmeyi öğrenin.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: tr
og_description: Python ile görüntü PDF'lerinden metin çıkarın. Bu adım adım rehber,
  taranmış belgeleri asenkron OCR kullanarak metne nasıl dönüştüreceğinizi gösterir.
og_title: Görüntülerden PDF Metni Çıkarma – Python OCR Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Görüntü PDF'lerinden Metin Çıkarma – Taralı Belgeleri Metne Dönüştürmek için
  Python Rehberi
url: /tr/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden PDF Metni Çıkarma – Tarama Belgelerini Metne Dönüştürmek için Python Rehberi

Saatlerce yeniden yazmak zorunda kalmadan **extract text from images pdf**'yi çıkarmanız gerektiğinde? Bu rehberde, Python'da basit bir asenkron OCR iş akışı kullanarak **convert scanned documents to text** nasıl yapılacağını göstereceğiz.  

Eğer bir yığın taranmış PDF'ye bakıp “Daha hızlı bir yol olmalı” diye düşündüyseniz, doğru yerdesiniz. Her satır kodu adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve karşılaşabileceğiniz bazı uç durumları ele alacağız.

## Öğrenecekleriniz

- Bir OCR motoru başlatma ve tanıma dilini ayarlama.  
- PNG ve PDF'lerden oluşan karışık bir listeyi toplu tanıyıcıya beslemenin mekanikleri.  
- OCR işini asenkron olarak çalıştırarak uygulamanızın yanıt vermeye devam etmesini sağlama.  
- Sonuçları geri çekme, kaynak dosyalarla eşleştirme ve temiz bir çıktı üretme.  

**Önkoşullar**: Python 3.8+, `asyncio` veya `concurrent.futures` hakkında temel bir anlayış ve örnekteki `OcrEngine` sınıfına benzer bir OCR kütüphanesi (ör. Aspose.OCR, Tesseract sarmalayıcısı veya özel bir sarmalayıcı). Ağır bir kurulum gerekmez—kütüphaneyi kurun, hazırsınız.

![görüntülerden pdf metni çıkarma](https://example.com/placeholder.png "OCR çıktısının ekran görüntüsü – extract text from images pdf")

## Görüntülerden PDF Metni Çıkarma – OCR Motorunu Kurma

İlk olarak, belgelerinizin diliyle yapılandırılmış bir OCR motoru örneğine ihtiyacınız var. Bizim örneğimizde Fransızca kullanacağız, ancak istediğiniz desteklenen herhangi bir dile değiştirebilirsiniz.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Neden bu önemli**: Dili önceden ayarlamak doğruluğu büyük ölçüde artırır. Motor, dile özgü sözlükler ve karakter modelleri kullanır; yanlış dil beslemek bozuk çıktının yaygın bir kaynağıdır.

## Dosya Listesini Hazırlama – Görüntüler ve PDF'ler Birlikte

Toplu tanıyıcımız hem raster görüntüleri (`.png`, `.jpg`) hem de PDF kapsayıcılarını işleyebilir. Sadece dosya yollarının bulunduğu sade bir Python listesi verin.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**İpucu**: Listeyi düz tutun; motor her PDF sayfasını tanımadan önce dahili olarak görüntülere ayıracaktır. Binlerce dosyanız varsa, bellek dalgalanmalarını önlemek için listeyi daha küçük partilere bölmeyi düşünün.

## Asenkron Toplu Tanıma Başlatma

Ana iş parçacığını engellemek yerine OCR görevini arka planda başlatıyoruz. Metot, sonunda bir `OcrResult` nesnesi listesi tutacak bir `Future` döndürür.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Nasıl çalışır**: Motor, uygulamanın uygulanışına bağlı olarak bir iş parçacığı havuzu (veya async görev) oluşturur. Bu sayede UI güncellemek, daha fazla dosya almak veya ilerlemeyi kaydetmek gibi diğer işleri yapmaya devam edebilirsiniz; ağır işlem başka bir yerde gerçekleşir.

## OCR Çalışırken Faydalı Bir Şey Yapın

Yaygın bir hata, boş oturup geleceği sıkı bir döngüde sorgulamaktır. Bunun yerine ilgisiz bir işi halledebilirsiniz. Demonstrasyon amaçlı sadece bir durum satırı yazdıracağız.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Future Tamamlandığında Sonuçları Toplama

OCR çıktısını toplamak istediğinizde, `concurrent.futures`'dan `as_completed` kullanın. Bu desen, bir future ya da birden çok future olduğunda aynı şekilde çalışır.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Gördükleriniz**: Her dosya yolu, ardından çıkarılan düz metin temsiliyle birlikte. PDF'ler için `result.text` tüm sayfaların birleştirilmiş metnini içerir.

### Beklenen Çıktı (örnek)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Eğer eksik karakterler fark ederseniz, ayarladığınız dilin belge diliyle eşleştiğinden emin olun ve motoru beslemeden önce görüntüleri ön‑işleme (eğikliği düzeltme, kontrast artırma) yapmayı düşünün.

## Kenar Durumları ve Yaygın Tuzaklar

| Durum | Ne Yapmalı |
|-----------|------------|
| **Karışık diller** | Önce bir dil algılama adımı çalıştırın, ardından dil başına ayrı motorlar oluşturun. |
| **Devasa PDF'ler (> 100 MB)** | PDF'yi disk üzerinde tek tek sayfalara bölün (ör. `PyPDF2` kullanarak) ve ayrı girişler olarak besleyin. |
| **Latin dışı yazı sistemleri** | OCR kütüphanesinin gerekli dil paketini içerdiğinden emin olun; bazı kütüphaneler ek veri dosyaları indirmenizi ister. |
| **Performans darboğazı** | İş parçacığı havuzu boyutunu artırın (`engine.set_thread_pool_size(8)`) veya mevcutsa GPU‑hızlandırmalı bir arka plan seçin. |
| **Düşük çözünürlüklü görüntülerde eksik metin** | OpenCV ile ön‑işleme yapın: `cv2.resize`, `cv2.threshold` ve `cv2.medianBlur` kullanarak okunabilirliği artırın. |

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Bu dosyayı `extract_text_async.py` olarak kaydedin, `YOUR_DIRECTORY` kısmını dosyalarınızın yolu ile değiştirin, OCR paketini kurun (`pip install your-ocr-lib`) ve `python extract_text_async.py` komutunu çalıştırın. Konsolda daha önce gösterilen çıktıyı görmelisiniz.

## Sonraki Adımlar – Temel Çıkarma Ötesine Geçmek

- **Post‑processing**: Fazla boşlukları temizleyin, Unicode'u normalleştirin (`unicodedata.normalize`) veya OCR gürültüsünü temizlemek için bir imla denetleyicisi çalıştırın.  
- **Yapısal çıktı**: Sonuçları CSV, JSON olarak dışa aktarın veya doğrudan bir veritabanına kaydederek sonraki aramalara hazırlayın.  
- **Paralel partiler**: Yüzlerce dosyanız varsa birden çok future oluşturun ve bir kuyruk kullanarak CPU'yu meşgul tutun, belleği aşırı yüklemeden.  
- **Web çerçeveleriyle bütünleştirme**: Bu betiği bir Flask ya da FastAPI uç noktasına bağlayarak talep üzerine OCR hizmeti sunun.

---

### TL;DR

Artık **extract text from images pdf**'yi asenkron çalışan minimal bir Python betiğiyle nasıl yapacağınızı biliyorsunuz; bu sayede **convert scanned documents to text** işlemini programınız yanıt verirken gerçekleştirebilirsiniz. Dil ayarları, batch boyutları ve ön‑işleme püf noktalarıyla her karakteri yakalamak için deneyler yapın.

Paylaşmak istediğiniz bir varyasyon var mı—belki el yazısı notlarda OCR ya da bulut tabanlı bir hizmet? Yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmeli?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Klasörlerde OCR İşlemi Kullanarak Görüntülerden Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR Kullanarak Görüntülerden Metin Çıkarma – İzin Verilen Karakterler](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}