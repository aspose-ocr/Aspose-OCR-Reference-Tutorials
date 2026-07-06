---
category: general
date: 2026-05-31
description: OCR ilgi bölgesini kullanarak OCR için görüntü yüklemeyi ve dikdörtgenden
  metin çıkarmayı öğrenin; faturadaki tutarı tanımak için mükemmeldir.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: tr
og_description: Tek bir öğreticide OCR için görüntü yükleme, dikdörtgenden metin çıkarma
  ve faturadan metin tanıma konularında bölge ilgi alanını (ROI) ustalaşın.
og_title: OCR İlgi Alanı – Adım Adım Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR İlgi Bölgesi – Python'da Dikdörtgenden Metin Çıkarma
url: /tr/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR İlgi Bölgesi – Python’da Dikdörtgenden Metin Çıkarma

Hiç **ocr region of interest** bir taranmış faturanın belirli bir kısmını tüm sayfayı motorun içine vermeden çıkarmayı düşündünüz mü? İlk defa bulanık bir makbuzu elinize alıp “Sağ alt köşede bir yerde bulunan tutarı nasıl çıkarırım?” diye düşünüyorsanız yalnız değilsiniz. İyi haber, OCR kütüphanesine tam olarak nerede bakması gerektiğini söyleyebilir, böylece hız ve doğruluğu büyük ölçüde artırabilirsiniz.

Bu rehberde, **load image for OCR**, bir **region of interest** tanımlama ve ardından **extract text from rectangle** işlemini gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz; sonunda **recognize text from invoice** yaparak klasik “tutarı nasıl çıkarırım” sorusuna yanıt bulacaksınız. Belirsiz referanslar yok—sadece somut kod, net açıklamalar ve daha önce bilmek isteyeceğiniz birkaç profesyonel ipucu.

---

## Ne Oluşturacaksınız

Bu öğreticinin sonunda, aşağıdaki işlevi gören küçük bir Python betiğiniz olacak:

1. Diskten bir fatura görüntüsü yükler.  
2. Toplam tutarın bulunduğu dikdörtgen bir ROI işaretler.  
3. OCR’u yalnızca bu ROI içinde çalıştırır.  
4. Temizlenmiş tutar dizesini ekrana yazdırır.  

Tüm bunlar ROI destekleyen herhangi bir OCR kütüphanesiyle çalışır—burada popüler araçlar olan Tesseract veya EasyOCR’a benzer bir hayali `SimpleOCR` paketini kullanacağız. İsterseniz değiştirebilirsiniz; kavramlar aynı kalır.

---

## Önkoşullar

- Python 3.8+ yüklü (`python --version` komutu ≥3.8 göstermeli).  
- Pip ile kurulabilir bir OCR paketi (ör. `pip install simpleocr`).  
- Bir fatura görüntüsü (PNG veya JPEG) erişebileceğiniz bir klasörde.  
- Python fonksiyonları ve sınıfları hakkında temel bilgi (karmaşık bir şey değil).

Bu koşullara sahipseniz harika—derhal başlayalım. Değilseniz önce görüntüyü temin edin; geri kalan adımlar dosyanın içeriğinden bağımsızdır.

---

## Adım 1: Load Image for OCR

Her OCR iş akışının ilk ihtiyacı, okunacak bir bitmap’dir. Çoğu kütüphane, dosya yolunu kabul eden basit bir `load_image` metodu sunar. İşte `SimpleOCR` motorumuzla bunu nasıl yapacağınız:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Betiği farklı bir çalışma dizininden çalıştırdığınızda “dosya bulunamadı” hatalarını önlemek için mutlak yollar ya da `os.path.join` kullanın.

---

## Adım 2: Define OCR Region of Interest

Motorun tüm sayfayı taramasına izin vermek yerine, tutarın tam olarak nerede olduğunu *tam olarak* söylüyoruz. Bu, **ocr region of interest** adımıdır ve özellikle belge gürültülü başlıklar veya altbilgiler içerdiğinde güvenilir çıkarımın anahtarıdır.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Bu sayılar neden? `x` ve `y`, sol‑üst köşeden piksel offset’leridir; `width` ve `height` ise kutunun boyutlarını tanımlar. Emin değilseniz, görüntüyü herhangi bir editörde açın, cetveli etkinleştirin ve koordinatları not alın. Birçok IDE, imleç konumunu üzerine gelince gösterir.

---

## Adım 3: Extract Text from Rectangle

ROI ayarlandığına göre, motoru **recognize text from invoice** yapmaya ama sadece az önce eklediğimiz dikdörtgenle sınırlı kalmaya çağırıyoruz. Çağrı, genellikle ham dize, güven skorları ve bazen sınırlayıcı kutuları içeren bir sonuç nesnesi döndürür.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Arka planda, `recognize()` her ROI üzerinden döner, o dilimi kırpar, OCR modelini çalıştırır ve sonuçları birleştirir. Bu yüzden sıkı bir **extract text from rectangle** bölgesi tanımlamak, toplu işler için işlem süresini saniyelerce kısaltabilir.

