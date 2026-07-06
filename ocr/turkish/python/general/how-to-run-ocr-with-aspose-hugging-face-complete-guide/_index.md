---
category: general
date: 2026-04-29
description: Tarama dosyalarınızda OCR çalıştırmayı, Hugging Face modelini otomatik
  olarak kullanmayı ve Aspose OCR ile dakikalar içinde taramalardan metin tanımayı
  öğrenin.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: tr
og_description: Aspose OCR kullanarak taramalarda OCR nasıl çalıştırılır, Hugging
  Face modelini otomatik olarak indirir ve temiz, noktalama işaretli metin elde eder.
og_title: Aspose ve Hugging Face ile OCR Nasıl Çalıştırılır – Tam Rehber
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Aspose ve Hugging Face ile OCR Nasıl Çalıştırılır – Tam Rehber
url: /tr/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose & Hugging Face ile OCR Çalıştırma – Tam Kılavuz

Hiç **OCR çalıştırmanın** taranmış belgeler yığını üzerinde saatlerce ayar yapmadan nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede geliştiriciler, **tarama üzerinden metin tanıma** işlemini hızlıca yapmak istiyor, ancak model indirme ve son‑işleme aşamalarında takılıyorlar.  

İyi haber: Bu öğreticide, **bir Hugging Face modeli** kullanan, otomatik olarak modeli indiren ve çıktıya noktalama ekleyerek metnin insan tarafından yazılmış gibi okunmasını sağlayan hazır bir çözüm gösteriyoruz. Sonunda, klasördeki her görüntüyü işleyen ve her taramanın yanına temiz bir `.txt` dosyası bırakan bir betiğe sahip olacaksınız.

## Gerekenler

- Python 3.8+ (kod f‑string kullandığı için daha eski sürümler yeterli olmayacak)
- `aspose-ocr` paketi (`pip install aspose-ocr` ile kurulur)
- İlk model indirme için internet erişimi  
- Görüntü taramaları içeren bir klasör (`.png`, `.jpg` veya `.tif`)

Hepsi bu—ekstra ikili dosyalar yok, manuel model ayarlamaları yok. Hadi başlayalım.

