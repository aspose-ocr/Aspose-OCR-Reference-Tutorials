---
category: general
date: 2026-02-28
description: Çok sayfalı TIFF dosyasından C# ile aranabilir PDF oluşturun. Bu kılavuz,
  görüntüyü aranabilir PDF'ye dönüştürmeyi, tam bir C# OCR örneğiyle gösterir.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: tr
og_description: Aspose.OCR kullanarak bir TIFF'ten aranabilir PDF oluşturun. Görüntüleri
  aranabilir PDF'lere dönüştürmek için bu adım adım C# OCR örneğini izleyin.
og_title: C# ile Aranabilir PDF Oluştur – Görüntüden PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: C# ile Aranabilir PDF Oluşturma – Görüntüden PDF'ye OCR
url: /tr/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Aranabilir PDF Oluşturma – Görüntüden PDF OCR

Tarama belgesinden **aranabilir PDF** oluşturmanız gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Tek başınıza değilsiniz. Birçok ofis iş akışında aranabilir PDF, bir çıkmaz dosya ile aranabilir bir arşiv arasındaki farktır.  

Bu öğreticide, çok sayfalı bir TIFF'i aranabilir PDF'e dönüştüren tam bir **c# ocr example** üzerinden geçeceğiz, hepsi Aspose.OCR ile. Sonunda **image to searchable pdf** nasıl yapılır, **convert tiff to pdf** nasıl yapılır tam olarak bilecek ve herhangi bir .NET projesine ekleyebileceğiniz çalıştırmaya hazır bir kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

* C# projesinde Aspose.OCR'ı nasıl kurup referanslayacağınızı.  
* TIFF'i yükleme, dili ayarlama ve `RecognizeToPdf` metodunu çağırma adımlarını.  
* Her adımın neden önemli olduğunu – bellek yönetiminden dil seçimine kadar.  
* Büyük belgelerle başa çıkma, yaygın OCR sorunlarını giderme ve çözümü diğer görüntü formatlarına genişletme ipuçları.

**Prerequisites** – güncel bir .NET SDK (4.6+ veya .NET Core 3.1+), Visual Studio (veya tercih ettiğiniz IDE) ve bir Aspose.OCR lisansı (ücretsiz deneme testi için çalışır). Başka dış kütüphane gerekmez.

---

## Aranabilir PDF Oluşturma – Genel Bakış

Yüksek seviyede süreç şu şekilde görünür:

1. **Initialize** `OcrEngine`.  
2. **Load** kaynak görüntüyü (bizim örneğimizde bir TIFF).  
3. **Configure** dil ayarlarını daha iyi doğruluk için.  
4. **Run** OCR ve **save** sonucu doğrudan aranabilir bir PDF olarak kaydedin.  

Hepsi bu kadar. Aspose API'si zor işi üstlenir, böylece ayrı OCR ve PDF kütüphanelerini birleştirmeniz gerekmez.

---

## Adım 1: Aspose.OCR'ı Kurun ve Projenizi Ayarlayın

İlk olarak, Aspose.OCR NuGet paketini ekleyin:

```bash
dotnet add package Aspose.OCR
```

Veya Visual Studio'da Package Manager Console'u tercih ediyorsanız:

```powershell
Install-Package Aspose.OCR
```

Paket geri yüklendikten sonra, proje dosyanızı açın ve referansı doğrulayın:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Pro ipucu:** En son kararlı sürümü (Aspose web sitesini kontrol edin) kullanın; böylece hata düzeltmeleri ve en yeni dil paketlerini alırsınız.

---

## Adım 2: TIFF'i PDF'e Dönüştür – Görüntüyü Yükleme

Şimdi, aranabilir hâle getirmek istediğiniz TIFF'i yükleyeceğiz. Aspose'un `Image.Load` metodu çok sayfalı TIFF'leri kutudan çıkar çıkmaz destekler.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Neden bu önemli:** Görüntüyü bir `using` bloğu içinde yüklemek, yönetilmeyen kaynakların hızlıca serbest bırakılmasını garanti eder—büyük belgeler işlenirken kritik öneme sahiptir.

---

## Adım 3: Görüntüden Aranabilir PDF – OCR Motoru Yapılandırması

