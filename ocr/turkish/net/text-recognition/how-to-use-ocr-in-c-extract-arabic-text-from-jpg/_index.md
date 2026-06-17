---
category: general
date: 2026-03-21
description: C#'ta OCR nasıl kullanılır, görüntü dosyalarından metin tanıma. Bir JPG'den
  Arapça metni çıkarıp düz metne dönüştürmeyi öğrenin.
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: tr
og_description: C#'ta OCR kullanarak görüntü dosyalarındaki metni nasıl tanıyacağınızı
  öğrenin. Bu rehber, bir JPG'den Arapça metni nasıl çıkarıp düzenlenebilir metne
  dönüştüreceğinizi gösterir.
og_title: C#'ta OCR Nasıl Kullanılır – JPG'den Arapça Metin Çıkarma
tags:
- OCR
- C#
- Aspose
- Arabic
title: C#'de OCR Nasıl Kullanılır – JPG'den Arapça Metin Çıkarma
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – JPG'den Arapça Metin Çıkarma

Hiç **OCR nasıl kullanılır** diye merak ettiniz mi, sabit diskinizde Arapça metin içeren bir resim olduğunda? Tek başınıza değilsiniz. Birçok geliştirici aynı duvara çarpıyor: bir JPEG'leri var, içindeki kelimelere ihtiyaçları var ve sıfırdan bir sinir ağı kodlamak istemiyorlar.  

İyi haber? Birkaç satır C# ile **görüntüden metin tanıma** dosyalarından her Arapça karakteri çıkarabilir ve saklayabileceğiniz, arayabileceğiniz ya da görüntüleyebileceğiniz temiz bir dize elde edebilirsiniz. Bu öğreticide tüm süreci adım adım inceleyeceğiz—kütüphaneyi kurma, dil modelini yapılandırma, taramayı çalıştırma ve sonunda sonucu yazdırma. Sonunda **JPG'yi metne dönüştürme** işlemini saniyeler içinde yapabilecek durumdasınız.

## Öğrenecekleriniz

- .NET için Aspose.OCR NuGet paketini kurun.
- Küçük işler için mükemmel olan CPU modunda OCR motorunu başlatın.
- Arapça dil modelini otomatik olarak yükleyin.
- JPEG görüntüsü üzerinde OCR çalıştırın ve tanınan metni alın.
- Büyük dosyalar veya eksik dil verileri gibi yaygın tuzakları yönetin.

OCR konusunda önceden bir deneyime ihtiyacınız yok; sadece temel C# ve Visual Studio bilgisi yeterli. Hazır mısınız? Hadi başlayalım.

## .NET için Aspose OCR'yi Kurun

Herhangi bir kod çalışmadan önce Aspose.OCR kütüphanesine ihtiyacınız var. NuGet paketi olarak gelir, bu yüzden kurulum tek bir komutla yapılır:

```bash
dotnet add package Aspose.OCR
```

Ya da Visual Studio UI'ı tercih ediyorsanız, **Tools → NuGet Package Manager → Manage NuGet Packages for Solution** menüsünü açın, **Aspose.OCR**'u aratın ve **Install**'a tıklayın. Paket, motorun ilk kullanımda indireceği dil veri dosyaları da dahil olmak üzere ihtiyacınız olan her şeyi getirir.

> **Pro tip:** Projenizin .NET 6 veya daha yeni bir sürümü hedeflediğinden emin olun; eski framework'ler hâlâ çalışır ama performans iyileştirmelerinden mahrum kalırsınız.

## OCR Motorunu Başlatın

Kütüphane yerinde olduğuna göre `OcrEngine` örneği oluşturabiliriz. Çoğu küçük ölçekli görev için varsayılan CPU modu fazlasıyla yeterlidir—ana bilgisayarın işlemcisini kullanır ve GPU hızlandırması için gereken ekstra kurulumu önler.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

Neden her seferinde yeni bir motor oluşturuyoruz? `OcrEngine` nesnesi dil, DPI ve çıktı formatı gibi yapılandırmaları tutar. Tek bir işlemle sınırlı tutarak temiz bir durum garantiler ve farklı dil modelleri arasında istem dışı karışıklıkları önlersiniz.

## Arapça Dil Modelini Yükleyin

Aspose, ihtiyaca göre dil paketlerini getirir. İlk kez `Language.Arabic` atadığınızda kütüphane yaklaşık 30 MB veri indirir ve makinenizdeki bir önbellek klasörüne kaydeder. Bu tek seferlik indirme, sonraki çalıştırmalarda ışık hızında performans sağlar.

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

Ek script'leri (örneğin İngilizce veya Hintçe) desteklemeniz gerektiğinde sadece enum değerini değiştirin—ekstra kod yazmanıza gerek yok. Motor her dili ayrı ayrı önbelleğe alır.

