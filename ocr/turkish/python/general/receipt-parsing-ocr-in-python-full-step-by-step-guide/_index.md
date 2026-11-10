---
category: general
date: 2026-06-28
description: Python'da fiş ayrıştırma OCR'u kolaylaştırıldı – fiş verilerini nasıl
  çıkaracağınızı, görüntü OCR'u nasıl yükleyeceğinizi öğrenin ve eksiksiz bir Python
  OCR örneğini görün.
draft: false
keywords:
- receipt parsing OCR
- how to extract receipt
- python ocr example
- load image ocr
- how to ocr receipt
language: tr
og_description: 'Python’da fiş ayrıştırma OCR: fiş verilerini nasıl çıkaracağınızı,
  görüntü OCR’sini nasıl yükleyeceğinizi öğrenin ve dakikalar içinde tam bir Python
  OCR örneği çalıştırın.'
og_title: Python’da Makbuz Ayrıştırma OCR – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Receipt parsing OCR in Python made easy – learn how to extract receipt
    data, load image OCR, and see a complete python OCR example.
  headline: Receipt Parsing OCR in Python – Full Step‑By‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- receipt parsing
- image processing
title: Python ile Makbuz Ayrıştırma OCR – Tam Adım Adım Rehber
url: /tr/python/general/receipt-parsing-ocr-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Makbuz Ayrıştırma OCR – Tam Adım‑Adım Kılavuz

Hiç bulanık bir süpermarket makbuzunu temiz, aranabilir JSON'a nasıl dönüştürebileceğinizi merak ettiniz mi? **Receipt parsing OCR** cevaptır ve bunu çalıştırmak için bilgisayarlı görme alanında doktora derecesine ihtiyacınız yok. Bu öğreticide, bir görüntüyü yükleyen, yapılandırılmış metin tanıması yapan ve güzel biçimlendirilmiş bir JSON dizesi üreten pratik bir **python ocr example** üzerinden adım adım ilerleyeceğiz—bu, muhasebe yazılımına veya analiz boru hatlarına beslemek için mükemmeldir.

Ayrıca yanıt bekleyen soruyu da ele alacağız: **how to extract receipt** verilerini güvenilir bir şekilde nasıl çıkarılır, tarama mükemmel olmasa bile. Sonunda, kişisel finans uygulaması ya da kurumsal düzeyde bir gider takibi sistemi geliştiriyor olsanız da, herhangi bir Python projesine ekleyebileceğiniz yeniden kullanılabilir bir betiğe sahip olacaksınız.

## Neler Öğreneceksiniz

* Python'da hafif bir OCR motoru kurmayı öğrenin.  
* Bir makbuz dosyası için **load image OCR** adımlarını öğrenin.  
* Yapılandırılmış tanıma yöntemini nasıl çağıracağınızı ve sonucu JSON'a dönüştüreceğinizi öğrenin.  
* Yaygın kenar durumlarıyla—döndürülmüş makbuzlar, düşük kontrast ve Unicode karakterleri—nasıl başa çıkılacağına dair ipuçları.  
* Bugün çalıştırabileceğiniz, tamamen kopyala‑yapıştır hazır bir kod örneği.

### Önkoşullar

