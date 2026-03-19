---
category: general
date: 2026-03-18
description: Python ile görüntüde OCR'yi hızlıca çalıştırın. PNG'den metin tanımayı,
  OCR için görüntüyü yüklemeyi ve görüntüden kelimeleri çıkarmayı adım adım öğrenin.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: tr
og_description: Python kullanarak görüntüde OCR çalıştırın. Bu öğreticide PNG'den
  metin tanıma, OCR için görüntüyü yükleme ve tam bir kod örneğiyle görüntüden kelimeleri
  çıkarma gösterilmektedir.
og_title: Görüntüde OCR Çalıştır – Python Rehberi
tags:
- OCR
- Python
- Image Processing
title: Görüntüde OCR Çalıştır – Tam Python OCR Örneği
url: /tr/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image – Complete Python OCR Example

Hiç **görüntüde OCR çalıştırma** ihtiyacı duydunuz ama nereden başlayacağınızı bilemediniz mi? Tek değilsiniz; birçok geliştirici taranmış belgelerden metin çıkarmaya ilk kez başladığında bu engelle karşılaşır. Bu öğreticide **Python OCR örneği** üzerinden **PNG dosyalarından metin tanıma**, **OCR için görüntü yükleme** ve **görüntüden kelimeleri güven puanlarıyla çıkarma** işlemlerini sadece birkaç satır kodla nasıl yapacağınızı göstereceğiz.

Gerekli kütüphane, motorun nasıl kurulacağı, her adımın neden önemli olduğu ve çıktının nasıl göründüğü konularını ele alacağız. Sonunda bu kod parçacığını projenize ekleyip herhangi bir görüntüden anında metin çekebileceksiniz. Gereksiz ayrıntı yok, sadece uygulanabilir, çalıştırılabilir bir çözüm.

## What You’ll Need

Başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8 veya daha yeni bir sürüm  
- `ocrengine` paketi (veya bir `OcrEngine` sınıfı sağlayan herhangi bir kütüphane). `pip install ocrengine` ile kurabilirsiniz – farklı bir OCR kütüphanesi (ör. `pytesseract`) kullanıyorsanız paket adını ona göre değiştirin.  
- İşlemek istediğiniz bir görüntü dosyası (PNG, JPG, vb.) – bu rehberde `invoice.png` dosyasını kullanacağız.  

Hepsi bu. Ağır bağımlılıklar, harici servisler yok, sadece saf Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt metin: run OCR on image örneği – işlenen taranmış fatura*

## Step 1 – Install and Import the OCR Library

İlk olarak OCR motorunu ortamımıza ekleyip içe aktaralım. Varsayımsal `ocrengine` paketini kullanıyorsanız import şu şekilde olur:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Neden önemli:** Doğru sınıfı içe aktarmak, daha sonra `setImageFromFile` ve `recognize` gibi metodları çağırmamızı sağlar. Bu adımı atlayınca Python `ModuleNotFoundError` verir ve görüntüyü bile yükleyemezsiniz.

## Step 2 – Create an OCR Engine Instance

Kütüphane hazır olduğuna göre, tanıma sürecinin yapılandırma ve durumunu tutacak bir motor nesnesine ihtiyacımız var.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*İpucu:* Bazı OCR motorları bu aşamada dil modelleri veya DPI ayarları gibi parametreleri değiştirmenize izin verir. Temel bir **python OCR örneği** için varsayılanlar yeterli, ancak düşük çözünürlüklü taramalarla çalışıyorsanız burada ayarlamaları gözden geçirin.

## Step 3 – Load the Image You Want to Process

Bir sonraki mantıklı adım **OCR için görüntü yükleme**. Motoru analiz etmek istediğiniz PNG (veya desteklenen başka bir format) dosyasının yoluna yönlendirirsiniz.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Arka planda ne oluyor?** Motor piksel verisini okur, tanıma algoritmasının anlayabileceği bir formata dönüştürür ve dahili olarak saklar. Dosya yolu yanlışsa `FileNotFoundError` alırsınız, bu yüzden görüntünün gerçekten var olduğundan emin olun.

## Step 4 – Run the Recognition Algorithm

Görüntü yüklendikten sonra **görüntüde OCR çalıştırma** ile metin içeriğini çıkarırız.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

Bu aşamada motor bitmap'i tarar, desen eşleştirme uygular ve tespit edilen her kelime, satır ve güven metriğini içeren bir nesne döndürür.

