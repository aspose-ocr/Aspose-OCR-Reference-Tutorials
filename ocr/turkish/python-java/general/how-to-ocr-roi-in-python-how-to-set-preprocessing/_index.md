---
category: general
date: 2026-03-28
description: Python'da ROI'yi OCR'lamak – Belirli görüntü bölgelerinden doğru metin
  çıkarımı için ön işleme seçeneklerini nasıl ayarlayacağınızı öğrenin.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: tr
og_description: Python'da ROI OCR Nasıl Yapılır – Bu kılavuz, tanımlı görüntü bölgelerinden
  güvenilir metin çıkarımı için ön işleme nasıl ayarlanacağını gösterir.
og_title: Python'da ROI'yi OCR'lamak – Ön işleme nasıl ayarlanır
tags:
- OCR
- Python
- Aspose
title: Python'da ROI'yi OCR'lamak – Ön işleme nasıl ayarlanır
url: /tr/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da ROI’yi OCR’lamak – Ön İşleme Nasıl Ayarlanır

Gürültülü bir fatura görüntüsünde **ROI’yi OCR’lamak** için tüm sayfayı belleğe almadan nasıl yapılacağını hiç merak ettiniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede sadece birkaç alana ihtiyacımız var—müşteri adı, adres, toplamlar—bu yüzden belgenin tamamını taramak gereksiz.  

İyi haber? Aspose OCR ile motorun **nerede bakacağını** tam olarak belirtebilir ve hatta önce görüntüyü temizlemesini isteyebilirsiniz. Bu öğreticide **ön işleme** seçeneklerini nasıl ayarlayacağınızı, İlgi Alanları (ROIs) tanımlamayı ve sadece birkaç Python satırıyla temiz metin çıkarmayı adım adım göstereceğiz.

Bu rehberin sonunda, herhangi bir fatura, makbuz veya formdan belirli blokları çıkaran, çalıştırmaya hazır bir betiğiniz olacak. Ek bir araç gerekmez, sadece Aspose OCR ve biraz Python mantığı.

---

## Gereksinimler

- **Python 3.8+** (kod, herhangi bir yeni sürümde çalışır)  
- **Aspose OCR for Python via .NET** – `pip install aspose-ocr` ile kurun  
- Referans alabileceğiniz bir örnek görüntü (ör. `invoice.png`) bir klasörde bulunmalı  
- Python fonksiyonları ve nesne‑yönelimli sözdizimi hakkında temel bilgi  

Eğer bunlara sahipseniz, harika—kod kısmına doğrudan geçelim.

---

![ROI’yi OCR’lama diyagramı](ocr-roi.png "ROI’yi OCR’lama örneği")

*Alt metin: bir fatura görüntüsü üzerindeki ROI kutularını gösteren ROI’yi OCR’lama diyagramı*

---

## Adım 1 – OCR Motorunu Başlatma (ROI’yi OCR’lamak)

Motorun *nerede* bakacağını söyleyebilmemiz için bir OCR işlemci örneğine ihtiyacımız var. Bu nesne tüm yapılandırmayı tutar ve tanıma işlemini yürütür.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Neden önemli*: `OcrEngine` sınıfı ağır işleri (yazı tipi algılama, düzen analizi vb.) soyutlar. Tek bir motor oluşturarak her görüntü için ağır kaynakları yeniden başlatmazsınız, bu da performansı hızlı tutar.

---

## Adım 2 – Kaynak Görüntünüzü Yükleyin (ROI’yi OCR’lamak)

Aspose Storage, görüntü yüklemeyi zahmetsiz hâle getirir. Dosya yolunu gösterin, işlemeye hazır bir `Image` nesnesi elde edin.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*İpucu*: Akışlarla (ör. bir web API üzerinden yüklenen görüntüler) çalışıyorsanız, `Image.load` metoduna dosya yolu yerine bir `BytesIO` nesnesi verebilirsiniz.

---

## Adım 3 – İlgi Alanlarını (ROIs) Tanımlayın

Şimdi temel soruya yanıt veriyoruz: **ROI’yi OCR’lamak** için motorun veri içerdiği kesin dikdörtgenleri belirtiyoruz. Her ROI, sol‑üst köşesi (`x`, `y`) ve boyutu (`width`, `height`) ile tanımlanır.

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*ROI’leri neden kullanmalı?*  
- **Hız** – Motor, görüntünün ilgisiz bölümlerini atlar.  
- **Doğruluk** – Küçük bir alana odaklanarak, diğer yerlerdeki gürültü tanıyıcıyı şaşırtamaz.  
- **Esneklik** – İhtiyacınız kadar ROI ekleyebilirsiniz; motor aynı sırada bir sonuç listesi döndürür.

---

## Adım 4 – Daha İyi OCR Doğruluğu İçin Ön İşlemeyi Nasıl Ayarlarsınız

