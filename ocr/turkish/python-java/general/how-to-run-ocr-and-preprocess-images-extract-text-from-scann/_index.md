---
category: general
date: 2026-04-26
description: Tarama yapılan bir formda OCR nasıl çalıştırılır, gürültüyü azaltmak
  için görüntüyü nasıl ön işleme tabi tutacağınızı öğrenin ve görüntüden hızlıca metin
  çıkarın.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: tr
og_description: Tarama belgelerinde OCR nasıl çalıştırılır, görüntüler nasıl ön işlenir,
  gürültü nasıl azaltılır ve metin verimli bir şekilde nasıl çıkarılır.
og_title: OCR Nasıl Çalıştırılır ve Görüntüler Nasıl Ön İşlenir – Hızlı Rehber
tags:
- OCR
- image processing
- Python
title: OCR Nasıl Çalıştırılır ve Görüntüler Nasıl Ön İşlenir – Taralı Formlardan Metin
  Çıkarma
url: /tr/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Nasıl Çalıştırılır – Görsellerden Metin Çıkarma İçin Tam Kılavuz

Hiç **OCR nasıl çalıştırılır** diye merak ettiniz mi, dağınık taranmış bir formdan temiz, aranabilir metin elde etmek? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede ham görüntü, lekeler, dengesiz aydınlatma ve OCR’ın kutudan çıktığı gibi zorlanmasına neden olan diğer tuhaflıklarla dolu.  

İyi haber? Sadece birkaç satır Python ve akıllı bir ön‑işleme hattı ile tanıma doğruluğunu büyük ölçüde artırabilir, **gürültüyü azaltabilir** ve ihtiyacınız olan tam kelimeleri çıkarabilirsiniz. Bu öğreticide, resmi yüklemekten son dizeyi yazdırmaya kadar her adımı adım adım göstereceğiz—bu sayede faturalar, makbuzlar veya herhangi bir taranmış belgeye uyarlayabileceğiniz hazır bir kod parçacığı elde edeceksiniz.

## Ne Oluşturacaksınız

- Alt OCR kütüphanesiyle iletişim kuran bir `OcrEngine` örneği.  
- Görüntüyü **ikili**leştiren ve lekeleri yumuşatmak için **median blur** uygulayan bir ön‑işleme zinciri.  
- `process()` metodunu çağırarak `text` özelliği üzerinden çıkarılan dizeyi döndüren basit bir çağrı.  

Sonunda, herhangi bir görüntü dosyası üzerinde çalıştırabileceğiniz ve çıktıyı doğrudan konsolda görebileceğiniz bağımsız bir betiğiniz olacak.

## Ön Koşullar

- Python 3.9+ (burada kullanılan sözdizimi en son kararlı sürümle uyumludur).  
- Kurgusal `aocr` paketi – Tesseract ya da modern bir OCR motorunun ince bir sarmalayıcısı gibi düşünün. `pip install aocr` ile kurun.  
- Referans verebileceğiniz bir klasörde bulunan taranmış bir görüntü (`scanned_form.jpg`).  

Gerçek bir OCR kütüphanesi olan `pytesseract` kullanıyorsanız, `OcrEngine` sınıfını uygun sınıfla değiştirebilirsiniz—diğer her şey aynı kalır.

![](how-to-run-ocr-example.png "OCR nasıl çalıştırılır örneği: taranmış bir form ve çıkarılan metin")

*Alt metin: OCR nasıl çalıştırılır bir taranmış belgede ve çıkarılan metni görüntüleme.*

---

## Adım 1: OCR Nasıl Çalıştırılır – Motoru Başlatma

Motor bir şey okuyabilmeden önce bir örnek oluşturmalıyız. `OcrEngine`i, daha sonra görsel veriyi yorumlayacak beyin olarak düşünün.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Neden önemli:** Motorun örneklenmesi, iç modelleri kurar, dil paketlerini yükler ve çalışma ortamını hazırlar. Bu adımı atlamak, `process()` çağırdığınızda genellikle `NoneType` hatasına yol açar.

---

## Adım 2: Görüntüyü Ön‑İşleme – Taranmış Formunuzu Yükleyin

Beyin hazır olduğuna göre, ona bir resim veriyoruz. Görüntü, `aocr.Image` tarafından desteklenen herhangi bir formatta olabilir.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **İpucu:** Geliştirme sırasında mutlak yollar kullanın; böylece betik farklı bir çalışma dizininden çalıştırıldığında “dosya bulunamadı” hataları almazsınız.

---

## Adım 3: Gürültüyü Azaltma – İkilileştirme ve Median Blur Uygulama

