---
category: general
date: 2026-06-16
description: OCR'de ilgi bölgesini tanımlayarak kimlik kartlarından İspanyolca metni
  çıkarın. OCR için görüntüyü nasıl yükleyeceğinizi ve ROI'yi verimli bir şekilde
  nasıl belirleyeceğinizi öğrenin.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: tr
og_description: OCR'de ilgi bölgesini tanımlayarak kimlik kartlarından İspanyolca
  metin çıkarın. Görüntüleri yükleme ve ROI'yi belirleme adım adım rehberi.
og_title: OCR'de İlgi Bölgesini Tanımlama – Tam Python Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: OCR'de İlgi Bölgesi Tanımlama – Tam Python Öğreticisi
url: /tr/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR'de İlgi Alanı Tanımlama – Tam Python Eğitimi

Hiç **OCR'de ilgi alanı tanımlamayı** merak ettiniz mi, böylece sadece gerçekten ihtiyacınız olan görüntü kısmını okuyabilirsiniz? Bu öğreticide tam olarak bunu adım adım gösterecek, ayrıca **OCR için görüntü yükleme** ve bir kimlik kartından sadece birkaç satır Python kodu ile İspanyolca metin çıkarma konularını ele alacağız.  

Gürültülü bir taramaya bakıp “İsim alanını daha temiz bir şekilde yakalamanın bir yolu olmalı” diye düşündüyseniz, doğru yerdesiniz. Sonunda, arka plan karmaşasından etkilenmeden ihtiyacınız olan kimlik kartı metnini çekebileceksiniz.

## Öğrenecekleriniz

- OCR çalıştırmadan önce **ilgi alanı tanımlamanız** gerektiği nedenleri.  
- Popüler bir Python OCR sarmalayıcısı kullanarak **OCR için görüntü yükleme** adımlarını.  
- Piksel koordinatlarıyla **ROI nasıl belirtilir**.  
- Kaynak dil İspanyolca olsa bile **kimlik kartı metni çıkarma** yöntemlerini güvenilir bir şekilde.  
- Döndürülmüş kartlar veya düşük kontrast taramalar gibi kenar durumlarını ele almanın ipuçları.  

Önceden OCR bilgisi gerekmiyor—sadece çalışan bir Python 3 ortamı ve denemek istediğiniz kimlik kartının bir JPEG'i yeterli.

---

![Define region of interest illustration](placeholder.png){alt="İlgi alanı örneği, bir kimlik kartı görüntüsü üzerinde vurgulanmış bir dikdörtgen gösteriyor"}

## Adım 1: OCR Kütüphanesini Kurun ve İçe Aktarın

İlk olarak, gördüğünüz snippet'e benzer bir `OcrEngine` sınıfı sunan bir kütüphane gerekir. Bu rehberde hayali `ocr` paketini kullanacağız, ancak aynı kavramlar `pytesseract`, `easyocr` ya da dil ve ROI ayarlamanıza izin veren herhangi bir sarmalayıcı için geçerlidir.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*İpucu:* `pytesseract` kullanıyorsanız, `Rectangle` sınıfı basit bir tuple `(left, top, width, height)` haline gelir. Akışın geri kalanı aynı kalır.

## Adım 2: OCR için Görüntüyü Yükleyin

Şimdi **OCR için görüntü yükleme** işlemini yapıyoruz. Motor bir `ocr.Image` nesnesi beklediği için, kimlik kartını içeren dosyayı ona gösteriyoruz. Yolun mutlak ya da betiğinizin çalışma dizinine göre göreli olduğundan emin olun.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Görüntü çok büyükse, önce yeniden boyutlandırmayı düşünün; OCR motorları genişliği 1500 px'in altında olan görüntülerde daha hızlı çalışır.

## Adım 3: ROI Nasıl Belirtilir (İlgi Alanı Tanımlama)

İşte öğretinin kalbi: **ROI nasıl belirtilir**. İlgi alanı, OCR motoruna “Sadece bu piksel sınırları içinde bak” diyen basit bir dikdörtgendir. Bunu, bir kimlik kartındaki isim alanının etrafına kutu çizmeye benzetin.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Bu sayılar neden? Örnek görüntümüzde isim, sol kenardan yaklaşık 120 px ve üstten 80 px uzakta yer alıyor. Kartlarınızın düzenine göre ayarlayın.  

*Kenar durumu:* Kart 90° döndürülmüşse, `width` ve `height` değerlerini değiştirin ve `left`/`top` koordinatlarını ona göre ayarlayın, ya da motorun önüne resmi Pillow ile önceden döndürün.

