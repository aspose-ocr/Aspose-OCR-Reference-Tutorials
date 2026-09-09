---
category: general
date: 2026-01-12
description: Python’da görüntüleri hızlı bir şekilde toplu OCR yapma ve JPEG dosyalarından
  metin çıkarma. Tam çalışan bir örnekle adım adım toplu işleme öğrenin.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: tr
og_description: Görüntüleri toplu OCR ile işleme ve JPEG dosyalarından metin çıkarma.
  Bu rehber, eksiksiz, hemen çalıştırılabilir bir Python çözümünü adım adım gösterir.
og_title: Görselleri Toplu OCR – Hızlı Python Öğreticisi
tags:
- OCR
- Python
- image processing
title: Görüntüleri Toplu OCR İşleme – JPEG Dosyalarından Metin Çıkarma İçin Hızlı
  Kılavuz
url: /tr/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görsellerde Toplu OCR Nasıl Yapılır – JPEG Dosyalarından Metin Çıkarma İçin Hızlı Kılavuz

Her dosya için ayrı bir betik yazmadan **how to batch OCR images**'ı merak ettiniz mi? Yalnız değilsiniz. Birçok projede—fatura tarama, arşiv dijitalleştirme veya içerik denetimi—tek seferde onlarca ya da yüzlerce JPEG dosyasından metin çekmemiz gerekir. İyi haber şu ki, bunu sadece birkaç Python satırıyla yapabilirsiniz ve herhangi bir işlem hattına ekleyebileceğiniz yeniden kullanılabilir bir motor elde edersiniz.

Bu öğreticide size tam olarak **how to batch OCR images**'ı göstereceğiz, ardından JPEG dosyalarından metin çıkarma, kenar durumlarını ele alma ve çıktıyı doğrulama adımlarını anlatacağız. Sonuna kadar, herhangi bir görüntü klasöründe çalıştırabileceğiniz bağımsız bir betiğe sahip olacak ve toplu işlem yapmanın performans ve bakım açısından neden önemli olduğunu anlayacaksınız.

## Öğrenecekleriniz

- Basit bir OCR motoru kurun ve İngilizce için yapılandırın.
- `pathlib` ile bir dizinden tüm JPEG dosyalarını toplayın.
- OCR motorunu bir kez çağırarak tüm toplu işlemi gerçekleştirin.
- Her görüntü için tanınan metnin önizlemesini gösterin.
- Büyük toplu işlemler, farklı diller ve yaygın tuzaklar için ipuçları.

**Prerequisites**: Python 3.8+, `ocr` kütüphanesi (veya uyumlu bir sarmalayıcı), ve analiz etmek istediğiniz JPEG görüntülerinin bulunduğu bir klasör. Harici hizmetlere gerek yok—her şey yerel olarak çalışır.

---

## Adım 1: OCR Motorunu Başlatma – How to Batch OCR Images'ın Temeli

**batch OCR images**'a geçmeden önce, metni okuyabilen bir motora ihtiyacımız var. Çoğu kütüphanede bir motor nesnesi oluşturur, isteğe bağlı olarak dili ayarlarsınız ve ardından her dosya için yeniden kullanırsınız.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Why this matters*: Motoru bir kez başlatmak, dil modellerini tekrar tekrar yükleme yükünü önler. Ayrıca tüm toplu işleme uygulanacak ayarları (ör. DPI, karakter beyaz listesi) tek bir yerden ayarlamanızı sağlar.

> **Pro tip**: Çok dilli belgeler işleyecekseniz, `ocr.Language.ENGLISH`'i `ocr.Language.MULTI` ile değiştirin veya toplu işlem başlamadan önce birden fazla dil paketini yükleyin.

---

## Adım 2: Tüm JPEG Dosyalarını Toplama – “JPEG Dosyalarından Metin Çıkarma” Bölümü

Motor hazır olduğuna göre, hangi görüntüler üzerinde çalışacağını ona söylememiz gerekiyor. `pathlib` kullanmak kodu platform bağımsız ve özlü hâle getirir.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Why this matters*: Dosya listesini önce toplayarak, tüm koleksiyonu OCR motoruna tek bir çağrıyla besleyebiliriz—tam da “how to batch OCR images”ın özüdür. Alt klasörleriniz varsa, `glob("**/*.jpg")`'ı yinelemeli arama için değiştirebilirsiniz.

