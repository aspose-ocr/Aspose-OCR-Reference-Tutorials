---
category: general
date: 2026-04-29
description: Aspose OCR kullanarak C#'de OCR nasıl yapılır – Hintçe metni çıkarma,
  PNG'den metin tanıma ve OCR dilini anında değiştirme.
draft: false
keywords:
- how to perform OCR
- extract Hindi text
- multi language OCR
- recognize text from PNG
- change OCR language
language: tr
og_description: Aspose OCR ile C#’ta OCR nasıl yapılır. Hintçe metni çıkarmayı, PNG
  dosyalarından metin tanımayı ve OCR dilini dinamik olarak değiştirmeyi öğrenin.
og_title: C#'de OCR Nasıl Yapılır – Tam Çok Dilli Eğitim
tags:
- OCR
- C#
- Aspose
title: C#'ta OCR Nasıl Yapılır – Çok Dilli Rehber
url: /tr/net/ocr-configuration/how-to-perform-ocr-in-c-multi-language-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Yapılır – Çok Dilli Rehber

Birden fazla dil içeren görüntülerde **OCR nasıl yapılır** diye hiç merak ettiniz mi? Belki yan yana bir Rus fişi ve bir Hint broşürü var ve her ikisinin metnini ayrı araçlar kullanmadan elde etmeniz gerekiyor. Bu, uluslararası belgelerle çalışan herkes için yaygın bir baş ağrısı.  

Bu öğreticide, Aspose OCR ile **OCR nasıl yapılır** konusunu, Hint metnini çıkarmayı, PNG dosyalarından metin tanımayı ve hatta **OCR dilini** anında değiştirmeyi gösteren temiz, uçtan uca bir yöntem sunacağız. Sonunda, desteklenen dillerin herhangi bir kombinasyonu için çalışan yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- Aspose OCR motorunu bir .NET projesinde nasıl kuracağınız.  
- Statik bir dil yapılandırması ile çalışma zamanında dilleri değiştirme arasındaki fark.  
- Bir görüntüden Hint metnini nasıl çıkaracağınız ve kütüphanenin dil paketlerini otomatik olarak neden indirebildiği.  
- PNG dosyalarını ele alma, eksik dil modülleriyle başa çıkma ve yaygın sorunları giderme ipuçları.

> **Pro ipucu:** Zaten tek bir dil için Aspose OCR kullanıyorsanız, bunu bir **çok dilli OCR** çözümüne dönüştürmek için sadece birkaç satırı değiştirmeniz yeterlidir.

---

## Ön Koşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6 veya üzeri (veya .NET Framework 4.7+) | Aspose OCR modern çalışma zamanlarını hedefler; eski sürümler dil paketi otomatik indirme desteğini kaçırabilir. |
| Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`) | `OcrEngine` sınıfını ve dil enumlarını sağlar. |
| Bilinen bir klasöre yerleştirilmiş iki örnek PNG görüntüsü (`russian.png` ve `hindi.png`) | Tek bir çalıştırmada **PNG'den metin tanıma** ve **Hint metni çıkarma** gösterir. |
| İnternet bağlantısı (yeni bir dil ilk kez talep edildiğinde) | Kütüphane, gerekli dil modülünü talep üzerine çeker. |

Ek OCR ikili dosyaları veya harici araçlar gerekmez—Aspose tüm ağır işi halleder.

---

## Adım 1 – Aspose OCR'yi Kurun ve Motoru Oluşturun

İlk olarak: Aspose OCR paketini projenize ekleyin. Package Manager Console'u açın ve şu komutu çalıştırın:

```powershell
Install-Package Aspose.OCR
```

Şimdi bir `OcrEngine` örneği oluşturabiliriz. Motoru, çalışma zamanında yeniden yapılandırılabilen akıllı bir tarayıcı olarak düşünün.

```csharp
using Aspose.OCR;
using System;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

Neden motoru sadece bir kez oluşturuyoruz? Aynı örneği yeniden kullanmak, yerel OCR kütüphanelerinin tekrar tekrar yüklenmesinden kaynaklanan yükü önler; bu, büyük toplularda fark edilebilir.

---

## Adım 2 – Rus Metnini Tanıma (İlk Dil)

Hindinceye geçmeden önce, motorun bilinen bir dille çalıştığını kanıtlayalım. Dili Rusça olarak ayarlıyoruz, bir PNG besliyoruz ve sonucu yazdırıyoruz.

