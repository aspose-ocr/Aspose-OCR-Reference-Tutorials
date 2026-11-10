---
category: general
date: 2026-06-25
description: Python kullanarak OCR için görüntüyü ön işleme tabi tutun ve taranmış
  belgelerden metni tanıyın. Tam kodlu adım adım öğretici.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: tr
og_description: Python ile OCR için görüntüyü ön işleme tabi tutun ve taranmış belgelerden
  metni tanıyın. Bu ayrıntılı, çalıştırılabilir öğreticiyi izleyin.
og_title: Python'da OCR için Görüntü Ön İşleme – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR için Görüntü Ön İşleme – Tam Kılavuz
url: /tr/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR için Görüntü Ön İşleme – Tam Kılavuz

Görseli **OCR için ön işleme** nasıl yapacağınızı hiç merak ettiniz mi, böylece metin temiz ve güvenilir çıkıyor? Yalnız değilsiniz—çoğu geliştirici, taranmış sayfa eğri olduğunda ya da kontrast dengesiz olduğunda aynı sorunu yaşıyor. İyi haber şu ki, birkaç satır Python kodu bu karışıklığı düzeltebilir, resmi ikili hâle getirebilir ve size net, aranabilir bir metin sunabilir.

Bu öğreticide, popüler bir OCR kütüphanesi kullanarak **OCR için görüntü ön işleme** *ve* **taran belge dosyalarından metin tanıma** adımlarını adım adım inceleyeceğiz. Sonunda çalıştırmaya hazır bir betiğiniz olacak, her ayarın neden önemli olduğunu anlayacak ve zor durumlar için nasıl ayarlama yapacağınızı bileceksiniz.

## Gereksinimler

- Python 3.8 ve üzeri (kod 3.10+’da da çalışır)
- `OcrEngine`, `ImagePreProcessingOptions` ve `Image` sınıflarını sunan bir OCR paketi (örneğin, örnekte kullanılan hayali `ocr` modülü)
- Biraz eğik veya düşük kontrastlı taranmış ya da fotoğraflanmış bir belge
- Sevdiğiniz IDE ya da basit bir terminal—ağır GUI gerekmez

Hepsi bu. Ekstra ikili dosya yok, Docker gereksizliği yok. Hadi başlayalım.

## OCR için Görüntü Ön İşleme – Adım Adım

Aşağıda temel iş akışı beş net aşamaya bölünmüş olarak verilmiştir. Her aşama **neden** yaptığımızı, tam **kod**u ve arka planda neler olduğuna dair kısa bir **açıklama** içerir.

### Adım 1: OCR Motoru Örneği Oluşturma

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Neden önemli:*  
`OcrEngine` nesnesi işlemin beyni gibidir. Dil paketleri, güven eşiği gibi yapılandırmaları ve—bizim için en önemlisi—görüntü‑ön işleme bayraklarını tutar. İlk olarak örneklemek, sonraki ipuçlarını etkinleştirmek için temiz bir başlangıç sağlar.

### Adım 2: Otomatik Eğik Düzeltme ve İkili Hale Getirmeyi Etkinleştirme

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Neden önemli:*  
- **Deskewing** (Eğik Düzeltme) görüntüyü döndürerek metin satırlarının yatay olmasını sağlar. OCR motorları, temel çizgi birkaç dereceden fazla eğildiğinde zorlanır.  
- **Binarization** (İkili Hale Getirme) resmi saf siyah‑beyaz hâle çevirir, karakter sınıflandırıcılarını karıştırabilecek arka plan gürültüsünü ortadan kaldırır.  
Her iki seçenek de modern kütüphanelerde *otomatik* olsa da, hâlâ açmanız gerekir—bu yüzden açık atama yapılır.

> **Pro ipucu:** Kaynak görüntüleriniz zaten mükemmel hizalanmışsa, işleme süresinden bir milisaniye tasarruf etmek için `auto_deskew=False` ayarlayabilirsiniz.

### Adım 3: İşlemek İstediğiniz Eğik Görüntüyü Yükleyin

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Neden önemli:*  
`Image.load` yöntemi dosyayı belleğe okur ve OCR motorunun anlayabileceği bir nesneye sarar. Ayrıca DPI gibi meta verileri çıkarır; bu, eğik düzeltme için varsayılan ölçek faktörünü etkileyebilir.

> **Köşe durumu:** Görüntü çok sayfalı bir TIFF ise, her sayfayı döngüyle işlemek ya da `ocr.MultiPageImage.load` gibi bir yardımcı kullanmak gerekir. Aynı ön işleme ayarları her sayfaya uygulanır.

### Adım 4: Ön‑işlenmiş Görüntüde OCR Gerçekleştirme

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Neden önemli:*  
Bu noktada motor, daha önce etkinleştirdiğimiz eğik düzeltme ve ikili hale getirme adımlarını uygular, ardından temiz bitmap üzerinde sinir ağı (veya klasik Tesseract‑stil boru hattı) çalıştırır. Dönen `result` nesnesi genellikle düz metni, güven skorlarını ve bazen her kelime için konumsal verileri içerir.