> **Edge case**: Görüntüleriniz karışık uzantılara sahipse (`.jpeg`, `.JPG`), glob desenini şu şekilde genişletin: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Adım 3: Tüm Toplu İşlemi Tek Bir Çağrıyla İşleme – Toplu OCR'ın Gerçek Gücü

Modern OCR kütüphanelerinin çoğu, dosya yolu iterable'ı kabul eden bir `process_batch` (veya benzer isimli) metot sunar. Bu, **how to batch OCR images**'ı verimli bir şekilde yapmanın kalbidir.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Why this matters*: Tek bir toplu çağrı, Python‑to‑C geçiş sayısını azaltır, dil modelini bellekte tutar ve genellikle iç paralelleştirmeyi etkinleştirir. Sonuç, tanınan metin ve güven skorlarını içeren nesneler listesi olur.

> **Performance note**: Çok büyük toplu işlemler (binlerce görüntü) için, aşırı bellek tüketimini önlemek amacıyla listeyi daha küçük parçalara (ör. 200 dosya) bölmeyi düşünün.

---

## Adım 4: Çıkarılan Metnin Önizlemesini Gösterme – Hızlı Doğrulama

Toplu işlem tamamlandıktan sonra, her sonucun ilk birkaç karakterine göz atmak faydalıdır. Bu, OCR'ın JPEG dosyalarınızdan gerçekten metin çıkardığını doğrulamanıza yardımcı olur.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Why this matters*: Kısa bir önizleme, her dosyayı açmadan bariz hataları (ör. boş çıktı, bozuk karakterler) fark etmenizi sağlar. Sistematik sorunlar fark ederseniz, motor ayarlarını değiştirip toplu işlemi yeniden çalıştırabilirsiniz.

> **Common pitfall**: Yeni satır karakterlerini temizlemeyi unutmak, önizlemenin karışık görünmesine sebep olur. `replace("\n", " ")` satırı bunu temizler.

---

## Tam Çalışan Örnek – Tüm Adımlar Birleştirildi

Aşağıda, kopyalayıp yapıştırabileceğiniz, dizin yolunu ayarlayabileceğiniz ve çalıştırabileceğiniz tam betik yer alıyor. Bu, **how to batch OCR images** iş akışının baştan sona tümünü gösterir.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Expected output** (örnek):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Eğer önizleme anlamlı bir metin gösteriyorsa, toplu bir yaklaşım kullanarak **extracted text from JPEG files**'ı başarıyla gerçekleştirmişsiniz demektir.

---

## Büyük Toplu İşlemler ve İleri Senaryoları Ele Alma

### Büyük İş Yüklerini Parçalara Bölme

Binlerce görüntüyle çalışırken bellek darboğazı olabilir. Listeyi daha küçük parçalara bölün:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Dilleri Değiştirme

Belgeleriniz Fransızca veya İspanyolca içeriyorsa, toplu işlemden önce dili değiştirin:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Sonuçları Diske Kaydetme

Yazdırmak yerine, her OCR sonucunu bir `.txt` dosyasına yazmak isteyebilirsiniz:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Sonuç

Artık **how to batch OCR images** ve kompakt bir Python betiği kullanarak **extract text from JPEG files**'ı güvenilir bir şekilde yapabildiğinizi biliyorsunuz. Motoru bir kez başlatarak, tüm JPEG yollarını toplayarak, tek bir toplu işlemle işleyerek ve çıktıyı önizleyerek hem hız hem de basitlik elde edersiniz. Buradan iş akışını genişletebilir—çok dilli desteği ekleyebilir, sonuçları bir veritabanına kaydedebilir veya betiği daha büyük bir belge‑işleme hattına entegre edebilirsiniz.

Bir sonraki adıma hazır mısınız? `ocr` kütüphanesini Tesseract ile değiştirmeyi deneyin, farklı görüntü ön‑işleme (eşikleme, yeniden boyutlandırma) yöntemleriyle deney yapın veya çıkarılan metni otomatik sınıflandırma için bir doğal‑dil‑işleme modeline besleyin. Gökyüzü sınırdır ve üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

Kodlamaktan keyif alın, ve OCR toplu işlemlerinizin her zaman hatasız olmasını dileriz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}