Ham taramalar genellikle rastgele noktalar, dengesiz arka plan veya hafif gölgeler içerir. İki klasik hile—**ikilileştirme** ve **median blur**—karakter kenarlarını kaybetmeden görüntüyü temizler.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Daha Derine İnmek

- **İkilileştirme**: `threshold=180` değeri algoritmaya şunu söyler: “180’den daha parlak olanlar beyaz, geri kalanlar siyah olsun.” Taramanız çok karanlık ya da çok aydınlıksa bu sayıyı ayarlayın.  
- **Median Blur**: `2` yarıçapı, filtrenin 5×5 piksel penceresine bakıp merkez pikseli medyan değerle değiştirdiği anlamına gelir. Bu, izole lekeleri yumuşatırken harf darbelerini korur.

> **Köşe durumu:** Belgenizde renkli vurgulamalar varsa, basit bir ikili eşik bu renkleri silebilir. Bu durumda, `aocr.ImageFilters.adaptive_threshold()` kullanmayı düşünün—bu, eşik değerini görüntü boyunca yerel olarak ayarlar.

---

## Adım 4: Metin Çıkarma – OCR İşlemini Çalıştırma

Temiz bir görüntü elde ettiğimize göre, motorun sihrini şimdi serbest bırakıyoruz.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Arka planda ne oluyor?** Motor, piksel matrisinin üzerinden bir sinir ağı (veya eski desen eşleştirici) çalıştırır, tanınan her glifi Unicode karakterlerine çevirir ve bunları satır ve paragraf hâline getirir.

---

## Adım 5: Metin Çıkarma – Sonucu Yazdırma

`ocr_result` nesnesi kullanışlı bir `text` özelliği sunar. Şimdi ne elde ettiğimize bakalım.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Beklenen Çıktı

Eğer taranmış form şunları içeriyorsa:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Şu şekilde bir çıktı görmelisiniz:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Ön‑işleme adımının, daha önce “Amount” kelimesini “Am0unt” yapan izole noktaları nasıl ortadan kaldırdığını fark edin. Bu, OCR’dan **önce gürültüyü azaltma** gücüdür.

---

## Yaygın Tuzaklar & Çözüm Önerileri

| Belirti | Muhtemel Neden | Hızlı Çözüm |
|---------|----------------|-------------|
| Bozuk karakterler (örn. “@#%”) | Görüntü çok karanlık ya da çok aydınlık | `binarize()` içindeki `threshold` değerini ayarlayın; `adaptive_threshold` deneyin. |
| Eksik kelimeler | Gürültü hâlâ mevcut | `median_blur` için `radius` değerini artırın veya bir `gaussian_blur` filtresi ekleyin. |
| Yanlış dil (örn. İngiliz harfleri Çince’ye dönüşüyor) | Yanlış dil paketi yüklendi | Kütüphane destekliyorsa `OcrEngine()` oluştururken `language="eng"` parametresini geçin. |
| Büyük dosyalarda yavaş işlem | Yüksek çözünürlük | İkilileştirmeden önce görüntüyü küçültün: `aocr.ImageFilters.resize(width=1200)`. |

---

## Daha İleri – Sonraki Adımlar ve İlgili Konular

- **Toplu işleme**: Yukarıdaki mantığı bir döngüye sararak yüzlerce dosyayı otomatik olarak işleyin.  
- **Yapısal çıktı**: `ocr_result.text` üzerinde düzenli ifadeler kullanarak tarih veya tutar gibi alanları çekin.  
- **Alternatif kütüphaneler**: `aocr` yerine `pytesseract` kullanın—kod sadece motor başlatma adımında değişir.  
- **PDF’ler için görüntü ön‑işleme**: Her PDF sayfasını bir görüntüye dönüştürün, ardından aynı hattı uygulayın.  

Bu genişletmeler, çözümünüzü tek bir formdan kurumsal ölçekli belge alım hattına kadar ölçeklendirmenizi sağlar.

---

## Sonuç

**OCR nasıl çalıştırılır** konusunu baştan sona ele aldık, **görüntüyü ön‑işleme** ile **gürültüyü azaltma** yöntemlerini gösterdik ve **görüntüden metin çıkarma** için temiz, tekrarlanabilir bir betik sunduk. Ana çıkarım? Birkaç basit filtre—ikilileştirme ve median blur—gürültülü bir taramayı güvenilir bir veri kaynağına dönüştürerek saatlerce manuel temizlikten tasarruf sağlar.

Kendi belgelerinizle betiği deneyin, eşik değerlerini ayarlayın ve doğruluğun nasıl yükseldiğini izleyin. Hazır olduğunuzda toplu işleme keşfedin ya da çıktıyı bir veritabanına entegre ederek aranabilir arşivler oluşturun. İyi kodlamalar, OCR’ınız daima kusursuz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}