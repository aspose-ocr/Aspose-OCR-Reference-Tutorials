---
category: general
date: 2026-03-26
description: Arapça PNG görüntülerinde OCR çalıştırmayı ve Arapça metni hızlı bir
  şekilde çıkarmayı öğrenin. Bu rehber, adım adım Python kodu ile görüntüyü metne
  dönüştürmeyi gösterir.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: tr
og_description: Arapça PNG görüntülerinde OCR nasıl çalıştırılır? Arapça metni çıkarmak,
  tanımak ve görüntüyü Python kullanarak metne dönüştürmek için bu kapsamlı rehberi
  izleyin.
og_title: Arapça PNG'de OCR Nasıl Çalıştırılır – Görüntüden Metin Çıkarma
tags:
- OCR
- Python
- Arabic
title: Arapça PNG'de OCR Nasıl Çalıştırılır – Görüntüden Metin Çıkarma
url: /tr/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arapça PNG Üzerinde OCR Çalıştırma – Görüntüden Metin Çıkarma

Arapça metin içeren bir görüntüde **OCR nasıl çalıştırılır** diye hiç merak ettiniz mi? Belki taranmış bir makbuz, tarihi bir el yazması ya da sadece bir sosyal medya gönderisinin ekran görüntüsüne sahipsiniz ve metni aranabilir bir formatta ihtiyacınız var. Tek başınıza değilsiniz—dünya çapındaki geliştiriciler, sağ‑dan‑sol dillerle çalışırken bu sorunu sıkça yaşarlar.

Bu öğreticide, bir PNG dosyasında **OCR nasıl çalıştırılır** gösteren, Arapça metni çıkaran ve sonucu konsola yazdıran eksiksiz, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Belirsiz “belgelere bakın” bağlantıları yok; sadece kopyalayıp‑yapıştırabileceğiniz kod ve her satırın neden önemli olduğuna dair açıklamalar. Sonunda, kaynak zor bir Arapça PNG olsa bile **görüntüyü metne dönüştürme** işlemini güvenilir bir şekilde yapabilecek olacaksınız.

> **Neler öğreneceksiniz**
> - Arapça için bir Python OCR motoru kurma  
> - PNG görüntüsü yükleme ve yaygın tuzakları ele alma  
> - Arapça metni tanıma ve çıktıyı doğrulama  
> - Farklı görüntü kalitelerinden **Arapça metin çıkarma** ipuçları  

Başlamadan önce, Python 3.8+ yüklü olduğundan ve `ocr` kütüphanesinin (örnek kodda kullanılan) güncel bir sürümüne sahip olduğunuzdan emin olun. Sanal ortam kullanıyorsanız, şimdi etkinleştirin—bu, bağımlılıkların düzenli kalmasını sağlar.

## Gereksinimler

- Python 3.8 veya daha yeni bir sürüm  
- `ocr` paketi (`pip install ocr‑engine` – gerçek paket adıyla değiştirin)  
- Referans alabileceğiniz bir yerde konumlandırılmış bir Arapça PNG görüntüsü (`arabic_doc.png`)  
- Python fonksiyonları ve sınıfları hakkında temel bilgi  

Hepsi bu. Ağır çerçeveler yok, Docker konteynerleri yok—sadece saf Python.

## Adım 1: OCR Kütüphanesini Kurma ve İçe Aktarma

İlk iş olarak, OCR motoruna ihtiyacımız var. Kullanacağımız kütüphane, basit bir API'ye sahip `OcrEngine` sınıfını sunar.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*`Imaging`'i ayrı ayrı neden içe aktarıyoruz?* `Imaging` alt modülü, PNG, JPEG ve TIFF formatlarını kutudan çıkar çıkmaz anlayan kullanışlı bir `Image.load` yöntemi sağlar. Bu adımı atlamak, ham baytları kendiniz işlemenizi gerektirir; bu çoğu kullanım senaryosu için gereksizdir.

## Adım 2: OCR Motoru Örneğini Oluşturma

Şimdi motorun bir örneğini oluşturuyoruz. Bu nesneyi, görüntüyü işleyecek “beyin” olarak düşünün.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro ipucu:** Ardışık olarak birçok görüntü işleyecekseniz, aynı `ocr_engine` örneğini yeniden kullanın. Dil modellerini önbelleğe alır, bu da sonraki tanıma işlemlerini hızlandırır.

## Adım 3: Dili Arapça Olarak Ayarlama

Arapça Latin alfabesi değildir; kendi karakter setine, sağ‑dan‑sol yönüne ve bağlamsal şekillendirmeye sahiptir. Bu yüzden motorun hangi dil modelini yükleyeceğini açıkça belirtmemiz gerekir.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Bu satırı unutursanız, motor varsayılan olarak İngilizceyi kullanır ve karışık bir çıktı alırsınız—bunu çok sık gördüm.

## Adım 4: PNG Görüntünüzü Yükleyin

İşte **görüntüyü metne dönüştürme** kısmının gerçekten başladığı yer. Arapça metin içeren PNG dosyasını yükleyeceğiz.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Yaygın Kenar Durumları

