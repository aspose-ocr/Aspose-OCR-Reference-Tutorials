---
category: general
date: 2026-01-12
description: Python OCR öğreticisi, bir görüntüden tablo metnini nasıl çıkaracağınızı
  gösterir. Görüntüden tablo okumayı öğrenin ve Aspose OCR ile seçilen metni çıkarın.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: tr
og_description: Python OCR öğreticisi, bir görüntüden tablo metnini nasıl çıkaracağınızı,
  görüntüden tablo okuyacağınızı ve Aspose OCR kullanarak seçili metni nasıl çıkaracağınızı
  öğretir.
og_title: 'Python OCR Eğitimi: Görüntülerden Tablo Metnini Çıkar'
tags:
- OCR
- Python
- AsposeOCR
title: 'Python OCR Öğreticisi: Görsellerden Tablo Metnini Çıkarma'
url: /tr/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Öğreticisi: Görüntülerden Tablo Metnini Çıkarma

Hiç bir **python ocr tutorial**'a ihtiyacınız oldu mu ki taranmış bir formdan tablo çıkarmayı gerçekten gösteriyor? Tek başınıza değilsiniz. Çoğu öğretici genel metin çıkarımıyla durur, size ihtiyacınız olan düzenli veri ızgarasını nasıl izole edeceğinizi tahmin ettirir.  

Bu rehberde gerçek bir senaryoyu adım adım inceleyeceğiz: bir görüntüden tablo okuma, yalnızca ihtiyacınız olan seçili metni çıkarma ve sonunda sonuçları yazdırma. Yol boyunca **how to extract table** verisini güvenilir bir şekilde nasıl çıkaracağınıza dair ipuçları da ekleyeceğiz, böylece her seferinde tekerleği yeniden icat etmek zorunda kalmayacaksınız.

## Öğrenecekleriniz

- Aspose OCR'yi Python için nasıl kuracağınız.
- Tabloyu içeren dikdörtgen bir bölgeyi nasıl tanımlayacağınız.
- **extract table text** ve **read table from image** için tam adımlar.
- Çoklu dil veya düzensiz tablo düzenleriyle başa çıkma ipuçları.
- Bugün projenize ekleyebileceğiniz tam, çalıştırılabilir bir betik.

**Önkoşullar**  
- Python 3.8 ve üzeri.  
- OCR kavramlarına temel aşinalık (derin uzmanlık gerekmez).  
- Açık bir tablo içeren bir PNG veya JPEG görüntüsü (biz buna `form_with_table.png` diyeceğiz).  

Eğer bunlara sahipseniz, hadi başlayalım—gereksiz ayrıntı yok, sadece uygulanabilir kod.

![python ocr tutorial example of table region](table_region_example.png){alt="python ocr öğreticisi örneği tablo bölgesini gösteriyor"}

## Adım 1: Aspose OCR'yi Yükleyin ve İçe Aktarın

İlk olarak: Aspose OCR kütüphanesine ihtiyacınız var. Paket PyPI'da, tek bir `pip` komutu işi halleder.

```bash
pip install aspose-ocr
```

Şimdi modülü ve ihtiyacınız olacak yardımcıları içe aktarın.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Pro tip:* Bağımlılıkları bir `requirements.txt` dosyasında tutun. Ortamı yeniden oluşturmayı çok kolaylaştırır.

## Adım 2: OCR Motorunu Başlatın (Python OCR Öğreticisi Çekirdeği)

Motoru oluşturmak, herhangi bir **python ocr tutorial**'nin kalbidir. Burada ayrıca varsayılan dili İngilizce olarak ayarlıyoruz—daha sonra istediğiniz gibi değiştirebilirsiniz.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Neden dili ayarlıyoruz? Motor, hangi karakterleri bekleyeceğini bildiğinde OCR doğruluğu büyük ölçüde artar. Çok dilli formlarla çalışıyorsanız, bir dil listesi belirleyebilir veya bölge bazında geçersiz kılabilirsiniz (aşağıya bakın).

## Adım 3: Görüntünüzü Yükleyin

Aspose OCR, en yaygın görüntü formatlarıyla çalışır. Dosya yolunu gösterin, ardından işleme hazır bir `Image` nesnesine sahip olacaksınız.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Kenar durumu:* 5 MB üzerindeki büyük görüntüler işlem süresini yavaşlatabilir. Performans sorunları ortaya çıkarsa yeniden boyutlandırmayı veya sıkıştırmayı düşünün.

## Adım 4: Tablo Bölgesini Tanımlayın (Görüntüden Tablo Okuma)

