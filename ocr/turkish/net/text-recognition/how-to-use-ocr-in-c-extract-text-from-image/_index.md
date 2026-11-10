---
category: general
date: 2026-03-05
description: C#'ta OCR'ı kullanarak görüntüden metin çıkarmak. Görüntüyü metne dönüştürmeyi,
  Korece karakterleri okumayı ve OCR için görüntüyü hızlıca yüklemeyi öğrenin.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: tr
og_description: C#'ta OCR nasıl kullanılır ve görüntüden anında metin çıkarılır. Bu
  rehber, görüntüyü metne dönüştürmeyi, Korece karakterleri okumayı ve OCR için görüntüyü
  yüklemeyi gösterir.
og_title: C#'da OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma
tags:
- OCR
- C#
- Aspose
title: C#'da OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma

Korece metinle dolu bir ekran görüntünüz olduğunda ve düz metin olarak geri almanız gerektiğinde **OCR nasıl kullanılır** diye hiç merak ettiniz mi? Bu konuda yalnız değilsiniz. Bu öğreticide, **görüntüden metin çıkarma**, **görüntüyü metne dönüştürme** ve hatta Aspose.OCR ile **Korece karakterleri okuma** konularını gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

Ayrıca **OCR için görüntü yükleme** adımını da ele alacağız, böylece daha sonra “dosya bulunamadı” hatasıyla karşılaşmazsınız. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz bağımsız bir programınız olacak.

## Gereksinimler

- .NET 6+ (or .NET Framework 4.7.2 and later) – kod her iki ortamda da çalışır.
- Aspose.OCR for .NET – Aspose web sitesinden ücretsiz deneme sürümünü alabilirsiniz.
- Korece metin içeren bir örnek görüntü (`korean_doc.png`).
- Sevdiğiniz IDE (Visual Studio, Rider, VS Code – ne isterseniz).

Başka üçüncü‑taraf kütüphane gerekmez.

## Adım 1: Projeyi Kurun ve Aspose.OCR'yi Ekleyin

İlk olarak, yeni bir console uygulaması oluşturun:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ardından Aspose.OCR NuGet paketini ekleyin:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Bir lisans dosyanız varsa, proje kök dizinine yerleştirin; aksi takdirde ücretsiz deneme sürümü çalışır ancak çıktıya bir filigran ekler.

## Adım 2: OCR Nasıl Kullanılır – Motoru Başlatma

Şimdi C# kodunu yazacağız. **OCR nasıl kullanılır** sorusunun ilk adımı, `OcrEngine` nesnesini örneklemektir. Bu nesne kütüphanenin kalbidir; ileride ihtiyaç duyacağınız tüm ayarları tutar.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Neden önemli:** Uygun bir motor örneği olmadan dili ayarlayamaz, görüntü yükleyemez veya sonuçları alamazsınız. Motor ayrıca dahili kaynakları yönetir, bu yüzden bir kez oluşturup tekrar kullanmak, sürekli yeni nesneler oluşturmak yerine daha verimlidir.

## Adım 3: Dili Seçin – Korece Karakterleri Okuyun

Bir sonraki satır, motorun hangi dili arayacağını belirtir. Amacımız **Korece karakterleri okumak** olduğu için `OcrLanguage.Korean` ayarlıyoruz. Kullanım durumunuza bağlı olarak bunu Arapça, Tayca, Gujarati vb. dillerle değiştirebilirsiniz.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Neden önemli:** Dil seçimi doğruluğu büyük ölçüde artırır. OCR motoru, dile özgü sözlükler ve karakter modelleri kullanır; yanlış dil sağlamak bozuk çıktılar üretebilir.

## Adım 4: OCR için Görüntü Yükleme – Görüntüyü Metne Dönüştürme

Motor herhangi bir iş yapmadan önce **OCR için görüntü yükleme** gerekir. `ImageStream.FromFile` yöntemi dosyayı motorun anlayacağı bir formata okur.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Görüntü farklı bir klasördeyse, yolu sadece ayarlayın. Çalışma zamanında yürütülebilir dosyanın dosyayı bulabilmesi için dosyanın *Build Action* özelliğini “Copy if newer” olarak ayarlamayı unutmayın.