| Sorun | Belirti | Çözüm |
|-------|---------|-----|
| Görüntü çok karanlık | Çıktı birçok boşluk içeriyor | Pillow ile ön işleme (`ImageEnhance.Brightness`) |
| PNG bir alfa kanalı içeriyor | Bazı OCR motorları şeffaf pikselleri yanlış okur | Yüklemeden önce RGB'ye dönüştür (`image.convert("RGB")`) |
| Metin döndürülmüş | Tanınan metin ters görünüyor | Motor'a göndermeden önce görüntüyü döndür (`image.rotate(90, expand=True)`) |

## Adım 5: Tanıma İşlemini Çalıştırma

Tüm ayarlar yapıldıktan sonra, motoru işini yapması için son olarak çağırıyoruz.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

`recognize` metodu, **ham Unicode dizesi**, güven skorları ve sınırlama kutuları içeren bir nesne döndürür. Çoğu geliştirici için düz metin yeterlidir.

## Adım 6: Tanınan Arapça Metni Çıktılamak

Şimdi sonucu yazdırıyoruz. Gerçek bir uygulamada, bir dosyaya, veritabanına yazabilir ya da bir çeviri API'sine besleyebilirsiniz.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Betik çalıştırıldığında, konsolunuzda Arapça karakterlerin görüntülendiğini görmelisiniz (terminalinizin Unicode desteklediğinden emin olun). Eğer soru işaretleri ya da boş dizeler görürseniz, dil ayarını ve görüntü kalitesini tekrar kontrol edin.

### Beklenen Çıktı

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Eğer çıktı yukarıdaki satıra benzer görünüyorsa, tebrikler—bir PNG'den başarıyla **Arapça metin çıkardınız**!

## Tam Çalışan Örnek

Aşağıda, kopyalayıp‑yapıştırmaya hazır tam betik yer alıyor. `YOUR_DIRECTORY/arabic_doc.png` ifadesini kendi dosyanızın yolu ile değiştirin.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

`python run_ocr.py` (veya dosyanıza verdiğiniz ad) ile çalıştırın. Her şey doğru kurulduysa, Arapça cümleyi konsola yazdırılmış olarak göreceksiniz.

## Farklı Görüntü Formatlarında OCR Çalıştırma

Aynı kod JPEG, TIFF veya BMP için de çalışır—sadece dosya uzantısını değiştirin. `Image.load` metodu formatı otomatik olarak algılar, böylece **görüntüyü metne dönüştürme** için ekstra bir kod eklemenize gerek kalmaz.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Unutmayın, kaynak görüntünün kalitesi **Arapça metni tanıma** adımının doğruluğunu büyük ölçüde etkiler. Yüksek çözünürlük, düşük sıkıştırmalı görüntüler en iyi sonuçları verir.

## PNG'den Metin Çıkarma: Daha İyi Doğruluk İçin İpuçları

1. **DPI Önemlidir** – En az 300 dpi hedefleyin. Daha düşük DPI genellikle karakter kaçırılmasına yol açar.  
2. **Kontrast Krallıktır** – Görüntüyü OCR motoruna vermeden önce kontrastı artırmak için görüntü işleme araçlarını (ör. OpenCV) kullanın.  
3. **Gürültü Giderme** – Küçük lekeler modeli şaşırtabilir; medyan filtreleme yardımcı olur.  

İşte OCR'dan önce bir PNG'yi iyileştirmek için Pillow kullanan hızlı bir kod parçacığı:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Sıkça Sorulan Sorular

**S: Bu, Arapça dışındaki sağ‑dan‑sol dillerde de çalışır mı?**  
C: Kesinlikle. Dil kodunu değiştirmeniz yeterli (`"ar"` → İbranice için `"he"`, Farsça için `"fa"`), motor uygun modeli yükleyecektir.

**S: Bir klasördeki birden fazla PNG'den metin çıkarmam gerekirse ne yapmalıyım?**  
C: Dosyalar üzerinde döngü kurun, aynı `ocr_engine` örneğini yeniden kullanın ve sonuçları bir listede toplayın ya da her birini ayrı bir `.txt` dosyasına yazın.

**S: Her kelime için güven skorları alabilir miyim?**  
C: Evet. `ocr_result` genellikle bir `get_confidences()` metodu sunar. Kalite kontrolü için her güven skorunu ilgili kelimeyle eşleştirin.

## Sonraki Adımlar

Artık Arapça PNG'lerde **OCR nasıl çalıştırılır** bildiğinize göre, aşağıdaki takip fikirlerini değerlendirin:

- **Toplu işleme:** Betiği `os.listdir` ile birleştirerek bir dizindeki tüm dosyalardan **Arapça metin çıkarın**.  
- **Son‑işleme:** PDF'lerde sağ‑dan‑sol çıktıyı doğru göstermek için `arabic_reshaper` ve `python-bidi` kütüphanelerini kullanın.  
- **Entegrasyon:** Çıkarılan metni bir arama indeksine (ör. Elasticsearch) besleyerek taranmış belgeleri aranabilir hâle getirin.

Bu konular, burada ele alınan temeller üzerine inşa edilir ve basit bir **görüntüyü metne dönüştürme** betiğini üretime hazır bir iş akışına dönüştürmenize yardımcı olur.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}