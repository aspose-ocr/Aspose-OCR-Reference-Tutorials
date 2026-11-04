---
category: general
date: 2026-03-28
description: Görüntüde OCR çalıştırmayı, Hugging Face modelini otomatik olarak indirmeyi,
  OCR metnini temizlemeyi ve Aspose OCR Cloud kullanarak Python’da LLM modelini yapılandırmayı
  öğrenin.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: tr
og_description: Görüntüde OCR çalıştırın ve çıktıyı otomatik indirilmiş bir Hugging Face
  modeli kullanarak temizleyin. Bu kılavuz, Python’da LLM modelini nasıl yapılandıracağınızı
  gösterir.
og_title: Görüntüde OCR Çalıştır – Tam Aspose OCR Cloud Öğreticisi
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Aspose OCR Cloud ile Görüntüde OCR Çalıştırma – Tam Adım Adım Kılavuz
url: /tr/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Çalıştırma – Tam Aspose OCR Cloud Öğreticisi

Hiç bir görüntü dosyasında OCR çalıştırmanız gerekti, ancak ham çıktı karışık bir karmaşa gibi göründü mü? Benim deneyimime göre en büyük sorun tanıma değil—temizlik. Neyse ki, Aspose OCR Cloud size *OCR metnini temizleyebilen* bir LLM post‑işlemcisi ekleme imkanı sunuyor. Bu öğreticide ihtiyacınız olan her şeyi adım adım göstereceğiz: **Hugging Face modelinin indirilmesinden** LLM yapılandırmasına, OCR motorunun çalıştırılmasına ve sonunda sonucun cilalanmasına kadar.

Bu rehberin sonunda çalıştırmaya hazır bir betiğiniz olacak:

1. Hugging Face'ten kompakt bir Qwen 2.5 modelini çeker (sizin için otomatik indirilir).  
2. Modeli ağın bir kısmını GPU, geri kalanını CPU'da çalışacak şekilde yapılandırır.  
3. El yazısı not görüntüsü üzerinde OCR motorunu yürütür.  
4. Tanınan metni temizlemek için LLM'yi kullanır ve size insan tarafından okunabilir bir çıktı verir.

> **Prerequisites** – Python 3.8+, `asposeocrcloud` paketi, en az 4 GB VRAM'li bir GPU (isteğe bağlı ama tavsiye edilir) ve ilk model indirmesi için bir internet bağlantısı.

---

## İhtiyacınız Olanlar

- **Aspose OCR Cloud SDK** – `pip install asposeocrcloud` komutu ile kurun.  
- **Bir örnek görüntü** – örneğin, yerel bir klasöre yerleştirilmiş `handwritten_note.jpg`.  
- **GPU desteği** – CUDA destekli bir GPU'nuz varsa, betik 30 katmanı GPU'ya aktarır; aksi takdirde otomatik olarak CPU'ya geçer.  
- **Yazma izni** – betik modeli `YOUR_DIRECTORY` içinde önbelleğe alır; klasörün mevcut olduğundan emin olun.

## Adım 1 – LLM Modelini Yapılandırma (Hugging Face modelini indirme)

İlk olarak Aspose AI'ye modeli nereden alacağını söylememiz gerekir. `AsposeAIModelConfig` sınıfı otomatik indirme, kuantizasyon ve GPU katman tahsislerini yönetir.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Neden önemli?** – `int8`'e kuantize etmek bellek kullanımını büyük ölçüde azaltır (≈ 4 GB vs 12 GB). Modeli GPU ve CPU arasında bölmek, mütevazı bir RTX 3060'da bile 3 milyar parametreli bir LLM çalıştırmanıza olanak tanır. GPU'nuz yoksa `gpu_layers=0` ayarlayın ve SDK her şeyi CPU'da tutar.

> **İpucu:** İlk çalıştırmada ~ 1.5 GB indirilecektir, bu yüzden birkaç dakika ve stabil bir bağlantı sağlayın.

## Adım 2 – Model Yapılandırmasıyla AI Motorunu Başlatma

Şimdi Aspose AI motorunu başlatıyor ve az önce oluşturduğumuz yapılandırmayı ona veriyoruz.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Arka planda ne oluyor?** SDK, mevcut bir model için `directory_model_path`'i kontrol eder. Eşleşen bir sürüm bulursa anında yükler; aksi takdirde Hugging Face'ten GGUF dosyasını indirir, açar ve çıkarım hattını hazırlar.

## Adım 3 – OCR Motorunu Oluşturma ve AI Post‑İşlemcisini Ekleme

