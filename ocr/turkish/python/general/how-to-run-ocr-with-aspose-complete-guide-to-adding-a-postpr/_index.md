---
category: general
date: 2026-02-22
description: Aspose kullanarak görüntülerde OCR çalıştırmayı ve AI destekli sonuçlar
  için post‑işlemci eklemeyi öğrenin. Adım adım Python öğreticisi.
draft: false
keywords:
- how to run OCR
- how to add postprocessor
language: tr
og_description: Aspose ile OCR nasıl çalıştırılır ve daha temiz metin için post‑işlemci
  nasıl eklenir keşfedin. Tam kod örneği ve pratik ipuçları.
og_title: Aspose ile OCR Nasıl Çalıştırılır – Python’da Postprocessor Ekleme
tags:
- Aspose OCR
- Python
- AI post‑processing
title: Aspose ile OCR Nasıl Çalıştırılır – Post İşlemci Eklemeye Tam Kılavuz
url: /tr/python/general/how-to-run-ocr-with-aspose-complete-guide-to-adding-a-postpr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose ile OCR Çalıştırma – Postprocessör Eklemeye Dair Tam Kılavuz

Hiç **OCR'ı** bir fotoğraf üzerinde, onlarca kütüphaneyle uğraşmadan çalıştırmayı merak ettiniz mi? Tek başınıza değilsiniz. Bu öğreticide, OCR çalıştırmanın yanı sıra Aspose’un AI modeli kullanarak **postprocessör eklemenin** nasıl yapılacağını gösteren bir Python çözümünü adım adım inceleyeceğiz.  

SDK’yı kurmaktan kaynakları serbest bırakmaya kadar her şeyi ele alacağız, böylece çalışan bir betiği kopyalayıp yapıştırabilir ve birkaç saniye içinde düzeltilmiş metni görebilirsiniz. Gizli adımlar yok, sadece sade İngilizce açıklamalar ve tam kod listesi.

## Gereksinimler

İşe başlamadan önce çalışma istasyonunuzda aşağıdakilerin olduğundan emin olun:

| Gereklilik | Neden Önemli |
|------------|--------------|
| Python 3.8+ | `clr` köprüsü ve Aspose paketleri için gerekli |
| `pythonnet` (pip install pythonnet) | Python’dan .NET etkileşimini sağlar |
| Aspose.OCR for .NET (Aspose’tan indirin) | Çekirdek OCR motoru |
| İnternet erişimi (ilk çalıştırmada) | AI modelinin otomatik indirilmesini sağlar |
| Örnek bir görüntü (`sample.jpg`) | OCR motoruna besleyeceğimiz dosya |

Eğer bunlardan biri size yabancı geliyorsa endişelenmeyin—kurulumu çok kolay ve daha sonra ana adımlara değineceğiz.

## Adım 1: Aspose OCR’ı Kurun ve .NET Köprüsünü Ayarlayın  

**OCR çalıştırmak** için Aspose OCR DLL’lerine ve `pythonnet` köprüsüne ihtiyacınız var. Aşağıdaki komutları terminalinizde çalıştırın:

```bash
pip install pythonnet
# Download the Aspose.OCR for .NET zip from https://downloads.aspose.com/ocr/python-net
# Unzip it and note the folder path, e.g., C:\Aspose\OCR\Net
```

DLL’ler diske yerleştirildikten sonra, Python’un onları bulabilmesi için klasörü CLR yoluna ekleyin:

```python
import sys, os, clr

# Adjust this path to where you extracted the Aspose OCR binaries
aspose_path = r"C:\Aspose\OCR\Net"
sys.path.append(aspose_path)

# Load the main assembly
clr.AddReference("Aspose.OCR")
clr.AddReference("Aspose.OCR.AI")
```

> **İpucu:** `BadImageFormatException` alırsanız, Python yorumlayıcınızın DLL mimarisiyle (her ikisi de 64‑bit ya da 32‑bit) eşleştiğini doğrulayın.

## Adım 2: Ad Alanlarını İçe Aktarın ve Görüntünüzü Yükleyin  

Şimdi OCR sınıflarını kapsam içine alabilir ve motoru bir görüntü dosyasına yönlendirebiliriz:

