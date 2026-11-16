---
category: general
date: 2026-04-26
description: Python'un OCR motorunu kullanarak el yazısı metni tanıyın. Görüntüden
  metin nasıl çıkarılır, el yazısı modu nasıl açılır ve el yazısı notları nasıl hızlıca
  okunur öğrenin.
draft: false
keywords:
- recognize handwritten text
- extract text from image
- read handwritten notes
- turn on handwritten mode
- create OCR engine python
language: tr
og_description: Python ile el yazısı metni tanıyın. Bu öğreticide, görüntüden metin
  nasıl çıkarılır, el yazısı modu nasıl etkinleştirilir ve basit bir OCR motoru kullanarak
  el yazısı notlar nasıl okunur gösterilmektedir.
og_title: Python’da el yazısı metni tanıma – Tam OCR Rehberi
tags:
- OCR
- Python
- Handwriting Recognition
title: Python'da el yazısı metni tanıma – OCR Motoru Öğreticisi
url: /tr/python/general/recognize-handwritten-text-in-python-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da el yazısı metni tanıma – OCR Motoru Öğreticisi

Hiç **el yazısı metni tanıma** ihtiyacı hissettiniz ama “nereden başlamalıyım?” sorusunda takıldınız mı? Tek başınıza değilsiniz. Toplantı notlarını dijitalleştiriyor ya da taranmış bir formdan veri çekiyor olun, güvenilir bir OCR sonucu elde etmek bir unicorn peşinde koşmak gibi hissettirebilir.  

İyi haber: sadece birkaç Python satırıyla **extract text from image** dosyalarından metin çıkarabilir, **turn on handwritten mode** özelliğini açabilir ve sonunda **read handwritten notes** yapabilirsiniz, karmaşık kütüphaneler aramadan. Bu rehberde **create OCR engine python** tarzı kurulumdan sonucu ekranda yazdırmaya kadar tüm süreci adım adım göstereceğiz.

## Öğrenecekleriniz

- `ocr` paketini kullanarak **create OCR engine python** örneği oluşturmayı.  
- Hangi dil ayarının yerleşik el yazısı desteği sağladığını.  
- Motorun el yazısı ile çalıştığını bilmesi için **turn on handwritten mode** çağrısının tam şeklini.  
- Bir not fotoğrafını nasıl besleyeceğinizi ve **recognize handwritten text** yapmayı.  
- Farklı görüntü formatlarıyla başa çıkma, yaygın sorunları giderme ve çözümü genişletme ipuçları.

Gereksiz şeyler yok, “belgelere bak” gibi çıkmazlar yok—sadece bugün kopyalayıp yapıştırıp test edebileceğiniz tam, çalıştırılabilir bir betik.

## Önkoşullar

İlerlemeye başlamadan önce şunların olduğundan emin olun:

1. Python 3.8+ yüklü (kod f‑string kullanıyor).  
2. Hayali `ocr` kütüphanesi (`pip install ocr‑engine` – kullandığınız gerçek paket adıyla değiştirin).  
3. El yazısı bir notun net bir görüntü dosyası (JPEG, PNG veya TIFF çalışır).  
4. Biraz merak—diğer her şey aşağıda ele alınmıştır.

> **Pro tip:** Görüntünüz gürültülü ise, OCR motoruna göndermeden önce Pillow ile hızlı bir ön işleme adımı (ör. `Image.open(...).convert('L')`) uygulayın. Bu genellikle doğruluğu artırır.

## Python ile el yazısı metni nasıl tanımlarsınız

Aşağıda **creates OCR engine python** nesnelerini oluşturan, el yazısı için yapılandıran ve çıkarılan dizeyi ekrana yazdıran tam betik yer alıyor. Betiği `handwriting_ocr.py` olarak kaydedin ve terminalinizden çalıştırın.

```python
# handwriting_ocr.py
import ocr                     # The OCR library that provides OcrEngine
import os

def main():
    # Step 1: Create an OCR engine instance
    # This is the core object that will do all the heavy lifting.
    ocr_engine = ocr.OcrEngine()

    # Step 2: Choose a language that includes handwritten support.
    # EXTENDED_LATIN covers most Western alphabets and knows how to
    # handle cursive strokes.
    ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)

    # Step 3: Turn on handwritten mode.
    # Without this flag the engine assumes printed text and will miss
    # most of the nuances in a scribble.
    ocr_engine.enable_handwritten_mode(True)

    # Step 4: Define the path to your handwritten image.
    # Replace the placeholder with the actual location of your file.
    image_path = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")

    # Basic validation – makes debugging easier.
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 5: Recognize text from the image.
    # The recognize_image method returns a result object that holds
    # both the raw text and confidence scores.
    handwritten_result = ocr_engine.recognize_image(image_path)

    # Step 6: Display the extracted text.
    # This is where you finally **read handwritten notes** programmatically.
    print("=== Extracted Text ===")
    print(handwritten_result.text)

if __name__ == "__main__":
    main()
```

### Beklenen Çıktı

Betik başarıyla çalıştığında, aşağıdakine benzer bir şey göreceksiniz:

```
=== Extracted Text ===
Meeting notes:
- Discuss quarterly targets
- Assign tasks to Alice & Bob
- Follow‑up email by Friday
```

OCR motoru herhangi bir karakter algılayamazsa, `text` alanı boş bir dize olacaktır. Bu durumda, görüntü kalitesini iki kez kontrol edin veya daha yüksek çözünürlüklü bir tarama deneyin.