## JPG Görüntüsü Üzerinde OCR Çalıştırın

Motor hazır ve Arapça modeli yüklendiğinde, işlemek istediğiniz görüntüyü ona yönlendirin. Yol mutlak ya da göreli olabilir; dosyanın var olduğundan ve okunabilir olduğundan emin olun.

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**Köşe durumu:** JPEG'iniz çok büyükse (5 MB üzeri) önce ölçeklendirmek isteyebilirsiniz. Büyük görüntüler bellek kullanımını artırır ve tanıma süresini yavaşlatabilir. `System.Drawing` ya da `ImageSharp` kullanarak hızlı bir ön‑boyutlandırma, işleme süresini önemli ölçüde azaltabilir.

## Tanınan Metni Alın ve Görüntüleyin

`Recognize` metodu bir `OcrResult` nesnesi döndürür. `Text` özelliği, motorun okuyabildiği her şeyin düz metin temsilini içerir.

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

Programı çalıştırdığınızda Arapça karakterlerin konsola yazdırıldığını, orijinal sıralama ve satır sonlarını koruduğunu görmelisiniz. Metni bir dosyaya kaydetmek isterseniz sadece `File.WriteAllText` ile yazın.

### Tam Çalışan Örnek

Hepsini bir araya getirerek, işte tamamen hazır, çalıştırılabilir bir konsol uygulaması:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Beklenen çıktı (örnek):**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

Çıktı bozuk görünüyorsa, görüntünün net olduğundan ve dilin `Arabic` olarak ayarlandığından emin olmak için tekrar kontrol edin. Bulanık taramalar veya döndürülmüş sayfalar, OCR'ın takılmasının yaygın nedenlerindendir.

## Sık Sorulan Sorular & İpuçları

- **Görüntü hem Arapça hem de İngilizce içeriyorsa ne olur?**  
  `ocrEngine.Settings.Language = Language.Multilingual;` ayarını yaparak Aspose'un birden fazla script'i otomatik algılamasını sağlayın.

- **İşlemeyi GPU ile hızlandırabilir miyim?**  
  Evet—uyumlu bir grafik kartınız ve CUDA çalışma zamanı yüklüyse, varsayılan motoru `new OcrEngine(OcrEngineMode.Gpu)` ile değiştirin.

- **UI'da sağ‑dan‑sola (RTL) renderlamayı nasıl yönetirim?**  
  Ham dize Unicode'dur; çoğu modern UI çerçevesi (WinForms, WPF, ASP.NET) uygun `FlowDirection` ayarlandığında RTL düzeni otomatik destekler.

- **Görüntü boyutu konusunda bir limit var mı?**  
  Teknik olarak yok, ancak bellek tüketimi çözünürlükle artar. Çok büyük taramalar (ör. taranmış kitaplar) için sayfayı tek tek işlemek daha iyidir.

## Görsel Genel Bakış

Aşağıda, görüntü dosyasından çıkarılan metne kadar olan akışı gösteren basit bir diyagram yer alıyor.  

![C#'ta Görüntüden Metne Dönüşümünü Gösteren OCR Akış Diyagramı](/images/ocr-flow.png)

*Alt metin:* *C#'ta görüntüden metne dönüşümü gösteren OCR akış diyagramı.*

## Sonraki Adımlar

Artık **OCR nasıl kullanılır** konusunda Arapça JPEG'lerde ustalaştığınıza göre çözümü genişletebilirsiniz:

- **Toplu işleme:** Bir klasördeki tüm görüntüler üzerinde döngü kurun ve her sonucu ayrı bir `.txt` dosyasına yazın.
- **Son‑işleme:** Gereksiz noktalama işaretlerini veya satır sonlarını temizlemek için düzenli ifadeler (regex) kullanın.
- **Entegrasyon:** Çıkarılan dizeleri bir arama indeksine (ör. Azure Cognitive Search) besleyerek taranmış belgeler üzerinde tam metin araması yapın.

Başka dillere meraklıysanız sadece `Language` enum değerini değiştirin. Tabloları ya da el yazısı notları çıkarmak ister misiniz? Aspose.OCR ayrıca tanıma öncesinde blokları bölümlendirebilen `LayoutAnalysis` özellikleri de sunar.

---

### TL;DR

Artık **OCR nasıl kullanılır** konusunda C# ile **JPG'den Arapça metin çıkarma**, **görüntüden metin tanıma** ve **JPG'yi metne dönüştürme** işlemlerini biliyorsunuz. Yukarıdaki tam, çalıştırılabilir örnek, NuGet paketini kurmaktan son dizeyi yazdırmaya kadar her adımı gösteriyor. Bir örnek görüntü alın, kodu yapıştırın ve sihrin gerçekleşmesini izleyin—harici hizmetlere gerek yok. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}