```python
import System
import aspose.ocr as ocr
import aspose.ocr.ai as ocr_ai
import System.Drawing

# Create the OCR engine instance
ocr_engine = ocr.OcrEngine()

# Load the image you want to process
image_path = r"YOUR_DIRECTORY/sample.jpg"
ocr_engine.set_image(System.Drawing.Image.FromFile(image_path))
```

`set_image` çağrısı, GDI+ tarafından desteklenen herhangi bir formatı kabul eder; PNG, BMP veya TIFF, JPG kadar sorunsuz çalışır.

## Adım 3: Post‑Processing İçin Aspose AI Modelini Yapılandırın  

İşte **postprocessör eklemenin** nasıl yapılacağını gösteren kısım. AI modeli bir Hugging Face deposunda bulunur ve ilk kullanımda otomatik olarak indirilir. Birkaç mantıklı varsayımla yapılandıralım:

```python
# A silent logger – Aspose AI expects a callable, we give it a no‑op lambda
logger = lambda msg: None

# Initialise the AI processor
ai_processor = ocr_ai.AsposeAI(logger)

# Build the model configuration
model_cfg = ocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_cfg.hugging_face_quantization = "int8"
model_cfg.gpu_layers = 20          # Use GPU if available; otherwise falls back to CPU
model_cfg.context_size = 2048

# Apply the configuration
ai_processor.initialize(model_cfg)
```

> **Neden Önemli:** AI post‑processörü, büyük bir dil modeli kullanarak yaygın OCR hatalarını (ör. “1” ile “l”, eksik boşluklar) temizler. `gpu_layers` ayarı, modern GPU’larda çıkarımı hızlandırır ancak zorunlu değildir.

## Adım 4: Post‑Processor’ı OCR Motoruna Bağlayın  

AI modeli hazır olduğunda, onu OCR motoruna bağlarız. `add_post_processor` metodu, ham OCR sonucunu alıp düzeltilmiş bir versiyon döndüren bir çağrılabilir (callable) bekler.

```python
# Hook the AI post‑processor into the OCR pipeline
ocr_engine.add_post_processor(lambda result: ai_processor.run_postprocessor(result))
```

Bu noktadan itibaren, `recognize()` her çağrısı ham metni otomatik olarak AI modeline gönderir.

## Adım 5: OCR’ı Çalıştırın ve Düzeltlenmiş Metni Alın  

Şimdi gerçek an—**OCR’ı çalıştıralım** ve AI‑geliştirilmiş çıktıyı görelim:

```python
# Perform recognition
ocr_result = ocr_engine.recognize()

# The .text property holds the corrected string
print("Corrected text:", ocr_result.text)
```

Tipik bir çıktı şu şekildedir:

```
Corrected text: The quick brown fox jumps over the lazy dog.
```

Orijinal görüntüde gürültü veya alışılmadık fontlar varsa, AI modelinin ham motorun kaçırdığı bozuk kelimeleri düzelttiğini göreceksiniz.

## Adım 6: Kaynakları Temizleyin  

Hem OCR motoru hem de AI işlemcisi yönetilmeyen kaynaklar tahsis eder. Bunları serbest bırakmak, özellikle uzun‑çalışan servislerde bellek sızıntılarını önler:

```python
# Release the AI model first
ai_processor.free_resources()

# Then dispose of the OCR engine
ocr_engine.dispose()
```

> **Köşe Durumu:** OCR’ı bir döngü içinde tekrar tekrar çalıştıracaksanız, motoru canlı tutun ve sadece işiniz bittiğinde `free_resources()` çağırın. AI modelini her yinelemede yeniden başlatmak belirgin bir ek yük getirir.

## Tam Betik – Tek‑Tıkla Hazır  

Aşağıda, yukarıdaki tüm adımları içeren eksiksiz, çalıştırılabilir program yer alıyor. `YOUR_DIRECTORY` kısmını `sample.jpg` dosyasının bulunduğu klasörle değiştirin.