OCR'ı çalıştırmadan önce, motorun hangi dili bekleyeceğini belirteceğiz. İngilizce çoğu durumda işe yarar, ancak herhangi bir `OcrLanguage` enum değerini kullanabilirsiniz.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Uzman notu:** Doğru dili seçmek, hatalı tanıma oranını büyük ölçüde azaltır. Karışık dilleriniz varsa, `|` operatörüyle birleştirebilirsiniz; örn., `OcrLanguage.English | OcrLanguage.French`.

---

## Adım 4: C# OCR Örneği – Tanıma ve Kaydetme

Motor hazır olduğunda, `RecognizeToPdf` metodunu çağırın. Bu metod, aranabilir PDF'i doğrudan diske yazar ve orijinal görüntünün arkasına görünmez bir metin katmanı ekler.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Bu satır çalıştırıldıktan sonra, `output.pdf` orijinal TIFF sayfalarını ve herhangi bir PDF okuyucusunun arama yapabileceği gizli bir metin katmanını içerecek.

---

## Adım 5: C# Görüntüden PDF – Sonucu Doğrulama

Her şeyin çalıştığını doğrulayalım. Oluşturulan PDF'i Adobe Reader'da (veya herhangi bir görüntüleyicide) açın ve kaynak TIFF'te bulunduğunu bildiğiniz bir kelimeyi aramayı deneyin.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Arama sonuç veriyorsa, bir görüntüden başarıyla **create searchable pdf** yapmış oldunuz. Aksi takdirde, dil ayarını veya kaynak TIFF'in kalitesini tekrar kontrol edin.

---

## Tam Çalışan Örnek

Tüm parçaları bir araya getirerek, derleyip çalıştırabileceğiniz bağımsız bir konsol uygulaması:

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Expected output** (in the console):

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

`output.pdf` dosyasını açın ve orijinal TIFF'ten herhangi bir kelimeyi görüntüleyicinin arama kutusuna yazarak eşleşmelerin vurgulandığını görmelisiniz.

![Aranabilir PDF Örneği](placeholder-image.png){: .align-center alt="aranabilir pdf örneği oluşturma"}

*Yukarıdaki ekran görüntüsü, gizli metin katmanı etkin bir şekilde bir görüntüleyicide açılmış aranabilir PDF'i göstermektedir.*

---

## Yaygın Sorular & Kenar Durumları

### TIFF'im çok büyük (yüzlerce sayfa) olsaydı ne olur?

Aspose.OCR sayfaları tek tek akıtır, ancak yine de bellek sınırlarına takılabilirsiniz. TIFF'i partiler halinde işlemeyi düşünün:

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Daha sonra, sayfa‑sayfa PDF'leri bir PDF kütüphanesiyle birleştirin (örneğin, Aspose.PDF).

### Farklı bir formata, örneğin aranabilir DOCX'e çıktı alabilir miyim?

Evet—`RecognizeToPdf` yerine `RecognizeToDocument` kullanın. API, PDF metodunun aynısını sunar, sadece hedef dosya uzantısını değiştirin.

### İngilizce dışındaki dilleri nasıl ele alırım?

`OcrLanguage.English` yerine uygun enum değerini koyun, örneğin `OcrLanguage.Spanish`. Dilleri birleştirebilirsiniz de:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### Şifre korumalı PDF'ler hakkında ne yapılmalı?

OCR adımından sonra, oluşturulan PDF'i Aspose.PDF ile açıp şifreleme uygulayabilirsiniz:

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Özet

TIFF görüntülerinden C# kullanarak **create searchable PDF** dosyaları oluşturmak için ihtiyacınız olan her şeyi ele aldık. Aspose.OCR'ı kurmaktan, görüntüyü yüklemeye, dili yapılandırmaya, OCR çalıştırmaya ve sonunda aranabilir çıktıyı doğrulamaya kadar, artık diğer formatlara uyarlayabileceğiniz sağlam bir **c# ocr example**'a sahipsiniz.  

Daha ileri gitmeye hazırsanız, şunları deneyin:

* **Convert TIFF to PDF** – aranabilir olmayan arşivler için (sadece OCR adımını atlayın).  
* **image to searchable pdf** ile deneyler yapın

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}