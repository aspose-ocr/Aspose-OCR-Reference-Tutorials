---
category: general
date: 2026-01-12
description: Aspose OCR kullanarak görüntülerde dili nasıl tespit edersiniz – görüntüden
  metin çıkarmayı öğrenin, karışık dil OCR'ını yönetin ve Python’da OCR kullanın.
draft: false
keywords:
- how to detect language
- extract text from image
- how to extract text
- how to use OCR
- mixed language OCR
language: tr
og_description: Aspose OCR kullanarak görüntülerde dili nasıl tespit edersiniz – görüntüden
  metin çıkarmak ve karışık dil OCR'ını yönetmek için adım adım rehber.
og_title: Karışık Metin için OCR ile Dil Nasıl Tespit Edilir
tags:
- OCR
- Python
- Aspose
title: Karışık Metinlerde OCR ile Dil Nasıl Tespit Edilir
url: /tr/python-java/general/how-to-detect-language-with-ocr-for-mixed-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Karışık Metinlerde OCR ile Dili Nasıl Algılayabilirsiniz

Görsellerde Aspose OCR kullanarak dili algılamak, çok dilli belgelerle çalışırken yaygın bir zorluktur. Aynı sayfada hem İngilizce hem de Fransızca içeren bir **görüntüden metin nasıl çıkarılır** diye hiç merak ettiniz mi? Bu öğreticide, OCR'ı dili tanımlamak, metni çekmek ve karışık‑dil senaryolarını sorunsuz bir şekilde ele almak için nasıl kullanacağınızı tam olarak gösteren çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz.

İhtiyacınız olan her şeyi kapsayacağız: Aspose OCR motorunu kurma, hangi dilleri dikkate alacağını belirtme, örnek bir fatura görüntüsü yükleme, OCR sürecini çalıştırma ve sonunda tespit edilen dili çıkarılan metinle birlikte yazdırma. Sonunda, “karışık dil OCR'ı nasıl kullanılır” sorusuna kendi projelerinizde yanıt verebileceksiniz; ister bir fatura iş akışı, bir fiş tarayıcısı ya da bir belge arşivleme aracı geliştirin.

> **Önkoşullar** – Python 3.8+ yüklü olmalı, pip hakkında temel bilgiye sahip olmalı ve bir Aspose OCR lisansına (deneme sürümü bu demo için yeterli) sahip olmalısınız. Başka harici kütüphane gerekmez.

---

## Aspose OCR ile Dili Nasıl Algılayabilirsiniz

İlk adım, bir OCR motoru örneği oluşturmak ve hangi dilleri araması gerektiğini belirtmektir. Aspose OCR, dilleri birleştirmek için bir bit‑mask kullanır; bu sayede İngilizce, Fransızca, İspanyolca ya da ihtiyacınız olan herhangi bir kombinasyonu desteklemek kolaydır.

```python
# Step 1: Import Aspose OCR and create an OCR engine instance
import asposeocr as ocr

# Create the engine; this object will drive the whole process
ocr_engine = ocr.OcrEngine()
```

**Neden önemli:** Motoru başlatmak temeldir. Bunu yapmadan hiçbir OCR metodunu çağıramazsınız ve motor, daha sonra **dili algılamak** için gerekli tüm yapılandırmayı tutar.

---

## OCR Kullanarak Görüntüden Metin Çıkarma

Şimdi motorun hangi dillerin mümkün olduğunu bilmesi gerekiyor. `ENGLISH | FRENCH` bit‑maskını ayarlayarak motorun görüntünün her bölgesi için en iyi eşleşmeyi otomatik olarak seçmesini sağlarız.

```python
# Step 2: Tell the engine which languages to consider and enable auto‑detection
ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.FRENCH   # bit‑mask of possible languages
ocr_engine.auto_detect_language = True                         # let the engine pick the best match
```

**Neden önemli:** `auto_detect_language` özelliğini etkinleştirmek, karışık‑dil bir belgede **dili nasıl algılayacağınız** sorusunun özüdür. Motor metni tarar, her dili puanlar ve en yüksek güvene sahip olanı döndürür. Bu adımı atlayıp dili kendiniz tahmin etmeye çalışırsanız, karışık dil OCR'ının amacını boşa çıkarmış olursunuz.

---

## Karışık Dil OCR Ayarlarını Yapılandırma

Motoru bir görüntüye beslemeden önce, görüntüyü yüklememiz gerekir. Aspose OCR, temel dosya formatını soyutlayan kendi `Image` sınıfını kullanır.

