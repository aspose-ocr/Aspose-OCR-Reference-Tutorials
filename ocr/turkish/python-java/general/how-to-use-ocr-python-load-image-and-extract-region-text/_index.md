---
category: general
date: 2026-06-25
description: Python'da OCR nasıl kullanılır – OCR için görüntüyü nasıl yükleyeceğinizi,
  bölgede metni nasıl tanıyacağınızı ve bölge metnini hızlıca nasıl çıkaracağınızı
  öğrenin.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: tr
og_description: Python'da OCR nasıl kullanılır – bir görüntüyü yükleme, belirli bir
  bölgede metni tanıma ve fatura numarasını çıkarma adım adım rehberi.
og_title: 'OCR Python Nasıl Kullanılır: Görüntüyü Yükle ve Bölge Metnini Çıkar'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'OCR Python Nasıl Kullanılır: Görüntüyü Yükle ve Bölge Metnini Çıkar'
url: /tr/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Python Kullanımı: Görüntüyü Yükleme ve Bölge Metnini Çıkarma

**Python’da OCR kullanımı** düşündüğünüzden daha basittir. Taralı bir faturaya bakıp, tüm sayfayı ayrıştırmadan sadece fatura numarasını nasıl alacağınızı merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, optik karakter tanıma ile ilk kez uğraşırken bu sorunu yaşar. Bu rehberde bir görüntüyü OCR için nasıl yükleyeceğimizi, bir dikdörtgen tanımlamayı, o bölgede metni tanımayı ve sonunda bölge metnini çıkarmayı adım adım göstereceğiz. Sonunda ihtiyacınız olan herhangi bir metin parçasını izole eden, çalıştırmaya hazır bir betiğiniz olacak.

> *Pro tip:* PDF’lerle çalışıyorsanız, önce her sayfayı bir görüntüye dönüştürün—çoğu OCR kütüphanesi PNG/JPEG’i en iyi şekilde işler.

## Gereksinimler

- Python 3.8+ (en son kararlı sürüm önerilir)  
- `OcrEngine` sınıfını sunan bir OCR kütüphanesi (ör. **ocr**, `pip install ocr-lib` ile)  
- Örnek bir görüntü—burada `invoice.png` dosyasını kontrol ettiğiniz bir klasöre koyacağız  
- Dikdörtgenler (x, y, width, height) hakkında temel bilgi  

Ağır bağımlılıklar yok, GPU gerekmez—sadece düz CPU çalışması, bu da taşınabilirliği artırır.

---

## OCR Kullanımı: Motoru Başlatma (Adım 1)

Metin okunmadan önce bir OCR motoru örneğine ihtiyacınız var. Bunu, piksel desenlerini analiz edecek beyin olarak düşünün.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Neden önemli:* Motoru başlatmak dil modellerini yükler ve varsayılan yapılandırmaları ayarlar. Bu adımı atlamak, `recognize_region` çağrısı yaptığınız anda bir istisna fırlatır.

---

## OCR İçin Görüntüyü Yükleme (Adım 2)

Motor hazır olduğunda, ona bir görüntü veririz. Kütüphanenin `Image.load` yöntemi yaygın formatları işler ve bitmap’i normalleştirir.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Dosya bulunamazsa Python bir `FileNotFoundError` fırlatır. Yolun mutlak ya da betiğinizin çalışma dizinine göre göreli olduğundan emin olun.  

*Köşe durum:* Bazı OCR motorları gri tonlamalı bir görüntü bekler. Düşük doğruluk görürseniz, önce görüntüyü dönüştürün:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Bölgedeki Metni Tanıma (Adım 3)

Bölgeyi tanımlamak, motorun *nerede* bakacağını belirtmektir. `Rectangle` alt‑piksel hassasiyeti için kayan‑nokta değerler alır; bu, yüksek çözünürlüklü taramalarla çalışırken kullanışlıdır.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – dikdörtgenin sol‑üst köşesi (piksel cinsinden)  
- **width, height** – kutunun boyutu  

