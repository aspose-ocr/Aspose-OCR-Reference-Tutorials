---
category: general
date: 2026-01-12
description: Aspose OCR kullanarak PDF'lerde OCR çalıştırma, PDF OCR'yi yükleme, el
  yazısı OCR modunu etkinleştirme ve son işleme için bir Hugging Face OCR modelini
  entegre etme.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: tr
og_description: Aspose OCR ile PDF'lerde OCR nasıl çalıştırılır, el yazısı OCR modunu
  etkinleştirin ve Hugging Face OCR modeli kullanarak doğruluğu artırın.
og_title: PDF'lerde OCR Nasıl Çalıştırılır – Tam Kılavuz
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: PDF'lerde OCR Nasıl Çalıştırılır – El Yazısı Modu ile Adım Adım Rehber
url: /tr/python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'lerde OCR Çalıştırma – Tam Kılavuz

Hiç **OCR nasıl çalıştırılır** sorusunu, dağınık el yazması içeren çok‑dilli bir PDF üzerinde merak ettiniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—örneğin fatura dijitalleştirme ya da tarihi mektupların arşivlenmesi—düz metin çıkarımı yeterli olmuyor. Bu kılavuz, PDF'lerde OCR nasıl çalıştırılır, PDF OCR nasıl yüklenir, el yazması OCR moduna nasıl geçilir ve ardından **Hugging Face OCR modeli** ile imla ve dilbilgisi düzeltmeleri nasıl yapılır, adım adım gösteriyor.

Kurulumdan GPU hızlandırmasına, Hugging Face'ten hafif bir Qwen modelinin entegrasyonuna kadar ihtiyacınız olan her şeyi ele alacağız. Sonunda, herhangi bir Python projesine ekleyebileceğiniz hazır bir betiğe sahip olacaksınız.

> **Önkoşullar**  
> • Python 3.9 ve üzeri  
> • Aspose OCR Cloud lisansı (ortam değişkeni olarak ayarlanmalı)  
> • İsteğe bağlı: daha hızlı çıkarım için CUDA‑uyumlu bir GPU  

---

## Bu Kılavuzda Neler Ele Alınıyor

- Ortam değişkeninden Aspose OCR lisansının etkinleştirilmesi  
- `load_pdf OCR` ile PDF yükleme ve **el yazması OCR modu** etkinleştirme  
- Blok‑seviyesinde metin ve dil verisi elde etmek için yapılandırılmış OCR çalıştırma  
- Post‑işleme için **Hugging Face OCR modeli** (Qwen 2.5‑3B‑Instruct) kurulumu  
- Blok‑blok imla kontrolü ve dilbilgisi düzeltmesi uygulama  
- Bellek sızıntılarını önlemek için AI kaynaklarının temizlenmesi  

Eğer daha önce saf bir OCR motoru kullanıp el yazması notlarda anlamsız karakterler gördüyseniz, “el yazması OCR modu” bayrağı eksik olan parçayı tamamlayacak. Ayrıca Hugging Face modeli sayesinde, Python ortamınızdan çıkmadan profesyonel bir temizlik elde edeceksiniz.

---

