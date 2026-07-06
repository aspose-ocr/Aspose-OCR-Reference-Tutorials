---
category: general
date: 2026-04-26
description: Python’da OCR için görüntü yüklemek amacıyla threading nasıl kullanılır.
  Geri aramalar, arka plan iş parçacıkları ve görüntü yükleme ile asenkron OCR işleme
  birkaç adımda öğrenin.
draft: false
keywords:
- how to use threading
- load image for OCR
- python threading OCR
- async OCR callback
- background thread image processing
language: tr
og_description: Python'da OCR için görüntüyü yüklemek amacıyla threading nasıl kullanılır.
  Bu kılavuz, geri aramalar ve arka plan yürütme ile tam, çalıştırılabilir bir örnek
  gösterir.
og_title: OCR için Görüntüyü Yüklemek İçin Threading Nasıl Kullanılır
tags:
- Python
- Threading
- OCR
- Image Processing
title: OCR için Görüntüyü Yüklemek İçin Threading Nasıl Kullanılır
url: /tr/python-java/general/how-to-use-threading-to-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Threading Kullanarak OCR İçin Görüntü Yükleme Nasıl Yapılır

Uygulamanızın donmasına neden olmadan OCR için görüntüyü yüklemek için **threading nasıl kullanılır** diye hiç merak ettiniz mi? Bu, masaüstü tarayıcı, web servisi ya da büyük resimleri işleyen basit bir betik geliştiriyor olsanız da karşınıza çıkabilecek bir senaryodur. İyi haber? Birkaç satır Python ve doğru threading deseni, OCR motoru sihrini yaparken UI'nizin hızlı kalmasını sağlayacak.

Bu öğreticide, büyük bir PNG'yi yükleme, OCR'yi arka plan thread'inde başlatma ve sonucu bir callback ile işleme gibi tam bir uçtan uca örnek üzerinden ilerleyeceğiz. Sonunda sadece **threading nasıl kullanılır** değil, aynı zamanda **OCR için görüntü nasıl yüklenir** konusunda temiz ve yeniden kullanılabilir bir yöntem de öğreneceksiniz.

## Gereksinimler