```python
# ------------------------------------------------------------
# How to Run OCR with Aspose and How to Add Postprocessor
# ------------------------------------------------------------
import sys, clr, System, os
import aspose.ocr as ocr
import aspose.ocr.ai as ocr_ai
import System.Drawing

# ----------------------------------------------------------------
# 1️⃣  Set up CLR paths – adjust to your local Aspose folder
# ----------------------------------------------------------------
aspose_path = r"C:\Aspose\OCR\Net"   # <--- change this!
sys.path.append(aspose_path)
clr.AddReference("Aspose.OCR")
clr.AddReference("Aspose.OCR.AI")

# ----------------------------------------------------------------
# 2️⃣  Create OCR engine and load image
# ----------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
image_file = r"YOUR_DIRECTORY/sample.jpg"   # <--- your image here
ocr_engine.set_image(System.Drawing.Image.FromFile(image_file))

# ----------------------------------------------------------------
# 3️⃣  Initialise the AI post‑processor
# ----------------------------------------------------------------
logger = lambda msg: None                # silent logger
ai_processor = ocr_ai.AsposeAI(logger)

model_cfg = ocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_cfg.hugging_face_quantization = "int8"
model_cfg.gpu_layers = 20
model_cfg.context_size = 2048
ai_processor.initialize(model_cfg)

# ----------------------------------------------------------------
# 4️⃣  Hook the AI processor into the OCR pipeline
# ----------------------------------------------------------------
ocr_engine.add_post_processor(lambda result: ai_processor.run_postprocessor(result))

# ----------------------------------------------------------------
# 5️⃣  Run OCR and print corrected text
# ----------------------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Corrected text:", ocr_result.text)

# ----------------------------------------------------------------
# 6️⃣  Release resources
# ----------------------------------------------------------------
ai_processor.free_resources()
ocr_engine.dispose()
```

Betik dosyasını `python ocr_with_postprocess.py` ile çalıştırın. Her şey doğru kurulduysa, konsolda sadece birkaç saniye içinde düzeltilmiş metni göreceksiniz.

## Sık Sorulan Sorular (SSS)

**S: Bu Linux’ta çalışır mı?**  
C: Evet, .NET runtime’ı ( `dotnet` SDK ) kurulu olduğu sürece ve Linux için uygun Aspose ikili dosyaları bulunduğu sürece çalışır. Yol ayırıcılarını (`/` yerine `\`) ayarlamanız ve `pythonnet`’in aynı runtime’a karşı derlenmiş olması gerekir.

**S: GPU’m yoksa ne yapmalıyım?**  
C: `model_cfg.gpu_layers = 0` olarak ayarlayın. Model CPU’da çalışır; çıkarım daha yavaş olur ama yine de işlevsel.

**S: Hugging Face deposunu başka bir modelle değiştirebilir miyim?**  
C: Kesinlikle. `model_cfg.hugging_face_repo_id` değerini istediğiniz repo ID’siyle değiştirin ve gerekirse `quantization` ayarını güncelleyin.

**S: Çok sayfalı PDF’lerle nasıl başa çıkılır?**  
C: Her sayfayı bir görüntüye dönüştürün (ör. `pdf2image` kullanarak) ve aynı `ocr_engine` üzerinden sırayla besleyin. AI post‑processörü görüntü bazında çalışır, böylece her sayfa için temizlenmiş metin elde edersiniz.

## Sonuç  

Bu rehberde **OCR’ı** Aspose’un .NET motoru üzerinden Python ile nasıl çalıştıracağınızı ve **postprocessör ekleyerek** çıktıyı otomatik olarak nasıl temizleyeceğinizi gösterdik. Tam betik kopyala‑yapıştır ve çalıştır hazır—gizli adım yok, ilk model indirmesi dışındaki ekstra indirme de yok.  

Buradan ilerleyerek:

- Düzeltlenmiş metni bir sonraki NLP boru hattına besleyebilirsiniz.
- Alan‑spesifik sözlükler için farklı Hugging Face modelleri deneyebilirsiniz.
- Binlerce görüntünün toplu işlenmesi için bir kuyruk sistemiyle çözümü ölçeklendirebilirsiniz.

Deneyin, parametreleri ayarlayın ve AI’nın OCR projelerinizdeki ağır işi üstlenmesine izin verin. İyi kodlamalar!  

![Diagram illustrating the OCR engine feeding an image, then passing raw results to the AI post‑processor, finally outputting corrected text – how to run OCR with Aspose and post‑process](https://example.com/ocr-postprocess-diagram.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}