OCR motoru karakter tanımanın ağır işini yapar. `ocr_ai.run_postprocessor`'ı ekleyerek tanımanın ardından otomatik olarak **temiz OCR metni** etkinleştiriyoruz.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Neden bir post‑işlemci kullanmalı?** Ham OCR genellikle yanlış yerlerde satır sonları, hatalı noktalama işaretleri veya gereksiz semboller içerir. LLM, çıktıyı düzgün cümlelere yeniden yazar, yazım hatalarını düzeltir ve hatta eksik kelimeleri tahmin edebilir—temelde ham dökümü cilalı bir metne dönüştürür.

## Adım 4 – Bir Görüntü Dosyasında OCR Çalıştırma

Her şey bağlandığına göre, motoru bir görüntü ile besleme zamanı.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Köşe durumu:** Görüntü büyükse (> 5 MP), işleme hızını artırmak için önce yeniden boyutlandırmak isteyebilirsiniz. SDK, bir Pillow `Image` nesnesini kabul eder, bu yüzden gerektiğinde `PIL.Image.thumbnail()` ile ön işleme yapabilirsiniz.

## Adım 5 – AI'yi Tanınan Metni Temizletmek ve Her İki Versiyonu da Gösterme

Son olarak daha önce eklediğimiz post‑işlemciyi çağırıyoruz. Bu adım, *temizleme öncesi* ve *sonrası* arasındaki farkı gösterir.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Beklenen Çıktı

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

LLM'nin şu şekilde çalıştığını fark edin:

- Yaygın OCR hatalarını düzeltti (`Th1s` → `This`).  
- Gereksiz sembolleri kaldırdı (`&` → `and`).  
- Satır sonlarını düzgün cümlelere dönüştürdü.

## 🎨 Görsel Genel Bakış (Görüntüde OCR Çalıştırma İş Akışı)

![Görüntüde OCR Çalıştırma iş akışı](run_ocr_on_image_workflow.png "Model indirilmesinden temizlenmiş çıktıya kadar görüntüde OCR çalıştırma sürecini gösteren diyagram")

Yukarıdaki diyagram, tam iş akışını özetliyor: **Hugging Face modelini indir → LLM'yi yapılandır → AI'yi başlat → OCR motoru → AI post‑işlemci → temiz OCR metni**.

## Sık Sorulan Sorular & Uzman İpuçları

### GPU'm yoksa ne olur?

`AsposeAIModelConfig` içinde `gpu_layers=0` ayarlayın. Model tamamen CPU'da çalışacak, bu daha yavaş ama yine de işlevsel. Ayrıca çıkarım süresini makul tutmak için daha küçük bir modele (ör. `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) geçebilirsiniz.

### Modeli daha sonra nasıl değiştiririm?

`hugging_face_repo_id` değerini güncelleyin ve `ocr_ai.initialize(model_config)`'i yeniden çalıştırın. SDK sürüm değişikliğini algılayacak, yeni modeli indirecek ve önbellekteki dosyaları değiştirecektir.

### Post‑işlemci istemini özelleştirebilir miyim?

Evet. `custom_settings`'e `prompt_template` anahtarı içeren bir sözlük geçirin. Örneğin:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Temizlenmiş metni bir dosyaya kaydetmeli miyim?

Kesinlikle. Temizlemeden sonra sonucu `.txt` veya `.json` dosyasına yazarak sonraki işlemler için kullanabilirsiniz:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

## Sonuç

Size Aspose OCR Cloud ile **görüntü dosyalarında OCR çalıştırma**, otomatik **Hugging Face modeli indirme**, uzmanlıkla **LLM model ayarlarını yapılandırma** ve sonunda güçlü bir LLM post‑işlemci kullanarak **OCR metnini temizleme** konularını gösterdik. Tüm süreç tek bir, çalıştırması kolay Python betiğine sığar ve hem GPU destekli hem de sadece CPU'lu makinelerde çalışır.

Eğer bu iş akışına hâkimseniz, şu konularda denemeler yapabilirsiniz:

- **Farklı LLM'ler** – daha geniş bir bağlam penceresi için `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` deneyin.  
- **Toplu işleme** – bir klasördeki görüntüler üzerinde döngü kurup temizlenmiş sonuçları bir CSV'ye toplayın.  
- **Özel istemler** – AI'yi alanınıza göre özelleştirin (hukuki belgeler, tıbbi notlar vb.).

`gpu_layers` değerini istediğiniz gibi ayarlayabilir, modeli değiştirebilir veya kendi isteminizi ekleyebilirsiniz. Gökyüzü sınırdır ve şu an elinizdeki kod bir başlangıç noktasıdır.

İyi kodlamalar, ve OCR çıktılarınız daima temiz olsun! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}