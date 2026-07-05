---
category: general
date: 2026-07-05
description: Python OCR kullanarak görüntüden metin çıkarın. OCR için görüntüyü nasıl
  yükleyeceğinizi, bir bölgeden metni nasıl okuyacağınızı ve birkaç satır kodla faturadan
  metin nasıl çıkaracağınızı öğrenin.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: tr
og_description: Python OCR ile görüntüden metin çıkarın. Bu kılavuz, OCR için görüntünün
  nasıl yükleneceğini, bölgeden metnin nasıl okunacağını ve faturadan metnin hızlı
  bir şekilde nasıl çıkarılacağını gösterir.
og_title: Görüntüden Metin Çıkar – OCR ile Bölgeden Metin Okuma
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Görüntüden Metin Çıkar – OCR Kullanarak Bölgeden Metin Oku
url: /tr/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma – Bölgeden Metin Okuma OCR Kullanarak

Hiç **extract text from image** yapmanız gerekti, ancak sadece belirli bir kısmı önemli oldu mu—örneğin bir faturadaki toplam tutar? Tek başınıza değilsiniz. Birçok gerçek‑dünya projesinde, tüm resmi ayrıştırmak yerine **read text from region** yapmanız gerekir. Neyse ki, birkaç Python satırıyla bir görüntüyü OCR için yükleyebilir, ilgi bölgesi (ROI) tanımlayabilir ve tam olarak ihtiyacınız olan karakterleri çıkarabilirsiniz.

Bu öğreticide, **load image for OCR**, bir ROI ayarlamayı ve sonunda **extract text from invoice** gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, bölge‑tabanlı tanıma destekleyen herhangi bir popüler OCR kütüphanesiyle çalışan, hemen kullanabileceğiniz bir kod parçacığına sahip olacaksınız.

---

## Gerekenler

