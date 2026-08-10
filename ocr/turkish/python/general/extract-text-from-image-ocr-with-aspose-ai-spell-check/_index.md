---
category: general
date: 2026-05-03
description: Aspose OCR ve AI imla kontrolü kullanarak görüntüden metin çıkarın. Görüntüyü
  OCR ile nasıl işleyebileceğinizi, OCR için görüntüyü nasıl yükleyeceğinizi, faturadan
  metni nasıl tanıyacağınızı ve GPU kaynaklarını nasıl serbest bırakacağınızı öğrenin.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: tr
og_description: Aspose OCR ve AI imla kontrolü ile görüntüden metin çıkarın. Görüntüyü
  OCR'lamak, OCR için görüntüyü yüklemek ve GPU kaynaklarını serbest bırakmak hakkında
  adım adım rehber.
og_title: Resimden metin çıkarma – Tam OCR ve Yazım Denetimi Rehberi
tags:
- OCR
- Aspose
- AI
- Python
title: görüntüden metin çıkarma – Aspose AI Yazım Denetimi ile OCR
url: /tr/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin çıkarma – Tam OCR ve Yazım‑Denetimi Rehberi

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz ama hangi kütüphanenin hem hız hem de doğruluk sağlayacağını bilmiyor muydunuz? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—fatura işleme, makbuz dijitalleştirme veya sözleşme tarama gibi—bir resimden temiz, aranabilir metin elde etmek ilk engeldir.

İyi haber şu ki Aspose OCR, hafif bir Aspose AI modeliyle birleştirildiğinde bu işi birkaç Python satırıyla halledebilir. Bu öğreticide **görüntüyü OCR nasıl yapılır** konusunu adım adım inceleyecek, resmi doğru şekilde yükleyecek, yerleşik bir yazım denetimi sonrası işleyiciyi çalıştıracak ve sonunda **GPU kaynaklarını serbest bırakacağız** böylece uygulamanız bellek dostu kalır.

Bu rehberin sonunda **fatura** görüntülerinden metin tanıyabilecek, yaygın OCR hatalarını otomatik olarak düzeltebilecek ve bir sonraki toplu işlem için GPU'nuzu temiz tutabileceksiniz.

---

## Gereksinimler

- Python 3.9 ve üzeri (kod tip ipuçları kullanıyor ancak daha eski 3.x sürümlerinde de çalışır)
- `aspose-ocr` ve `aspose-ai` paketleri (kurulum için `pip install aspose-ocr aspose-ai` komutunu kullanın)
- CUDA‑destekli bir GPU isteğe bağlıdır; script GPU bulunamazsa CPU'ya geçer.
- Örnek bir görüntü, örn. `sample_invoice.png`, referans alabileceğiniz bir klasöre yerleştirilmiş.

Ağır ML çerçeveleri yok, büyük model indirmeleri yok—sadece çoğu GPU'ya rahatça sığan küçük bir Q4‑K‑M kuantize modeli.

---

## Adım 1: OCR Motorunu Başlatma – görüntüden metin çıkarma

İlk olarak bir `OcrEngine` örneği oluşturur ve hangi dili beklediğinizi belirtirsiniz. Burada İngilizce'yi seçiyoruz ve düz‑metin çıktısı istiyoruz; bu, sonraki işlemler için idealdir.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Neden önemli?**: Dili ayarlamak karakter kümesini daraltır, doğruluğu artırır. Düz‑metin modu, genellikle sadece görüntüden metin çıkarmak istediğinizde ihtiyacınız olmayan düzen bilgilerini kaldırır.

---

## Adım 2: OCR için Görüntüyü Yükleme – görüntüyü OCR nasıl yapılır

Şimdi motora gerçek bir resim veriyoruz. `Image.load` yardımcı fonksiyonu yaygın formatları (PNG, JPEG, TIFF) anlar ve dosya‑IO inceliklerini soyutlar.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**İpucu:** Kaynak görüntüleriniz büyükse, motora göndermeden önce yeniden boyutlandırmayı düşünün; daha küçük boyutlar tanıma kalitesini etkilemeden GPU bellek kullanımını azaltabilir.

---

## Adım 3: Aspose AI Modelini Yapılandırma – faturadan metin tanıma

Aspose AI, otomatik olarak indirebileceğiniz küçük bir GGUF modeliyle gelir. Örnek, `Qwen2.5‑3B‑Instruct‑GGUF` deposunu `q4_k_m` olarak kuantize edilmiş şekilde kullanır. Ayrıca çalışma zamanına GPU'da 20 katman ayırmasını söylüyoruz; bu, hız ve VRAM kullanımını dengeler.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Arka planda:** Kuantize model yaklaşık 1.5 GB disk alanı kaplar, tam hassasiyetli bir modelin bir kısmıdır, ancak yine de tipik OCR yazım hatalarını işaretleyecek kadar dil nüansını yakalar.