```python
# Step 3: Load the image that contains mixed‑language text
invoice_image = ocr.Image.load("YOUR_DIRECTORY/mixed_lang_invoice.png")
```

> **İpucu:** En iyi sonuçlar için görüntü çözünürlüğünü yaklaşık 300 dpi tutun. Daha düşük çözünürlükler, özellikle aksanlı Fransızca harflerde, dil algılamasının ince karakterleri kaçırmasına neden olabilir.

---

## OCR Sürecini Çalıştırma ve Sonuçları Alma

Motor yapılandırıldı ve görüntü yüklendi, artık OCR sürecini çalıştırabiliriz. `process` metodu, tespit edilen dil kodunu ve tam çıkarılan metni içeren bir `OcrResult` nesnesi döndürür.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(invoice_image)

# Step 5: Display the detected language and extracted text
print("Detected language:", ocr_result.language)   # e.g. ENGLISH or FRENCH
print("Extracted text:", ocr_result.text)
```

**Beklenen çıktı**

```
Detected language: ENGLISH
Extracted text: Invoice #12345
Date: 01/02/2026
Total: $1,250.00
...
```

Görüntü Fransızca bölümler içeriyorsa, tespit edilen dil olarak `FRENCH` görür ve ilgili Fransızca metin ekrana yazdırılır.

---

## Görsel Örneği (SEO için Alt Metin)

![how to detect language in mixed language OCR image](mixed_lang_invoice.png)

*Yukarıdaki ekran görüntüsü, hem İngilizce hem de Fransızca metin içeren örnek bir faturayı gösterir; OCR motorunun **dili algılayabildiğini** ve içeriği tek bir geçişte çıkarabildiğini ortaya koyar.*

---

## Yaygın Tuzaklar ve Pro İpuçları

| Sorun | Neden Oluşur | Nasıl Çözülür / Hafifletilir |
|-------|--------------|------------------------------|
| **Bulanık veya düşük‑çözünürlüklü taramalar** | Motor karakterleri ayırt edemez, bu da yanlış dil algılamasına yol açar. | ≥300 dpi tarayın, OCR'dan önce görüntü keskinleştirme uygulayın. |
| **Bit‑maskta eksik dil** | Bir dili eklemeyi unutursanız, motor ilk eşleşmeye döner ve genellikle hatalı sonuç verir. | Beklediğiniz her dili mutlaka listeleyin; `|` operatörüyle birden çok dili birleştirebilirsiniz. |
| **Karışık betikler (ör. Latin + Kiril)** | Aspose OCR ek dil paketlerine ihtiyaç duyabilir. | Ek dil paketlerini kurun ve maskeye ekleyin. |
| **Büyük dosyalar bellek dalgalanmalarına neden olur** | Devasa bir görüntüyü belleğe yüklemek script'in çökmesine yol açabilir. | DPI'yi koruyarak `Image.resize` ile ölçek küçültün veya görüntüyü parçalar halinde işleyin. |

**Pro ipucu:** Ham metni aldıktan sonra, boşlukları ve satır sonlarını normalleştiren hızlı bir post‑işleme adımı çalıştırın. Bu, sonraki aşamalarda (ör. fatura numarası çıkarma) çok daha basit bir ayrıştırma sağlar.

---

## Özet: Öğrendikleriniz

Artık Aspose OCR kullanarak karışık‑dil bir görüntüde **dili nasıl algılayacağınızı** biliyorsunuz ve **görüntüden metin nasıl çıkarılır** sorusunun tam bir uçtan uca örneğini gördünüz. Dil bit‑maskını yapılandırarak, otomatik algılamayı etkinleştirerek ve sonuç nesnesini işleyerek, İngilizce ve Fransızca (veya diğer diller) karışımı içeren faturaları, fişleri veya herhangi bir belgeyi güvenilir bir şekilde işleyebilirsiniz.

### Sonraki Adımlar

- PDF'lerden **metin çıkarma** işlemini, her sayfayı önce bir görüntüye dönüştürerek deneyin.  
- Diğer ikincil anahtar kelimeleri keşfedin: daha hızlı işleme için OCR bölgeleri ayarlama gibi tam **how to use OCR** API yüzeyini inceleyin.  
- Üç veya daha fazla dil arasında geçiş yapan **karışık dil OCR** gibi daha karmaşık senaryolara dalın.

Kodu istediğiniz gibi değiştirin, kendi görüntülerinizde test edin ve motorun ağır işi yapmasına izin verin. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}