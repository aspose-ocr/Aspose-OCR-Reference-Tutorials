---
category: general
date: 2026-03-29
description: Aspose OCR kullanarak C#'ta görüntüden metin çıkarın. Otomatik döndürme
  OCR'ını ve taranmış görüntüyü nasıl eğriltip düzelteceğinizi öğrenerek mükemmel
  sonuçlar elde edin.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: tr
og_description: Aspose OCR kullanarak görüntüden metin çıkarın. Bu kılavuz, otomatik
  döndürme OCR ve C#'ta taranmış görüntünün eğimini düzeltmeyi gösterir.
og_title: C#'ta Görüntüden Metin Çıkarma – Otomatik Döndürme OCR ve Eğik Düzeltme
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C# ile Görüntüden Metin Çıkarma – Otomatik Döndürme OCR ve Eğik Düzeltme Rehberi
url: /tr/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma C# – Otomatik Döndürme OCR & Çarpıtma Düzeltme Rehberi

Görüntüden **extract text from image** ihtiyacınız hiç oldu mu, ancak dosya garip bir açıyla geldi? Bu, özellikle taranmış faturalar, fotoğraflanmış makbuzlar veya eğik PDF'lerle uğraşırken yaygın bir baş ağrısıdır. İyi haber şu ki, kendiniz özel bir döndürme algoritması yazmak zorunda değilsiniz. Aspose OCR'nun yerleşik *auto rotate OCR* özelliğini kullanarak motorun resmi düzleştirmesine izin verebilir ve ardından **extract text from image** tek bir adımda yapabilirsiniz.  

Bu öğreticide, aşağıdaki özelliklere sahip tam, çalıştırılabilir bir C# programını adım adım inceleyeceğiz:

* Otomatik yönlendirme ve çarpıtma düzeltme ile OCR motorunu başlatır,
* Döndürülmüş veya çarpıtılmış bir resmi tanır,
* Algılanan döndürme açısını ve çıkarılan metni döndürür.

Harici hizmetler yok, karmaşık matematik yok—sadece birkaç satır kod ve gerektiğinde *how to deskew scanned image* konusunun net bir açıklaması.

## İhtiyacınız Olanlar

