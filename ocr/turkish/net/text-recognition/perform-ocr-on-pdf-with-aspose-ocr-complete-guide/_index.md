---
category: general
date: 2026-05-06
description: Aspose OCR kullanarak C#'de PDF dosyalarında OCR nasıl yapılır öğrenin.
  Bu öğreticide ayrıca PDF'den metin nasıl çıkarılır ve OCR için PDF nasıl yüklenir
  gösterilmektedir.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: tr
og_description: Aspose OCR kullanarak C#'de PDF üzerinde OCR nasıl yapılır keşfedin.
  Adım adım kod, açıklamalar ve PDF'den metni verimli bir şekilde çıkarmak için ipuçları.
og_title: Aspose OCR ile PDF'de OCR Yapın – Tam Rehber
tags:
- Aspose OCR
- C#
- PDF processing
title: Aspose OCR ile PDF'de OCR Yapma – Tam Rehber
url: /tr/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile PDF Üzerinde OCR Yapma – Tam Kılavuz

PDF dosyalarında **OCR yapma** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilmiyor muydunuz? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—örneğin otomatik fatura işleme veya arşiv raporlarını dijitalleştirme—taratılmış bir PDF'den metin çıkarabilmek bir zorunluluktur.  

Bu öğreticide, sadece Aspose OCR kütüphanesini kullanarak **PDF üzerinde OCR yapma** işlemini göstermekle kalmayıp, **PDF'den metin çıkarma**, **PDF'yi OCR için yükleme** ve çok‑dilli belgelerle başa çıkma konularını da ele alacağız. Sonunda, taranmış herhangi bir PDF'yi aranabilir, düzenlenebilir metne dönüştüren, çalıştırmaya hazır bir C# programına sahip olacaksınız.

## Öğrenecekleriniz

- .NET projesinde Aspose OCR nasıl kurulur.  
- **PDF'yi OCR için yükleme** ve motorun beslenmesi için gereken tam adımlar.  
- Farklı dilleri ayrı sayfalara eşleme—PDF İngilizce, Fransızca ve Almanca karışık olduğunda faydalı.  
- Çıktıyı doğrulama ve yaygın sorunları giderme yolları.  

> **Pro ipucu:** Büyük PDF'lerle çalışıyorsanız, sayfaları paralel işleyerek çalışma süresinden dakikalar kazanın. Daha sonra buna değineceğiz.

## Ön Koşullar

- .NET 6.0 veya üzeri (kod .NET Core ve .NET Framework ile de çalışır).  
- Geçerli bir Aspose OCR lisansı veya geçici bir değerlendirme anahtarı.  
- `multilang.pdf` adlı taranmış bir PDF, kodunuzdan referans verebileceğiniz bir klasörde bulunmalı.  

Başka üçüncü‑taraf paketine ihtiyaç yok.

---

## Adım 1 – Aspose OCR'ı Yükleyin ve Motoru Oluşturun

İlk olarak, projenize Aspose.OCR NuGet paketini ekleyin:

```bash
dotnet add package Aspose.OCR
```

Paket yüklendikten sonra OCR motorunu örnekleyebilirsiniz. Bu nesne işlemin kalbidir; görüntüleri, PDF'leri okuyup metne dönüştürmeyi bilir.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **Neden önemli:** Motoru bir kez başlatıp sayfalar arasında yeniden kullanmak bellek tüketimini azaltır ve işleme hızını artırır.

---

## Adım 2 – PDF Belgesini OCR İçin Yükleyin

Motor PDF'leri doğrudan açabilir, ancak hangi dosya üzerinde çalışacağını ona söylemeniz gerekir. Bu, birçok geliştiricinin gözden kaçırdığı **PDF'yi OCR için yükleme** adımıdır.

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

`YOUR_DIRECTORY` ifadesini makinenizdeki gerçek yol ile değiştirin. Dosya bir kaynak olarak gömülü ise, akış (stream) üzerinden de yükleyebilirsiniz.

> **Köşe durumu:** PDF şifre korumalıysa, `ocrEngine.LoadPdf(path, password)` çağrısı ile şifreyi sağlayın.

---

## Adım 3 – Sayfalara Dilleri Eşleştirin (İsteğe Bağlı ama Güçlü)

Sık sık taranmış bir PDF farklı dillerde sayfalar içerir. Varsayılan olarak Aspose OCR İngilizce varsayar ve bu da Fransızca veya Almanca sayfalarda kötü sonuçlara yol açar. Motorun her sayfa için hangi dili kullanacağını belirten basit bir sözlük oluşturacağız.

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **Bunu neden yaparsınız:** Doğru dili sağlamak, özellikle aksanlı karakterler ve dile özgü noktalama işaretleri için doğruluğu büyük ölçüde artırır.

