---
category: general
date: 2026-04-26
description: Belgelerinizi toplu OCR ile işleyip taramalardan metin çıkarmayı Python’da
  nasıl yapacağınızı öğrenin. JSON çıktısı için OcrEngine ile adım adım toplu işleme
  öğrenin.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: tr
og_description: Taradığınız dosyaları toplu OCR ile işleyip taramalardan tek bir betik
  içinde metin çıkarmanın yolu. Tam kod, ipuçları ve uç durum yönetimi.
og_title: Batch OCR Nasıl Yapılır – Hızlı Python Rehberi
tags:
- OCR
- Python
- Automation
title: Toplu OCR Nasıl Yapılır – Taramalardan Metni Verimli Şekilde Çıkarma
url: /tr/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Toplu OCR Nasıl Yapılır – Taramalardan Metin Verimli Şekilde Çıkarma

Hiç **toplu OCR** yaparak bir dağ taranmış PDF'yi aklınızı kaybetmeden nasıl işleyebileceğinizi merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli olarak, *“Taramalardan metni tek seferde nasıl çıkarabilirim?”* sorusunu soruyor. İyi haber şu ki, birkaç satır Python bu zahmetli işi sorunsuz, otomatik bir akışa dönüştürebilir.

Bu öğreticide, **taramalardan metin çıkaran**, sonuçları JSON olarak kaydeden ve sonunda hızlı bir kontrol sağlayan, tamamen çalıştırılabilir bir çözümü adım adım inceleyeceğiz. Harici hizmetler yok, sihir yok—sadece saf Python, `OcrEngine` sınıfı ve biraz klasör yönetimi.

## Ne Kazanacaksınız

- Görüntü klasöründeki herhangi bir dosya için **toplu OCR** yapan tam işlevsel bir betik.
- Her satırın *neden* var olduğunu açıklayan net açıklamalar, sadece *ne* yaptığını değil.
- Boş klasörler, görüntü olmayan dosyalar ve büyük partilerle başa çıkma ipuçları.
- JSON çıktısının gerçekten çıkarılan metni içerdiğini doğrulamanın bir yolu.

### Önkoşullar (en temel gereksinimler)

| Gereksinim | Neden Önemli |
|------------|--------------|
| Python 3.8+ | Modern sözdizimi ve tip ipuçları |
| `OcrEngine` library (or a compatible wrapper) | Çekirdek OCR işlevselliği |
| Tarama görüntü dosyaları içeren bir dizin (PNG, JPG, TIFF) | Girdi verisi |
| Çıktı klasörü için yazma izinleri | JSON sonuçlarını kaydetme |

Eğer bunlara sahipseniz, harika—hadi başlayalım.

![toplu OCR iş akışı](image-placeholder.png){alt="toplu OCR iş akışı"}

## Adım 1 – OCR Motorunu Başlatma (toplu OCR nasıl yapılır)

Herhangi bir şeyi işlemeye başlamadan önce bir OCR motoru örneğine ihtiyacımız var. Bunu, her görüntüyü okuyup metin üretecek “beyin” olarak düşünün. Motoru bir kez başlatıp tüm parti boyunca yeniden kullanmak en verimli yaklaşımdır.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Aynı örneği neden yeniden kullanmalıyız?**  
> Her dosya için yeni bir motor oluşturmak, ağır modelleri belleğe tekrar tekrar yükler ve partiyi dramatik şekilde yavaşlatır. Tek bir örnek modeli RAM'de tutar ve binlerce görüntüyü fark edilir bir yavaşlama olmadan işleyebilmenizi sağlar.

## Adım 2 – Taramalarınızın Klasörünü Belirtin (taramalardan metin çıkarma)

Taramalarınız bir yerde diskte duruyor. Betiğe nerede olduklarını söyleyelim. Mutlak yollar, betik farklı bir çalışma dizininden başlatıldığında “dosya bulunamadı” hatalarını önler.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Pro ipucu:**  
> Windows kullanıyorsanız, `os.path.abspath` ile ileri eğik çizgiler (`/`) sorunsuz çalışır, bu yüzden ters eğik çizgileri kaçırmanıza gerek yok.

## Adım 3 – JSON Sonuçlarının Nereye Gideceğini Seçin

Muhtemelen OCR sonuçları için düzenli bir klasör istersiniz. Çıktıyı kaynağın dışına tutmak, daha sonra temizlemeyi veya JSON'u başka bir akışa beslemeyi kolaylaştırır.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Klasörü programlı olarak neden oluşturmalıyız?**  
> Klasör eksik olsa bile betiğin çökmesini engeller ve `exist_ok=True` işlemi idempotent hâle getirir—betiği birden fazla kez çalıştırdığınızda hata almazsınız.

## Adım 4 – Parti İşlemini Çalıştırın (toplu OCR nasıl yapılır)