| Gereksinim | Neden Önemli |
|--------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.6+) | Aspose OCR, bu çalışma zamanlarını hedefleyen bir NuGet paketi olarak sunulur. |
| Visual Studio 2022 (or any C# editor) | NuGet paketlerini eklemeyi ve konsol uygulamasını çalıştırmayı kolaylaştırır. |
| A sample image (`rotated_document.jpg`) | Dosya JPEG, PNG, BMP veya TIFF olmalı ve tamamen dik olmamalıdır. |
| Aspose.OCR NuGet package (`Install-Package Aspose.OCR`) | `OcrEngine`, `PreprocessingFilters` ve ilgili tipleri sağlar. |

Bu kutucukları işaretlediyseniz, hazırsınız demektir. Aksi takdirde, NuGet üzerinden en yeni Aspose OCR paketini alın—tek tıkla kurulum.

---

## Adım 1 – OCR Motorunu Başlatma (Eylemde Birincil Anahtar Kelime)

İlk yaptığımız şey bir `OcrEngine` örneği oluşturmak ve ona **auto rotate OCR** ve **deskew** özelliklerini etkinleştirmesini söylemektir. Bu iki bayrak, `PreprocessingFilters` bir `[Flags]` niteliğine sahip enum olduğu için bitwise OR (`|`) ile birleştirilir.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Why this matters:**  
> *Auto‑rotate OCR* görüntünün metin tabanını inceler, doğru yönlendirmeyi tahmin eder ve tanımadan önce içsel olarak döndürür. *Auto‑deskew* ise taranmış belgelerde sıkça görülen hafif eğimleri aynı şekilde düzeltir. İkisini de etkinleştirerek, manuel görüntü düzenlemesi yapmadan en iyi **extract text from image** sonuçlarını garantilersiniz.

---

## Adım 2 – Görüntüyü Tanıma ve Sonucu Alma

Şimdi motorun bir dosya yolunu almasını sağlarız. `RecognizeImage` metodu, algılanan döndürme açısını, güven skorlarını ve düz metin çıktısını içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** Bir akış (ör. yüklenen bir dosya) ile çalışıyorsanız, bunun yerine `ocrEngine.RecognizeImage(Stream)` kullanın. Aynı ön işleme bayrakları geçerli olduğundan **auto rotate OCR** avantajlarını hâlâ elde edersiniz.

---

## Adım 3 – Döndürme Açısını ve Çıkarılan Metni Görüntüleme

Son olarak, konsola iki bilgi parçası yazdırırız: motorun resmin döndürülmesi gerektiğini düşündüğü açı ve gerçek çıkarılan metin.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı** (girdi görüntüsüne bağlı olarak sayılarınız farklı olacaktır):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Görüntü zaten dikse, döndürme açısı `0°` olur ve *auto‑deskew* algoritması sayesinde temiz metin alırsınız.

---

## Adım 4 – Tarama Görüntüsünü Çarpıtma Düzeltme (İkincil Anahtar Kelime Derin İnceleme)

*how to deskew scanned image* sorusunu, OCR motoru sıfır olmayan bir döndürme raporladığında merak edebilirsiniz. Motorun içinde, Aspose OCR baskın metin satırı yönünü tespit etmek için bir **Hough transform** uygular. Ardından bitmap'i bu açının tersine döndürerek metni etkili bir şekilde düzleştirir.

**When does it matter?**  
* Kağıdı hafif bir açıyla besleyen tarayıcılar (ofis ortamlarında yaygın).  
* El ile çekilen akıllı telefon fotoğrafları—ufuk nadiren mükemmeldir.  

**Edge case handling:**  
Eğer sonucun `RotationAngle` değeri olağandışı büyükse (ör. > 45°), motor görüntüyü yanlış yorumlamış olabilir (belki bir logo ya da metin içermeyen bir grafik). Bu durumda şunları yapabilirsiniz:

1. Motoru beslemeden önce `System.Drawing` kullanarak görüntüyü manuel olarak döndürün, ya da  
2. Belgenin zaten dik olduğunu biliyorsanız `AutoRotate` özelliğini devre dışı bırakıp sadece `AutoDeskew`'i tutun.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Adım 5 – Yaygın Tuzaklar ve Pro İpuçları (E‑E‑A‑T Eylemde)

| Tuzak | Neden Oluşur | Çözüm |
|---------|----------------|-----|
| **Blurry or low‑resolution images** | OCR doğruluğu büyük ölçüde düşer; döndürme tespiti başarısız olabilir. | En az 300 dpi taramalar kullanın; OCR'den önce bir keskinleştirme filtresi uygulayın. |
| **Mixed languages** | Motor varsayılan olarak İngilizce'yi seçer; yabancı karakterler bozulur. | `Language = Language.English | Language.Spanish` (veya uygun kombinasyon) ayarlayın. |
| **Large files (> 10 MB)** | Bellek baskısı `OutOfMemoryException` hatasına yol açabilir. | Görüntüyü önce küçültün veya `OcrEngine.RecognizeRegion` ile parçalar halinde işleyin. |
| **Incorrect file path** | `FileNotFoundException` programı durdurur. | Dayanıklılık için `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` kullanın. |

> **Pro tip:** Her zaman `ocrResult.RotationAngle` ve (varsa) `ocrResult.Confidence` değerlerini kaydedin. Bu metrikler, farklı ön işleme ayarlarıyla yeniden denemenin değerli olup olmadığını belirlemenize yardımcı olur.

---

## Adım 6 – Örneği Genişletme (Sırada Ne Var?)

Artık **extract text from image** işlemini otomatik döndürme ve çarpıtma düzeltme ile yapabildiğinize göre, aşağıdaki adımları değerlendirin:

* **Batch processing** – Bir klasördeki tüm görüntüler üzerinde döngü kurun, her sonucu bir veritabanına kaydedin ve `RotationAngle > 5°` olanları manuel inceleme için işaretleyin.  
* **PDF conversion** – Çıkarılan metni orijinal görüntüyle birleştirerek Aspose.PDF kullanarak aranabilir bir PDF oluşturun.  
* **Language detection** – Aspose.OCR'nin `AutoDetectLanguage` bayrağını kullanarak motorun en uygun dili otomatik seçmesini sağlayın.  

Bu adımların hepsi aynı temel prensibe dayanır: kütüphanenin yönlendirmeyi halletmesine izin verin, siz iş mantığına odaklanın.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, `dotnet add package Aspose.OCR` komutunu çalıştırın, ardından `dotnet run` yapın. Konsolda açı ve temiz metin çıktısını görmelisiniz.

---

## Sonuç

Aspose OCR'nin *auto rotate OCR* ve zorlayıcı *how to deskew scanned image* sorununu halletmesine izin vererek C#'ta **extract text from image** nasıl yapılır gösterdik. İki ön işleme bayrağını etkinleştirerek motor, eğik resimleri otomatik olarak düzleştirir, doğru yönlendirmeyi tespit eder ve doğru metni sunar—manuel görüntü düzenlemesi gerektirmez.

Daha büyük toplu işlemler, farklı diller ya da çıktıyı aranabilir bir PDF'e entegre etme gibi deneyler yapmaktan çekinmeyin. OCR motoru ağır işi üstlendiğinde, siz sadece iş akışınızı geliştirebilirsiniz.

**Belge hattınızı bir üst seviyeye taşımaya hazır mısınız?** Kodu alın, kendi taramalarınıza yönlendirin ve döndürme açıları kaybolsun. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}