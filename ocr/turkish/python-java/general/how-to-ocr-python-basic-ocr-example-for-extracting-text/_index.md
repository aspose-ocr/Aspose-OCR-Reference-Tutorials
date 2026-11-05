---
category: general
date: 2026-04-26
description: 'Python ile OCR nasıl yapılır: Görüntüden metin çıkarmayı ve temel bir
  OCR örneği kullanarak tiff dosyasını Python ile okumayı öğrenin. Hızlı, çalıştırılabilir
  kod dahil.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: tr
og_description: 'python ile ocr nasıl yapılır: Görüntüden metin çıkarma, tiff dosyasını
  python ile okuma ve taranmış görüntü metnini basit, çalıştırılabilir bir script
  ile dönüştürmeyi gösteren adım adım bir rehber.'
og_title: Python ile OCR nasıl yapılır – Metin Çıkarma için Temel OCR Örneği
tags:
- OCR
- Python
- Image Processing
title: Python ile OCR nasıl yapılır – Metin Çıkarma için Temel OCR Örneği
url: /tr/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python ile ocr nasıl yapılır – Metin Çıkarma için Temel OCR Örneği

Masada taranmış bir TIFF dosyası olduğunda **python ile ocr nasıl yapılır** diye merak ettiniz mi? Sadece bir sürü görüntü dosyasına bakıp “Bu dosyadan kelimeleri nasıl çıkarırım?” diye soran tek kişi siz değilsiniz. İyi haber şu ki, doğru kütüphane ve birkaç net adımla bir resmi düz metne dönüştürmek çocuk oyuncağı.

Bu öğreticide, bir TIFF dosyasını okuyan, metni çıkaran ve konsola yazdıran **temel bir OCR örneği** üzerinden ilerleyeceğiz. Sonunda **görüntüden metin çıkarma** dosyalarını tam olarak nasıl yapacağınızı, TIFF formatının inceliklerini nasıl yöneteceğinizi ve **tarama görüntüsü metnini dönüştürme** ihtiyacınız olduğunda neyi ayarlamanız gerektiğini öğreneceksiniz. Gizli bir sihir yok—bugün kopyala‑yapıştır yapıp çalıştırabileceğiniz sade bir Python kodu.

## İhtiyacınız Olanlar

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.9+ (en yeni kararlı sürüm tercih edilir).
- Pip ile kurulabilen bir OCR kütüphanesi. Bu rehberde popüler araçları taklit eden hayali bir `aocr` paketi kullanacağız; daha sonra `pytesseract` ya da `easyocr` ile değiştirebilirsiniz.
- İşlemek istediğiniz bir TIFF görüntüsü – dosya adını `input.tiff` olarak belirleyin ve kodda referans vereceğiniz bir klasöre koyun.
- Komut satırıyla temel bir aşinalık (paketi kurmak için yeterli).

Hepsi bu. Ağır bağımlılıklar, Docker konteynerleri yok, sadece birkaç satır kod.

## Adım 1 – Bağımlılıkları Kur ve İçe Aktar (python ile ocr nasıl yapılır)

İlk olarak OCR paketini edinin. Bir terminal açıp şu komutu çalıştırın:

```bash
pip install aocr
```

Gerçek bir kütüphane tercih ediyorsanız `aocr` yerine `pytesseract` yazın ve Tesseract motorunu ayrı olarak kurun.

