---
category: general
date: 2026-03-26
description: Bir OCR motorunda dili nasıl ayarlayacağınız ve görüntülerden el yazısı
  metni nasıl çıkaracağınız – görüntüyü metne dönüştürmek için adım adım öğretici.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: tr
og_description: Bir OCR motorunda dili nasıl ayarlayacağınızı ve görüntülerden el
  yazısı notları nasıl çıkaracağınızı öğrenin. Görüntüyü dakikalar içinde metne dönüştürmeyi
  keşfedin.
og_title: OCR İçin Dil Nasıl Ayarlanır – El Yazısı Metni Kolayca Çıkarın
tags:
- OCR
- Python
- Image Processing
title: OCR için Dil Nasıl Ayarlanır ve El Yazısı Metin Nasıl Çıkarılır – Tam Rehber
url: /tr/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Dil Nasıl Ayarlanır ve El Yazısı Metin Nasıl Çıkarılır – Tam Kılavuz

Hiç **dil ayarlamayı** OCR motorunuzda nasıl yapacağınızı merak ettiniz mi, böylece gerçekten ihtiyacınız olan karakterleri anlayabilsin? Belki bir market listesi, bir toplantı notu ya da karalanmış bir diyagram fotoğrafınız var ve metni çıkaramıyorsunuz. İyi haber? Bilgisayarlı görme alanında doktora yapmanıza gerek yok—sadece birkaç satır Python ve doğru bayraklar yeterli.

Bu öğreticide **el yazısı metni** bir PNG’den çıkarmak, resmi düz metne dönüştürmek ve her ayarın “neden”ini açıklamak için adım adım ilerleyeceğiz. Sonunda, ister bir not‑alma uygulaması ister toplu‑işlem hattı olsun, el yazısı notları tanıyabileceksiniz.

> **İhtiyacınız olanlar**  
> • Python 3.8+ (kod 3.10’da da çalışır)  
> • `ocr` kütüphanesi (veya `OcrEngine`i ortaya çıkaran uyumlu bir sarmalayıcı)  
> • `note_handwritten.png` gibi bir örnek görüntü – genişletilmiş Latin karakterleri içeren herhangi bir görüntü yeterli.

Haydi başlayalım.

---

## Dil Nasıl Ayarlanır ve El Yazısı Tanıma Nasıl Etkinleştirilir

İlk yapmanız gereken OCR motoruna hangi alfabeyi beklemesi gerektiğini söylemek. Bu adımı atlayınca motor, genellikle aksanlı harfleri veya özel sembolleri yanlış tanıyan genel bir setle çalışır.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**Bunun önemi:**  
- **ExtendedLatin**, “ñ”, “ø” ve “ç” gibi birçok Avrupa notunda yaygın karakterleri kapsar.  
- `recognize_handwritten` bayrağı, temel modeli basılı‑metin OCR’dan el yazısı darbeleri üzerine eğitilmiş bir sinir ağına değiştirir. Bu bayrak olmadan motor karalamalarınızı gürültü olarak görür.

> **Pro ipucu:** Birden fazla dilde belge işliyorsanız, dil başına ayrı bir motor örneği oluşturun ya da her çağrıdan önce dinamik olarak `ocr_engine.language`i değiştirin. Böylece kullanılmayan karakter setlerini yüklemenin getirdiği yükten kaçınırsınız.

![Screenshot of OCR engine configuration showing how to set language](/images/ocr-set-language.png "How to set language on OCR engine")

*Image alt text: “How to set language on OCR engine configuration screen.”*

---

## PNG Görüntüden El Yazısı Metin Çıkarma

Motor artık ne arayacağını bildiğine göre, bir görüntü besleme zamanı. `recognize_image` metodu zengin bir sonuç nesnesi döndürür; `text` özelliği sizin ilgilendiğiniz düz dizeyi tutar.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

Betik çalıştırıldığında aşağıdakine benzer bir şey görmelisiniz:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

Bu çıktı, **görüntüyü metne dönüştürme** işlemini başarıyla yaptığınızı ve motorun sağladığınız dil ayarını dikkate aldığını kanıtlar.

**Yaygın tuzaklar**  
- **Yanlış yol** – Dosya konumunu iki kez kontrol edin; eksik dosya `FileNotFoundError` verir.  
- **Düşük çözünürlüklü görüntü** – El yazısı OCR, 300 dpi’nin altında zorlanır. Çıktı bozuk görünüyorsa ölçeklendirin ya da yeniden tarayın.  
- **Renk terslemesi** – Arka plan koyu, mürekkep açık ise önce renkleri ters çevirin (`Pillow` yardımcı olabilir).