---

## Adım 4: AsposeAI'yi Başlatma ve Yazım‑Denetimi Son İşlemcisini Eklemek

Aspose AI, hazır bir yazım‑denetimi son işlemci içerir. Bunu ekleyerek, her OCR sonucu otomatik olarak temizlenir.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Neden son işlemci kullanmalı?** OCR motorları sık sık “Invoice” kelimesini “Invo1ce”, “Total” kelimesini “T0tal” gibi okur. Yazım‑denetimi, ham dize üzerinde hafif bir dil modeli çalıştırarak bu hataları, özel bir sözlük yazmadan düzeltir.

---

## Adım 5: OCR Sonucunda Yazım‑Denetimi Son İşlemcisini Çalıştırma

Her şey bağlandıktan sonra, tek bir çağrı düzeltilmiş metni verir. Ayrıca orijinal ve temizlenmiş sürümleri de yazdırıyoruz, böylece iyileşmeyi görebilirsiniz.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Bir fatura için tipik çıktı şöyle görünebilir:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

“Invo1ce” kelimesinin doğru “Invoice” kelimesine dönüştüğüne dikkat edin. Bu, yerleşik AI yazım‑denetiminin gücüdür.

---

## Adım 6: GPU Kaynaklarını Serbest Bırakma – GPU kaynaklarını güvenli bir şekilde serbest bırakma

Bunu uzun ömürlü bir hizmette (örneğin, dakikada onlarca fatura işleyen bir web API) çalıştırıyorsanız, her toplu işlemden sonra GPU bağlamını serbest bırakmalısınız. Aksi takdirde bellek sızıntıları görür ve sonunda “CUDA out of memory” hataları alırsınız.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Pro ipucu:** `free_resources()` fonksiyonunu bir `finally` bloğu içinde veya bir bağlam yöneticisiyle çağırın; böylece bir istisna oluşsa bile her zaman çalışır.

---

## Tam Çalışan Örnek

Tüm parçaları bir araya getirdiğinizde, herhangi bir projeye ekleyebileceğiniz bağımsız bir script elde edersiniz.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Dosyayı kaydedin, görüntü yolunu ayarlayın ve `python extract_text_from_image.py` komutunu çalıştırın. Temizlenmiş fatura metninin konsola yazdırıldığını görmelisiniz.

---

## Sıkça Sorulan Sorular (SSS)

**S: Bu sadece CPU'lu makinelerde çalışır mı?**  
C: Kesinlikle. GPU algılanmazsa, Aspose AI CPU çalıştırmaya geçer, ancak daha yavaş olur. `model_cfg.gpu_layers = 0` ayarlayarak CPU'yu zorlayabilirsiniz.

**S: Faturalarım İngilizce dışındaki bir dilde olursa ne olur?**  
C: `ocr_engine.language` değerini uygun enum değeriyle değiştirin (örneğin, `aocr.Language.Spanish`). Yazım‑denetimi modeli çok dilli, ancak dil‑özel bir modelle daha iyi sonuçlar alabilirsiniz.

**S: Bir döngüde birden fazla görüntüyü işleyebilir miyim?**  
C: Evet. Yükleme, tanıma ve son‑işlem adımlarını bir `for` döngüsü içine taşıyın. Aynı AI örneğini yeniden kullanıyorsanız, döngüden sonra veya her toplu işlemden sonra `ocr_ai.free_resources()` çağırmayı unutmayın.

**S: Model indirmesi ne kadar büyük?**  
C: Kuantize `q4_k_m` versiyonu yaklaşık 1.5 GB. İlk çalıştırmadan sonra önbelleğe alınır, böylece sonraki çalıştırmalar anında gerçekleşir.

---

## Sonuç

Bu öğreticide Aspose OCR kullanarak **görüntüden metin çıkarma**, küçük bir AI modeli yapılandırma, yazım‑denetimi son işlemcisini uygulama ve güvenli bir şekilde **GPU kaynaklarını serbest bırakma** nasıl yapılır gösterdik. İş akışı, resmi yüklemekten temizlik yapmaya kadar her şeyi kapsar ve **faturadan metin tanıma** senaryoları için güvenilir bir boru hattı sunar.

Sonraki adımlar? Yazım‑denetimini özel bir varlık‑çıkarma modeliyle değiştirmeyi deneyin

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}