---
category: general
date: 2026-03-26
description: Python’da OCR nasıl yapılır ve görüntü dosyalarından metin nasıl tanınır
  öğrenin. Bu rehber, PNG’den metin çıkarmayı ve görüntüyü hızlı bir şekilde metne
  dönüştürmeyi gösterir.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: tr
og_description: Python'da OCR nasıl yapılır? Görüntüden metin tanıma, PNG'den metin
  çıkarma ve deneme lisansı ile görüntüyü metne dönüştürme konusunda bu rehberi izleyin.
og_title: Python'da OCR Nasıl Yapılır – Tam Kılavuz
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR Nasıl Yapılır – Tam Adım Adım Öğretici
url: /tr/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Nasıl Yapılır – Tam Adım‑Adım Öğretici  

Telefonunuzla yeni çektiğiniz bir resimde **OCR nasıl yapılır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler her yerde, karmaşık yerel kütüphanelerle uğraşmadan görüntü dosyalarından metin tanımanın güvenilir bir yoluna ihtiyaç duyuyor.  

Bu öğreticide, hafif bir Python sarmalayıcı kullanarak **OCR nasıl yapılır**, **recognize text from image** ve **extract text from PNG** gösteren uygulamalı bir örnek üzerinden ilerleyeceğiz. Sonunda sadece birkaç satır kodla **convert image to text** yapabilecek ve yerleşik deneme modunu kullandığımız için lisans sıkıntısı yaşamayacaksınız.  

## Öğrenecekleriniz  

* OCR motoru için deneme lisansını nasıl ayarlayacağınızı (dosya yolu gerekmez).  
* **recognize text from image** nesnelerine yapılan tam çağrı sırasını.  
* **extract text from PNG** dosyalarını nasıl çıkaracağınızı ve eksik fontlar gibi yaygın sorunları nasıl ele alacağınızı.  
* Deneme lisansından üretim lisansına geçerken çözümü ölçeklendirme ipuçları.  

**Önkoşullar** – Python 3.8+ ve `ocr` paketi (`pip install ocr` ile kurulabilir) gerekir. Başka bir dış araç gerekmez.  

---  