İşte asıl kısım: `ocr_engine`'i `input_dir` içindeki her dosyayı gezmeye, OCR çalıştırmaya ve `output_dir` içine JSON dökmeye yönlendirin. `format="json"` bayrağı, motorun sonucu aşağı akış araçlarının sevdiği yapılandırılmış bir biçimde serileştirmesini sağlar.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Arkada Ne Oluyor?

1. **Dosya keşfi** – Motor, `input_folder`'ı gizli dosyaları yok sayarak özyinelemeli tarar.
2. **Dosya doğrulama** – Yalnızca desteklenen görüntü uzantıları (`.png`, `.jpg`, `.tif` vb.) OCR modeline gönderilir.
3. **OCR yürütme** – Her görüntü OCR motoruna gönderilir; metin, güven skorları ve düzen verileri yakalanır.
4. **JSON serileştirme** – Sonuç, aynı temel ada sahip ancak `.json` uzantılı bir dosya olarak `output_folder` içinde yazılır.

> **Köşe durumları yönetimi:**  
> - **Boş klasör:** Motor “Dosya bulunamadı” mesajı verir ve sorunsuz bir şekilde döner.  
> - **Bozuk görüntü:** Dosya atlanır, `batch_errors.log` içinde bir hata kaydı oluşturulur ve işlem devam eder.  
> - **Büyük parti (10k+ dosya):** Bellek kullanımı düşük kalır çünkü her görüntü bağımsız işlenir.

## Adım 5 – Dönüşümün Tamamlandığını Doğrulama

Basit bir `print` ifadesi, konsolda anlık geri bildirim sağlar. Üretim akışlarında bunu bir log çağrısı veya e‑posta bildirimiyle değiştirebilirsiniz.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Bu satırı gördüğünüzde, `json_output` klasörünü güvenle inceleyebilirsiniz. Her JSON dosyası kabaca şu şekilde görünecektir:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Artık bu JSON dosyalarını bir veritabanına, bir arama indeksine veya herhangi bir downstream analiz aracına besleyebilirsiniz.

## Sık Sorulan Sorular (ve hızlı cevaplar)

**S: PDF'leri görüntü yerine işlemek istersem ne yapmalıyım?**  
C: Önce her PDF sayfasını bir görüntüye dönüştürün (ör. `pdf2image` kullanarak) ve elde edilen PNG/JPG dosyalarını `input_dir` içine koyun. Toplu OCR mantığı değişmez.

**S: Çıktı formatını düz metin olarak değiştirebilir miyim?**  
C: Kesinlikle. `format="json"` yerine `format="txt"` koyun, motor sadece çıkarılan metni içeren bir `.txt` dosyası yazar.

**S: Taramalarım birden fazla alt‑klasörde—betik özyinelemeli mi?**  
C: Evet. `batch_process` varsayılan olarak dizin ağacını yürür. Düz bir çıktı isterseniz, `flatten=True` (kütüphane destekliyorsa) ayarlayın veya JSON dosya adlarını sonradan işleyin.

**S: Latin dışı alfabelerle nasıl başa çıkılır?**  
C: `OcrEngine`'i bir dil parametresiyle başlatın, ör. `OcrEngine(lang="spa+eng")`. Toplu döngüde başka bir değişiklik yapmanıza gerek yok.

## Profesyonel İpuçları ve Yaygın Tuzaklar

- **Batch boyutu önemli:** CPU dalgalanmaları fark ederseniz, dosyalar arasında basit bir `time.sleep(0.1)` ekleyerek süreci yavaşlatın.  
- **Loglama:** `print` çağrısını Python'un `logging` modülüyle değiştirerek zaman damgaları ve hata seviyeleri yakalayın.  
- **Dosya adı çakışmaları:** İki tarama aynı temel ada sahip ama farklı alt‑klasörlerde bulunuyorsa, JSON dosyaları birbirinin üzerine yazılır. Çıktı adına göreceli yolun bir hash'ini ekleyerek bunu önleyin.  
- **Bellek sızıntıları:** Bazı OCR arka planları yerel kaynakları tutar. Kütüphane bir temizlik yöntemi sağlıyorsa, betiğin sonunda `ocr_engine.close()` çağırın.

## Tam Script – Kopyalayıp Yapıştırmaya Hazır

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Beklenen konsol çıktısı**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

JSON'u bir metin düzenleyiciyle `json_output` içindeki herhangi bir dosyayı açarak ya da Python içinde yükleyerek doğrulayabilirsiniz:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Konsolda çıkarılan ham OCR‑metninin yazdırıldığını görmelisiniz.

## Sonuç

**Toplu OCR** ile bir klasördeki tüm taranmış görüntüleri nasıl işleyip **taramalardan metin** çıkarıp temiz, makine‑okunur JSON dosyalarına dönüştürebileceğinizi ele aldık. Yaklaşım kasıtlı olarak basit: motoru bir kez kurun, bir klasöre yönlendirin ve kütüphane ağır işi halletsin. Bundan sonra şunları yapabilirsiniz:

- JSON'u ...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}