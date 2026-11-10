---
category: general
date: 2026-06-28
description: Python'da OCR için otomatik döndürme, ikilileştirme ve gürültü giderme
  ile görüntüyü ön işleme. Bir OCR motoru kullanarak yapılandırılmış JSON çıktısı
  alın.
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: tr
og_description: Python’da otomatik döndürme, ikilileştirme ve gürültü giderme ile
  OCR için görüntüyü ön işleme. Bir OCR motoru kullanarak yapılandırılmış JSON çıkarmayı
  öğrenin.
og_title: OCR için Görüntüyü Ön İşleme – Tam Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR için Görüntüyü Ön İşleme – Tam Python Rehberi
url: /tr/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Ön İşleme – Tam Python Rehberi

Görselin OCR için **preprocess image for OCR** (görüntüyü OCR için ön işleme) nasıl yapılır merak ettiniz mi? Tek başınıza değilsiniz—çoğu geliştirici, taranmış belgeleri bozuk çıktığında aynı duvara çarpar. İyi haber? Birkaç doğru adım—auto‑rotate, binarization ve denoising—dağınık bir fotoğrafı temiz, makine‑okunur metne dönüştürebilir.

Bu öğreticide, sadece görüntüyü temizlemekle kalmayıp aynı zamanda güzel yapılandırılmış bir JSON dosyası da sunan bir **Python** iş akışını adım adım inceleyeceğiz. Sonuna kadar OCR için bir görüntüyü auto‑rotate nasıl yapılır, OCR için görüntü binarizasyonu nasıl uygulanır ve **OCR engine Python** örneğine beslemeden önce OCR görüntü verileri nasıl gürültüden arındırılır öğrenmiş olacaksınız.

## Gerekenler

- Python 3.9+ (herhangi bir yeni sürüm çalışır)
- `Pillow` görüntü işleme için (`pip install pillow`)
- `ocrutil` – OCR motorunu saran hayali bir yardımcı kütüphane (`pip install ocrutil` ile kurulur)
- Referans alabileceğiniz bir klasöre yerleştirilmiş örnek eğik görüntü (`skewed.jpg`)

Hepsi bu—ağır çerçeveler yok, GPU sihri yok. Sadece sade Python ve birkaç kullanışlı kütüphane.

## Adım 1: Görüntünüzü Yükleyin – OCR için Hazırlık

İlk iş: kalan işlem hattının üzerinde çalışabileceği bir görüntü nesnesine ihtiyacımız var.

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*Neden önemli:* Görüntüyü Pillow ile yüklemek, tüm orijinal piksel verilerini korumamızı sağlar; bu, daha sonra binarizasyon uyguladığımızda kritik öneme sahiptir. Bu adımı atlamak ya da düşük kaliteli bir yükleyici kullanmak OCR doğruluğunu zaten bozabilir.

## Adım 2: OCR için Görüntüyü Otomatik Döndürme (auto rotate image OCR)

Telefonla çekilen bir fotoğraf genellikle eğik ya da hatta ters olur. `ocrutil.auto_rotate` yardımcı fonksiyonu metin taban çizgisini algılar ve görüntüyü buna göre döndürür.

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*İpucu:* Belgelerinizin her zaman dik olduğunu biliyorsanız bu adımı atlayabilirsiniz, ancak gerçek dünyada “auto rotate image OCR” size çok fazla manuel temizlikten tasarruf sağlar.

## Adım 3: OCR için Görüntü Ön İşleme – Binarizasyon + Gürültü Giderme

Şimdi konunun özüne geliyoruz: **preprocess image for OCR**. En etkili iki yöntem şunlardır:

1. **Binarization** – resmi saf siyah‑beyaz hâle dönüştürmek, karakter kenarlarını keskinleştirir.
2. **Denoising** – OCR motorunun glif olarak algılayabileceği lekeleri kaldırır.

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

Bu adımdan sonra görüntüyü (ör. `img.show()`) incelerseniz, arka planla keskin bir kontrast fark edeceksiniz—iyi bir OCR motorunun tam istediği şey.

## Adım 4: OCR Motorunu Kurun (OCR engine Python)

Elinizde temiz bir görüntü olduğunda OCR motorunu örnekleyebiliriz. `ocrutil.OcrEngine` sınıfı, popüler bir açık kaynak OCR arka ucunu (Tesseract gibi) sarmalar ve dostane bir Python API'si sunar.

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*Neden bunu yapıyoruz:* Ön işlenmiş görüntüyü **OCR engine Python** nesnesine sağlamak, motorun size sunabileceğiniz en yüksek kalite verisiyle çalışmasını garanti eder; bu da doğrudan daha yüksek doğruluk anlamına gelir.