---

## Adım 4: How to Extract Amount – Clean the Output

OCR mükemmel değildir; genellikle gereksiz boşluklar, satır sonları ya da yanlış okunmuş karakterler (ör. “S” yerine “5”) elde edersiniz. Basit bir `strip()` ve küçük bir regex çoğu para değeri için işinizi görür.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Neden önemli:** Tutarı bir veritabanına ya da ödeme geçidine göndermeyi planlıyorsanız, öngörülebilir bir formata ihtiyacınız var. Boşlukları temizlemek ve sayısal olmayan karakterleri filtrelemek, sonraki hataları önler.

---

## Adım 5: Recognize Text from Invoice – Full Script

Hepsini bir araya getirdiğimizde, tam ve çalıştırılabilir betik aşağıdadır. `extract_amount.py` olarak kaydedin ve `python extract_amount.py` komutuyla çalıştırın.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Beklenen Çıktı

```
Amount: 1,245.67
```

ROI yanlış hizalanmışsa, `Amount: 1245.6S` gibi bir şey görebilirsiniz—gereksiz “S”ye dikkat edin. Dikdörtgen koordinatlarını ayarlayın ve çıktı temiz olana kadar tekrar çalıştırın.

---

## Yaygın Tuzaklar & Kenar Durumları

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI too small** | Tutar metni kesilir, kısmi tanıma olur. | `width`/`height` değerlerini %10‑20 artırın ve yeniden test edin. |
| **Incorrect DPI** | Düşük çözünürlüklü taramalar (≤150 dpi) OCR doğruluğunu düşürür. | Görüntüyü 300 dpi’ye yeniden örnekleyin ya da tarayıcıdan daha yüksek DPI isteyin. |
| **Multiple currencies** | Regex ilk sayısal grubu alır, bu bir fatura numarası olabilir. | Regex’i para birimi simgeleri (`$`, `€`, `£`) öncesinde arayacak şekilde iyileştirin. |
| **Rotated invoices** | OCR motorları dik metin varsayar; döndürülmüş sayfalar tanıma hatası verir. | ROI eklemeden önce bir döndürme düzeltmesi (`ocr_engine.rotate(90)`) uygulayın. |
| **Noise in background** | Gölge ya da damga modeli karıştırır. | Basit bir eşikleme (`cv2.threshold`) ya da gürültü azaltma filtresi kullanın. |

Bu kenar durumlarını erken ele almak, ileride saatlerce hata ayıklamaktan sizi kurtarır.

---

## Gerçek Dünya Projeleri İçin Pro İpuçları

- **Batch Processing:** Bir klasördeki faturalar üzerinde döngü kurun, ROI’yi dinamik olarak (ör. şablon algılamaya dayalı) hesaplayın ve sonuçları CSV’ye kaydedin.  
- **Template Matching:** Birden fazla fatura düzeniyle çalışıyorsanız, `template_id → ROI coordinates` haritasını JSON’da tutun. Hızlı bir düzen sınıflandırıcısıyla ROI’yi değiştirin.  
- **Parallel Execution:** `concurrent.futures.ThreadPoolExecutor` kullanarak birden çok OCR örneğini aynı anda çalıştırın—yüksek hacimli back‑office hatları için mükemmel.  
- **Confidence Filtering:** Çoğu OCR sonucu bir güven skoru içerir. Belirli bir eşik (ör. %85) altındaki sonuçları atın ve manuel inceleme için işaretleyin.

---

## Sonuç

**ocr region of interest**, **load image for OCR**, **extract text from rectangle** ve sonunda **recognize text from invoice** adımlarını kapsayan her şeyi ele aldık; klasik **how to extract amount** sorusuna yanıt bulduk. Betik kompakt, ancak farklı belge formatları, diller ve OCR arka uçlarıyla uyum sağlayacak kadar esnek.

Temelleri kavradığınıza göre, iş akışını genişletmeyi düşünün: barkod tarama ekleyin, bir PDF ayrıştırıcıyla bütünleştirin ya da çıkarılan tutarı bir muhasebe API’sine gönderin. ROI iyi tanımlandığı sürece her zaman daha hızlı ve temiz sonuçlar elde edeceksiniz.

Bir sorunla karşılaşırsanız, aşağıya yorum bırakın—iyi OCR’lamalar!

![ocr bölgesi örneği](https://example.com/ocr_roi_example.png "ocr bölgesi örneği")


## Sonraki Öğrenmeniz Gerekenler

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}