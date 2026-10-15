---
category: general
date: 2026-01-12
description: Aspose OCR ve hafif bir Hugging Face modeli kullanarak fatura görüntülerinde
  OCR çalıştırma ve metin çıkarma. Modeli indirmeyi, OCR hatalarını düzeltmeyi ve
  görüntüde OCR yapmayı öğrenin.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: tr
og_description: Fatura görüntülerinde OCR çalıştırma, metin çıkarma ve Hugging Face
  LLM ile hataları düzeltme. Kusursuz sonuçlar için bu kapsamlı rehberi izleyin.
og_title: Fatura Görüntülerinde OCR Nasıl Çalıştırılır – Tam Kılavuz
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Fatura Görüntülerinde OCR Nasıl Çalıştırılır – Tam Adım‑Adım Kılavuz
url: /tr/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fatura Görsellerinde OCR Çalıştırma – Tam Adım‑Adım Kılavuz

Hiç **OCR nasıl çalıştırılır** sorusunu taranmış bir faturada sormuş ve temiz, aranabilir metni saatler harcamadan elde etmek istemiş miydiniz? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede ham OCR çıktısı hatalarla doludur—örneğin “O” yerine “0”, “l” yerine “1” ya da hatta bütün kelimeler karışık. İyi haber? Birkaç Python satırıyla sadece **perform OCR on image** dosyalarını çalıştırmakla kalmaz, aynı zamanda Hugging Face'ten hafif bir model kullanarak **correct OCR errors** otomatik olarak düzeltebilirsiniz.

Bu öğreticide, bilmeniz gereken her şeyi adım adım göstereceğiz: bir fatura görselini yüklemek, ham metni çıkarmak, bir kuantize model indirmek ve sonucu cilalayarak aşağı akış işlemleri için hazır mükemmel bir transkripsiyon elde etmek. Sonuna geldiğinizde tek bir tekrarlanabilir betik ile **extract text from invoice** PDF'lerden veya PNG'lerden metin çıkarabileceksiniz.

## Gereksinimler & Kurulum

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.9+ | Modern sözdizimi ve tip ipuçları |
| `aspose-ocr` package | `ocr.OcrEngine` örnekte kullanılan sağlar |
| `aspose-ai` package | `AsposeAI` post‑processor'ı sağlar |
| Access to a GPU (optional) | GPU erişimi (isteğe bağlı) – LLM katmanlarını hızlandırır; aksi takdirde CPU yeterli çalışır |
| Internet connection (first run) | İnternet bağlantısı (ilk çalıştırmada) – Otomatik olarak **download Hugging Face model** gereklidir |

