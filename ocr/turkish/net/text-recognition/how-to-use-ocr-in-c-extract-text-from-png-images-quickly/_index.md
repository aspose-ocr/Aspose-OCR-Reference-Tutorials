---
category: general
date: 2026-03-29
description: Aspose ile OCR kullanarak PNG dosyalarından metin çıkarma ve görüntüleri
  metne dönüştürme. C#'ta adım adım asenkron OCR öğrenin.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: tr
og_description: Aspose ile C#'ta OCR kullanarak PNG dosyalarından metin çıkarma. Bu
  rehber, asenkron OCR, kod ve ipuçları konusunda size yol gösterir.
og_title: C#'ta OCR Nasıl Kullanılır – PNG Görüntülerinden Metin Çıkarma
tags:
- OCR
- C#
- Aspose
title: C#'de OCR Nasıl Kullanılır – PNG Görsellerinden Metni Hızlıca Çıkarın
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – PNG Görüntülerinden Metni Hızlıca Çıkarın

Hiç **OCR nasıl kullanılır** diye merak ettiniz mi ve birkaç PNG ekran görüntüsünden metin çıkarmak istediniz mi? Belki taranmış makbuzlar, faturalar veya UI taslaklarınız var ve bu metni aranabilir bir biçimde ihtiyacınız var. İyi haber? Aspose.OCR ile sadece birkaç satır asenkron C# kodu kullanarak görüntüleri metne dönüştürebilirsiniz.  

Bu öğreticide, PNG dosyalarından metni nasıl çıkaracağınızı adım adım gösterecek, her adımın neden önemli olduğunu açıklayacak ve her sayfa için tanınan metni ekrana yazdıran çalıştırmaya hazır bir program sunacağız. Sonuna geldiğinizde **görüntülerden metin çıkarma** işlemini belge incelemeden yapabilecek duruma geleceksiniz.

## Neler Öğreneceksiniz

- Aspose.OCR NuGet paketini kurma ve referans ekleme.  
- OCR motorunu başlatma ve dili ayarlama (bu örnekte İngilizce).  
- Hızlı, bloklamayan işleme için `RecognizeImagesAsync` metoduna bir PNG dosyaları dizisi gönderme.  
- `OcrResult` nesneleri üzerinden döngü kurarak çıkarılan stringleri çıktı olarak alma.  

Harici servis yok, karmaşık geri çağrılar yok— sadece .NET 6+ üzerinde çalışan temiz, async C#.

---

## Önkoşullar

| Gereksinim | Sebep |
|-------------|--------|
| .NET 6 SDK (veya daha yeni) | `async Main` gibi modern dil özellikleri. |
| Visual Studio 2022 veya VS Code | Kodu derleyip çalıştırmak için IDE. |
| Aspose.OCR NuGet paketi (`Aspose.OCR`) | Örnekte kullanılan `OcrEngine` sınıfını sağlar. |
| Birkaç PNG görüntüsü (`page1.png`, `page2.png`, …) | OCR sürecinin girdi dosyaları. |

Zaten bir .NET projeniz varsa sadece `dotnet add package Aspose.OCR` komutunu çalıştırın. Aksi takdirde `dotnet new console -n OcrDemo` ile yeni bir konsol uygulaması oluşturun.

---

## Adım 1: Aspose.OCR'ı Kurun ve Projeyi Hazırlayın

İlk olarak OCR kütüphanesini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

Neden önemli: Aspose.OCR, yerel OCR motorunu, dil paketlerini ve basit bir API'yi içinde barındırır. NuGet üzerinden eklemek, sürüm uyumluluğu ve otomatik güncellemeler garantiler.

---

## Adım 2: OCR Motorunu Başlatın ve Bir Dil Seçin

Motorun hangi dili arayacağını bilmesi gerekir. İngilizce en yaygın dildir, ancak `Language.Spanish`, `Language.French` gibi dilleri de tercih edebilirsiniz.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Pro ipucu:** Dili her zaman açıkça ayarlayın; varsayılan bırakmak doğruluğu düşürebilir ve işleme süresini artırabilir.

---

## Adım 3: PNG Dosyalarının Listesini Hazırlayın

Tek bir dosya ya da bir dizi gönderebilirsiniz. Dizi gönderdiğinizde motor, dosyaları asenkron olarak toplu işleyebilir; bu, birkaç sayfa için idealdir.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Görüntüleriniz bir alt klasörde ise, göreli yolu ekleyin (`"images/page1.png"`). Yol hatalıysa motor net bir `FileNotFoundException` fırlatır— dosya adlarını iki kez kontrol edin.

---