- Python 3.8+ (kod 3.10'da da çalışır)  
- `OcrEngine` sınıfını sunan bir OCR paketi (demo için hayali bir `ocr` modülü kullanacağız; `pytesseract`, `easyocr` veya ROI desteği sunan herhangi bir kütüphane ile değiştirin)  
- Açık, basılı metin içeren örnek bir görüntü—ör. `invoice.png`—  
- Python fonksiyonları ve sınıfları hakkında temel aşinalık (derin öğrenme geçmişi gerekmez)

Eğer bunlara zaten sahipseniz, harika—hadi başlayalım. Yoksa, python.org adresinden en son Python'u indirin ve OCR paketini `pip install your-ocr-lib` ile kurun.

![Görüntüden metin çıkarma örneği](extract-text-from-image.png "Görüntüden metin çıkarma – bölge tabanlı OCR demo")

*Yukarıdaki resim, **extract text from image** hedefleyeceğimiz bölgeyi (kırmızı dikdörtgen) göstermektedir.*

## Adım 1: OCR Kütüphanesini Kurun ve İçe Aktarın

İlk olarak, OCR kütüphanesinin ortamınızda mevcut olduğundan emin olun. Aşağıdaki içe aktarma deseni, yüksek seviyeli bir `OcrEngine` sınıfı sunan çoğu paket için çalışır.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** `pytesseract` kullanıyorsanız, Tesseract ikili dosyasını ayrı olarak kurmanız ve `pytesseract.pytesseract.tesseract_cmd` yolunu ayarlamanız gerekir.

## Adım 2: OCR Motorunu Oluşturun ve Dili Ayarlayın

Motoru oluşturmak basittir, ancak dili belirtmek doğruluğu büyük ölçüde artırır, özellikle sayılar ve İngilizce kelimeler içeren faturalar için.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Neden bunu yapıyoruz? OCR motoru karakterleri tahmin etmek için dil modelleri kullanır; ona İngilizce bekleyeceğini söylemek, “0”ı “O” olarak yanlış okuma gibi yanlış pozitifleri azaltır.

## Adım 3: OCR için Görüntüyü Yükleyin

Şimdi gerçekten **load image for OCR** yapıyoruz. Çoğu kütüphane bir dosya yolu ya da Pillow görüntü nesnesi kabul eder. Burada basitlik için kütüphanenin yerleşik yükleyicisini kullanıyoruz.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Yolun doğru dizini gösterdiğinden emin olun; yaygın bir hata, betik farklı bir çalışma dizininden çalıştırıldığında göreli yolu unutmak.

## Adım 4: İlgi Bölgesi (ROI) Tanımlayın

ROI tanımlamak, **read text from region** işleminin kalbidir. Bunu, faturadaki toplam tutarı içeren kısmın etrafına bir dikdörtgen çizmeye benzetin.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` ve `top`, dikdörtgenin sol‑üst köşesinin X ve Y koordinatlarını temsil eder.  
- `width` ve `height` kutunun boyutunu ayarlar.  
- Piksel koordinatlarını gösteren bir görüntü görüntüleyici ile farklı değerlerle deney yapabilirsiniz.

> **ROI'nin önemi:** Tüm sayfada OCR çalıştırmak CPU döngülerini boşa harcar ve genellikle alakasız metin, tablo veya grafiklerden gürültü getirir. Bir bölgeye odaklanarak daha temiz sonuçlar ve daha hızlı işleme elde edersiniz.

## Adım 5: Belirtilen Bölge Üzerinde OCR Gerçekleştirin

Her şey ayarlandığında, sonunda **extract text from image** yapıyoruz—ancak sadece tanımladığımız ROI içinde.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

`recognize` metodu genellikle ham dizeyi, güven skorlarını ve bazen her kelime için sınırlayıcı kutuları içeren bir nesne döndürür. Bizim amacımız sadece düz metni almaktır.

## Adım 6: Çıkarılan Metni Çıktılayın

Sonucu yazdıralım ve ne elde ettiğimize bakalım. Bu adım, gerçek bir senaryoda **extract text from invoice** gösterir.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Beklenen Çıktı

```
Text inside ROI:
Total Amount: $1,245.67
```

Eğer faturanız farklı bir düzen kullanıyorsa, dikdörtgenin içinde bulunan metni göreceksiniz—belki bir fatura numarası, tarih veya PO referansı.

## Adım 7: Her Şeyi Yeniden Kullanılabilir Bir Fonksiyona Sarın (İsteğe Bağlı)

Çözümü birden fazla fatura için yeniden kullanılabilir hâle getirmek için mantığı bir fonksiyon içinde kapsüllayın. Bu aynı zamanda **ocr on region**'ı genel bir yardımcı program olarak gösterir.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Artık fonksiyonu herhangi bir fatura ile çağırabilirsiniz:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Issue | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Blank output** | ROI aslında herhangi bir metni kapsamaz (yanlış koordinatlar). | Piksel değerlerini bir görüntü düzenleyici ile tekrar kontrol edin; görsel bir hata ayıklama katmanı ekleyin. |
| **Garbage characters** | Düşük görüntü çözünürlüğü veya düşük kontrast. | Görüntüyü ön‑işleme tabi tutun: gri tonlamaya dönüştürün, eşikleme uygulayın (`cv2.threshold`). |
| **Wrong language** | Motor, gerekli karakter setine sahip olmayan bir dil varsayar. | `ocr_engine.language` değerini açıkça `ENGLISH` ya da uygun yerel ayara ayarlayın. |
| **Performance lag** | Büyük görüntülerde OCR'ı tekrar tekrar çalıştırmak. | Görüntüyü yüklemeden önce yeniden boyutlandırın, ya da önce kırparak sadece ROI'yi işleyin. |

## Örneği Genişletmek: Birden Çok ROI

Bazen bir faturada ihtiyacınız olan birden fazla alan bulunur—örneğin toplam tutar ve fatura tarihi için **extract text from invoice**. Dikdörtgenlerin bir listesi üzerinde döngü yapabilirsiniz:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Bu desen kodunuzu temiz tutar ve ileride daha fazla bölge eklemeyi kolaylaştırır.

## Sonuç

Python OCR kullanarak **extract text from image** yapmak için tam, uçtan uca bir iş akışını ele aldık, belirli bir bölgeye odaklanarak. **load image for OCR**, bir **region of interest** tanımlayarak ve motoru çağırarak, **read text from region**'ı güvenilir bir şekilde yapabilirsiniz—faturalardan toplamları, makbuzlardan tarihleri veya başka herhangi bir yerel veriyi çekmek için mükemmeldir.  
Denemekten çekinmeyin

## Sonra Ne Öğrenmelisiniz?

Bu öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüden Metin Çıkarma – Aspose.OCR ile .NET için OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [OCR'da Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}