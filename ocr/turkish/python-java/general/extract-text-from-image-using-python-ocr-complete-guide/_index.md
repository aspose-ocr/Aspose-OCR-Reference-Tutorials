---
category: general
date: 2026-06-06
description: Dakikalar içinde Python OCR ile görüntüden metin çıkarın. Çok dilli görüntü
  OCR'ını keşfedin, otomatik dil tespiti OCR'ını ve OCR metnini doğru bir şekilde
  nasıl çıkaracağınızı öğrenin.
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: tr
og_description: Python OCR ile görüntüden hızlıca metin çıkarın. Çok dilli görüntü
  OCR'ını, otomatik dil algılamalı OCR'ı ve OCR metnini adım adım nasıl çıkaracağınızı
  öğrenin.
og_title: Python OCR Kullanarak Görüntüden Metin Çıkarma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: Python OCR Kullanarak Görüntüden Metin Çıkarma – Tam Rehber
url: /tr/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma – Python OCR Tam Kılavuz

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz mu, ama hangi kütüphanenin birden fazla dili otomatik olarak işleyebileceğinden emin olmadınız mı? Yalnız değilsiniz—geliştiriciler uluslararası belgeler, makbuzlar veya taranmış broşürlerle çalışırken *OCR metni nasıl çıkarılır* sorusunu sürekli soruyor. Bu öğreticide, yalnızca bir görüntüden metin çıkarmakla kalmayıp aynı zamanda **dili anlık olarak algılayan** pratik bir Python örneği üzerinden çok dilli görüntü OCR'ını nasıl kolayca yapabileceğinizi göstereceğiz.

OCR paketinin kurulumundan **otomatik dil algılama OCR** özelliğini etkinleştirmeye, örnek bir resim üzerinde motoru çalıştırmaya ve sonunda hem algılanan dili hem de çıkarılan dizeyi yazdırmaya kadar her şeyi ele alacağız. Sonunda, ister bir çeviri hattı ister veri‑işleme servisi kuruyor olun, herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Görüntüden Metin Çıkarma – Ortamı Hazırlama

Koda geçmeden önce çalışma ortamınızın aşağıdaki minimum gereksinimleri karşıladığından emin olun:

- Python 3.8 ve üzeri (kütüphane, eski sürümlerin göz ardı ettiği tip ipuçları kullanıyor)
- `pip` paket yönetimi için
- En az iki farklı dilde (ör. İngilizce + İspanyolca) metin içeren bir görüntü dosyası

Bu demoyu çalıştırmak için OCR kütüphanesine de ihtiyacınız olacak. Bu rehberde, gerçek dünyada popüler olan Tesseract veya EasyOCR gibi araçları yansıtan, ancak temiz bir Python API'si sunan hayali `ocr` paketini kullanacağız.

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **Pro ipucu:** İzin hataları alırsanız komutu `python -m` ile ön ekleyin ya da bir sanal ortam kullanın—global site‑paketlerinizi düzenli tutar.

## OCR Motoru Örneği Oluşturma

Kütüphane hazır olduğuna göre, ilk mantıklı adım **bir OCR motoru örneği oluşturmak**tır. Motoru, görüntüleri beslemeden önce yapılandırabileceğiniz akıllı bir tarayıcı olarak düşünün.

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

Motoru ayrı bir nesne olarak örneklemek, statik bir metod çağırmaktan neden daha iyidir? Motor nesnesi, (dil tercihleri gibi) yapılandırma durumunu tutar ve bu sayede birden çok görüntüde aynı ayarları yeniden kullanabilir, her seferinde yeniden başlatma maliyetinden kaçınabilirsiniz.

## Otomatik Dil Algılama OCR'ı Etkinleştirme

Çoğu OCR aracı, `eng` İngilizce, `spa` İspanyolca gibi bir dil kodu belirtmenizi ister. Dili manuel tahmin etmek, **çok dilli görüntü OCR** akışının amacına aykırıdır. Neyse ki, `ocr` paketi, görüntüyü inceleyip sahne arkasında en uygun dil modelini seçen bir *otomatik dil algılama OCR* modu sunar.

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

Bu şekilde **dil algılama OCR**'ı etkinleştirmek, uzun bir dil kodu listesi tutmanız gerekmediği anlamına gelir. Motor, gördüğü alfabeyi—Latin, Kiril, Han vb.—eşleştirir ve uygun modeli otomatik olarak yükler.

## Çok Dilli Görüntü OCR'ı Gerçekleştirme

Motor hazır olduğuna göre, **görüntüden metin çıkarma** zamanıdır. `recognize_image` metodu bir dosya yolu alır ve hem ham metni hem de algılanan dili içeren bir sonuç nesnesi döndürür.

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