---

## Adım 4 – OCR'ı Çalıştırın ve Sonucu Yakalayın

Şimdi asıl iş burada gerçekleşiyor. `Recognize()` çağrısı, az önce belirlediğimiz dil haritasına göre *tüm* sayfaları işler.

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

`recognitionResult` nesnesi, her sayfadan tanınan metni birleştiren bir `Text` özelliği içerir.

---

## Adım 5 – Çıkarılan Metni Çıktılayın

Son olarak, birleştirilmiş metni konsola yazdırıyoruz—ya da bir dosyaya, veritabanına ya da başka bir downstream sisteme yazabilirsiniz.

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

Dosya tercih ediyorsanız:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **Doğrulama ipucu:** Oluşan `extracted_text.txt` dosyasını açın ve her dilden bilinen kelimeleri arayın. Fransızca aksanlar bozuk görünüyorsa, dil haritanızı tekrar kontrol edin.

---

## Tam Çalışan Örnek

Tüm parçaları bir araya getirdiğimizde, tamamen çalıştırılabilir bir program elde ederiz. Yeni bir konsol projesine kopyalayıp **F5** tuşuna basın.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**Beklenen çıktı** (kısaltılmış):

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## Büyük PDF'ler ve Performans İyileştirmeleri

PDF'niz yüzlerce sayfa içeriyorsa, şu ayarlamaları göz önünde bulundurun:

1. **Parçalı işleme** – Aynı anda 50 sayfa işleyin, ardından ara sonuçları diske yazın.  
2. **Paralellik** – `Parallel.ForEach` kullanarak ayrı `OcrEngine` örnekleriyle çalışın (her motor başlatıldıktan sonra iş parçacığı güvenlidir).  
3. **Bellek yönetimi** – Her parçadan sonra `ocrEngine.Dispose()` çağrısı yaparak yerel kaynakları serbest bırakın.

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## Yaygın Tuzaklar & Çözüm Yolları

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| Fransızca sayfalarda bozuk karakterler | Yanlış dil ayarı | `PageLanguageProvider`'ın bu sayfalar için `OcrLanguage.French` döndürdüğünden emin olun. |
| Boş çıktı dosyası | PDF yüklenmedi (yanlış yol) | Yolun doğru olduğundan ve dosyanın başka bir işlem tarafından kilitlenmediğinden emin olun. |
| Çok büyük PDF'lerde bellek dışı hata | Motor tüm PDF'yi bir kerede yüklüyor | `LoadPdf`'nin tek‑sayfa aşırı yüklemesini kullanın veya parçalar halinde işleyin. |
| Yavaş işleme (> 5 dk 100 sayfa için) | Tek iş parçacıklı yürütme | Yukarıda gösterildiği gibi paralel işleme etkinleştirin. |

---

## Sonraki Adımlar – Temel OCR'ın Ötesine Geçmek

Artık **PDF üzerinde OCR yapma** ve **PDF'den metin çıkarma** becerilerine sahipsiniz; şimdi şunları düşünebilirsiniz:

- **Aranabilir PDF oluşturma** – Aspose.PDF kullanarak OCR metnini orijinal PDF'ye gömün, böylece aranabilir hâle gelsin.  
- **Veri çıkarma** – Düzenli ifadelerle fatura numaraları, tarih veya tutar gibi bilgileri çıkarın.  
- **AI entegrasyonu** – OCR çıktısını bir dil modeline (ör. Azure OpenAI) besleyerek özetleme veya sınıflandırma yapın.  

Tüm bu uzantılar hâlâ temel **PDF'yi OCR için yükleme** yeteneğine dayanır; yani temelinizi zaten atmış durumdasınız.

---

## Sonuç

Aspose OCR kullanarak C# ile **PDF üzerinde OCR yapma** ve **PDF'den metin çıkarma** için ihtiyacınız olan her şeyi kapsadık. Kütüphaneyi kurmaktan PDF'yi yüklemeye, sayfa bazlı dilleri atamaya, tanıma motorunu çalıştırmaya ve sonunda **PDF'den metin çıkarma** ve kaydetmeye kadar, bu öğretici size bağımsız, üretim‑hazır bir çözüm sunar.  

Paralel işleme, farklı dil kombinasyonları denemeye ya da OCR metnini diğer belge‑işleme kütüphaneleriyle birleştirmeye özgürsünüz. Bir sorunla karşılaşırsanız, yukarıdaki sorun giderme tablosuna bakın ya da bir yorum bırakın—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}