![OCR nasıl yapılır örneği](https://example.com/ocr-demo.png "Python’da OCR nasıl yapılır – tanınan metin gösterildi")  

*Görsel alt metni: Python’da OCR nasıl yapılır – örnek çıktı*  

## Adım 1 – Deneme Lisansını Etkinleştirme (Dosya Yolu Gerekmez)  

Motorun bir şey okuyabilmesi için geçerli bir lisansa ihtiyacı vardır. Deneme modu, deneyler ve küçük projeler için mükemmeldir.  

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Why this matters:* Lisans nesnesi OCR kütüphanesine bir sandbox içinde çalıştığınızı bildirir. Bu adımı atlayarsanız, motor `recognize()` çağrısında `LicenseError` hatası verir.  

**Pro tip:** Ücretli bir lisansa geçerken, yukarıdaki iki satırı `ocr.License("path/to/your/license.key").apply()` ile değiştirin.  

## Adım 2 – OCR Motoru Örneğini Oluşturma  

Deneme lisansı aktif olduğuna göre, ana motoru örnekleyelim. Bu, görüntüyü inceleyip karakterlerin nerede olduğunu belirleyecek “beyin” gibidir.  

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Why this matters:* `OcrEngine`, dil paketleri ve DPI ayarları gibi yapılandırmaları tutar. Daha sonra bunları ayarlayabilirsiniz, ancak varsayılan ayar çoğu yalnızca İngilizce PNG için yeterlidir.  

## Adım 3 – İşlemek İstediğiniz PNG’yi Yükleyin  

Burada **recognize text from image** işlemini gerçekleştiriyoruz. `ocr.Imaging.Image.load()` metodu PNG, JPEG, BMP ve birkaç başka formatı destekler.  

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* PNG’niz indeksli bir palet (ekran görüntüleri için yaygın) kullanıyorsa, yükleyici otomatik olarak 24‑bit RGB tamponuna dönüştürür. Bu dönüşüm çok küçük bir performans kaybına yol açabilir, ancak doğru OCR sonuçlarını garanti eder.  

## Adım 4 – OCR’ı Çalıştırın ve Metni Alın  

Son olarak motoru çalıştırıp düz metin sonucunu alıyoruz.  

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Beklenen çıktı** (\"Hello World\" içeren basit bir görüntü örneği):  

```
Hello World
```

Görüntü birden fazla satır içeriyorsa, çıktı satır sonlarını korur; bu sayede CSV ayrıştırıcıları veya NLP boru hatları gibi sonraki süreçlere kolayca beslenebilir.  

## Opsiyonel: Daha İyi Doğruluk İçin İnce Ayar  

* **Dil paketleri:** `ocr_engine.set_language("eng")` (varsayılan) veya Fransızca için `"fra"`.  
* **DPI ölçekleme:** `ocr_engine.set_dpi(300)` düşük çözünürlüklü taramalarda sonuçları iyileştirebilir.  
* **Ön‑işleme:** `set_image` öncesinde ikili eşikleme (`ocr.Imaging.Image.threshold()`) uygulamak, gürültülü arka planlarda daha temiz metin elde etmenizi sağlar.  

Bu ayarlamalar, hızlı bir demo’dan yüzlerce dosyayı günde işleyen üretim‑düzeyi **ocr tutorial python** çözümüne geçerken faydalıdır.  

## Tam Betik – Kopyala & Yapıştır Hazır  

Aşağıda tüm adımları birleştiren, çalıştırılabilir tam betik yer alıyor. `run_ocr.py` olarak kaydedin ve `YOUR_DIRECTORY/sample1.png` kısmını kendi PNG dosyanızın yolu ile değiştirin.  

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Komut satırından çalıştırın:  

```bash
python run_ocr.py
```

Çıktı olarak konsola çıkarılan metni görmelisiniz. Boş bir dize alırsanız, görüntünün gerçekten net, yüksek kontrastlı metin içerdiğini ve deneme lisansının hatasız uygulandığını tekrar kontrol edin.  

## Yaygın Sorular & Tuzaklar  

* **“Bu JPEG ile çalışır mı?”** – Kesinlikle. `load()` yöntemi formatı otomatik algılar, bu yüzden kod değişikliği yapmadan PNG’yi JPEG ile değiştirebilirsiniz.  
* **“Görüntü döndürülmüşse ne olur?”** – Motor yönü otomatik algılayabilir, ancak en iyi sonuçlar için `set_image` öncesinde `input_image.rotate(90)` ile önceden döndürebilirsiniz.  
* **“Bir döngüde birden fazla görüntüyü işleyebilir miyim?”** – Evet. Yükleme ve `recognize()` çağrılarını bir `for` döngüsü içine taşımanız yeterli; aynı `ocr_engine` örneği yeniden kullanılabilir, bu da az bir ek yük tasarrufu sağlar.  

## Sonraki Adımlar – Demo’dan Üretime  

Şimdi **OCR nasıl yapılır** bildiğinize göre şu ek konuları inceleyin:  

* **Toplu işleme** – Bu betiği `os.listdir()` ile birleştirerek toplu olarak **extract text from PNG** dosyalarından metin çıkarın.  
* **PDF ile Entegrasyon** – PDF sayfalarını PNG’ye dönüştürmek için `pdf2image` kullanın, ardından aynı pipeline’a besleyin.  
* **Son‑işleme** – Yaygın OCR hatalarını (ör. “0” vs “O”) temizlemek için regex veya bulanık eşleştirme uygulayın.  

Bu adımlar, **convert image to text** temel fikrini genişleterek OCR iş akışınızın faydasını artırır.  

---  

### TL;DR  

Python’da **OCR nasıl yapılır** konusundaki her şeyi kapsadık: deneme lisansını etkinleştirin, bir motor oluşturun, PNG’yi yükleyin, tanıma işlemini çalıştırın ve sonucu yazdırın. Birkaç satır kodla **recognize text from image**, **extract text from PNG** ve **convert image to text** işlemlerini gerçekleştirebilir, ardından istediğiniz uygulamaya yönlendirebilirsiniz. DPI veya dil ayarlarını değiştirin, motorun ağır işini size bıraksın. İyi kodlamalar!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}