Şimdi eğlenceli kısım: motoru tablonun *nerede* olduğunu söylemek. Bir `OcrRegion` ve içinde bir `Rectangle` (x, y, genişlik, yükseklik) sağlarsınız. Koordinatlar piksel tabanlıdır, bu yüzden biraz deneme yapmanız gerekebilir.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Neden bölge kullanıyoruz? OCR'yi sadece tablo alanıyla sınırlayarak **extract selected text** daha hızlı elde eder ve çevredeki etiket ya da grafik gürültüsünden kaçınırız. Ayrıca motor, tek tip bir düzen üzerine odaklanabildiği için doğruluk da artar.

## Adım 5: Tanımlı Bölge Üzerinde OCR Çalıştırın

Bölge ayarlandıktan sonra `process_region` metodunu çağırıyoruz. Metod, ham metin, güven puanları ve gerekirse daha sonra kullanabileceğiniz sınırlayıcı kutular içeren bir `OcrResult` nesnesi döndürür.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Birden fazla tablo çıkarmanız gerekiyorsa, farklı dikdörtgenlerle Adım 4‑5'i tekrarlamanız yeterlidir.

## Adım 6: Çıkarılan Tablo Metnini Çıktılayın

Son olarak, tablonun metinsel temsilini yazdırın—ya da saklayın. Aspose OCR, genellikle satırlarla hizalanan satır sonlarıyla düz metin döndürür, bu da son‑işlemeyi oldukça basit hâle getirir.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Beklenen çıktı** (örnek):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Bu dizeyi artık `csv` ayrıştırıcılarına, pandas DataFrame'lerine ya da herhangi bir sonraki analiz hattına besleyebilirsiniz.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, hemen çalıştırabileceğiniz tam betik burada. `YOUR_DIRECTORY/form_with_table.png` ifadesini görüntünüzün gerçek yolu ile değiştirin.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Betik `python extract_table.py` komutuyla çalıştırın. Her şey uyumluysa, tablo konsola yazdırılacaktır.

## Yaygın Sorular ve Kenar‑Durum İşleme

**Tablo tam olarak dikdörtgen değilse ne olur?**  
Tabloyu birden fazla üst üste binen bölgeye ayırabilir ya da tüm alanı kapsayan daha büyük bir dikdörtgen kullanıp ardından metni (ör. satır sonlarına göre bölerek) işleyebilirsiniz.

**Sadece belirli sütunları çıkarabilir miyim?**  
Tam tablo metnini elde ettikten sonra Python'un `csv` ya da `pandas` kütüphanelerini kullanarak ihtiyacınız olan sütunları dilimleyebilirsiniz. OCR adımı, dikdörtgen içindeki her şeyi döndürür.

**İngilizce dışındaki tablolarla nasıl çalışırım?**  
`ocr_engine.language` (veya `region.language`) değerini uygun enum ile ayarlayın; örneğin `ocr.Language.FRENCH` ya da `ocr.Language.ENGLISH | ocr.Language.SPANISH` gibi birden fazla dili birleştirebilirsiniz.

**Her hücre için sınırlayıcı kutular alınabilir mi?**  
Aspose OCR, `region_result.words` içinde her kelimenin sınırlayıcı kutusunu döndürebilir. Bu kutuları bir ızgaraya eşleştirmeniz gerekir—gelişmiş düzen analizi için faydalıdır.

## Daha İyi Doğruluk İçin İpuçları

- **Clean the image**: OCR'ye vermeden önce görüntüyü ikiliye çevirin ya da kontrastı artırın. Pillow gibi kütüphaneler yardımcı olur.  
- **Avoid compression artifacts**: Mümkün olduğunca taramaları PNG olarak kaydedin.  
- **Mind DPI**: 300 dpi ideal bir değerdir; daha düşük değerler karakter kaçırmaya yol açabilir.  
- **Test different rectangle sizes**: Biraz daha büyük dikdörtgenler, tabloya ait kaçak karakterleri yakalama eğilimindedir.

## Sonraki Adımlar

Artık Aspose OCR ile **how to extract table** verisini ustaca kullandığınıza göre şunları keşfedebilirsiniz:

- Çıkarılan metni Python'un `csv` modülüyle bir CSV dosyasına dönüştürmek.  
- Veriyi analiz için bir **pandas** DataFrame'ine beslemek.  
- El yazısı formları okumak için OCR kullanmak (farklı bir motor ya da ek eğitim gerektirir).  
- Basit bir `for` döngüsüyle onlarca taranmış formun toplu işlenmesini otomatikleştirmek.  

Bu uzantıların her biri, bu **python ocr tutorial**'de ele alınan temel kavramlar üzerine inşa edildiği için ölçeklendirme konusunda sizi iyi bir konuma getirir.

---

*Keyifli kodlamalar! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—çıkarma işlemini ince ayarlamanıza yardımcı olmaktan memnuniyet duyarım.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}