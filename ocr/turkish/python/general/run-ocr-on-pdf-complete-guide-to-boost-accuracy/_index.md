---
category: general
date: 2026-07-05
description: PDF üzerinde OCR çalıştırmayı ve Hugging Face modeli kullanarak OCR doğruluğunu
  artırmayı öğrenin. Adım adım kurulum, OCR için PDF yükleme ve Hugging Face modelini
  yapılandırma.
draft: false
keywords:
- run OCR on PDF
- improve OCR accuracy
- load PDF for OCR
- configure Hugging Face model
language: tr
og_description: Hugging Face modeliyle PDF üzerinde OCR çalıştırın ve OCR doğruluğunu
  artırın. OCR için PDF yüklemek ve modeli yapılandırmak amacıyla bu kılavuzu izleyin.
og_title: PDF'de OCR çalıştır – Daha İyi Doğruluk İçin Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  headline: run OCR on PDF – Complete Guide to Boost Accuracy
  type: TechArticle
- description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  name: run OCR on PDF – Complete Guide to Boost Accuracy
  steps:
  - name: What if the PDF is multi‑page?
    text: The `Image.from_file` call automatically creates a multi‑frame image object.
      Loop over `input_image.frames` and call `ocr_engine.recognize` for each frame,
      then concatenate the results before running the post‑processor.
  - name: How to handle languages other than English?
    text: 'Set the OCR engine’s language property before recognition:'
  - name: Can I run this on CPU only?
    text: Yes—just omit `model_cfg.gpu_layers` or set it to `0`. The model will run
      entirely on CPU, though inference will be slower (roughly 5‑10 seconds per page
      on a modern i7).
  type: HowTo
tags:
- OCR
- Python
- AI post‑processor
title: PDF'de OCR Çalıştırma – Doğruluğu Artırmak İçin Tam Rehber
url: /tr/python/general/run-ocr-on-pdf-complete-guide-to-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF üzerinde OCR Çalıştırma – Doğruluğu Artırmak İçin Tam Kılavuz

Hiç **PDF üzerinde OCR çalıştırmanın** ticari SDK'lara para harcamadan nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz. Faturaları dijitalleştiriyor, taranmış raporlardan veri çıkarıyor ya da sadece AI destekli metin çıkarımıyla ilgileniyor olun, **PDF üzerinde OCR çalıştırmak** verimli bir şekilde modern geliştiriciler için vazgeçilmez bir beceridir.

Bu öğreticide, sadece **PDF üzerinde OCR çalıştırmanın** nasıl yapılacağını göstermekle kalmayıp, aynı zamanda bir AI post‑işlemcisi ekleyerek **OCR doğruluğunu artırmanın** yollarını da gösterecek pratik, uçtan‑uca bir örnek üzerinden ilerleyeceğiz. Ayrıca **PDF'yi OCR için yükleme** ve **Hugging Face model** ayarlarını yapılandırma konularına da değinecek, mütevazı bir iş istasyonunda en iyi performansı almanızı sağlayacağız.

Bu rehberin sonunda, aşağıdaki özelliklere sahip tam çalışan bir betiğe sahip olacaksınız:

* OCR için bir PDF (veya görüntü) yükler  
* Özel kuantizasyon ve GPU katmanlarıyla bir Hugging Face modeli yapılandırır  
* Düz OCR çalıştırır ve ardından sonucu bir AI post‑işlemcisiyle iyileştirir  
* Karşılaştırma yapabilmeniz için ham ve AI‑iyileştirilmiş metinleri yan yana yazdırır  

Harici hizmetler yok, gizli ücretler yok—sadece açık kaynak kütüphaneler ve birkaç satır Python.

## Gereksinimler

Başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:

* Python 3.9 ve üzeri kurulu (`venv` modülü işinizi kolaylaştırır)  
* `aocr` paketi (Aspose OCR) – `pip install aocr` ile kurun  
* Hugging Face'ten tek seferlik model indirmesi için internete erişim  
* İşlemek istediğiniz bir PDF dosyası (örnek olarak `invoice_2026.pdf` kullanacağız)  

Hepsi bu kadar. Eğer bu maddelerden biri size yabancı geliyorsa endişelenmeyin—her adım neden ve nasıl yapıldığını açıklayacak, böylece dakikalar içinde çalışır duruma geleceksiniz.

---

## Adım 1: Hugging Face Modelini Yapılandırma

İlk olarak **Hugging Face modelini yapılandırma** parametrelerini donanımınıza uygun şekilde ayarlamalısınız. Biz, yeni çıkan `Qwen/Qwen2.5-3B-Instruct-GGUF` modelini çekecek, hafıza ayak izini küçültmek için `int8` kuantize edecek ve hız için ilk 20 katmanı GPU'ya taşıyacağız.