## Step 5 – Iterate Over Recognized Words and Display Confidence

Her OCR iş akışının en faydalı kısmı **her bir çıkarılan token için güveni** görebilmektir. Bu, motorun her kelimeye ne kadar emin olduğunu gösterir ve düşük güvenilir sonuçları filtrelemenize olanak tanır.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Beklenen çıktı** (örnek):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Artık **görüntüden hangi kelimelerin çıkarıldığını** ve her bir tespitin ne kadar güvenilir olduğunu tam olarak görebilirsiniz. Bu, herhangi bir **görüntüden kelimeleri çıkarma** boru hattının temelidir.

## Handling Common Edge Cases

### What If the Image Is Grayscale?

Bazı OCR motorları renkli görüntülerde daha iyi çalışır. Eğer genel olarak düşük güven görüyorsanız, PNG'yi daha yüksek kontrastlı siyah‑beyaz bir versiyona dönüştürüp motorun içine vermeyi deneyin. Pillow bu konuda yardımcı olur:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Dealing With Multiple Languages

Belgeniz hem İngilizce hem de İspanyolca içeriyorsa, çok dilli bir model kullanarak **PNG'den metin tanıma** yapmanız gerekir. Çoğu motor, başlatma sırasında dil listesini ayarlamanıza izin verir:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtering Low‑Confidence Words

Bazen sadece %90 ve üzeri güvene sahip kelimelere ihtiyacınız olur. Hızlı bir filtreleme şöyle yapılır:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Full, Ready‑to‑Run Script

Her şeyi bir araya getirdiğimizde, tek bir dosyayı kopyalayıp hemen çalıştırabileceğiniz (PNG yolunu kendi dosyanıza göre değiştirmeniz yeterli) bir script elde ederiz.

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Şu komutla çalıştırın:

```bash
python run_ocr_on_image.py
```

Konsola, daha önce gösterildiği gibi kelimelerin ve güven yüzdelerinin listesi basılacaktır.

## Frequently Asked Questions

**Does this work with JPG or TIFF files?**  
Kesinlikle. `setImageFromFile` metodu, alt kütüphanenin çözebildiği herhangi bir formatı kabul eder; bu yüzden **görüntüde OCR çalıştırma** JPG, TIFF, BMP vb. dosyalarla da mümkündür.

**Can I process multiple images in a loop?**  
Elbette. Yükleme ve tanıma adımlarını bir dosya yolu listesi üzerinde `for` döngüsüyle tekrarlayın. Kütüphane her görüntü için yeni bir motor örneği gerektiriyorsa, motoru döngü içinde yeniden başlatmayı unutmayın.

**What if I need the text in a single string instead of per‑word?**  
Çoğu OCR sonuç nesnesi, tüm belgeyi tek bir string olarak döndüren bir `getText()` metoduna sahiptir. Örnek:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Next Steps and Related Topics

Artık **görüntüde OCR çalıştırma** konusunda temel bilgiye sahipsiniz, aşağıdaki konuları keşfetmeyi düşünebilirsiniz:

- **Post‑processing**: Faturalardan çıkarılan tarih, tutar veya kimlik gibi verileri temizlemek için düzenli ifadeler kullanın.  
- **Batch processing**: `os.listdir()` ile bir klasördeki tüm taranmış belgeleri işleyin.  
- **Alternative libraries**: `pytesseract` popüler bir açık kaynak seçenektir; iş akışı benzerdir—sadece motor çağrılarını değiştirin.  
- **Exporting results**: Çıkarılan kelimeleri ve güven puanlarını CSV'ye yazarak sonraki analizlerde kullanın.  

Bu uzantıların her biri, burada oluşturduğumuz temelin üzerine inşa edilerek ham OCR verilerini eyleme dönüştürülebilir hâle getirir.

---

### TL;DR

Kısa ve öz bir **python OCR örneği** gösterdik; bu örnek **OCR için görüntü yükleme**, **görüntüde OCR çalıştırma** ve **görüntüden kelimeleri çıkarma** işlemlerini güven puanlarıyla raporlayarak gerçekleştiriyor. Tam script çalıştırılmaya hazır ve artık **PNG'den metin tanıma** (veya diğer formatlar) ihtiyacı olan herhangi bir projeye uyarlayabilirsiniz. Deneyin, güven eşiklerini ayarlayın ve uygulamalarınızın dakikalar içinde metin‑bilinçli hâle gelmesini izleyin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}