- Python 3.9+ (kullandığımız sözdizimi herhangi bir yeni sürümde çalışır)
- `pillow` görüntü işleme için (`pip install pillow`)
- `pytesseract` Tesseract OCR için ince bir sarmalayıcıdır (`pip install pytesseract`)
- Makinenize Tesseract OCR motoru kurulu olmalı (indirmek için [tesseract‑ocr.org](https://github.com/tesseract-ocr/tesseract))
- İşlemek istediğiniz büyük bir görüntü dosyası (`large_image.png` bu kılavuzda)

Ekstra framework yok, async/await yok—sadece klasik `threading` ve bir callback.

## Adım 1: Threading Modülünü İçe Aktarın (Arka Plan Çalıştırma İçin Gerekli)

İlk yaptığımız şey `threading` modülünü içe aktarmaktır. Bu modül, herhangi bir fonksiyonu ayrı bir işletim sistemi thread'inde çalıştırmamızı sağlayan `Thread` sınıfını sunar.

```python
import threading
```

*Neden önemli*: OCR'yi ana thread'de çalıştırırsanız, programınız (özellikle bir GUI) OCR bitene kadar donacaktır. İşi bir arka plan thread'ine devrederek, ana thread UI'yi güncellemek, kullanıcı girdisini işlemek veya başka görevler başlatmak için serbest kalır.

## Adım 2: OCR Bittiğinde Çağrılacak Bir Callback Tanımlayın

Callback, başka bir kod parçasının işi bittiğinde çağırdığı basit bir fonksiyondur. Burada tanınan metni yazdıracağız, ancak onu saklayabilir, ağ üzerinden gönderebilir veya bir UI widget'ını güncelleyebilirsiniz.

```python
def ocr_done(result_text: str) -> None:
    """Called when the OCR thread finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)   # Display the recognized text
```

*Pro ipucu*: Callback'i hafif tutun. Callback içinde ağır işlem yapmak, threading amacını bozar çünkü yine de onu çağıran thread'i (genellikle ana thread) engeller.

## Adım 3: İşlemek İstediğiniz Görüntüyü Yükleyin

Görüntüyü yüklemek OCR'dan ayrı bir konudur, ancak yine de genel iş akışının bir parçasıdır. Pillow kullanmak bunu çok basit hale getirir.

```python
from PIL import Image

def load_image(path: str) -> Image.Image:
    """Loads an image from disk and returns a Pillow Image object."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img
    except Exception as exc:
        raise RuntimeError(f"Failed to load image: {exc}") from exc
```

*Neden burada yapıyoruz*: Görüntü çok büyükse, ana thread'de yüklemek zaten bir takılmaya neden olabilir. Gerçek dünyadaki birçok uygulamada yüklemeyi bir thread'e de taşırsınız, ancak açıklık için senkron tutuyoruz.

## Adım 4: Küçük Bir OCR Motor Sarmalayıcısı Oluşturun

Orijinal kod parçası `engine.process_async` kullanıyordu. Bunu, içinde bir thread başlatan ve iş bittiğinde verilen callback'i çağıran küçük bir sınıfla taklit edeceğiz.

```python
import pytesseract

class SimpleOcrEngine:
    """A minimal OCR engine that runs pytesseract in a background thread."""

    def __init__(self, image: Image.Image):
        self.image = image

    def _run_ocr(self, callback):
        """Internal method executed in the worker thread."""
        try:
            # pytesseract returns the recognized text as a plain string
            text = pytesseract.image_to_string(self.image)
            callback(text)
        except Exception as exc:
            callback(f"OCR failed: {exc}")

    def process_async(self, callback):
        """Public method to start OCR on a new thread."""
        worker = threading.Thread(target=self._run_ocr, args=(callback,))
        worker.daemon = True          # Daemon so it won’t block program exit
        worker.start()
        print("OCR thread started…")
```

*Açıklama*:  
- `_run_ocr` ağır işi yapar.  
- `process_async` bir `Thread` nesnesi oluşturur, onu daemon olarak işaretler (thread hâlâ çalışıyor olsa bile yorumlayıcının çıkabilmesi için) ve başlatır.  
- Callback, OCR metnini ya da bir hata mesajını alır.

## Adım 5: Her Şeyi Birleştirip OCR Çalışırken Başka İşler Yapın

Şimdi tüm akışı düzenliyoruz: görüntüyü yüklüyoruz, motoru örnekliyoruz, async OCR'yi başlatıyoruz ve ana thread'i başka bir şeyle meşgul tutuyoruz (burada sadece bir mesaj yazdırıyoruz).

```python
if __name__ == "__main__":
    # 1️⃣ Load the image you want to OCR
    img_path = "YOUR_DIRECTORY/large_image.png"
    image = load_image(img_path)

    # 2️⃣ Create the OCR engine instance
    engine = SimpleOcrEngine(image)

    # 3️⃣ Start OCR on a background thread, passing our callback
    engine.process_async(callback=ocr_done)

    # 4️⃣ Do other work while OCR runs (simulated with a loop)
    for i in range(5):
        print(f"Main thread doing other work… ({i+1}/5)")
        # In a real app you might update a progress bar, handle UI events, etc.
        threading.Event().wait(0.5)  # Sleep 0.5 s without blocking the OS thread

    # Give the OCR thread a moment to finish before the script exits
    threading.Event().wait(2)
    print("Script finished.")
```

**Beklenen çıktı (kısaltılmış):**

```
Image 'YOUR_DIRECTORY/large_image.png' loaded – size: (3840, 2160)
OCR thread started…
Main thread doing other work… (1/5)
Main thread doing other work… (2/5)
...
--- Async OCR finished ---
The quick brown fox jumps over the lazy dog.
Script finished.
```

OCR başarısız olursa, callback metin yerine bir hata mesajı yazdıracaktır.

---

## Bu Yaklaşımın Daha İyi Çalışmasının Sebebi

- **Yanıt Verebilirlik**: Ana thread OCR çağrısında asla bloklanmaz, bu büyük görüntüler için saniyeler sürebilir.
- **Ölçeklenebilirlik**: Birden fazla `SimpleOcrEngine` örneği oluşturabilir, her birini kendi thread'inde çalıştırarak bir grup görüntüyü eşzamanlı işleyebilirsiniz.
- **Sorumlulukların Ayrılması**: Yükleme, işleme ve sonuç yönetimi temiz bir şekilde ayrılmıştır, bu da kodun test edilmesini ve bakımını kolaylaştırır.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Tuzak | Ne Olur | Çözüm |
|------|----------|------|
| Thread'i *daemon* olarak işaretlemeyi unutmak | Ana iş bittiğinde script, OCR thread'i hâlâ çalıştığı için takılır. | `worker.daemon = True` **veya** çıkmadan önce thread'i `join()` yapın. |
| Sonuç için kilitsiz global değişken kullanmak | Birden fazla thread aynı anda yazdığında yarış koşulları veriyi bozabilir. | Sonucu bir callback aracılığıyla (bizim yaptığımız gibi) iletin veya `queue.Queue` gibi thread‑güvenli konteynerler kullanın. |
| Büyük bir görüntüyü ana thread'de yüklemek | Arka plan OCR başlamadan UI donar. | Görüntü yüklemeyi de bir thread'e taşıyın veya tembel yükleme tekniklerini kullanın. |
| Worker thread içinde istisnaları ele almamak | Yakalanmamış istisnalar thread'i sessizce öldürür, sonuç elde edemezsiniz. | OCR mantığını `try/except` ile sarın ve hatayı callback'e iletin. |

## Bu Deseni Genişletmek

- **İlerleme Raporlama**: OCR thread'inden ana thread'e ara yüzde ilerleme yüzdelerini itmek için paylaşılan bir `queue.Queue` kullanın.
- **Thread Havuzu**: Toplu işleme için bireysel `Thread` nesnelerini `concurrent.futures.ThreadPoolExecutor` ile değiştirin.
- **GUI Entegrasyonu**: Tkinter veya PyQt uygulamasında, UI güncellemelerinin ana thread'de gerçekleşmesini sağlamak için callback'i `after()` (Tkinter) veya `QTimer.singleShot` (Qt) ile zamanlayın.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```python
import threading
from PIL import Image
import pytesseract

def ocr_done(result_text: str) -> None:
    """Callback invoked when OCR finishes."""
    print("\n--- Async OCR finished ---")
    print(result_text)

def load_image(path: str) -> Image.Image:
    """Load an image and report its size."""
    try:
        img = Image.open(path)
        print(f"Image '{path}' loaded – size: {img.size}")
        return img

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}