Gerekli kütüphaneleri şu şekilde kurabilirsiniz:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro ipucu:** LLM'yi GPU'da çalıştırmayı planlıyorsanız, CUDA desteğiyle `torch` kurun (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Ortam hazır olduğuna göre, koda geçelim.

---

## Adım 1 – OCR Motorunu Başlatma ve Fatura Görselinizi Yükleme

İlk yapmanız gereken, Aspose'un OCR motorunun bir örneğini oluşturup işlemek istediğiniz dosyaya yönlendirmektir. Bu adım, herhangi bir görselde **how to run OCR** temelini oluşturur.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Neden önemli:** `load_image` PNG, JPEG, TIFF ve hatta PDF sayfalarını kabul eder, böylece format ne olursa olsun **perform OCR on image** verisi üzerinde çalışabilirsiniz.

---

## Adım 2 – Ham Metni Yakalamak İçin Temel OCR Çalıştırma

Görsel yüklendikten sonra motor ham bir transkripsiyon üretebilir. Bu çıktı genellikle gürültülüdür, bu yüzden daha sonra bir düzeltme adımı çalıştıracağız.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Tipik ham çıktı şu şekilde görünebilir:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

“Sıfır (`0`) yerine “O” harfi gördünüz mü? İşte düzeltmeyi daha sonra yapacağımız tam bu tip hata.

---

## Adım 3 – Hafif bir LLM ile AI Post‑Processor'ı Yapılandırma

Şimdi, mütevazı donanımlarda çalışabilecek kadar küçük ama fatura dilini anlayacak kadar güçlü bir **download Hugging Face model** getiriyoruz. Örnekte Qwen 2.5 3B‑Instruct GGUF modeli kullanılıyor, `int8` olarak kuantize edilerek çok küçük bir bellek ayak izi sağlıyor.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Neden bu model?** `int8` kuantizasyonu dosyayı ~1.2 GB'ye küçültür, bu da çoğu dizüstü bilgisayarda uygulanabilir kılar. GPU katmanları çıkarımı hızlandırır, ancak kod GPU bulunmadığında sorunsuzca CPU'ya geçer.

---

## Adım 4 – Ham OCR Sonucunda LLM‑Tabanlı Düzeltme Çalıştırma

Model hazır olduğunda ham metni post‑processor'a besliyoruz. LLM, transkripsiyonu yeniden yazar, yaygın OCR hatalarını düzeltir ve sayıları normalleştirir.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Beklenen temizlenmiş çıktı:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Sıfırların tekrar “O” harfine dönüştüğünü ve “Am0unt”un artık “Amount” olduğunu görebilirsiniz. Bu, **correct OCR errors** otomatik olarak yapmanın özüdür.

---

## Adım 5 – Kaynakları Serbest Bırakma ve Temizleme

Büyük dil modelleri GPU belleğini tutabilir, bu yüzden işiniz bittiğinde kaynakları serbest bırakmak iyi bir uygulamadır.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Bir toplu işlemde çok sayıda fatura işlemek istiyorsanız, modeli yüklü tutabilir ve sadece betiğin sonunda serbest bırakabilirsiniz.

---

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `.py` dosyasına koyup çalıştırabileceğiniz tek bir betik:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Betik çalıştırıldığında önceki “AI‑corrected” bloğuna benzer bir çıktı üretmelidir. Görsel yolunu başka bir fatura veya makbuzla değiştirerek toplu olarak **extract text from invoice** dosyalarından metin çıkarabilirsiniz.

---

## Sıkça Sorulan Sorular & Kenar Durumları

### GPU'um yoksa ne olur?

`gpu_layers` parametresi isteğe bağlıdır. `0` olarak ayarlayın veya atlayın, model tamamen CPU'da çalışacaktır. Daha yavaş çıkarım bekleyin—modern bir dizüstü bilgisayarda sayfa başına yaklaşık 2–3 saniye.

### Faturalarım çok sayfalı PDF'ler. Nasıl ele alırım?

Her sayfayı ayrı bir görsele dönüştürün (ör. `pdf2image` kullanarak) ve aynı betikle sayfalar üzerinde döngü yapın. OCR motoru her görseli bağımsız işleyebilir ve LLM her metin bloğunu düzeltecektir.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Model indirme işlemi bir güvenlik duvarı arkasında başarısız oluyor mu?

Modeli Hugging Face model hub'ından manuel olarak indirin, yerel bir klasöre açın ve `hugging_face_repo_id`'yi yerel yola yönlendirin:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Düzeltmenin doğruluğu ne kadar?

Tipik İngilizce faturalarda, LLM yaygın OCR hatalarının >%95'ini düzeltir. Karmaşık el yazısı notlar hâlâ manuel inceleme gerektirebilir.

---

## Üretim Kullanımı için İpuçları & Püf Noktaları

- **Batch processing:** Adım 2‑4'ü bir fonksiyona sarın ve dosya yolu listesi verin. Modeli yeniden yüklemekten kaçınmak için aynı `AsposeAI` örneğini yeniden kullanın.
- **Logging:** `print` yerine Python'un `logging` modülünü kullanarak ham ve düzeltilmiş çıktıları denetim izleri için kaydedin.
- **Error handling:** OCR çağrısını `try/except` bloklarıyla sarın. Bir görsel başarısız olursa dosya adını kaydedin ve devam edin.
- **Performance tuning:** `gpu_layers` ile deney yapın. GPU'da daha fazla katman çıkarımı hızlandırır ancak VRAM kullanımını artırır.

---

## Sonuç

Başlangıçtan sona kadar fatura görsellerinde **how to run OCR** konusunu ele aldık, **perform OCR on image**, **download Hugging Face model** ve **correct OCR errors** otomatik olarak nasıl yapacağınızı gösterdik. Tam betik, herhangi bir Python tabanlı otomasyon hattına ekleyebileceğiniz pratik bir iş akışı sunar.

Sonraki adımlar? Düzeltmiş metin üzerinde düzenli ifadeler kullanarak **extract key fields** (fatura numarası, tarih, toplam) genişletmeyi deneyin veya temizlenmiş çıktıyı aranabilir kayıtlar için bir veritabanına gönderin. Farklı bir dil veya alan‑spesifik bilgi gerekiyorsa Hugging Face'ten başka hafif LLM'lerle de deney yapabilirsiniz.

Kodlamaktan keyif alın, ve OCR sonuçlarınız her zaman kristal‑temiz olsun! 

![fatura görüntüsünde OCR nasıl çalıştırılır](ocr_invoice_example.png "faturada OCR nasıl çalıştırılır")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}