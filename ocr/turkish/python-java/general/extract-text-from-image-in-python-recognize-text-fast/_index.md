---
category: general
date: 2026-07-05
description: Python OCR kullanarak görüntüden metin çıkarın. Görüntüden metni tanımayı,
  OCR için görüntüyü yüklemeyi ve sadece birkaç satırda OCR dilini ayarlamayı öğrenin.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: tr
og_description: Python OCR ile görüntüden metin çıkarın. Bu rehber, görüntüden metni
  tanıma, OCR için görüntüyü yükleme, Python tarzı OCR motoru oluşturma ve OCR dilini
  ayarlama konularını gösterir.
og_title: Python'da Görüntüden Metin Çıkar – Metni Hızlı Tanı
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python'da Görüntüden Metin Çıkar – Metni Hızlı Tanı
url: /tr/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma – Metni Hızlı Tanıma

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz mu ama hangi kütüphaneyi seçeceğinizi bilemediniz mi? Kendinize *görüntüden metin nasıl tanınır* sorusunu sorduysanız ve harici araçlarla uğraşmak istemiyorsanız, doğru yerdesiniz. Bu öğreticide küçük bir OCR motoru oluşturacağız, bir resme yönelteceğiz ve metni çıkaracağız—başka bir şey eklemeyecek, bir şey eksiltmeyecek.

Her adımı adım adım inceleyeceğiz: **ocr motoru python oluşturma**, **ocr dili ayarlama**, **ocr için resmi yükleme**, tanıma işlemini asenkron başlatma ve sonunda sonucu okuma. Sonunda, belge dijitalleştiricisi ya da memeleri okuyan bir sohbet botu olsun, istediğiniz projeye ekleyebileceğiniz bağımsız bir betiğiniz olacak.

## Gerekenler

- Python 3.8+ (kod 3.10 ve üzeri sürümlerde de çalışır)  
- `ocr` paketi (Tesseract’ın ince bir sarmalayıcısı – `pip install ocr` ya da tercih ettiğiniz fork ile kurun)  
- Okunabilir metin içeren bir resim dosyası (`.jpg`, `.png`, vb.)  
- Asenkron kısım için biraz sabır (hızlı, söz veriyoruz)

Hepsi bu—ağır bağımlılıklar yok, yerel derlemeler yok. Sisteminizde zaten Tesseract kuruluysa, `ocr` sarmalayıcı otomatik olarak bulur.

## Adım 1: OCR Motorunu Oluşturma – Çıkarma İşleminin Kalbi

İlk iş: alttaki OCR motoruyla iletişim kurabilecek bir motor nesnesine ihtiyacınız var. Bunu, resmi daha sonra işleyecek “beyin” olarak düşünün.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Neden önemli*: motor olmadan dil ayarları ya da asenkron yetenekler için bir bağlamınız olmaz. `OcrEngine` sınıfı, Tesseract’a yapılan düşük seviyeli komut satırı çağrılarını soyutlayarak temiz bir Python API’si sunar.

## Adım 2: OCR Dilini Ayarlama – motora ne beklediğini söyleyin

Belgeniz İngilizce ise varsayılanı bırakabilirsiniz, ancak açıkça ayarlamak iyi bir pratiktir. Bu aynı zamanda **ocr dili ayarlama** işlemini diğer yerel ayarlar için nasıl yapacağınızı gösterir.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **İpucu**: Çok dilli PDF’ler için `[ocr.Language.ENGLISH, ocr.Language.FRENCH]` gibi bir liste geçirebilirsiniz. Motor, her iki dili de otomatik olarak deneyecektir.

## Adım 3: OCR İçin Resmi Yükleme – resmi belleğe aldırma

Şimdi **ocr için resmi yükleme** işlemini yapıyoruz. Sarmalayıcı tembel yüklemeyi destekler, yani dosya motorun ihtiyacı olana kadar okunmaz.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Köşe durumu*: Resim çok büyükse (5 MB üzeri), tanıma hızını artırmak için önce yeniden boyutlandırın. Bunu Pillow ile yapabilirsiniz:

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Adım 4: Asenkron Tanıma Başlatma – uygulamanızı engellemeyin

OCR çalıştırmak büyük taramalarda bir iki saniye sürebilir. `recognize_async` metodu, daha sonra sorgulayabileceğiniz bir future döndürür, böylece **OCR arka planda çalışırken başka işler yapabilirsiniz**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Neden async? Bir web sunucusunda tek bir isteğin tüm çalışan havuzunu durdurmasını istemezsiniz. Future nesnesi size kontrol verir: async kod içinde `await` edebilir ya da gerçekten sonuca ihtiyacınız olduğunda bloklayabilirsiniz.

## Adım 5: Sonucu Almak – gerektiğinde sadece bloklayın

Metne gerçekten ihtiyacınız olduğunda `future.get()` çağırın. Bu çağrı **sadece burada bloklanır**, yani programınızın geri kalanı OCR bitene kadar yanıt vermeye devam eder.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Eğer bir `asyncio` döngüsü içindeyseniz, `await future` kullanabilirsiniz – sarmalayıcı her iki stili de destekler.

## Adım 6: Tanınan Metni Kullanma – veriniz hazır

Artık bir `result` nesneniz var, düz metni almak çok basit. Hadi ekrana bastıralım ve aynı zamanda bir dosyaya nasıl yazabileceğinizi gösterelim.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Beklenen çıktı** (kısaltılmış):

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Eğer resimde metin yoksa, `result.text` boş bir string olur—bu durumu nazikçe ele alın.

## Tam Çalışan Örnek – Tüm Adımlar Tek Betikte

Aşağıda eksiksiz, çalıştırmaya hazır program bulunuyor. Kopyalayıp yapıştırın, `image_path`’i ayarlayın, ve hazırsınız.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Not**: `"YOUR_DIRECTORY/large_document.jpg"` ifadesini gerçek resim yolunuzla değiştirin. Betik, Tesseract yüklü ve `PATH` içinde olduğu sürece Windows, macOS ve Linux’da çalışır.

## Yaygın Tuzaklar & Kaçınma Yolları

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Garbage karakterler** | Yanlış dil veya eksik dil veri dosyaları. | `engine.language` değerinin metinle eşleştiğinden ve ilgili `.traineddata` dosyasının Tesseract’ın `tessdata` klasöründe bulunduğundan emin olun. |
| **Büyük resimlerde yavaş performans** | OCR, piksel sayısıyla orantılı olarak yavaşlar. | Motorun önüne resimi yeniden boyutlandırın veya örnekleyin (Pillow örneğine bakın). |
| **Future hiç çözülmüyor** | Resim dosyası bozuk ya da okunamıyor. | `future.get()` çağrısını try/except bloğuna alın ve tanımadan önce `image.is_valid()` ile doğrulayın. |
| **Unicode kaybı** |  |  |

## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}