Şimdi ihtiyacımız olanları içe aktaralım. `pathlib`’ten `Path` sınıfı, işletim sistemine bağımlı olmadan dosya yollarıyla çalışmamızı sağlayan temiz bir yol sunar.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*`Path` neden kullanılır?* Çünkü `/` ve `\` gibi ayırıcıları soyutlar ve dizinleri birleştirirken alt sistemle uğraşmazsınız. Bu küçük detay, betiği bir CI sunucusuna taşıdığınızda baş ağrısını önler.

## Adım 2 – OCR Motoru Örneği Oluştur (temel ocr örneği)

Şimdi OCR motorunu başlatalım. `OcrEngine`’i, resmi okuyup karakterleri üreten bir beyin olarak düşünün.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

Çoğu OCR kütüphanesi burada dil, DPI veya güven eşiği gibi ayarları değiştirmenize izin verir. Bu **temel OCR örneği** için varsayılanları kullanacağız, ancak çok dilli belgelerle çalışmanız gerektiğinde `ocr_engine.config`’ı keşfedebilirsiniz.

## Adım 3 – TIFF Görüntünüzü Yükleyin (python ile tiff dosyası oku)

İşte **python ile tiff dosyası oku** kısmının devreye girdiği yer. TIFF’ler çok sayfalı olabilir, ancak `Image.load` varsayılan olarak ilk sayfayı alır—tek sayfalı taramalar için mükemmeldir.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

`"YOUR_DIRECTORY"` ifadesini `input.tiff` dosyanızın bulunduğu gerçek klasörle değiştirin. Betiğin nerede çalıştığından emin değilseniz, `Path.cwd()` mevcut çalışma dizinini yazdırır—yol sorunlarını ayıklamak için kullanışlıdır.

## Adım 4 – OCR İşlemini Çalıştır (görüntüden metin çıkarma)

Şimdi sihir gerçekleşir. `process()` çağrısı resmi OCR hattından geçirir ve bir sonuç nesnesi döndürür.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Arka planda motor, görüntüyü gri tonlamaya dönüştürüp eşikleme uygulayabilir ve bir sinir ağına besleyebilir. Bu adımları yönetmeniz gerekmez; kütüphane bunları sizin yerinize halleder.

## Adım 5 – Tanınan Metni Yazdır (tarama görüntüsü metnini dönüştürme)

Son olarak metni dışa aktarın. Gerçek projelerde muhtemelen bir dosyaya ya da veritabanına yazarsınız, ancak örneği sade tutmak için ekrana bastırıyoruz.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Betik çalıştırıldığında aşağıdakine benzer bir çıktı görmelisiniz:

```
Hello, world!
This is a sample scanned document.
```

Çıktı bozuk görünüyorsa, kaynak görüntünün net olduğundan ve OCR dilinin metinle eşleştiğinden emin olun.

## Tam Çalışan Betik

Hepsini bir araya getirdiğimizde, işte eksiksiz, anında çalıştırılabilir program:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Beklenen Çıktı

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

**Tarama görüntüsü metnini** aranabilir bir PDF’e dönüştürmeniz gerekiyorsa, `ocr_result.text`’i `reportlab` gibi bir PDF oluşturucuya yönlendirebilirsiniz—ama bu ayrı bir öğreticinin konusu.

## Yaygın Tuzaklar & Profesyonel İpuçları

- **Düşük çözünürlüklü taramalar**: OCR, 150 DPI altında zorlanır. TIFF bulanıksa, Pillow (`Image.open(...).resize(...)`) ile önce ölçeklendirin.
- **Çok sayfalı dosyalar**: Çok sayfalı TIFF’ler için `Image.load_multi_page()` (kütüphaneniz destekliyorsa) üzerinden döngü kurup sonuçları birleştirin.
- **Dil desteği**: Çoğu motor varsayılan olarak İngilizce’yi kullanır. Örneğin İspanyolca için `ocr_engine.language = "spa"` ayarlayın.
- **Boşluk yönetimi**: OCR sık sık gereksiz satır sonları ekler. `str.splitlines()` ya da düzenli ifadelerle çıktıyı temizleyin.
- **Performans**: Toplu işlemde, her dosya için yeni bir `OcrEngine` oluşturmak yerine tek bir örnek yeniden kullanın.

## Örneği Genişletmek

Artık tek bir görüntü için **python ile ocr nasıl yapılır** konusunu kavradığınıza göre, aşağıdaki adımları değerlendirin:

1. **Toplu işleme** – Bir klasördeki TIFF’ler üzerinde döngü kurup her sonucu bir `.txt` dosyasına yazın.
2. **Pandas ile bütünleştirme** – Çıkarılan metni meta verilerle birlikte saklayarak hızlı analiz yapın.
3. **Hibrit yaklaşım** – OCR’ı `spaCy` gibi NLP kütüphaneleriyle birleştirerek taranmış faturalardan varlıkları (isim, tarih, tutar) çıkarın.
4. **Alternatif dosya formatları** – API ya da veritabanından gelen görüntüler için `Image.load` yerine `Image.from_bytes` kullanın.

Tüm bu adımlar, **görüntüden metin çıkarma** ve **tarama görüntüsü metnini** makinelerin anlayabileceği bir forma dönüştürme temel fikri üzerine inşa edilmiştir.

## Sonuç

Net, uçtan uca bir **temel OCR örneği** üzerinden **python ile ocr nasıl yapılır**, **python ile tiff dosyası oku** ve **görüntüden metin çıkarma** işlemlerini sadece birkaç satır kodla gösterdik. Betik bağımsız, hata yönetimi içeriyor ve sonucu doğrudan ekrana yazdırıyor; bu da taranmış belgeleri düzenlenebilir metne dönüştürmek isteyen her proje için sağlam bir temel oluşturur.

Denemeler yapmaktan çekinmeyin—OCR arka ucunu değiştirin, ön işleme adımlarını ayarlayın ya da çıktıyı sonraki bir iş akışına bağlayın. Güvenilir bir şekilde **tarama görüntüsü metnini** aranabilir, sorgulanabilir verilere dönüştürebildiğinizde sınır yoktur.

Kenar durumları, dil paketleri ya da performans ayarları hakkında sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!

![python ile ocr örneği](/images/ocr-python-example.png "python ile ocr betik çıktısının ekran görüntüsü")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}