```csharp
        // Step 2: Configure the engine for Russian and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianImagePath = @"YOUR_DIRECTORY/russian.png";
        var russianOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianImagePath));
        Console.WriteLine("Russian: " + russianOcrResult.Text);
```

**Arka planda ne oluyor?**  
`OcrEngine.LoadImage` PNG'yi Aspose'un iç bitmap formatına okur. `Config.Language` özelliği OCR motoruna hangi sözlüğün ve karakter setinin uygulanacağını söyler. `Recognize` çağrıldığında, motor Kiril alfabesi karakterlerine göre ayarlanmış bir sinir ağı modelini çalıştırır ve düz metin çıktısını içeren bir `OcrResult` nesnesi döndürür.

> **Beklenen çıktı (örnek)**  
> `Russian: Привет, мир! Это тестовое изображение.`

Eğer bozuk karakterler görürseniz, görüntünün bozulmadığını ve Rusça dil modülünün mevcut olduğunu (temel paketle birlikte gelir) iki kez kontrol edin.

---

## Adım 3 – Hintçe'ye Geçiş – **OCR Dilini** Dinamik Olarak Değiştirin

Şimdi eğlenceli kısma: motoru yeniden oluşturmadan dili değiştirmek. Aspose OCR, ilk kez talep ettiğinizde Hindi modülünü indirecek, bu yüzden sadece bir kez internet bağlantısına ihtiyacınız var.

```csharp
        // Step 3: Switch the engine to Hindi (the language module will be downloaded automatically) and recognize the image
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiImagePath = @"YOUR_DIRECTORY/hindi.png";
        var hindiOcrResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiImagePath));
        Console.WriteLine("Hindi: " + hindiOcrResult.Text);
    }
}
```

**Bu neden çalışıyor?**  
`Config.Language` ayarlayıcısı tembel‑yükleme rutinini tetikler. İstenen dil paketi diskte yoksa, Aspose CDN'sine bağlanır, sıkıştırılmış modülü çeker, önbelleğe alır ve ardından tanımaya devam eder. Bu tasarım, çalışma zamanında içeriğe uyum sağlayan **çok dilli OCR** boru hatları oluşturmanıza olanak tanır.

> **Örnek Hindi çıktısı**  
> `Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।`

Aynı `ocrEngine` nesnesinin hem Kiril hem de Devanagari yazı tiplerini sorunsuz bir şekilde işlediğine dikkat edin. Bu, **OCR dilini** anında değiştirmenin gücüdür.

---

## Adım 4 – PNG Dosyalarını Verimli Bir Şekilde İşleme

Yukarıdaki her iki örnek de PNG görüntüleri kullanır; bu, ekran görüntüleri ve taranmış belgeler için yaygın bir formattır. PNG kayıpsızdır, yani piksel verileri bozulmadan kalır—OCR için mükemmeldir. Ancak büyük PNG'ler bellek tüketebilir. İşte birkaç hızlı ipucu:

1. **Gerekirse yeniden boyutlandır** – Görüntü genişliği 2000 px'yi aşarsa, Aspose'a göndermeden önce `System.Drawing.Image` ile küçültün.
2. **DPI ayarla** – Bazı OCR motorları 300 DPI'den fayda sağlar. Bunu, özel çözünürlükle bir `Bitmap` kabul eden `OcrEngine.LoadImage` aşırı yüklemesiyle ekleyebilirsiniz.

```csharp
using System.Drawing;

// Example of downscaling a huge PNG
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/large.png");
int maxWidth = 2000;
if (original.Width > maxWidth)
{
    int newHeight = (int)((double)original.Height / original.Width * maxWidth);
    Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));
    original.Dispose(); // free original memory
    original = resized;
}
var result = ocrEngine.Recognize(OcrEngine.LoadImage(original));
```

Bu ayarlamalar bellek kullanımını düşük tutar ve genellikle doğruluğu artırır çünkü OCR motoru daha yönetilebilir bir piksel ızgarasıyla çalışır.

---

## Adım 5 – Hepsini Bir Araya Getirme – Tam Çalışan Örnek

