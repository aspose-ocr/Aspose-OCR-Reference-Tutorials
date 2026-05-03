---
category: general
date: 2026-05-03
description: Aspose OCR ve AI imla kontrolü kullanarak toplu OCR görüntüleri nasıl
  işlenir. Görüntülerden metin çıkarmayı, imla kontrolü uygulamayı, ücretsiz AI kaynaklarından
  yararlanmayı ve OCR hatalarını düzeltmeyi öğrenin.
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: tr
og_description: Aspose OCR ve AI yazım denetimi kullanarak toplu OCR görüntüleri nasıl
  işlenir. Görüntülerden metin çıkarmak, yazım denetimi uygulamak, ücretsiz AI kaynaklarından
  yararlanmak ve OCR hatalarını düzeltmek için adım adım kılavuzu izleyin.
og_title: Aspose OCR ile Toplu OCR Nasıl Yapılır – Tam Python Eğitimi
tags:
- OCR
- Python
- AI
- Aspose
title: Aspose OCR ile Toplu OCR Nasıl Yapılır – Tam Python Rehberi
url: /tr/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Toplu OCR Nasıl Yapılır – Tam Python Rehberi

Hiç **toplu OCR** işlemini, her dosya için ayrı bir betik yazmadan, taranmış PDF’ler ya da fotoğraflardan oluşan bir klasörü işlemek zorunda kaldınız mı? Yalnız değilsiniz. Gerçek dünyadaki birçok işlem hattında **görüntülerden metin çıkarma**, yazım hatalarını temizleme ve sonunda tahsis ettiğiniz AI kaynaklarını serbest bırakma ihtiyacınız olacak. Bu öğretici, Aspose OCR, hafif bir AI post‑işlemcisi ve birkaç Python satırıyla bunu tam olarak nasıl yapacağınızı gösteriyor.

OCR motorunu başlatma, bir AI yazım denetleyicisi bağlama, bir klasördeki resimleri döngüye sokma ve ardından modeli temizleme adımlarını birlikte inceleyeceğiz. Sonunda **OCR hatalarını otomatik olarak düzelten** ve **AI kaynaklarını serbest bırakan** hazır bir betiğe sahip olacaksınız, böylece GPU’nuz mutlu kalacak.

## Gereksinimler

- Python 3.9+ (kod tip ipuçları içeriyor ancak daha eski 3.x sürümlerinde de çalışır)
- `asposeocr` paketi (`pip install asposeocr`) – OCR motorunu sağlar.
- Hugging Face modeli `bartowski/Qwen2.5-3B-Instruct-GGUF` erişimi (otomatik indirilir).
- En az birkaç GB VRAM’a sahip bir GPU (betik `gpu_layers = 30` olarak ayarlar, gerekirse azaltabilirsiniz).

Harici servis yok, ücretli API yok – her şey yerel olarak çalışır.

---

## Adım 1: OCR Motorunu Kur – **Toplu OCR** için Verimli Ayarlar

Binlerce resmi işlemeye başlamadan önce sağlam bir OCR motoruna ihtiyacımız var. Aspose OCR, tek bir çağrıda dil ve tanıma modunu seçmemize izin veriyor.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**Neden önemli:** `recognize_mode` değerini `Plain` olarak ayarlamak, çıktıyı hafif tutar; bu, daha sonra bir yazım denetimi çalıştırmayı planladığınızda idealdir. Düzen bilgisine ihtiyacınız olursa `Layout`'a geçebilirsiniz, ancak bu toplu işlerde genellikle istenmeyen bir ek yük getirir.

> **Pro ipucu:** Çok dilli taramalarla uğraşıyorsanız, `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]` gibi bir liste geçirebilirsiniz.

---

## Adım 2: AI Post‑İşlemcisini Başlat – OCR Çıktısına **Yazım Denetimi Uygula**

Aspose AI, istediğiniz modeli çalıştırabilen yerleşik bir post‑işlemci sunar. Burada Hugging Face’dan kuantize bir Qwen 2.5 modelini çekiyor ve yazım denetimi rutinini bağlıyoruz.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**Neden önemli:** Model `q4_k_m` olarak kuantize edilmiştir; bu, bellek kullanımını büyük ölçüde azaltırken hâlâ makul bir dil anlayışı sunar. `set_post_processor` çağrısı, Aspose AI’ye beslediğimiz her dize üzerinde **yazım denetimi uygula** adımını otomatik olarak çalıştırmasını söyler.

> **Dikkat:** GPU’nuz 30 katmanı kaldıramıyorsa, sayıyı 15 ya da hatta 5’e düşürün – betik hâlâ çalışır, sadece biraz daha yavaş olur.

---

## Adım 3: Tek Bir Resimde OCR Çalıştır ve **OCR Hatalarını Düzelt**

OCR motoru ve AI yazım denetleyicisi hazır olduğuna göre, bunları birleştiriyoruz. Bu fonksiyon bir resmi yüklüyor, ham metni çıkarıyor ve ardından AI post‑işlemcisini çalıştırarak temizliyor.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**Neden önemli:** Ham OCR dizesini doğrudan AI modeline vermek, **OCR hatalarını düzelt** adımını herhangi bir regex ya da özel sözlük yazmadan gerçekleştirir. Model bağlamı anlar, bu yüzden “recieve” → “receive” gibi ve daha ince hataları bile düzeltebilir.

