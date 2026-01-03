---
category: general
date: 2026-01-02
description: Aspose OCR ile özel bir günlükleyici kullanarak AI'yi nasıl kaydedeceğinizi
  öğrenin. Bu kılavuz, özel bir günlükleyici örneğini, Aspose OCR'yi nasıl içe aktaracağınızı
  ve özel günlükleyiciyi nasıl ayarlayacağınızı kapsar.
draft: false
keywords:
- how to log ai
- use custom logger
- custom logger example
- import aspose ocr
- set custom logger
language: tr
og_description: Aspose OCR'yi özel bir logger ile kullanarak AI kaydetmeyi öğrenin.
  Aspose OCR'yi içe aktarma, özel bir logger ayarlama ve çıktıyı görme adımlarını
  adım adım izleyin.
og_title: Aspose OCR ile AI'yi Günlüğe Kaydetme – Özel Günlükleyici Örneği
tags:
- Aspose OCR
- Python
- Logging
title: Aspose OCR ile AI'yi Günlüğe Kaydetme – Özel Günlükleyici Örneği
url: /tr/python/general/how-to-log-ai-with-aspose-ocr-custom-logger-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile AI Günlüğü Nasıl Tutulur – Özel Logger Örneği

Aspose OCR ile oynarken **AI nasıl günlüğe kaydedilir** diye hiç merak ettiniz mi? Belki varsayılan konsol logger'ını denediniz ve “Bu yeterli, ama daha şık bir şey yapabilir miyim ya da logları bir dosyaya gönderebilir miyim?” dediniz. Yalnız değilsiniz. Bu öğreticide **özel bir logger örneği** üzerinden tam bir örnek gösterecek, ihtiyacınız olan kodu sunacak ve *neden* her bir parçanın önemli olduğunu açıklayacağız.

Bu rehberi tamamladığınızda şunları yapabilecek durumdasınız:

* **Aspose OCR**'ı Python’da sorunsuz bir şekilde içe aktarın.  
* **Özel bir logger** ayarlayın ve AI motorunun yaydığı her mesajı yakalayın.  
* Çıktıyı doğrulayın ve logger'ı kendi loglama çerçevenize uyarlayın.

Harici bir dokümantasyona gerek yok – ihtiyacınız olan her şey burada.

---

## Önkoşullar

İlerlemeye başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Sebep |
|------------|-------|
| Python 3.8+ | `asposeocr` paketi modern Python sürümlerini hedefler. |
| `asposeocr` kütüphanesi kurulu (`pip install asposeocr`) | Kullanacağımız `asposeocr.ai` modülünü sağlar. |
| Fonksiyonlar ve çağrılabilirler hakkında temel bilgi | Özel bir logger oluşturmak için gerekir. |

Eğer bunlardan birine sahip değilseniz, kütüphaneyi şimdi kurun:

```bash
pip install asposeocr
```

---

## Adım 1 – Aspose OCR ve AI modülünü içe aktarın

**Aspose OCR**'ı **içe aktarmak** istediğinizde ilk yapmanız gereken `asposeocr.ai` ad alanını çekmektir. Bu, tüm AI‑tabanlı OCR işlemlerinin giriş noktası olan `AsposeAI` sınıfına erişmenizi sağlar.

```python
# Step 1: Import the Aspose OCR AI module
import asposeocr.ai as ai
```

*Neden önemli:* Doğru modülü içe aktarmak, doğru backend ile iletişim kurduğunuzdan emin olmanızı sağlar. `.ai` alt‑modülünü atlayıp sadece klasik OCR API'sini alırsanız, ihtiyacımız olan loglama kancalarına ulaşamazsınız.

---

## Adım 2 – Varsayılan AI motorunu (konsol logger) oluşturun

Aspose OCR, doğrudan `stdout`'a yazan yerleşik bir logger ile gelir. Temel davranışı görebilmek için bunu çalıştıralım.

```python
# Step 2: Create an AI engine that logs to the console by default
default_engine = ai.AsposeAI()
```

`default_engine` ile herhangi bir OCR işlemi çalıştırdığınızda şu tür mesajlar görürsünüz:

```
[INFO] AsposeAI initialized – version 23.10
[DEBUG] Loading language model...
```

Bu mesajlar hızlı hata ayıklama için faydalıdır, ancak üretim ortamları için yeterince esnek değildir. Bu yüzden bir sonraki adıma geçiyoruz.

---

## Adım 3 – Özel bir logger tanımlayın (bir `str` kabul eden herhangi bir callable)

**Özel bir logger**, tek bir `str` argümanı alan herhangi bir Python callable'ı olabilir. Aşağıda mesajların başına `[AI LOG]` ekleyen minimal bir örnek var. `print` ifadesini `logging.info`, dosyaya yazma veya bir izleme servisine gönderme ile değiştirebilirsiniz.

```python
# Step 3: Define a custom logger (any callable that accepts a string)
def custom_logger(message: str):
    # You could replace this with `logging.info(message)` or any other sink.
    print("[AI LOG]", message)
```

*Neden işe yarar:* `AsposeAI` yapıcı, “string‑ile‑çağır” protokolünü uygulayan bir `logging` argümanı arar. Bu imzaya uyan bir fonksiyon sağladığınızda, her log satırının nasıl işlendiği tamamen sizin kontrolünüzde olur.

---

## Adım 4 – Özel logger'ı kullanan bir AI motoru oluşturun

Şimdi her şeyi birleştirme zamanı. `custom_logger`'ı `AsposeAI` yapıcısına `logging` parametresiyle geçin. Motor, içsel her mesajı sizin fonksiyonunuza yönlendirecek.