![how to run OCR example](https://example.com/ocr-demo.png "how to run OCR example")

## Adım 1: Aspose OCR Sınıflarını İçe Aktarın ve Ortamı Hazırlayın

Aspose OCR kütüphanesinden gerekli sınıfları alarak başlıyoruz. Her şeyi baştan içe aktarmak betiği düzenli tutar ve eksik bağımlılıkları fark etmeyi kolaylaştırır.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Neden önemli*: `OcrEngine` ağır işi yaparken, `AsposeAI` büyük bir dil modelini daha akıllı son‑işleme için bağlamamızı sağlar. İçe aktarmayı atlayarsanız kod derlenmez—bu yüzden unutmayın.

## Adım 2: GPU‑Duyarlı bir Hugging Face Modeli Yapılandırın  

Şimdi Aspose’a modelin nereden çekileceğini ve kaç katmanın GPU’da çalıştırılacağını söylüyoruz. `allow_auto_download="true"` bayrağı **modelin otomatik indirilmesi** işini sizin için halleder.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Pro ipucu**: GPU’nuz yoksa `gpu_layers=0` olarak ayarlayın. Model CPU’ya geçer, daha yavaş olur ama yine de çalışır.

### Neden Hugging Face Modeli Seçilmeli?

Hugging Face, kullanıma hazır LLM’lerin devasa bir koleksiyonunu barındırır. `Qwen/Qwen2.5-3B-Instruct-GGUF` adresine işaret ederek, noktalama ekleyebilen, boşlukları düzeltebilen ve küçük OCR hatalarını bile onarabilen kompakt, talimat‑tuned bir model elde edersiniz. Bu, **use hugging face model** ifadesinin pratikteki özüdür.

## Adım 3: AI Motorunu Başlatın ve Noktalama Son‑İşlemesini Etkinleştirin  

AI motoru sadece şık sohbetler için değil—burada ham OCR çıktısını temizleyen bir *noktalama ekleyici* bağlıyoruz.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Ne oluyor?* `set_post_processor` çağrısı, OCR motoru tamamlandıktan sonra çalışan yerleşik bir son‑işleyici kaydeder. Ham dizeyi alır, gerekli yerlere virgül, nokta ve büyük harf ekler, böylece son metin çok daha okunaklı hâle gelir.

## Adım 4: OCR Motorunu Oluşturun ve AI Motorunu Bağlayın  

AI motorunu OCR motoruna bağlamak, karakterleri okuyabilen ve sonucu parlatabilen tek bir nesne elde etmemizi sağlar.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Bu adımı atlamazsanız OCR hâlâ çalışır, ancak noktalama desteğini kaybedersiniz—çıktı kelime yığını gibi görünür.

## Adım 5: Klasördeki Her Görüntüyü İşleyin  

İşte öğreticinin kalbi. Her görüntüyü döngüye alıyor, OCR çalıştırıyor, son‑işleyiciyi uyguluyor ve temiz metni yan yana bir `.txt` dosyasına yazıyoruz.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Beklenen Sonuç

Betik çalıştırıldığında aşağıdakine benzer bir çıktı verir:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Her satır güven puanını (hızlı bir sağlık kontrolü) gösterir ve `invoice_001.png.txt`, `receipt_2024.tif.txt` gibi dosyalar oluşturur; bu dosyalar noktalama eklenmiş, insan tarafından okunabilir metin içerir.

### Kenar Durumları & Varyasyonlar

- **İngilizce dışı taramalar**: `hugging_face_repo_id` değerini çok‑dilli bir modele (ör. `microsoft/Multilingual-LLM-GGUF`) değiştirin.
- **Büyük partiler**: Döngüyü `concurrent.futures.ThreadPoolExecutor` içinde çalıştırarak paralel işleme geçin, ancak GPU bellek sınırlarına dikkat edin.
- **Özel son‑işleme**: `"punctuation_adder"` ifadesini, alan‑spesifik temizlik (ör. fatura numaralarını kaldırma) ihtiyacınıza göre kendi betiğinizle değiştirin.

## Adım 6: Kaynakları Temizleyin  

İş bittiğinde kaynakları serbest bırakmak bellek sızıntılarını önler; özellikle uzun‑ömürlü bir hizmet içinde çalışıyorsanız bu çok önemlidir.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Bu adımı atlamak GPU belleğinin hâlâ dolu kalmasına neden olur ve sonraki çalışmaları sabote eder.

## Özet: OCR’u Baştan Sona Çalıştırma  

Sadece birkaç satır kodla, **OCR’u** bir klasör taraması üzerinde nasıl çalıştıracağınızı, **Hugging Face modelini** ilk çalıştırmada otomatik indiren ve **tarama üzerinden metin tanıma** işlemini noktalama ekleyerek nasıl otomatikleştireceğinizi gösterdik. Tam betik kopyala‑yapıştır, yol ayarlarını yap ve çalıştır hazır.

## Sonraki Adımlar & İlgili Konular  

- **Toplu son‑işleme**: Daha hızlı toplu işlem için `ocr_engine.run_batch_postprocessor`’ı keşfedin.  
- **Alternatif modeller**: OCR ile birlikte konuşmadan metne dönüşüm ihtiyacınız varsa `openai/whisper` ailesini deneyin.  
- **Veritabanı entegrasyonu**: Çıkarılan metni SQLite veya Elasticsearch’te saklayarak aranabilir arşivler oluşturun.  

Denemekten çekinmeyin—modeli değiştirin, `gpu_layers` değerini ayarlayın veya kendi son‑işleyicinizi ekleyin. Aspose OCR’un esnekliği ile Hugging Face model hub’ının çeşitliliği, herhangi bir belge‑dijitalleştirme projesi için çok yönlü bir temel sağlar.

---

*Kodlamanız keyifli olsun! Bir sorunla karşılaşırsanız aşağıya yorum bırakın ya da daha derin yapılandırma seçenekleri için Aspose OCR belgelerine göz atın.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}