*PDF'den OCR metni nasıl çıkarılır* diye merak ediyorsanız, aynı motor `recognize_pdf` sunar—sadece metod adını değiştirin. Altındaki algılama mantığı aynı kalır, böylece aynı **otomatik dil algılama OCR** özelliğinden yararlanırsınız.

## Algılanan Dil ve Çıkarılan Metni Görüntüleme

Son olarak, motorun bulduklarını ekrana bastırıyoruz. Sonuç nesnesi `detected_language` (ör. `en` veya `es` gibi bir BCP‑47 etiketi) ve `text` (ham OCR çıktısı) özelliklerini sunar.

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

Örnek görüntümüz üzerinde scripti çalıştırdığınızda aşağıdakine benzer bir çıktı almanız gerekir:

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

Motorun İngilizce'yi birincil dil olarak doğru bir şekilde tanımladığını, aynı zamanda İspanyolca satırı da yakaladığını göreceksiniz—bu, sağlam bir **çok dilli görüntü OCR** çözümünden beklediğiniz tam olarak budur.

### Algılama Başarısız Olursa Ne Olur?

Bazen görüntü bulanık ya da alfabe çok egzotik olduğunda OCR motoru varsayılan bir dile (genellikle İngilizce) geri dönebilir. Bu gibi durumlarda bir dil listesi zorlayabilirsiniz:

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

Ancak unutmayın, dilleri zorlamak **otomatik dil algılama OCR**'ın rahatlığını ortadan kaldırır; bu yüzden yalnızca bilinen bir dil alt kümesi olduğunda kullanın.

## Yaygın Tuzaklar ve OCR Metnini Güvenilir Çıkarma

Otomatik algılamaya rağmen, birkaç küçük sorun işinizi zorlaştırabilir:

1. **Düşük çözünürlüklü görüntüler** – OCR doğruluğu 150 dpi altında hızla düşer. Görüntüyü büyütün ya da daha yüksek çözünürlüklü bir tarama isteyin.
2. **Gürültü ve sıkıştırma artefaktları** – Görüntüyü motora vermeden önce basit bir eşik filtresi (`opencv` veya `Pillow`) uygulayın.
3. **Tek sayfada karışık alfabeler** – Bazı motorlar aynı anda Latin ve CJK karakterlerini işlemek konusunda zorlanır. Gerekirse sayfayı bölüp ayrı bölgelere ayrı ayrı tanıma uygulayın.

Bu sorunları ele almak, **görüntüden metin çıkarma** sürecinin kalitesini büyük ölçüde artırır, özellikle gerçek dünya çok dilli belgelerle çalışırken.

## Tam Çalışan Örnek

Aşağıda, tartıştığımız tüm adımları birleştiren, çalıştırmaya hazır tam script yer alıyor. `multilingual_ocr.py` olarak kaydedin ve komut satırından çalıştırın.

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Beklenen çıktı** (örnek görüntünün İngilizce ve İspanyolca metin içerdiği varsayılırsa):

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

`multilang_page.png` dosyasını, içinde başka dillerde metin bulunan herhangi bir resimle değiştirmekten çekinmeyin—**otomatik dil algılama OCR** sayesinde script hâlâ mantıklı bir dil etiketi ve ilgili metni sağlayacaktır.

![Görüntüden metin çıkarma örneği](https://example.com/ocr-sample.png "Görüntüden metin çıkarma")

## Sonuç

Artık bir görüntüden **OCR metni nasıl çıkarılır**, **otomatik dil algılama OCR** nasıl etkinleştirilir ve **çok dilli görüntü OCR** senaryoları minimum kodla nasıl yönetilir, biliyorsunuz. Bir OCR motoru örneği oluşturup, otomatik dil algılamayı açıp `recognize_image` çağırarak hem dil tanımlayıcısını hem de ham metni güvenilir bir şekilde alabilirsiniz.

Sırada ne var? Çıkarılan dizeleri bir çeviri API'sine gönderin, aranabilir bir veri tabanına kaydedin ya da birden fazla sayfayı tek bir PDF raporunda birleştirin. Aynı yüksek‑seviye iş akışını koruyarak farklı OCR arka uçları (Tesseract, EasyOCR, Google Vision) ile de deneyler yapabilirsiniz—**dil algılama OCR** arayüzünün tutarlılığı sayesinde.

Herhangi bir tuhaflıkla karşılaşırsanız, “Yaygın Tuzaklar” bölümüne geri dönün ya da görüntü ön‑işleme adımlarını ayarlayın. Kodlamanın tadını çıkarın ve bir sonraki projenizin doğru‑algılanan, kusursuz‑çıkarılan metinlerle dolu olmasını dileriz!


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Resmi Metne Dönüştür – URL'den Görüntü Üzerinde OCR Yap](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Resimden Metin Çıkarma – Aspose.OCR ile .NET için OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Aspose OCR ile birden fazla dilde metin tanıma](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}