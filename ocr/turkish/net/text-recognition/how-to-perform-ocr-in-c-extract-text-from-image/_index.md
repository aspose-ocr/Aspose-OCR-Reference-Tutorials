---
category: general
date: 2026-03-13
description: C#'ta OCR nasıl yapılır ve OcrEngine kullanarak görüntüden metin nasıl
  çıkarılır. Görüntüyü hızlıca metne dönüştürmeyi, adım adım eksiksiz bir rehberle
  öğrenin.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: tr
og_description: C#'ta OCR nasıl yapılır? Bu rehber, görüntüden metin nasıl çıkarılır,
  görüntü nasıl metne dönüştürülür ve OcrEngine kullanarak resimden metin nasıl okunur
  gösterir.
og_title: C#'ta OCR Nasıl Yapılır – Görüntüden Metin Çıkarma
tags:
- OCR
- C#
- Image Processing
title: C#'ta OCR Nasıl Yapılır – Görüntüden Metin Çıkarma
url: /tr/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Yapılır – Görüntüden Metin Çıkarma

C#'ta OCR yapmak, resim dosyalarından **metin okuması** gereken geliştiriciler için yaygın bir sorudur. Bu rehberde `OcrEngine` kütüphanesini kullanarak görüntüden metin çıkarmayı, birkaç satır kodla resimleri aranabilir string'lere dönüştürmeyi adım adım göstereceğiz.  

Eğer bir taranmış faturaya, el yazısı bir nota veya bir ekran görüntüsüne bakıp *“metni nasıl çıkarırım?”* diye merak ettiyseniz, doğru yerdesiniz. Ayrıca toplu işleme için görüntüyü metne dönüştürmeye de değineceğiz, böylece tüm iş akışını otomatikleştirebilirsiniz.

---

## Gerekenler

Before we dive, make sure you have:

- **.NET 6.0 veya üzeri** (kullandığımız API .NET Standard 2.0+ ile çalışır)
- **OcrEngine** NuGet paketi (veya `Language`, `Image`, `Recognize` ve `Text` özelliklerini sunan herhangi bir uyumlu OCR kütüphanesi)
- Örnek bir görüntü dosyası, örn. `hindi_page.jpg`, koddan referans alabileceğiniz bir klasöre yerleştirin
- C# sözdizimi hakkında temel bir anlayış – ileri düzey hilelere gerek yok

Hepsi bu. Harici hizmetler, API anahtarları yok, sadece işi yapan yerel bir kütüphane.

---

## Adım‑Adım Uygulama

Aşağıda süreci mantıksal parçalara ayırıyoruz. Her bölüm net bir başlık, kısa bir kod snippet'i ve adımın **neden** önemli olduğuna dair bir açıklama içerir—sadece **ne** yaptığını değil.

### OCR Nasıl Yapılır – Temel Adımlar

The overall flow can be summarized in five actions:

1. **Create** bir OCR motoru örneği oluştur
2. **Select** tanımak istediğiniz dili seç
3. **Load** metni içeren görüntüyü yükle
4. **Run** tanıma algoritmasını çalıştır
5. **Read** çıkarılan metni oku

Bu iskelet; ardından gelen bölümler bunu detaylandırır.

---

### Görüntüden Metin Çıkarma – Motoru Oluştur

İlk olarak, OCR motoru ile iletişim kurabilen bir nesneye ihtiyacımız var.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*Neden önemli:* `OcrEngine` örneği oluşturmak, tüm iç tamponları ayırır ve görüntü analizinde gereken yerel DLL'leri yükler. Bu adımı atlamak, daha sonra çağırabileceğiniz bir tanıyıcı olmamanıza neden olur.

> **Pro tip:** Eğer birden fazla görüntüyü ardışık işlemek istiyorsanız, aynı `ocrEngine` örneğini canlı tutun. Dil modellerini yeniden kullanır ve sonraki çağrıları hızlandırır.

---

### Görüntüyü Metne Dönüştür – Dili Seç

OCR doğruluğu, ona sağladığınız dil modeline büyük ölçüde bağlıdır. Hindi, Tamil veya başka bir yazı sistemi için `Language` özelliğini uygun şekilde ayarlayın.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*Neden önemli:* Motor, dil‑spesifik karakter setleri ve istatistiksel modeller kullanır. Yanlış dil sağlamak, özellikle Latin dışı scriptlerde bozuk çıktı üretir.

> **Köşe durum:** Çok‑dilli destek gerekiyorsa, bazı kütüphaneler bir yedek liste ayarlamanıza izin verir, örn. `ocrEngine.Language = Language.Multilingual;`.

---

### Resimden Metin Oku – Kaynak Görüntüyü Yükle

Şimdi motoru görsel metni içeren dosyaya yönlendiriyoruz.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*Neden önemli:* `ImageStream.FromFile` ham dosyayı OCR çekirdeğinin anlayabileceği bir bitmap formatına dönüştürür. Bozuk veya desteklenmeyen bir format (örneğin SVG) gönderirseniz istisna oluşur.