---

## Yardımcı Fonksiyonla Görüntüyü Metne Dönüştürme

Onlarca dosyada OCR çalıştırmayı planlıyorsanız, mantığı yeniden kullanılabilir bir fonksiyona sarın. Bu, kodun test edilmesini ve diğer işlem hatlarıyla bütünleştirilmesini de kolaylaştırır.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

Yardımcı, **el yazısı nasıl çıkarılır** mantığını izole eder; böylece Flask uç noktasından, CLI aracından ya da toplu işten her seferinde yapılandırmayı yeniden yazmadan çağırabilirsiniz.

---

## Gerçek Dünya Senaryolarında El Yazısı Notları Tanıma

Aşağıda **el yazısı notları tanıma** ihtiyacı duyabileceğiniz birkaç durum ve bu kurulumun nasıl uyarlanacağı yer alıyor:

| Senaryo | Dil neden önemli? | Önerilen ayar |
|----------|-------------------|-----------------|
| **Çok dilli market listeleri** | Öğeler aksan içerebilir (ör. “crème”) | Liste başına `ocr_engine.language`i değiştirin veya destekleniyorsa `ocr.Language.AutoDetect` kullanın |
| **Sınıf tahtası fotoğrafları** | Kireç hafif darbeler üretebilir | Görüntü kontrastını artırdıktan sonra motoru besleyin |
| **Tıbbi reçeteler** | El yazısı genellikle dağınıktır | İlaç isimleri için bir yazım‑düzeltme sözlüğüyle OCR’ı eşleştirin |

Her durumda, temel adımlar—**dil nasıl ayarlanır**, el yazısı modu nasıl etkinleştirilir ve `recognize_image` nasıl çağrılır—aynı kalır. Bu tutarlılık, yaklaşımın hem sağlam hem de bakımının kolay olmasını sağlar.

---

## Kenar Durumları & İleri Düzey Ayarlar

1. **Toplu işleme** – Motoru bir kez yükleyin, dosyalar üzerinde döngü kurun ve sadece gerektiğinde `language` özelliğini değiştirin. Böylece başlatma maliyeti azalır.  
2. **Latin dışı betikler** – Cyrillic ya da Arapça işlemek istiyorsanız, `ExtendedLatin` yerine uygun enum’u (ör. `ocr.Language.Cyrillic`) kullanın. Aynı desen geçerli olur.  
3. **Kısmi tanıma** – Çok kısa darbeler için motor boş dize döndürebilir. Hızlı bir tutarlılık kontrolü (`if not result.text.strip(): …`) ile ikinci bir modele geçebilir ya da kullanıcıdan yeniden tarama isteyebilirsiniz.  
4. **Performans profili** – Büyük veri setlerinde `recognize_image` çağrısını zamanlayın. Eğer darboğaz oluşturuyorsa, `concurrent.futures.ThreadPoolExecutor` ile paralelleştirmeyi düşünün.

---

## Tam Çalışan Örnek

Aşağıda `handwritten_ocr.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam betik yer alıyor. Komut satırından herhangi bir görüntüyü işaretleyebilmeniz için argüman ayrıştırma da içeriyor.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

Şöyle çalıştırın:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

Önceki kod parçacığıyla aynı çıktıyı görmelisiniz; bu da **görüntüyü metne dönüştürme** ve **el yazısı notları tanıma** işlemlerini başarıyla tamamladığınızı doğrular.

---

## Sonuç

**OCR motorunda dil nasıl ayarlanır**, el‑yazısı‑metin bayrağı nasıl etkinleştirilir ve **herhangi bir görüntüden el yazısı metin çıkaran** yeniden kullanılabilir bir fonksiyon nasıl oluşturulur konularını ele aldık. Yukarıdaki adımları izleyerek, tek bir not ya da taranmış belgeler arşivi olsun, güvenilir bir şekilde **görüntüyü metne dönüştürebilirsiniz**.

Şimdi farklı dil paketleriyle denemeler yapın, bir klasördeki görüntüleri toplu‑işleyin ya da bu mantığı JSON sonuç dönen bir web servisine entegre edin. Temel prensipler aynı kalır ve `ocr` kütüphanesinin esnekliği sayesinde hemen hemen her kullanım senaryosuna uyum sağlayabilirsiniz.

Kenar durumları, performans veya betiği diğer dillere genişletme hakkında sorularınız mı var? Yorum bırakın ya da GitHub’da bana mesaj atın – iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}