## Adım‑Adım Açıklama

### Adım 1 – **create OCR engine python** örneği

`OcrEngine` sınıfı giriş noktasıdır. Boş bir not defteri gibi düşünün—hangi dili bekleyeceğini ve el yazısı ile mi çalıştığını söyleyene kadar hiçbir şey gerçekleşmez.

### Adım 2 – El yazısını destekleyen bir dil seçin

`ocr.Language.EXTENDED_LATIN` sadece “İngilizce” değildir. Latin temelli bir dizi betiği bir araya getirir ve kritik olarak, el yazısı örnekleriyle eğitilmiş modelleri içerir. Bu adımı atlamak, motorun varsayılan olarak basılı metin modelini kullanması nedeniyle bozuk çıktılara yol açar.

### Adım 3 – **turn on handwritten mode**

`enable_handwritten_mode(True)` çağrısı iç bir bayrağı değiştirir. Motor, gerçek dünyadaki notlarda gördüğünüz düzensiz boşluklar ve değişken çizgi kalınlıkları için ayarlanmış sinir ağına geçer. Bu satırı unutmak yaygın bir hatadır; motor notlarınızı gürültü olarak değerlendirir.

### Adım 4 – Görüntüyü besleyin ve **recognize handwritten text**

`recognize_image` ağır işi yapar: bitmap'i ön işler, el yazısı modelinden geçirir ve `text` özelliğine sahip bir nesne döndürür. Kalite ölçütüne ihtiyacınız varsa `handwritten_result.confidence` değerini de inceleyebilirsiniz.

### Adım 5 – Sonucu yazdırın ve **read handwritten notes**

`print(handwritten_result.text)` başarılı bir şekilde **extract text from image** yaptığınızı doğrulamanın en basit yoludur. Üretimde muhtemelen dizeyi bir veritabanına kaydeder veya başka bir servise iletirsiniz.

## Kenar Durumları ve Yaygın Varyasyonların Ele Alınması

| Situation | What to Do |
|-----------|------------|
| **Görüntü döndürülmüş** | `recognize_image` çağırmadan önce Pillow ile döndürün (`Image.rotate(angle)`). |
| **Düşük kontrast** | Gri tonlamaya çevirin ve adaptif eşikleme uygulayın (`Image.point(lambda p: p > 128 and 255)`). |
| **Birden fazla sayfa** | Dosya yolu listesi üzerinde döngü yapın ve sonuçları birleştirin. |
| **Latin dışı betikler** | `EXTENDED_LATIN` yerine `ocr.Language.CHINESE` (veya uygun) kullanın ve `enable_handwritten_mode(True)` satırını koruyun. |
| **Performans endişeleri** | Birçok görüntüde aynı `ocr_engine` örneğini yeniden kullanın; her seferinde başlatmak ek yük getirir. |

### Bellek kullanımıyla ilgili pro ipucu

Yüzlerce notu toplu olarak işliyorsanız, işiniz bittiğinde `ocr_engine.dispose()` çağırın. Bu, Python sarmalayıcısının tutabileceği yerel kaynakları serbest bırakır.

## Hızlı Görsel Özet

![el yazısı metni tanıma örneği](https://example.com/handwritten-note.png "el yazısı metni tanıma örneği")

*Yukarıdaki görüntü, betiğimizin düz metne dönüştürebileceği tipik bir el yazısı notu göstermektedir.*

## Tam Çalışan Örnek (Tek‑Dosya Betiği)

Kopyala‑yapıştır sadeliğini sevenler için, açıklayıcı yorumlar olmadan tüm betiği tekrar sunuyoruz:

```python
import ocr, os

ocr_engine = ocr.OcrEngine()
ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)
ocr_engine.enable_handwritten_mode(True)

img = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")
if not os.path.isfile(img):
    raise FileNotFoundError(f"Image not found: {img}")

result = ocr_engine.recognize_image(img)
print("=== Extracted Text ===")
print(result.text)
```

Run it with:

```bash
python handwriting_ocr.py
```

Artık konsolunuzda **recognize handwritten text** çıktısını görmelisiniz.

## Sonuç

Python'da **recognize handwritten text** yapmak için ihtiyacınız olan her şeyi ele aldık—yeni bir **create OCR engine python** çağrısı, doğru dili seçmek, **turn on handwritten mode** ve sonunda **extract text from image** yaparak **read handwritten notes**.

Tek, bağımsız bir betikle toplantı karalama fotoğrafından temiz, aranabilir metne geçebilirsiniz. Sonra, çıktıyı bir doğal dil işleme hattına beslemeyi, aranabilir bir indeksde saklamayı ya da seslendirme üretimi için bir transkripsiyon servisine geri göndermeyi düşünebilirsiniz.

### Buradan Sonra Nereye Gidilir?

- **Toplu işleme:** Betiği bir döngü içinde sararak bir klasördeki taramaları işleyin.  
- **Güvenilirlik filtresi:** Düşük kaliteli okumaları atmak için `result.confidence` kullanın.  
- **Alternatif kütüphaneler:** `ocr` tam uyumlu değilse, el yazısı modu için `--psm 13` parametresiyle `pytesseract`'ı keşfedin.  
- **UI entegrasyonu:** Flask veya FastAPI ile birleştirerek web tabanlı bir yükleme hizmeti sunun.

Belirli bir görüntü formatı hakkında sorularınız mı var ya da modeli ayarlamakta yardıma mı ihtiyacınız var? Aşağıya bir yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}