![OCR çalıştırma diyagramı](https://example.com/ocr-workflow.png "OCR nasıl çalıştırılır")

*Görsel alt metni: OCR çalıştırma iş akışı diyagramı*

---

## Adım 1: Gerekli Paketleri Yükleyin

İlk olarak Aspose OCR Cloud SDK ve `transformers` kütüphanesinin kurulu olduğundan emin olun. Terminalinizde aşağıdakileri çalıştırın:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **İpucu:** GPU hızlandırması kullanacaksanız, CUDA desteğiyle `torch` da kurun (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

---

## Adım 2: Aspose OCR Lisansını Etkinleştirin

Lisansı ortam değişkeninden etkinleştirmek, anahtarınızın kaynak kontrolünde yer almasını önler. Kabukta `ASPOSE_OCR_LICENSE` değişkenini ayarlayın, ardından `activate_from_env()` çağrısını yapın:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> Neden önemli: Geçerli bir lisans olmadan SDK, sayfa sayısını sınırlayan ve GPU kullanımını devre dışı bırakan deneme moduna geçer.

---

## Adım 3: OCR Motorunu El Yazması Modunda Başlatın

Bir `OcrEngine` oluşturur, GPU'yu (varsa) açar ve **el yazması OCR modu** isteğinde bulunuruz. Bu mod, alttaki sinir ağını el yazması darbeleriyle daha iyi başa çıkacak şekilde ayarlar.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **Not:** GPU'nuz yoksa, `set_use_gpu(False)` hâlâ çalışır; motor CPU'ya geri döner.

---

## Adım 4: PDF'nizi Yükleyin ve Yapılandırılmış OCR Çalıştırın

Şimdi gerçek anlamda **PDF OCR** yüklemesini yapıyoruz. `load_image` metodu PDF, TIFF, JPG vb. formatları kabul eder. Yapılandırılmış OCR, ham metin ve algılanan dili içeren bloklar döndürür.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

`structured_result.blocks` listesi aşağıdaki gibi görünebilir (kısaltılmıştır):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

---

## Adım 5: Post‑İşleme İçin Hugging Face OCR Modelini Yapılandırın

Hugging Face'ten **Qwen 2.5‑3B‑Instruct** modelini, düşük bellek ayak izi için `int8` kuantize edilmiş olarak kullanacağız. `AsposeAIModelConfig` sarmalayıcısı, Aspose AI post‑işlemcisine modeli nasıl indireceğini ve çalıştıracağını söyler.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **Bu model neden?** Qwen 2.5‑3B‑Instruct hız ve kalite arasında iyi bir denge kurar. `int8` kuantizasyonu RAM kullanımını ~4 GB'a düşürür, bu da çoğu modern dizüstü bilgisayarda uygulanabilir kılar.

---

## Adım 6: Blok‑Blok İmla Kontrolü Uygulayın

Her OCR bloğunu döngüyle işler, AI post‑işlemcisine verir ve düzeltilmiş metni algılanan diliyle birlikte yazdırırız. Bu, **PDF OCR yükle → post‑işlem** hattının çekirdeğidir.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### Beklenen Çıktı

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

Orijinal OCR'da “Helllo wrold” gibi hatalar varsa, model düzeltilmiş versiyonu verir.

---

## Adım 7: AI Kaynaklarını Temizleyin

İşiniz bittiğinde GPU belleğini serbest bırakmayı unutmayın. `free_resources()` çağrısı modeli kaldırır ve CUDA önbelleğini temizler.

```python
spell_corrector.free_resources()
```

---

## Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Belirti | Çözüm |
|-------|----------|-----|
| **GPU algılanmıyor** | `set_use_gpu(True)` sessizce CPU'ya geçiyor | CUDA sürücülerini (`nvidia-smi`) kontrol edin ve doğru `torch` tekerleğini kurun |
| **Model indirme başarısız** | `allow_auto_download` ağ hatası veriyor | Çıkış HTTPS izinlerini kontrol edin ya da GGUF dosyasını manuel indirip `hugging_face_repo_id`'yi yerel yola yönlendirin |
| **El yazması hâlâ bozuk** | `structured_result` içinde düşük güven skorları | `set_recognition_mode`'u `HANDWRITTEN` (zaten yapılmış) artırın ve OCR öncesi PDF'yi `opencv` ile keskinleştirme gibi ön‑işlemeyi düşünün |
| **GPU'da bellek yetersizliği** | `RuntimeError: CUDA out of memory` | `gpu_layers` sayısını azaltın (ör. 'a) ya da CPU çıkarımına geçin (`set_use_gpu(False)`) |

---

## İş Akışını Genişletmek

- **Toplu işleme:** Tüm betiği, PDF yolları listesi kabul eden ve düzeltilmiş çıktıyı ayrı `.txt` dosyalarına yazan bir fonksiyon içinde paketleyin.  
- **Özel sözlükler:** Alanınızda (ör. tıbbi kısaltmalar) özel terminoloji varsa, Hugging Face modelini küçük bir veri kümesiyle ince ayar yapın.  
- **Alternatif modeller:** Daha geniş bir bağlam penceresine ihtiyacınız varsa `Qwen/Qwen2.5-3B-Instruct-GGUF` yerine `mistralai/Mistral-7B-Instruct-v0.2` kullanın.

---

## Sonuç

Artık **PDF'lerde OCR nasıl çalıştırılır**, PDF OCR nasıl yüklenir, **el yazması OCR modu** nasıl etkinleştirilir ve **Hugging Face OCR modeli** ile doğruluk nasıl artırılır, biliyorsunuz. Tam betik—lisans aktivasyonu, GPU‑destekli motor, yapılandırılmış OCR, AI post‑işleme ve temizlik—geliştiricilerin sıkça sorduğu tüm adımları kapsıyor; “GPU'm yoksa ne olur?” sorusundan “kaynakları nasıl serbest bırakırım?” sorusuna kadar.

Kendi belgelerinizle deneyin, farklı modellerle oynayın ya da bu hattı daha büyük bir belge‑işleme servisine entegre edin. Aspose OCR ve Hugging Face AI kombinasyonunu ustalaştıktan sonra sınır yok.

---

**Sonraki Adımlar**

- Aynı iş akışını taranmış görüntüler (`.png`, `.jpg`) üzerinde deneyerek motorun nasıl uyum sağladığını görün.  
- Tablo çıkarımı için Aspose OCR **düzen analizi** özelliklerini keşfedin.  
- Model boyutunu daha da küçültmek için Hugging Face kuantizasyon tekniklerine derinlemesine bakın.

Mutlu OCR kodlamaları!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}