* Makinenizde yüklü Python 3.8 veya daha yeni bir sürüm.  
* `OcrEngine` sınıfı ve `Image` yardımcı sınıfı sağlayan bir OCR kütüphanesi (birçok kütüphane benzer API'ler sunar; bu kılavuzda genel bir sarmalayıcı varsayacağız).  
* Referans alabileceğiniz bir klasöre yerleştirilmiş bir makbuz görüntüsü (`receipt.png`).  
* İsteğe bağlı ama önerilen: görüntü işleme için `pip install pillow` ve OCR kütüphanenizin ihtiyaç duyduğu diğer bağımlılıklar.  

Eğer bunlardan herhangi birine sahip değilseniz, şimdi kurun—hiç sorun değil, çoğu paket için tek satırlık bir komut.

---

## Receipt Parsing OCR – Adım 1: Gerekli Modülleri Kurun ve İçe Aktarın

İlk olarak, Python ortamını hazırlayalım. Serileştirme için `json` ve OCR‑özel sınıfları içe aktaracağız.

```python
# Step 1: Import required modules
import json                     # Built‑in JSON handling
from ocr_library import OcrEngine, Image   # Replace with your actual library
```

*Neden önemli*: En üstte içe aktarmak betiği düzenli tutar ve OCR motorunun her yerde kullanılabilir olmasını sağlar. `json`'ı içe aktarmayı unutursanız, sonraki `json.dumps` çağrısı bir `NameError` ile patlayacaktır.

**Pro ipucu**: OCR kütüphaneniz farklı bir ad alanında (ör. `easyocr` veya `pytesseract`) bulunuyorsa, içe aktarma satırını buna göre ayarlayın. Öğreticinin geri kalanı aynı kalır.

---

## How to Extract Receipt Data – Adım 2: OCR Motoru Örneğini Oluşturun

Şimdi motoru başlatıyoruz. `OcrEngine()`'i makbuzu okuyacak beyin olarak düşünün.

```python
# Step 2: Create an OCR engine instance
engine = OcrEngine()
```

Çoğu modern OCR SDK'sı burada dil paketlerini veya algılama modlarını yapılandırmanıza izin verir. Tipik bir makbuz için İngilizce (veya makbuzun dili) ve mümkünse “structured” (yapılandırılmış) modunu tercih edersiniz.

> **Not**: Kütüphaneniz bir lisans anahtarı gerektiriyorsa, bunu argüman olarak geçirin: `engine = OcrEngine(api_key="YOUR_KEY")`.

---

## Load Image OCR – Adım 3: Motoru Makbuzunuza Yönlendirin

Motor hazır olduğunda, ona görüntü dosyasını vermemiz gerekir. İşte **load image OCR** burada devreye girer.

```python
# Step 3: Load the image to be processed
engine.set_image(Image.from_file("YOUR_DIRECTORY/receipt.png"))
```

*Ne oluyor*: `Image.from_file` PNG (veya JPG, TIFF, vb.) dosyasını okur ve OCR motorunun anlayabileceği bir formatta paketler. Makbuzunuz PDF ise, önce ilk sayfayı bir görüntüye dönüştürün—birçok kütüphane `pdf2image` yardımcı işlevi sunar.

**Kenar durumu**: Makbuzlar ters taranmış olsa bile, döndürdüğünüzde okunabilir olacaktır:

```python
# Optional: auto‑rotate if needed
image = Image.from_file("YOUR_DIRECTORY/receipt.png")
image = image.rotate(180) if image.is_upside_down() else image
engine.set_image(image)
```

---

## How to OCR Receipt – Adım 4: Yapılandırılmış Metin Tanımasını Çalıştırın

Şimdi sihir gerçekleşir. Motoru, öğeleri, toplamları ve tarihleri gruplamaya çalışan bir yapılandırılmış tarama yapması için istiyoruz.

```python
# Step 4: Perform structured text recognition
result = engine.recognize_structured()
```

OCR kütüphaneniz sadece basit bir `recognize()` yöntemi sunuyorsa, alanları hâlâ manuel olarak çıkarabilirsiniz, ancak `recognize_structured()` genellikle `items`, `total` ve `date` gibi anahtarlar içeren bir sözlük döndürür.

---

## Python OCR Example – Adım 5: Sonucu JSON'a Dönüştürün

Ham sonuç nesnesi genellikle özel bir sınıftır. Bunu düz bir Python sözlüğüne dönüştürmek, serileştirmeyi kolaylaştırır.

```python
# Step 5: Convert the recognition result to a nicely formatted JSON string
json_str = json.dumps(result.to_dict(), ensure_ascii=False, indent=2)
```

*Neden `ensure_ascii=False`?* Makbuzlar para birimi simgeleri (€, £) veya aksanlı karakterler içerebilir. Bu bayrak, karakterleri `\u00e9` gibi kaçış dizilerine dönüştürmek yerine korur.

---

## How to Extract Receipt – Adım 6: JSON Temsilini Çıktılayın

Son olarak, JSON'ı yazdırıyoruz (veya dosyaya kaydediyoruz) böylece bir veritabanına, bir elektronik tabloya veya bir API'ye yönlendirebilirsiniz.

```python
# Step 6: Output the JSON representation of the recognized data
print(json_str)
```

**Beklenen çıktı** (okunabilirlik için güzel biçimlendirilmiş):

```json
{
  "merchant": "Coffee House",
  "date": "2024-03-15",
  "items": [
    {"name": "Latte", "quantity": 1, "price": "3.50"},
    {"name": "Bagel", "quantity": 2, "price": "4.00"}
  ],
  "subtotal": "7.50",
  "tax": "0.60",
  "total": "8.10"
}
```

Eğer boş bir sözlük veya eksik alanlar görürseniz, makbuz görüntüsünün net olduğundan ve OCR motorunun doğru dile ayarlandığından emin olun.

---

## Pro İpuçları & Yaygın Tuzaklar (Bonus Bölüm)

| Sorun | Neden Olur | Hızlı Çözüm |
|-------|------------|-------------|
| **Bulanık veya düşük kontrastlı görüntü** | OCR, gürültü nedeniyle zorlanır | OpenCV ile ön işleme yapın: `cv2.threshold` veya `cv2.bilateralFilter` |
| **Döndürülmüş makbuz** | Motor, metnin dik durduğunu varsayar | `engine.detect_orientation()` ile yön tespit edin veya manuel olarak döndürün (Adım 3'e bakın) |
| **Latin olmayan karakterler** | Yanlış dil paketi | İspanyolca vb. için motoru `language="spa"` ile başlatın |
| **Büyük makbuzlar bellek hatasına neden olur** | Tüm görüntü bir kerede yüklendiği için | İlgili bölgeye kırpın: `engine.set_image(image.crop((x, y, w, h)))` |

---

## Sıradaki Adım? İş Akışını Genişletin

Python'da **receipt parsing OCR** konusunda uzmanlaştınız. İş akışını sürdürmek için birkaç fikir:

* **Batch processing** – bir klasördeki makbuz görüntüleri üzerinde döngü yapın ve her JSON'ı bir ana dosyaya ekleyin.  
* **Database insertion** – her makbuzu bir satır olarak saklamak için `sqlite3` veya `SQLAlchemy` kullanın.  
* **Machine‑learning enrichment** – çıkarılan öğeleri gider etiketleme için bir sınıflandırma modeline besleyin.  

Bunların hepsi, ele aldığımız temel adımlara dayanır ve her biri aynı **python ocr example** desenini içerir: yükle → tanı → serileştir → depola.

---

## Sonuç

Bu rehberde Python'da tam bir **receipt parsing OCR** iş akışını adım adım inceledik, **how to extract receipt** bilgisini, **load image OCR** nasıl yapılacağını gösterdik ve bugün çalıştırabileceğiniz işlevsel bir **python ocr example** sunduk. Altı adımı—kurulum, içe aktarma, örnekleme, yükleme, tanıma ve serileştirme—takip ederek artık herhangi bir makbuz işleme projesi için sağlam bir temele sahipsiniz.

Denemekten çekinmeyin: farklı OCR motorlarını deneyin, ön işleme ayarlarını değiştirin veya eksik alanlar için hata yönetimi ekleyin. Güvenilir OCR'yi Python'un esnekliğiyle birleştirdiğinizde sınır yoktur. Sorularınız veya bu tarif üzerine ilginç bir yaklaşımınız mı var? Aşağıya bir yorum bırakın, sohbeti sürdürelim.

Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüyü OCR Nasıl Yapılır – OCR Görüntü Tanıma’da Görüntü Üzerinde OCR Gerçekleştirme](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}