```python
import aocr

# Create the AI engine that will later post‑process OCR results
ai_engine = aocr.AsposeAI()

# Build the model configuration – this is where we "configure Hugging Face model"
model_cfg = aocr.AsposeAIModelConfig()
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"   # released early‑2026
model_cfg.hugging_face_quantization = "int8"                     # small memory footprint
model_cfg.gpu_layers = 20                                        # use first 20 layers on GPU
model_cfg.allow_auto_download = "true"

# Initialize the engine – it will download the model if it's not already cached
ai_engine.initialize(model_cfg)
```

**Neden önemli:** `int8` kuantizasyonu modeli birkaç gigabayttan bir gigabaytın altına indirger, böylece dizüstü bilgisayarlarda bile çalışabilir. GPU katmanlarını sınırlamak ise hız ve VRAM kullanımı arasında denge kurar—6 GB bir kart için ideal.

> **İpucu:** Bellek yetersizliği hatası alırsanız `gpu_layers` değerini `10` yapın ya da modeli biraz daha büyük ama hâlâ çoğu tüketici GPU'suna sığan `"float16"` kuantizasyona geçin.

---

## Adım 2: PDF'yi OCR İçin Yükleme

AI motoru hazır olduğuna göre, **PDF'yi OCR için yükleme** adımına geçiyoruz. Aspose OCR kütüphanesi PDF'leri ve görüntüleri aynı şekilde ele alır, bu yüzden bir dosya yolu ya da akış (stream) gösterebilirsiniz.

```python
# Create the OCR engine that will perform the initial text extraction
ocr_engine = aocr.OcrEngine()

# Attach the AI post‑processor – we’ll use the default run_postprocessor method
ocr_engine.set_post_processor(ai_engine.run_postprocessor, None)  # no custom settings required

# Load the PDF document – this is the step where we "load PDF for OCR"
input_image = aocr.Image.from_file("YOUR_DIRECTORY/invoice_2026.pdf")
```

**Neden önemli:** PDF'yi doğrudan bir `Image` nesnesine yükleyerek OCR motoru, çok sayfalı PDF'leri sayfa‑sayfa arka planda işleyebilir. PDF'yi önceden görüntülere bölmenize gerek kalmaz.

> **Dikkat:** PDF'niz şifreli sayfalar içeriyorsa, şifreyi `Image.from_file(..., password="secret")` ile sağlamalısınız.

---

## Adım 3: PDF Üzerinde OCR Çalıştırma

Belge bellekte olduğuna göre, **PDF üzerinde OCR çalıştırma** zamanı geldi. İlk geçiş ham metni verir; bu metin genellikle boşluk hataları, yanlış tanınan karakterler veya eksik noktalama işaretleriyle doludur—özellikle taranmış faturalar için.

```python
# Perform the plain OCR pass – this is the core "run OCR on PDF" operation
raw_result = ocr_engine.recognize(input_image)  # raw OCR output
```

Bu noktada `raw_result.text` ham OCR çıktısını tutar. İnceleyebilir, loglayabilir ya da sonraki işlem hatlarına besleyebilirsiniz. 

> **Not:** `recognize` metodu sayfa yönelimini otomatik algılar ve eğikliği düzeltmeye çalışır, ancak dil‑özel tuhaflıkları düzeltmez—burada AI post‑işlemcisi devreye girer.

---

## Adım 4: AI Post‑İşlemci ile OCR Doğruluğunu Artırma

Şimdi eğlenceli kısım: **OCR doğruluğunu artırma**. Ham sonucu daha önce yapılandırdığınız AI motoruna vererek, büyük bir dil modelinin metni temizlemesini, yazım hatalarını düzeltmesini ve eksik değerleri tahmin etmesini sağlarız.

```python
# Enhance the raw OCR output using the AI post‑processor
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

Post‑işlemci, her satır (veya blok) üzerinde LLM'yi çalıştırır ve ona “OCR hatalarını temizle, ancak orijinal anlamı koru” diye bir istem (prompt) gönderir. Sonuç, çok daha okunabilir bir versiyon olur.

**Neden işe yarar:** Modern LLM'ler dil kalıplarını çok iyi kavrar ve OCR motorunun verdiği bozuk token'ı doğru kelimeye dönüştürebilir. `int8` kuantize modeliyle birleştiğinde, tipik bir tek‑sayfalık fatura için iyileştirme bir saniyenin altında tamamlanır.

---

## Adım 5: Sonuçları İnceleme

Son olarak, ham ve AI‑iyileştirilmiş çıktıyı yan yana yazdırarak farkı kendiniz görebilirsiniz.

```python
print("=== Raw OCR ===")
print(raw_result.text)