> **Metin hâlâ bozuksa ne yapmalı?**  
> Görüntü çözünürlüğünü kontrol edin: OCR, 300 dpi veya üzeri çözünürlükte en iyi çalışır. Kaynağınız daha düşükse, yüklemeden önce ölçeklendirmeyi düşünün veya belge kaynağından orijinal taramayı isteyin.

### Adım 5: Tanınan Metni Çıktılamak

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Neden önemli:*  
`result.text` motorun okuyabildiği her şeyin düz‑string temsilidır. Hızlı hata ayıklama için ekrana yazdırmak kullanışlıdır; gerçek bir uygulamada muhtemelen bir `.txt` dosyasına, bir veritabanına yazar ya da sonraki bir NLP boru hattına beslersiniz.

---

## Taran Belgelerden Metin Tanıma – Temelin Ötesine Geçmek

Temel işlem hattı çalıştığına göre, gerçek dünyada **taran belgeden metin tanıma** görüntüleriyle karşılaştığınızda karşılaşabileceğiniz birkaç yaygın varyasyonu inceleyelim.

### 1. Çoklu Dillerle Çalışma

Belgeniz hem İngilizce hem de Fransızca içeriyorsa, motoru adım 1'den önce yapılandırın:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Çoğu OCR motoru ISO‑639‑2 kodlarını kabul eder; ekstra dil paketlerini yüklemek küçük bir ek yük getirir ancak çok dilli sayfalarda doğruluğu büyük ölçüde artırır.

### 2. İkili Hale Getirme Eşiklerini İnce Ayarlama

Otomatik ikili hale getirme çoğu durumda işe yarar, ancak bazı eski fotokopiler özel bir eşik gerektirir:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Arka plan kaybolana kadar, ancak soluk karakterler silinmeden, 120 ile 220 arasında değerlerle deneme yapın.

### 3. Düzen Bilgisi Çıkarma

Bazen ham metinden daha fazlasına ihtiyacınız olur—her paragrafın sayfadaki konumunu bilmek istersiniz. Birçok motor `result.blocks` koleksiyonunu sunar:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Bu, tabloları yeniden oluşturmak veya sütun sırasını korumak için paha biçilmezdir.

### 4. Bir Dosya Grubunu İşleme

Eğer JPEG'e dönüştürülmüş taranmış PDF'lerle dolu bir klasörünüz varsa, tüm akışı bir döngü içinde sarın:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Döngü aynı `engine` örneğini yeniden kullanır; bu, her dosya için yeniden oluşturulmasından daha verimlidir.

### 5. Düşük Çözünürlüklü Taramalarla Baş Etme

Düşük çözünürlüklü görüntüler (< 150 dpi) genellikle bulanık karakterler üretir. Hızlı bir çözüm, görüntüyü OCR motoruna vermeden önce yüksek kaliteli bir algoritma ile ölçeklendirmektir:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Yukarı ölçeklendirme sihirli bir şekilde detay eklemez, ancak ikili hale getirme adımı daha keskin kenarlarla çalışabilir ve hafif bir artış sağlar.

## Beklenen Çıktı

Orijinal beş adımlı betiği orta derecede eğik, 300 dpi bir tarama üzerinde çalıştırmak aşağıdakine benzer bir çıktı vermelidir:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Eğer bozuk karakterler görürseniz, ön işleme bayraklarını, görüntü çözünürlüğünü ve dil yapılandırmasını iki kez kontrol edin.

## Sonuç

Python kullanarak **OCR için görüntü ön işleme** ve **taran belgelerden metin tanıma** dosyaları için ihtiyacınız olan her şeyi ele aldık. Yeni bir motor örneğiyle başlayıp otomatik eğik düzeltme ve ikili hale getirmeyi etkinleştirdik, eğik bir resmi yükledik, tanıma işlemini gerçekleştirdik ve temiz metni yazdırdık. Yol boyunca çok dilli destek, manuel eşik ayarları, düzen çıkarma, toplu işleme ve düşük çözünürlük çözümlerini inceledik.

Betik'i kendi taramalarınızda deneyin—belki bir yığın makbuz, el yazısı bir form ya da eski bir gazete kesiti. Rahat olduğunuzda PDF oluşturma ekleyebilir ya da çıktıyı bir arama indeksine besleyebilirsiniz. Sınır yok.

**Bir sonraki meydan okumaya hazır mısınız?** *“Python ile Taran PDF'lerden Tablo Çıkarma”* ve *“TensorFlow ile Özel OCR Modelleri Eğitme”* öğreticilerimize göz atarak belge‑otomasyon aracınızı genişletmeye devam edin.

Kodlamaktan keyif alın, ve OCR'ınız her zaman net olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüden Metin Çıkarma – Aspose.OCR for .NET ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}