```python
# Step 4: Create an AI engine that uses the custom logger
engine_with_custom_logger = ai.AsposeAI(logging=custom_logger)
```

### Beklenen çıktı

Basit bir OCR çağrısı (ör. `engine_with_custom_logger.recognize("sample.png")`) şu şekilde bir çıktı üretir:

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.
```

Artık her satırın başında `[AI LOG]` olduğunu göreceksiniz; bu da `custom_logger` içinde tanımladığımız şeydir. Bu, **AI nasıl günlüğe kaydedilir** sorusunun tamamen sizin kontrolünüzde olduğunu kanıtlar.

---

## Tam Çalışan Örnek – İçe aktarmadan yürütmeye

Aşağıda `custom_logger_demo.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam betik yer alıyor. Aspose OCR'ı içe aktarmaktan özel logger ile basit bir OCR isteği yapmaya kadar tüm akışı gösterir.

```python
# custom_logger_demo.py
# -------------------------------------------------
# Demonstrates how to log AI using Aspose OCR
# with a user‑defined logger.
# -------------------------------------------------

import asposeocr.ai as ai

def custom_logger(message: str):
    """A tiny logger that prefixes messages."""
    print("[AI LOG]", message)

def main():
    # Use the custom logger when creating the AI engine
    ocr_engine = ai.AsposeAI(logging=custom_logger)

    # Path to an image you want to process (replace with your own)
    image_path = "sample.png"

    # Perform OCR – this will trigger the logger
    try:
        result = ocr_engine.recognize(image_path)
        print("\n--- OCR RESULT ---")
        print(result.text)  # Assuming the result object has a `text` attribute
    except Exception as e:
        print("[AI LOG] Error during OCR:", e)

if __name__ == "__main__":
    main()
```

**Çalıştırdığınızda ne beklemelisiniz**

```bash
python custom_logger_demo.py
```

```
[AI LOG] AsposeAI initialized – version 23.10
[AI LOG] Loading language model...
[AI LOG] Model loaded successfully.
[AI LOG] Starting OCR on sample.png
[AI LOG] OCR completed – 98% confidence.

--- OCR RESULT ---
Hello world! This is the extracted text.
```

Eğer **özel logger'ı** bir dosyaya yönlendirmek isterseniz, `custom_logger` içindeki `print` ifadesini şu şekilde değiştirin:

```python
def file_logger(message: str):
    with open("ocr.log", "a", encoding="utf-8") as f:
        f.write(message + "\n")
```

ve `AsposeAI` oluştururken `logging=file_logger` parametresini kullanın.

---

## Yaygın Sorular & Kenar Durumlar

| Soru | Cevap |
|------|-------|
| *Standart `logging` modülünü kullanabilir miyim?* | Kesinlikle. Bir logger örneği yapılandırın ve callable içinde `logger.info(message)` çağırın. |
| *Logger bir istisna fırlatırsa ne olur?* | SDK, logger'dan gelen istisnayı yakalar ve devam eder, ancak o log satırını kaybeder. Logger'ı basit tutun. |
| *Logger debug‑seviyesindeki mesajları da alıyor mu?* | Evet. AI motoru **tüm** iç mesajları (INFO, DEBUG, WARN) iletir. Sadece belirli seviyeleri istiyorsanız callable içinde filtreleyin. |
| *`logging` argümanı isteğe bağlı mı?* | Atlanırsa motor, yerleşik konsol logger'ına geri döner. |
| *Bu async kodda çalışır mı?* | Logger kendisi senkroniktir; async bir senaryoya ihtiyacınız varsa, çağrıyı bir `asyncio` coroutine içinde sarın ve gerektiğinde `await` kullanın. |

---

## Pro İpuçları – Logger'ınızı Üretime Hazır Hale Getirin

1. **Toplu yazma** – Her mesaj için dosya açıp kapatmak yavaştır. Buffering destekli bir `logging.FileHandler` kullanın.  
2. **Zaman damgaları ekleyin** – `datetime.now().isoformat()` ifadesini önek olarak ekleyin, böylece hata ayıklama daha kolay olur.  
3. **Log seviyeleri** – Granülerlik gerekiyorsa, imzayı `(level, message)` gibi bir tuple kabul edecek şekilde değiştirin ve SDK çağrısını (şu anda sadece string gönderiyor) buna göre uyarlayın; seviyeleri manuel olarak ayırabilirsiniz.  
4. **Konfigürasyonu merkezileştirin** – Logger tanımınızı ayrı bir modülde (`my_logging.py`) tutun ve `AsposeAI` örneği oluşturduğunuz her yerde içe aktarın.  

Bu püf noktaları, sadece *AI nasıl günlüğe kaydedilir* sorusuna değil, aynı zamanda gerçek dünyada *AI logları nasıl verimli bir şekilde tutulur* sorusuna da yanıt verir.

---

## Sonuç

Aspose OCR ile **AI nasıl günlüğe kaydedilir** sorusunu baştan sona ele aldık: kütüphaneyi içe aktarma, varsayılan motoru oluşturma, **özel logger örneği** yazma ve bu logger'ı AI motoruna bağlama. Kod eksiksiz, çalıştırılabilir ve tercih ettiğiniz herhangi bir loglama arka ucuna uyarlanabilir.

Daha ileri gitmek isterseniz, `print`‑tabanlı logger'ı Python’un `logging` modülüne, Datadog gibi bir bulut servisine veya yapılandırılmış JSON çıktısına yönlendirin. Desen aynı kalır—**özel logger kullan** ve `AsposeAI` örneği oluştururken **özel logger ayarla**.

Keyifli kodlamalar, ve loglarınız OCR sonuçlarınız kadar net olsun!

---

![how to log ai screenshot](image.png "how to log ai örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}