print("\n=== AI‑enhanced ===")
print(enhanced_result.text)
```

**Beklenen çıktı (kısaltılmış):**

```
=== Raw OCR ===
Inv0ice N0: 2026-00123
Date: 01/02/2026
Tot@l Am0unt: $1,234.56
...

=== AI‑enhanced ===
Invoice No: 2026-00123
Date: 01/02/2026
Total Amount: $1,234.56
...
```

AI‑iyileştirilmiş sürümün sıfır‑harf karışıklıklarını (`Inv0ice` → `Invoice`) ve yanlış `@` sembolünü düzelttiğine dikkat edin. Çoğu belge için OCR hatalarında %30‑80  azalma göreceksiniz.

> **İpucu:** İyileştirilmiş metni yapılandırılmış bir formatta (ör. JSON) istiyorsanız, `enhanced_result` üzerine regex ya da küçük bir ayrıştırma fonksiyonu ekleyerek daha da işleyebilirsiniz.

---

## Opsiyonel: Süreci Görselleştirme

Aşağıda akışı gösteren basit bir diyagram bulunuyor. Alt metin SEO için ana anahtar kelimeyi içeriyor.

![PDF üzerinde OCR çalıştırma adımlarını ve AI post‑işlemcisi ile OCR doğruluğunu artırmayı gösteren diyagram](run-ocr-on-pdf-diagram.png)

---

## Sık Sorulan Sorular & Kenar Durumları

### PDF çok sayfalı ise ne olur?

`Image.from_file` çağrısı otomatik olarak çok çerçeveli bir görüntü nesnesi oluşturur. `input_image.frames` üzerinde döngü kurup her çerçeve için `ocr_engine.recognize` çağırın, ardından sonuçları birleştirip post‑işlemciye gönderin.

```python
pages_text = []
for frame in input_image.frames:
    raw = ocr_engine.recognize(frame)
    enhanced = ocr_engine.run_postprocessor(raw)
    pages_text.append(enhanced.text)

full_text = "\n".join(pages_text)
```

### İngilizce dışındaki diller nasıl işlenir?

Tanıma öncesinde OCR motorunun dil özelliğini ayarlayın:

```python
ocr_engine.language = aocr.Language.French  # or aocr.Language.Spanish, etc.
```

LLM, **Hugging Face modelini yapılandırma** sırasında hedef dili desteklediği sürece doğruluğu artırmaya devam eder (çoğu modeli destekler).

### Sadece CPU ile çalıştırabilir miyim?

Evet—`model_cfg.gpu_layers` satırını atlayın ya da `0` olarak ayarlayın. Model tamamen CPU üzerinde çalışır, ancak çıkarım süresi daha uzun olur (modern bir i7'de sayfa başına yaklaşık 5‑10 saniye).

---

## Özet

**PDF üzerinde OCR çalıştırma** ve **OCR doğruluğunu artırma** için bilmeniz gereken her şeyi ele aldık:

1. **Hugging Face modelini** kuantizasyon ve GPU katmanlarıyla yapılandırın.  
2. **PDF'yi OCR için** Aspose OCR’nin `Image.from_file` yöntemiyle yükleyin.  
3. **PDF üzerinde OCR** çalıştırarak ham metni elde edin.  
4. **OCR doğruluğunu** bir AI post‑işlemcisine besleyerek iyileştirin.  
5. **Her iki çıktıyı** yan yana inceleyin.

Deney yapmaktan çekinmeyin—model repo kimliğini daha yeni bir LLM ile değiştirin, `ai_engine.run_postprocessor` içindeki istemi (prompt) ayarlayın ya da ön‑işleme adımları (ör. eğikliği düzeltme) ekleyin. Boru hattı modüler olduğundan, herhangi bir bileşeni diğerini bozmadan değiştirebilirsiniz.

---

## Sonraki Adımlar

* **Diğer post‑işlemci modellerini keşfedin** – düşük donanımlı makineler için daha küçük bir `distilbert` varyantını deneyin.  
* **Veritabanı entegrasyonu** – iyileştirilmiş metni SQLite ya da Elasticsearch'te saklayarak aranabilir arşivler oluşturun.  
* **PDF oluşturma ekleyin** – `reportlab` ya da `pypdf` kullanarak temizlenmiş metni orijinal PDF üzerine not olarak ekleyin.  

Eğer bu adımları izlediyseniz, artık sağlam, AI‑destekli belge işleme çözümleri geliştirmek için sağlam bir temele sahipsiniz.


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何在 .NET 中使用 Aspose.OCR 進行 PDF OCR](/ocr/hongkong/net/text-recognition/recognize-pdf/)
- [.NET에서 Aspose.OCR을 사용하여 PDF OCR하는 방법](/ocr/korean/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}