Tarayıcılardan veya telefonlardan gelen görüntüler genellikle eğik, düşük kontrastlı veya dengesiz aydınlatmalı olur. Aspose OCR, tanıma çalıştırılmadan önce yaygın düzeltmeleri etkinleştirmenizi sağlayan bir `PreprocessingOptions` nesnesi sunar.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Bu nasıl yardımcı olur*:  
- **Deskew** karakter şekillerini belirsiz kılan eğimi ortadan kaldırır.  
- **Binarize** renk gürültüsünü azaltır, OCR motoruna temiz bir ikili görüntü verir.  
- **Contrast** soluk çizgileri güçlendirir; bu, solmuş makbuzlar için özellikle faydalıdır.

Bu bayraklarla deney yapın—birini kapatın ve çıktının değişip değişmediğine bakın. İşte **ön işleme nasıl ayarlanır** sorusunun etkili cevabı.

---

## Adım 5 – Tanımlı ROIs İçinde Sadece OCR Yapın

Motor, görüntü, ROIs ve ön işleme hazır olduğunda `recognize` metodunu çağırma zamanı. Metod, `regions` koleksiyonunu içeren bir `OcrResult` nesnesi döndürür—her giriş, sağladığınız ROI sırasına karşılık gelir.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Sahne arkası*: Motor her ROI’yı kırpar, ön işleme hattını uygular ve temizlenmiş parçacık üzerinde tanıma modelini çalıştırır. Listeyi gönderdiğimiz için sonuç aynı sırada kalır, bu da son‑işlemeyi basitleştirir.

---

## Adım 6 – Çıkarılan Metni Okuyun ve Kullanın (ROI’yi OCR’lamak)

Son olarak, `regions` listesini döngüye alıp tanınan stringleri yazdırın—ya da saklayın. `Region` nesnesi, Unicode sonucu tutan bir `text` özelliği sunar.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Beklenen çıktı (örnek)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Metin karışık görünüyorsa, **ön işleme nasıl ayarlanır** kısmına geri dönün: belki `contrast` değerini artırın ya da renkli logolar için `binarize`ı devre dışı bırakın.

---

## Yaygın Tuzaklar ve Pro İpuçları

| Sorun | Neden Oluşur | Çözüm (Ön İşleme Nasıl Ayarlanır) |
|-------|--------------|-----------------------------------|
| Eğik metin anlamsız çıkar | `deskew` kapalı veya görüntü çok döndürülmüş | `preprocessing_options.deskew = True` |
| Sayılar nokta ya da rastgele işaret olur | Düşük kontrast veya agresif ikilileştirme | `contrast` değerini düşürün (ör. `1.2`) veya `binarize = False` |
| ROI koordinatları birkaç piksel kayıyor | Farklı DPI veya tarayıcı ölçeklemesi | Paint.NET gibi bir araçla tam piksel konumlarını ölçün, ya da her ROI’ya küçük bir kenar boşluğu (`+5` piksel) ekleyin |
| Bir bölge boş sonuç veriyor | ROI görüntü sınırları dışına çıkıyor | Görüntü boyutlarını kontrol edin: `source_image.width`, `source_image.height` |

---

## Çözümü Genişletmek (Farklı Senaryolarda ROI’yi OCR’lamak)

- **Dinamik ROIs**: Faturalarınız değişken düzenlere sahipse, önce hızlı bir tam‑sayfa OCR çalıştırıp “Customer:”, “Address:” gibi anahtar kelimeleri bulun ve ardından ROIs’ları anlık olarak hesaplayabilirsiniz.  
- **Toplu İşleme**: Yukarıdaki adımları bir fonksiyona paketleyip bir klasördeki görüntüler üzerinde döngü kurun. Bellek kullanımını düşük tutmak için aynı `ocr_engine` örneğini yeniden kullanın.  
- **JSON’a Dışa Aktarma**: Yazdırmak yerine bir sözlük oluşturup `json.dumps` ile dökün; bu, ERP sistemi gibi bir sonraki entegrasyonu çok basitleştirir.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Sonuç

Artık **ROI’yi OCR’lamak** için tam, çalıştırılabilir bir örneğe sahipsiniz ve **ön işleme nasıl ayarlanır** konusunda uzmanlaştınız. Motoru sadece ihtiyacınız olan dikdörtgenlerle sınırlayarak ve görüntüyü önceden temizleyerek daha hızlı, daha temiz sonuçlar elde edersiniz—fatura otomasyonu, form dijitalleştirme veya sayfanın sadece bir dilimini işlemek istediğiniz her senaryo için ideal.

Bir sonraki adıma hazır mısınız? Farklı bir belge türü için ROI koordinatlarını ayarlamayı deneyin ya da `sharpen` veya `noise_reduction` gibi ek ön işleme bayraklarıyla oynayın. Aspose OCR’un esnekliği, neredeyse her görüntü kalitesine uyacak bir pipeline oluşturmanıza olanak tanır.

Bir sorunla karşılaşırsanız, boş bölgeler için konsol çıktısını kontrol edin ve ön işleme ayarlarını yeniden gözden geçirin. Kodlamanın tadını çıkarın, OCR’unuz her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}