## Adım 4: Tüm Görüntülerde Asenkron OCR Çalıştırın

`RecognizeImagesAsync` metodu, bir `OcrResult` dizisi döndürür. Asenkron olduğu için UI (veya konsol) OCR arka planda çalışırken yanıt vermeye devam eder.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Neden async?**  
OCR'ı bir web API'sine ya da masaüstü uygulamasına entegre ediyorsanız, motor her pikseli tararken iş parçacığının bloklanmasını istemezsiniz. `await` iş parçacığını thread pool'a geri verir, ölçeklenebilirliği artırır.

---

## Adım 5: Her Sayfa İçin Çıkarılan Metni Gösterin

Artık sonuçlarımız var; bunlar üzerinden döngü kurup tanınan metni ekrana yazdıralım. `Text` özelliği, daha fazla işleme (ör. veritabanına kaydetme) hazır düz metin çıktısını içerir.

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Beklenen Çıktı

`page1.png` içinde “Invoice #12345” ve `page2.png` içinde “Total: $89.99” olduğunu varsayalım; aşağıdakine benzer bir çıktı görürsünüz:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

OCR hiçbir metin bulamazsa, `Text` özelliği boş bir string olur— üretim kodunda bunu `string.IsNullOrWhiteSpace` kontrolüyle ele alın.

---

## Tam Çalışan Örnek

Aşağıda `Program.cs` içine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Tüm using yönergeleri, async `Main` ve her adımı açıklayan yorumlar içerir.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Dosyayı kaydedin, PNG'lerinizi çalıştırılabilir dosyanın yanına (veya yolları ayarlayın) koyun ve çalıştırın:

```bash
dotnet run
```

Çıkarılan metnin konsola yazdırıldığını göreceksiniz; böylece **görüntüleri metne dönüştürme** işlemini başarıyla tamamlamış olacaksınız.

---

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Ne Yapmalı |
|-----------|------------|
| **Düşük çözünürlüklü PNG** | Tanıma başlamadan önce `ocrEngine.ImageProcessingOptions.Dpi` değerini artırın. |
| **Birden fazla dil** | `ocrEngine.Language = Language.English | Language.Spanish;` (bitwise OR) şeklinde ayarlayın. |
| **Yüzlerce dosyadan oluşan büyük batch** | Bellek dalgalanmalarını önlemek için (ör. 20 dosya) parçalar halinde `RecognizeImagesAsync` çağrısı yapın. |
| **Güven skoruna ihtiyaç** | Düşük kalite sonuçları filtrelemek için `ocrResults[i].Confidence` (0‑1 arasında bir float) kullanın. |

Bu ayarlamalar, demo aşamasından üretime geçerken OCR hattınızın sağlam kalmasını sağlar.

---

## Bonus: Sonuçları Bir Metin Dosyasına Kaydetme

Konsol çıktısı yerine kalıcı bir kopya isterseniz, ufak bir yardımcı ekleyin:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Artık **görüntülerden metin çıkarma** işlemini sonraki iş akışları (indeksleme, arama, dil modeli besleme vb.) için tek bir dosyada topladınız.

---

## Sonuç

Aspose ile C#'ta **OCR nasıl kullanılır** sorusunun cevabını adım adım gördük; **PNG dosyalarından metin çıkarma** ve **görüntüleri metne dönüştürme** işlemlerini verimli bir şekilde gerçekleştirdik. Async yaklaşım uygulamanızın yanıt vermesini sağlarken, sade API kodun okunabilirliğini ve bakımını artırır.  

Kendi belgelerinizle deneyin, farklı dilleri test edin ve çıktıyı bir arama indeksine ya da özetleme servisine bağlayın. Resimleri güvenilir bir şekilde aranabilir string'lere dönüştürdüğünüzde sınır yoktur.

---

### Sonraki Adımlar ve İlgili Konular

- **Diğer formatlardan (JPEG, TIFF) metin çıkarma** – sadece dosya uzantılarını değiştirin.  
- **Parallel.ForEach ile toplu işleme** büyük iş yükleri için.  
- **OCR sonrası temizlik** tarih, tutar veya kimlik gibi değerleri normalize etmek için düzenli ifadeler kullanma.  
- **Azure Cognitive Services entegrasyonu** bulut tabanlı OCR ve ek özellikler gerektiğinde.  

Herhangi bir sorunla karşılaşırsanız yorum bırakın ya da bu temel akışı nasıl genişlettiğinizi paylaşın. Mutlu kodlamalar!   ![OCR sonucu ekran görüntüsü, çıkarılan metni gösteriyor](/images/ocr-result.png){.align-center alt="OCR örneği çıktısı nasıl kullanılır"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}