## Adım 4: ROI İçinde OCR Çalıştırın

ROI tanımlandığında, motor dikdörtgen dışındaki her şeyi yok sayar. Bu sadece işleme süresini hızlandırmakla kalmaz, aynı zamanda arka plan grafikleri nedeniyle oluşan yanlış pozitifleri de azaltır.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

`recognize()` çağrısı, tanınan metni, güven skorlarını ve her kelime için sınırlayıcı kutuları içeren bir nesne döndürür.

## Adım 5: Kimlik Kartı Metnini Çıkarın (İspanyolca Çıktıyı Doğrulayın)

Son olarak, **kimlik kartı metnini** ROI sonucundan çıkarıyor ve ekrana yazdırıyoruz. Daha önce dili İspanyolca olarak ayarladığımız için OCR motoru “ñ” veya “á” gibi aksanlı karakterler için dil‑özel sözlükler kullanır, bu da doğruluğu artırır.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Beklenen Çıktı

```
ROI text: JUAN PÉREZ GARCÍA
```

Eğer bozuk karakterler görürseniz, görüntünün gerçekten İspanyolca olduğundan ve OCR kütüphanesinin dil veri dosyalarının kurulu olduğundan emin olun.

## Yaygın Tuzaklar ve Kaçınma Yolları

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Boş string döner | ROI hiçbir metinle kesişmiyor | Koordinatları bir görüntü görüntüleyicisiyle doğrulayın; mümkünse `engine.debug_draw_roi()` kullanın. |
| Çok fazla bozuk karakter | Yanlış dil paketi | İspanyolca dil verisini yeniden kurun ya da `ocr.Language.AUTO`'ya geçin. |
| Düşük güven skorları | Görüntü bulanık veya düşük kontrastlı | OpenCV ile ön işleme yapın – `cv2.GaussianBlur` ve `cv2.threshold` uygulayın. |
| ROI'ye rağmen tüm görüntüde OCR çalışıyor | Eski kütüphane sürümü kullanılıyor | En son `ocr` paketine yükseltin; eski sürümler ROI'yi yok sayıyordu. |

## Örneği Genişletme: Birden Çok ROI

Bazen birden fazla alan (ör. isim ve kimlik numarası) çekmeniz gerekir. Desen aynı kalır: `engine.region_of_interest` değerini değiştirin ve tekrar `recognize()` çağırın.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Kütüphane destekliyorsa, bir dikdörtgen listesiyle toplu işleme de yapabilirsiniz; bu da OCR motoruna yapılan tur sayısını azaltır.

## Tam Çalışan Betik

Her şeyi bir araya getirdiğimizde, **ilgi alanı tanımlayan**, **OCR için görüntü yükleyen** ve **kimlik kartından İspanyolca metin çıkaran** hazır bir betik elde ederiz.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Betik çalıştırıldığında isim konsola yazdırılacaktır. Diğer alanları hedeflemek için dikdörtgen değerlerini değiştirin; böylece herhangi bir kimlik‑kartı‑türü belge için yeniden kullanılabilir bir yardımcı programınız olur.

## Sonraki Adımlar

- **Toplu işleme:** Bir klasördeki kimlik kartları üzerinde döngü kurun ve her çıkarılan ismi bir CSV dosyasına kaydedin.  
- **Dil algılama:** Kullanıcının dili dinamik olarak seçmesine izin verin; `ocr.Language.AUTO` işinize yarayabilir.  
- **Son‑işleme:** OCR hatalarını temizlemek için regex desenleri uygulayın (ör. isimlerde görülen “0” karakterini “O” ile değiştirin).  

**İlgi alanı tanımlamayı** öğrenerek, özellikle İspanyolca belgelerle çalışırken **kimlik kartı metni çıkarma** işlemini hızlı ve doğru bir şekilde yapmanın güçlü bir yolunu keşfettiniz.

---

### TL;DR

**OCR'de ilgi alanı tanımlama**, **OCR için görüntü yükleme** ve **ROI'yi nasıl belirleyeceğinizi** gösterdik; böylece bir kimlik kartından **İspanyolca metin** çıkarabilirsiniz. Tam örnek bir dakikadan kısa sürede çalışır ve birkaç koordinat ayarıyla herhangi bir düzen için uyarlanabilir. Deneyin, dikdörtgeni ayarlayın ve OCR'un lazer gibi odaklandığını izleyin.

İyi kodlamalar!


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [OCR'de Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Aspose.OCR ile Dil Seçimi Kullanarak C#'ta Görüntü Metni Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose.OCR for .NET ile OCR Optimizasyonu – Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}