## Adım 5: Düz Metin Tanıma (Opsiyonel ama Kullanışlı)

Bazen sadece ham metne ihtiyacınız olur. Bu adım opsiyoneldir çünkü öğreticinin ana hedefi yapılandırılmış çıktı almak, ancak hızlı doğrulama kontrolleri için faydalıdır.

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

Orijinal belgeye benzeyen bir dize göreceksiniz, ancak herhangi bir düzen bilgisi olmadan. Metin bozuk görünüyorsa, ön işleme parametrelerini geri dönüp ayarlayın.

## Adım 6: Yapılandırılmış Veriyi Çıkar ve JSON Olarak Kaydet (OCR structured JSON output)

Modern OCR motorlarının gerçek gücü, düzen bilgilerini—tablolar, sütunlar ve hatta form alanları—döndürebilme yetenekleridir. `engine.recognize_structured()` tam da bunu yapar ve sonucu düzenli bir JSON dosyasına dökeceğiz.

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

JSON'un bir kesiti şöyle görünebilir:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*Bu size ne sağlar:* Veritabanına, bir API'ye veya raporlama aracına doğrudan besleyebileceğiniz makine‑okunur bir temsil—artık manuel kopyala‑yapıştır yok.

## Bonus: Görsel Onay (Alt Metinli Görüntü)

Aşağıda ön işleme hattının ön‑ve‑son anlık görüntüsü yer alıyor. Kontrastın nasıl arttığını ve gürültünün nasıl yok olduğunu fark edin.

![Preprocess image for OCR – original vs cleaned](/images/ocr_preprocess_example.png){: .align-center alt="preprocess image for OCR example"}

*Merak ediyorsanız:* `ocrutil.preprocess`'i kendi OpenCV rutininizle değiştirin ve yine aynı **preprocess image for OCR** felsefesini takip edeceksiniz—eşikleme, filtreleme, ardından besleme.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

- **Over‑binarizing:** Eşiği çok yüksek ayarlamak soluk karakterleri silebilir. Eksik harfler görürseniz, `ocrutil.preprocess` içinde eşiği düşürün.
- **Wrong DPI:** OCR motorları basılı materyal için ~300 dpi varsayar. Görüntünüz düşük çözünürlükteyse, ön işleme öncesinde ölçeklemeyi düşünün.
- **Skipping auto‑rotate:** 5 derece bile bir eğim satır tespitini bozabilir. “auto rotate image OCR” adımı ucuzdur ve ileride saatler süren hata ayıklamayı önler.

## İş Akışını Genişletme

Şimdi sağlam bir temeliniz olduğuna göre, şunları yapmak isteyebilirsiniz:

1. **Add language packs** (`engine.set_language('eng+spa')`) çok dilli belgeler için.  
2. **Integrate with Pandas** JSON tablolarını analiz için DataFrame'lere dönüştürmek.  
3. **Run batch processing** bir klasördeki görüntüler üzerinde döngü yaparak sonuçları bir ana JSON dosyasına eklemek.

Bu uzantıların tümü, motoru çağırmadan önce **preprocess image for OCR** temel fikrine dayanır.

## Sonuç

Python'da **preprocess image for OCR** nasıl yapılacağını yeni öğrendiniz—auto‑rotate, binarize, denoise ve sonunda temiz görüntüyü hem düz metin hem de zengin **OCR structured JSON output** üreten bir **OCR engine Python**'a teslim etmek. Bu adımları izleyerek tanıma oranlarını büyük ölçüde artıracak ve sonraki işlemler için hazır veriler elde edeceksiniz.

Bir üst seviyeye geçmeye hazır mısınız? Yerleşik `ocrutil.preprocess`'i özel bir OpenCV hattıyla değiştirin, farklı binarizasyon teknikleriyle deney yapın veya JSON'u bir raporlama panosuna besleyin. Gökyüzü sınırdır ve yeni inşa ettiğiniz temel, aynı görüntü‑kalitesi sorunlarına tekrar takılmanızı önleyecek.

Kodlamaktan keyif alın, ve OCR sonuçlarınız her zaman net olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [.NET için Aspose.OCR ile OCR Optimizasyonu – Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/)
- [OCR Görüntü Tanıma’da Eşik Değerini Nasıl Ayarlarsınız](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}