> **Dikkat:** Büyük görüntüler çok bellek tüketebilir. Yüksek çözünürlüklü taramaları işliyorsanız, motorun önüne geçmeden `Image.Resize` ile ölçeklendirmeyi düşünün.

---

### Görüntüyü Metne Dönüştür – Tanıma Çalıştır

Motor hazır ve görüntü yüklendiğinde, nihayet OCR sürecini çağırıyoruz.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*Neden önemli:* `Recognize` bir dizi iç adımı tetikler—ön‑işleme, segmentasyon, karakter sınıflandırması ve son‑işleme. Çağrı bloklayıcıdır, yani iş parçacığı metin hazır olana kadar bekler.

> **Performans notu:** Tipik bir masaüstünde, 300 dpi bir sayfayı tanımak < 1 saniye sürer. Sunucuda, UI donmalarını önlemek için bunu arka plan görevinde çalıştırmak isteyebilirsiniz.

---

### Metni Nasıl Çıkarırsınız – Sonucu Alın

Tanıma tamamlandığında, motor düz‑metin çıktısını `Text` özelliğinde saklar.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*Neden önemli:* `Text` özelliği, dosyaya yazabileceğiniz, veritabanına aktarabileceğiniz veya sonraki NLP boru hatlarına gönderebileceğiniz temiz, UTF‑8 bir string verir.

> **Beklenen çıktı:** Örnek Hindi sayfası için şöyle bir şey görebilirsiniz  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (Tam çıktı görüntü kalitesi ve dil modeline bağlıdır.)

---

## Gerçek‑Dünya Projeleri İçin Ek Hususlar

Aşağıda üretimde **görüntüden metin çıkarma** işlemi yaparken muhtemelen karşılaşacağınız bazı “ne‑olursa” senaryoları var.

### Döngüde Birden Çok Görüntüyü İşleme

Eğer onlarca dosya için **görüntüyü metne dönüştürmek** gerekiyorsa, adımları bir `foreach` döngüsü içinde sarın ve aynı `ocrEngine` örneğini yeniden kullanın:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### Düşük‑Kalite Taramalarla Baş Etme

- **Ön‑işlem** binarizasyon (`Image.Binarize()`), gürültü giderme veya eğikliği düzeltme ile yapın.
- **DPI artırın** tarama sırasında (300 dpi güvenli bir temel).
- **Dil modelini seçin** ki scriptin bağlaçlarını desteklesin (örnek: Hindi için Devanagari).

### Web Üzerinden Resimden Metin Okuma

Görüntü bir URL'den geldiğinde, önce bir bellek akışına indir.

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### İş Parçacığı Güvenliği ve Paralellik

Çoğu OCR kütüphanesi kutudan çıktığı gibi **iş parçacığı güvenli** değildir. **Resimden metin okuma** işlemini eşzamanlı yapmayı planlıyorsanız, her iş parçacığı için ayrı `OcrEngine` örnekleri oluşturun veya erişimi sıraya koymak için bir üretici‑tüketici kuyruğu kullanın.

---

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, **OCR nasıl yapılır**, **görüntüden metin çıkarma** ve **resimden metin okuma** işlemlerini tek bir bütün programda gösteren, çalıştırmaya hazır bir konsol uygulaması burada.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**Görmeniz gereken:** Konsol, `hindi_page.jpg` dosyasından çıkarılan Hindi cümlesini yazdırır ve ardından metin dosyasının oluşturulduğuna dair bir onay verir. Görüntü temizse, çıktı neredeyse orijinal basılı metinle aynı olur.

---

## Sonuç

Artık C#'ta **OCR nasıl yapılır** konusunu baştan sona biliyorsunuz, **görüntüden metin çıkarma**, **görüntüyü metne dönüştürme** ve **resimden metin okuma** işlemlerini basit bir `OcrEngine` iş akışıyla gerçekleştirebiliyorsunuz. Beş adımlı desen—oluştur, dili ayarla, yükle, tanı, oku—çoğu kullanım senaryosunu kapsar ve ek ipuçları toplu işler, düşük‑kalite taramalar ve web tabanlı kaynaklarla başa çıkmanıza yardımcı olur.

Bir sonraki meydan okumaya hazır mısınız? Dili İngilizceye değiştirin, bir PDF sayfasını görüntü olarak besleyin veya OCR çıktısını bir arama‑indeksi boru hattına bağlayın. C#'ta OCR temellerini kavradığınızda sınır yoktur.

Sorularınız veya işbirliği yapmayan zor bir görüntünüz mü var? Aşağıya yorum bırakın, birlikte sorun giderelim. Kodlamanın tadını çıkarın!  

![OCR nasıl yapılır örneği](images/ocr-example.png "OCR nasıl yapılır örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}