---

## Adım 4: **Görüntülerden Metin Çıkar** Toplu Olarak – Gerçek Toplu Döngü

İşte **toplu OCR** sihrinin ortaya çıktığı yer. Bir klasörü dolaşıyor, desteklenmeyen dosyaları atlıyor ve her düzeltilmiş çıktıyı bir `.txt` dosyasına yazıyoruz.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### Beklenen çıktı

*“The quick brown fox jumps over the lazzy dog.”* cümlesini içeren bir resim için şu şekilde bir metin dosyası görürsünüz:

```
The quick brown fox jumps over the lazy dog.
```

Çift “z”nin otomatik olarak düzeltildiğine dikkat edin – bu AI yazım denetiminin etkisi.

**Neden önemli:** OCR ve AI nesnelerini **bir kez** oluşturup tekrar kullanarak, modeli her dosya için yeniden yükleme yükünden kaçınırız. Bu, ölçekli **toplu OCR** işlemlerinin en verimli yoludur.

---

## Adım 5: Temizleme – **AI Kaynaklarını Serbest Bırak** doğru şekilde

İşiniz bittiğinde `free_resources()` çağrısı GPU belleğini, CUDA bağlamlarını ve modelin oluşturduğu geçici dosyaları serbest bırakır.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

Bu adımı atlamak, GPU tahsislerinin asılı kalmasına yol açabilir; bu da sonraki Python süreçlerinin çökmesine ya da VRAM’in tükenmesine neden olur. Bunu, toplu bir işin “ışıkları kapatma” kısmı olarak düşünün.

---

## Yaygın Tuzaklar & Ek İpuçları

| Sorun | Dikkat Edilecek | Çözüm |
|-------|------------------|-----|
| **Bellek yetersizliği hataları** | GPU birkaç on resimden sonra doluyor | `gpu_layers` değerini azaltın veya CPU’ya geçin (`model_cfg.gpu_layers = 0`). |
| **Dil paketi eksik** | OCR boş string döndürüyor | `asposeocr` sürümünün İngilizce dil verisini içerdiğinden emin olun; gerekirse yeniden kurun. |
| **Resim olmayan dosyalar** | Script rastgele bir `.pdf` dosyasında çöküyor | `if not file_name.lower().endswith(...)` kontrolü zaten onları atlıyor. |
| **Yazım denetimi uygulanmadı** | Çıktı ham OCR ile aynı | Döngüden önce `ai_processor.set_post_processor` çağrısının yapıldığını doğrulayın. |
| **Yavaş toplu hız** | Görüntü başına >5 saniye sürüyor | İlk çalıştırmadan sonra `model_cfg.allow_auto_download = "false"` yaparak modelin tekrar indirilmesini engelleyin. |

**Pro ipucu:** **Görüntülerden metin çıkar** işlemini İngilizce dışındaki bir dilde yapmak istiyorsanız, sadece `ocr_engine.language` değerini uygun enum ile değiştirin (ör. `aocr.Language.French`). Aynı AI post‑işlemci hâlâ yazım denetimi uygular, ancak en iyi sonuçlar için dil‑özel bir model tercih edebilirsiniz.

---

## Özet & Sonraki Adımlar

**Toplu OCR** sürecinin tamamını ele aldık:

1. **Başlat** – İngilizce için düz‑metin OCR motoru.  
2. **Yapılandır** – AI yazım denetimi modeli ve post‑işlemci bağlaması.  
3. **Çalıştır** – Her resimde OCR yap ve AI otomatik olarak **OCR hatalarını düzelt**.  
4. **Döngü** – Klasör üzerinden **görüntülerden metin çıkar** toplu olarak.  
5. **Temizle** – İş bittiğinde **AI kaynaklarını serbest bırak**.

Bundan sonra şunları yapabilirsiniz:

- Düzeltlenmiş metni bir sonraki NLP işlem hattına (duygu analizi, varlık çıkarımı vb.) yönlendirin.  
- `ai_processor.set_post_processor(your_custom_func, {})` ile yazım denetimini özel bir özetleyiciyle değiştirin.  
- GPU birden fazla akışı kaldırabiliyorsa, `concurrent.futures.ThreadPoolExecutor` ile klasör döngüsünü paralelleştirin.

---

## Son Düşünceler

Toplu OCR bir zahmet olmak zorunda değil. Aspose OCR’u hafif bir AI modeliyle birleştirerek **görüntülerden metin çıkar**, **yazım denetimi uygula**, **OCR hatalarını düzelt** ve **AI kaynaklarını temiz** bir çözüm elde edersiniz. Betiği bir test klasöründe çalıştırın, GPU katman sayısını donanımınıza göre ayarlayın ve dakikalar içinde üretime hazır bir işlem hattına sahip olun.

Modeli özelleştirme, PDF işleme ya da bu çözümü bir web servisine entegre etme konularında sorularınız mı var? Aşağıya yorum bırakın ya da GitHub’da bana mesaj atın. İyi kodlamalar, OCR’unuz her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}