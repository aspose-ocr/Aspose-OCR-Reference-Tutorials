---
category: general
date: 2026-02-24
description: Aspose.OCR ile C#'ta görüntüleri hızlıca toplu OCR yapın. Dizinden dosyaları
  nasıl okuyacağınızı, görüntüden metni nasıl tanıyacağınızı ve görüntüyü metne nasıl
  dönüştüreceğinizi birkaç adımda öğrenin.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: tr
og_description: Aspose.OCR kullanarak C#'ta toplu OCR görüntüleri. Bu öğreticide,
  klasörden dosyaları nasıl okuyacağınız, görüntüden metni nasıl tanıyacağınız ve
  görüntüyü verimli bir şekilde metne nasıl dönüştüreceğiniz gösterilmektedir.
og_title: C# ile Toplu OCR Görüntüleri – Tam Adım Adım Kılavuz
tags:
- C#
- OCR
- Aspose
title: C#'ta Toplu OCR Görüntüleri – Metin Çıkarma İçin Tam Kılavuz
url: /tr/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Toplu OCR Görüntüleri – Metin Çıkarma Tam Kılavuzu

Hiç **toplu OCR görüntüleri** işlemek zorunda kaldınız mı ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici, ilk kez **görüntülerden toplu olarak metin çıkarmaya** çalıştığında aynı engelle karşılaşıyor. İyi haber şu ki, birkaç satır C# ve Aspose.OCR ile dolu bir klasörü düzenli `.txt` dosyalarına dönüştürebilirsiniz.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: bir dizinden dosyaları okuma, her resmi OCR motoruna besleme ve sonunda **görüntüyü metne dönüştürme** dosyaları oluşturma; bu dosyaları indeksleyebilir, arayabilir veya sonraki işlem hatlarına aktarabilirsiniz. Sonunda, herhangi bir .NET çözümüne ekleyebileceğiniz bağımsız bir konsol uygulamanız olacak.

## Gereksinimler

- **.NET 6+** (örnek .NET 6 ile derlenir, ancak herhangi bir yeni sürüm de çalışır)
- **Aspose.OCR** NuGet paketi (`Install-Package Aspose.OCR`)
- İşlemek istediğiniz görüntü dosyalarından (`.png`, `.jpg`, vb.) oluşan bir klasör
- Visual Studio, Rider veya tercih ettiğiniz editör

Ek yapılandırma dosyası yok, harici hizmet yok—sadece yerel olarak çalışan saf C# kodu.

## Toplu OCR Görüntüleri – Projeyi Kurma

İlk olarak, yeni bir konsol projesi oluşturun:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Bu komut minimal bir proje oluşturur ve OCR kütüphanesini ekler. Geri yükleme tamamlandıktan sonra çekirdek mantığı eklemeye hazırsınız.

### Dizinden Dosyaları Okuma

Uygulamamıza kaynak görüntülerin nerede olduğunu ve oluşturulan metin dosyalarının nereye kaydedileceğini söylememiz gerekiyor. `System.IO` kullanmak bu işi çok kolaylaştırır.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Bu adımın önemi:** Çıktı dizini mevcut değilse program bir `.txt` dosyası yazmaya çalıştığında istisna fırlatır. `CreateDirectory` idempotenttir—klasör zaten varsa hiçbir şey yapmaz, bu yüzden her çalıştırmada güvenle çağrılabilir.

### Görüntüden Metin Tanıma ve Görüntüyü Metne Dönüştürme

Şimdi OCR motorunu başlatıp bulduğumuz her dosya üzerinde döngü oluşturuyoruz. Döngü, `Directory.GetFiles` ile bir joker karakter (`*.*`) kullanır, böylece *tüm* dosyaları alır; ancak isterseniz filtreyi `*.png` veya `*.jpg` olarak daraltabilirsiniz.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**Burada ne oluyor?**  
- `ocrEngine.RecognizeImage(imagePath)` bitmap'i okur, OCR algoritmasını çalıştırır ve bir `OcrResult` nesnesi döndürür.  
- `ocrResult.Text` motorun okuyabildiği her şeyin düz metin temsilini içerir.  
- `File.WriteAllText` çıkarılan metinle yeni bir dosya oluşturur (veya mevcut bir dosyanın üzerine yazar).