Bu sayıları nasıl bulacağınızı merak edebilirsiniz. Hızlı bir yol, görüntüyü herhangi bir editörde (ör. GIMP veya Paint.NET) açıp seçim aracını kullanarak koordinatları okumaktır.  

*Neden tüm sayfayı OCR’a vermeyelim?* Alanı sınırlamak gürültüyü azaltır, işleme süresini hızlandırır ve fatura numarası gibi küçük alanların doğruluğunu büyük ölçüde artırır.

---

## Bölge Metnini Çıkarma (Adım 4)

Bölge ayarlandıktan sonra, motoru sadece o dilimi tanıması için isteyin. Sonuç nesnesi ham metni ve güven skorlarını içerir.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

OCR motoru birden fazla dili destekliyorsa, isteğe bağlı bir dil kodu geçirebilirsiniz:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Yaygın tuzak:* Bazı motorlar tek bir dize yerine kelime listesi döndürür. Böyle bir durumda, kelimeleri birleştirin:

```python
text = " ".join(region_result.words)
```

---

## Çıkarılan Fatura Numarasını Görüntüleme (Adım 5)

Son olarak, çıkarılan metni yazdırın—ya da saklayın. Dizeyi, gereksiz boşlukları ya da sayısal olmayan karakterleri kaldırmak için de işleyebilirsiniz.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Doğru hizalanmış bir dikdörtgenle betiği çalıştırdığınızda aşağıdakine benzer bir çıktı almanız gerekir:

```
Invoice number: 20231578
```

Çöp karakterler alıyorsanız, dikdörtgen koordinatlarını tekrar kontrol edin ya da görüntü çözünürlüğünü artırmayı düşünün.

---

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, kopyalayıp yapıştırıp çalıştırabileceğiniz bağımsız bir betik şu şekildedir:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Dosyayı `extract_invoice.py` olarak kaydedin, `YOUR_DIRECTORY` kısmını gerçek klasörle değiştirin ve çalıştırın:

```bash
python extract_invoice.py
```

Konsolda fatura numarasının yazdırıldığını görmelisiniz.

---

## Sık Sorulan Sorular

**S: Fatura numarası süslü bir fontla basılmışsa ne olur?**  
C: Çoğu modern OCR motoru geniş bir font yelpazesini işler, ancak özel bir dil modeli eğiterek ya da görüntüyü ön‑işleme (ör. eşik filtresi uygulama) yaparak doğruluğu artırabilirsiniz.

**S: Aynı anda birden fazla alanı çıkarabilir miyim?**  
C: Kesinlikle. Her alan için bir `Rectangle` nesnesi listesi tanımlayın ve döngü içinde işleyerek sonuçları bir sözlükte saklayın.

**S: Çok sayfalı PDF’lerde bu çalışır mı?**  
C: Önce her sayfayı bir görüntüye dönüştürün (`pdf2image` gibi bir araçla), ardından aynı bölge‑bazlı çıkarma işlemini sayfa sayfa uygulayın.

---

## Sonuç

Bu öğreticide **Python’da OCR nasıl kullanılır** konusunu, bir görüntüyü yükleme, belirli bir bölgede metni tanıma ve o bölgenin metnini çıkarma adımlarıyla ele aldık—fatura numaraları, sipariş kimlikleri veya taranmış belgelerden küçük veri parçacıkları çekmek için ideal. İlgi alanını izole ederek hız, doğruluk ve daha az sonrası işleme zahmeti elde edersiniz.

Bir sonraki adıma hazır mısınız? Betiği, toplu fatura klasöründen **OCR için görüntü yükleme** işlemini gerçekleştirecek şekilde genişletin ya da **bölge içinde metin tanıma**yı tarih ve toplam tutar gibi farklı alanlar için deneyin. Aynı desen geçerli—sadece dikdörtgen koordinatlarını değiştirin.

Herhangi bir sorunla karşılaştıysanız ya da geliştirme öneriniz varsa, aşağıya yorum bırakın. İyi kodlamalar, OCR hatlarınız daima doğru olsun!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları ele alır. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Görüntüden Metin Çıkarma – Aspose OCR ile Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR’da Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [AspOCR Kullanımı: .NET için Görüntü OCR Filtrelerini Ön‑İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}