> **Yaygın tuzak:** Bir dize literalinde ters eğik çizgi (`\`) içeren bir yol vermek ve kaçış karakteri eklememek derleme hatasına neden olur. Ya çift ters eğik çizgi (`\\`) ya da verbatim string (`@"C:\path\file.png"`) kullanın.

## Adım 5: OCR Gerçekleştirme – Görüntüden Metin Çıkarma

Şimdi asıl iş burada gerçekleşir. `Recognize()` çağrısı OCR algoritmasını çalıştırır ve `Text` özelliği size ham dizeyi verir.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

Bu noktada **görüntüden metin çıkardınız** ve etkili bir şekilde **görüntüyü metne dönüştürdünüz**. Orijinal düzen satır sonları içeriyorsa sonuçta yeni satır karakterleri bulunabilir.

## Adım 6: Sonucu Göster – Çıktıyı Doğrulama

Son olarak, sonucu konsola yazdıralım ki çalıştığını doğrulayabilesiniz.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Programı çalıştırın:

```bash
dotnet run
```

### Beklenen Çıktı

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Eğer görüntüye benzer Korece karakterler görürseniz, tebrikler—Aspose.OCR ile **OCR nasıl kullanılır** konusunda uzmanlaştınız!

![how to use OCR example diagram](image.png)

*Image alt text: OCR kullanım örneği diyagramı, görüntünün yüklenmesinden tanınan metnin yazdırılmasına kadar olan akışı gösterir.*

## Kenar Durumları ve Varyasyonlar

### 1. Birden Çok Sayfayı İşleme

Eğer birden fazla sayfa içeren **görüntüden metin çıkarma** dosyalarına (ör. çok sayfalı TIFF) ihtiyacınız varsa, her sayfayı döngüye alıp her `ImageStream` örneği için `Recognize()` çağırın.

### 2. Düşük Kaliteli Taramalarla Baş Etme

Düşük çözünürlüklü görüntüler doğruluğu azaltabilir. `Recognize()` çağırmadan önce, Aspose'un ön işleme araçlarıyla görüntüyü iyileştirebilirsiniz:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Dilleri Dinamik Olarak Değiştirme

Karışık dilli bir belgeniz olduğunu varsayalım. Tanıma işlemleri arasında `ocrEngine.Language` değerini değiştirebilirsiniz:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Sonucu Bir Dosyaya Kaydetme

Eğer **görüntüyü metne dönüştürüp** saklamayı tercih ederseniz, dizeyi bir `.txt` dosyasına yazmanız yeterlidir:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Sıkça Sorulan Sorular

- **Bu kodu çalıştırmak için bir lisansa ihtiyacım var mı?**  
  Hayır. Ücretsiz deneme sürümü deneyler için yeterlidir, ancak çıktıya bir filigran ekler. Satın alınan lisans filigranı kaldırır ve tam performansı açar.

- **Bunu Linux'ta kullanabilir miyim?**  
  Kesinlikle. Aspose.OCR çapraz platformdur; sadece gerekli yerel bağımlılıkların (Linux'ta .NET Core için libgdiplus) kurulu olduğundan emin olun.

- **Görüntüm bir dosya yerine akış (stream) içinde olsaydı ne olur?**  
  `ImageStream.FromStream(yourStream)` kullanın – API herhangi bir `System.IO.Stream` kabul eder.

## Sonuç

Sizi adım adım **C#'ta OCR nasıl kullanılır** konusunda **görüntüden metin çıkarma**, **görüntüyü metne dönüştürme** ve **Korece karakterleri okuma** süreçlerinden geçirdik ve **OCR için görüntü yükleme** işlemini doğru şekilde yaptık. Yukarıdaki tam, çalıştırılabilir örnek doğrudan çalışmalı ve ek ipuçları daha ileri senaryolar için bir yol haritası sunar.

Bir sonraki meydan okumaya hazır mısınız? Farklı bir dil deneyin, PDF'leri sayfa sayfa işleyin veya OCR çağrısını bir web API'ye entegre edin, böylece kullanıcılar resim yükleyip anında metin sonuçları alabilir. Olasılıklar sonsuzdur ve artık üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}