Bu, **toplu OCR görüntüleri** işlem hattının tamamı, 30 satırdan az kodla.

## Profesyonel İpuçları ve Özel Durumlar

| Durum | Öneri |
|-----------|----------------|
| Görüntüler büyük ( > 5 MB ) | Tanıma hızını artırmak için yaklaşık 1500 px genişliğe yeniden ölçeklendirin, doğruluk kaybı olmadan. |
| PDF'leri desteklemeniz gerekiyor | Önce her PDF sayfasını bir görüntüye dönüştürün (ör. `Aspose.PDF` kullanarak), ardından aynı döngüye besleyin. |
| Bazı dosyalar görüntü değil (ör. `.txt`) | Basit bir filtre ekleyin: `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| Çok dilli destek istiyorsunuz | Döngüden önce `ocrEngine.Language = Language.English | Language.Spanish;` ayarlayın. |
| İlerleme raporlaması gerekiyor | `foreach` içinde `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` yazın. |

> **Pro ipucu:** OCR çağrısını bir `try/catch` bloğuna alın. Ara sıra bozuk bir görüntü `RecognizeImage`'in istisna fırlatmasına neden olur; bunu yakalamak tüm toplu işlemin durmasını engeller.

## Beklenen Çıktı

Program tamamlandığında, `outputFolder` her özgün görüntü için bir `.txt` dosyası içerecek:

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

Her dosya motorun çıkardığı ham metni tutar, örneğin:

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

Artık bu dosyaları bir arama indeksine besleyebilir, duygu analizi yapabilir veya sadece uyumluluk için arşivleyebilirsiniz.

## Sık Sorulan Sorular

**S: Bu Linux'ta çalışır mı?**  
C: Kesinlikle. Aspose.OCR çapraz platformdur ve burada kullanılan `System.IO` API'leri işletim sistemine bağımlı değildir. Sadece klasör yollarını (`/home/user/images`) ayarlamanız yeterlidir.

**S: **read files from directory** işlemini özyinelemeli (recursive) yapmak istersem ne yapmalıyım?**  
C: `SearchOption.TopDirectoryOnly` yerine `SearchOption.AllDirectories` kullanın. Daha derin klasörlerde izin sorunlarına dikkat edin.

**S: OCR ne kadar doğru?**  
C: Doğruluk, görüntü kalitesi, yazı tipi ve dile bağlıdır. En iyi sonuçlar için yüksek çözünürlüklü taramalar ve temiz arka planlar kullanın. Ayrıca `ocrEngine.Config`'i ayarlayarak eğrilik düzeltme veya gürültü azaltma etkinleştirebilirsiniz.

## Sonuç

Artık Aspose.OCR kullanarak C#'ta **toplu OCR görüntüleri** nasıl yapılacağını öğrendiniz; bir dizinden dosyaları okumaktan **görüntüden metin tanımaya** ve sonunda **görüntüyü metne dönüştürme** dosyalarına kadar. Yukarıdaki tam ve çalıştırılabilir örnek doğrudan çalışmalıdır ve ipuçları bölümü çözümü ölçeklendirmek veya özelleştirmek için bir yol haritası sunar.

Sonraki adımlar? WinForms veya WPF ile basit bir UI eklemeyi deneyin, çıktıyı Azure Cognitive Search ile bütünleştirin veya Aspose.OCR tarafından desteklenen diğer dillerle deney yapın. Temel döngüyü kavradıktan sonra sınır yoktur.

Kodlamaktan keyif alın, ve OCR toplularınız hatasız olsun!  

![Toplu OCR görüntüleri sürecinin diyagramı](batch-ocr-images-diagram.png "Toplu OCR görüntüleri iş akışı")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}