Aşağıda, **OCR nasıl yapılır**, **Hint metni çıkarma**, **PNG'den metin tanıma** ve motoru yeniden başlatmadan **OCR dilini değiştirme** konularını gösteren tam, çalıştırmaya hazır program bulunmaktadır.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class MultiLanguageOcrDemo
{
    static void Main()
    {
        // Create a single OCR engine instance (re‑use it for all languages)
        var ocrEngine = new OcrEngine();

        // ----------- Russian ----------
        ocrEngine.Config.Language = OcrLanguage.Russian;
        var russianPath = @"YOUR_DIRECTORY/russian.png";
        var russianResult = ocrEngine.Recognize(OcrEngine.LoadImage(russianPath));
        Console.WriteLine("Russian: " + russianResult.Text);

        // ----------- Hindi ------------
        // The first time this runs, the Hindi language pack will be downloaded automatically.
        ocrEngine.Config.Language = OcrLanguage.Hindi;
        var hindiPath = @"YOUR_DIRECTORY/hindi.png";
        var hindiResult = ocrEngine.Recognize(OcrEngine.LoadImage(hindiPath));
        Console.WriteLine("Hindi: " + hindiResult.Text);

        // ----------- Optional PNG optimization ----------
        // If you have very large PNGs, resize them before recognition (example shown earlier).
        // This block is optional and can be removed if your images are already sized appropriately.
    }
}
```

**Kodu çalıştırmak** şöyle bir çıktı verir:

```
Russian: Привет, мир! Это тестовое изображение.
Hindi: नमस्ते दुनिया! यह एक परीक्षण छवि है।
```

Eğer bu satırları görürseniz, tebrikler—tek bir motorla **Hint metni çıkarabilen** ve **PNG dosyalarından metin tanıyabilen** bir **çok dilli OCR** çözümü başarıyla oluşturmuşsunuz.

---

## Sıkça Sorulan Sorular (SSS)

| Soru | Cevap |
|----------|--------|
| *Aspose OCR için bir lisansa ihtiyacım var mı?* | Ücretsiz deneme anahtarı test için çalışır, ancak üretim kullanımı ticari lisans gerektirir. |
| *Bir görüntüde iki dilden fazla tanıyabilir miyim?* | Evet. `Config.Language`'ı `OcrLanguage.Multiple` olarak ayarlayın ve virgülle ayrılmış bir liste verin (ör. `Russian, Hindi`). |
| *Dil modülü indirilmezse ne olur?* | Güvenlik duvarı veya proxy ayarlarınızı kontrol edin. Ayrıca modülleri Aspose portalından önceden indirip `Data` klasörüne koyabilirsiniz. |
| *PNG tek desteklenen format mı?* | Hayır. Aspose OCR ayrıca JPEG, BMP, TIFF ve PDF (görüntü olarak) dosyalarını da işler. PNG sadece kayıpsız kalite için yaygın bir tercihtir. |

---

## Sonraki Adımlar ve İlgili Konular

- **Toplu işleme** – PNG'lerin bulunduğu bir klasörü döngüyle işleyin ve sonuçları bir CSV dosyasına kaydedin.  
- **PDF çıkarma** – Tarama yapılmış PDF'lerden metin çekmek için `OcrEngine.RecognizePdf` kullanın.  
- **Özel sözlükler** – Kullanıcı tarafından sağlanan kelime listeleriyle yerleşik dil paketlerini, alan‑spesifik sözlükler için genişletin.  
- **Performans ayarı** – Büyük görüntü setleriyle çalışırken `Parallel.ForEach` ile çağrıları paralelleştirin.  

Bu alanları keşfetmek, çeşitli senaryolarda **OCR nasıl yapılır** konusundaki ustalığınızı derinleştirecektir.

---

## Sonuç

Aspose OCR kullanarak C#'ta **OCR nasıl yapılır** öğrendiniz, dilleri anında değiştirdiniz ve bir PNG görüntüsünden başarıyla **Hint metni çıkardınız**. Temel çıkarım, tek bir `OcrEngine` örneğinin çok yönlü bir **çok dilli OCR** iş gücü olabileceğidir—sadece `Config.Language`'ı ayarlayın ve kütüphane geri kalanını halletsin.

Kodu çalıştırın, örnek görüntüleri kendi dosyalarınızla değiştirin ve ek dillerle denemeler yapın. Aspose OCR'nin esnekliği, hızlı bir prototipten üretim‑düzeyinde bir belge‑işleme boru hattına minimum değişiklikle ölçeklenebileceği anlamına gelir.

Kodlamaktan keyif alın ve metin‑çıkarma maceralarınız hatasız olsun! 

![OCR nasıl yapılır örneği](/images/ocr-demo.png "OCR nasıl yapılır örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}