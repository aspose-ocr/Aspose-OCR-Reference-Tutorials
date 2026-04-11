---
category: general
date: 2026-04-11
description: Aspose OCR for C#'de OCR'yi devre dışı bırakmayı, çevrim dışı çalıştırmayı,
  internet olmadan görüntüden metin çıkarmayı ve OCR için görüntüyü doğru şekilde
  yüklemeyi öğrenin.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: tr
og_description: Aspose OCR for C#'de OCR'yi nasıl devre dışı bırakır ve çevrim dışı
  çalıştırır, internet gerektirmeden görüntüden metin çıkarır ve OCR için görüntüyü
  kolayca yükler.
og_title: C#'de OCR Nasıl Devre Dışı Bırakılır – Çevrimdışı Aspose OCR Rehberi
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: C#'de OCR'ı Nasıl Devre Dışı Bırakılır – Çevrimdışı Aspose OCR Kılavuzu
url: /tr/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR'ı Devre Dışı Bırakma – Offline Aspose OCR Rehberi

Gerçekten çevrim dışı bir çözüm gerektiğinde **OCR'ı nasıl devre dışı bırakacağınızı** hiç merak ettiniz mi? Belki ağ bağlantısına güvenemeyen güvenli bir masaüstü uygulaması geliştiriyorsunuzdur ya da beklenmedik indirmelerden kaçınmak istiyorsunuzdur. Her iki durumda da güzel haber, Aspose OCR'ın otomatik kaynak indirmesini kapatmanıza, yerel bir klasöre yönlendirmenize ve her şeyi şirket içinde tutmanıza izin vermesidir. Bu öğreticide ayrıca **görüntüden metin çıkarma** dosyalarını ve **OCR için görüntüyü yükleme** işlemini sorunsuz bir şekilde nasıl yapacağınızı göreceksiniz.

Motoru başlatmadan tanınan Japonca metni yazdırmaya kadar her adımı gösteren eksiksiz, hemen çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Harici belgeler yok, gizli bir sihir yok; sadece projenize bugün ekleyebileceğiniz sade C# kodu. Sonunda otomatik indirme özelliğini devre dışı bırakmanın neden önemli olduğunu, kaynak yolunu nasıl ayarlayacağınızı ve hangi tuzaklara dikkat etmeniz gerektiğini öğreneceksiniz.

## Önkoşullar

- .NET 6.0 (veya herhangi bir yeni .NET sürümü) makinenizde kurulu olmalı.  
- Aspose.OCR for .NET NuGet paketi (`Install-Package Aspose.OCR`).  
- İhtiyacınız olan dil kaynaklarını (ör. Japon modeli) içeren bir klasör.  
- OCR çalıştırmak istediğiniz bir görüntü dosyası (`japan_doc.png`).  

Dil paketleri eksikse, onları Aspose portalından bir kez indirin, `AsposeOCRResources` gibi bir klasöre çıkarın ve hazırsınız. Otomatik indirme özelliğini devre dışı bıraktıktan sonra başka indirme gerçekleşmeyecek.

![OCR'ı çevrim dışı devre dışı bırakma](/images/how-to-disable-ocr.png "OCR'ı devre dışı bırakma illüstrasyonu")

## Adım 1 – OCR Motoru Örneğini Oluşturma  

İlk yapmanız gereken `OcrEngine`'i örneklemektir. Bu nesneyi, görüntünüzü okuyacak beyin olarak düşünün.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Neden önemli:** Motor olmadan hiçbir şeyi yapılandıramazsınız. Nesne, kütüphanenin internete erişip erişemeyeceğini belirten kritik bayrağı da içeren tüm ayarları tutar.

## Adım 2 – Otomatik Kaynak İndirmeyi Devre Dışı Bırakma  

Varsayılan olarak Aspose OCR eksik dil dosyalarını anında indirmeye çalışır. Her şeyi çevrim dışı tutmak için `AutoDownloadResources` anahtarını `false` olarak ayarlayın.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Pro ipucu:** Bunu kapatmak sadece gizliliği garanti etmekle kalmaz, aynı zamanda motorun güncellemeleri kontrol etmek için zaman harcamaması nedeniyle ilk tanıma çalışmasını hızlandırır.

## Adım 3 – Yerel Kaynak Klasörünüzü Belirtme  

Şimdi motoru, önceden indirilmiş dil paketlerinin bulunduğu yere yönlendirin. Bu, önkoşullarda belirttiğiniz yoldur.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Ne yanlış gidebilir?** Yol hatalıysa veya gerekli dil dosyası eksikse, motor bir `ResourceNotFoundException` hatası fırlatır. Klasör adını ve Japon modelinin (`jpn.traineddata`) mevcut olduğunu iki kez kontrol edin.

## Adım 4 – Yerel Dil Modelini Seçme  

Diskte gerçekten bulunan dili seçin. Örneğimizde Japonca kullanıyoruz, ancak `Language.Japanese` ifadesini indirdiğiniz başka bir dil ile değiştirebilirsiniz.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Köşe durum:** Bazı diller ek sözlükler gerektirir (ör. Çince). Bu yardımcı dosyaların da aynı kaynak klasöründe olduğundan emin olun.

## Adım 5 – OCR İçin Görüntüyü Yükleme  

İşte **OCR için görüntüyü yüklediğimiz** yer. `ImageStream.FromFile` yöntemi dosyayı Aspose'ın işleyebileceği bir akıma okur.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **İpucu:** Desteklenen formatlar PNG, JPEG, BMP ve TIFF'tir. PDF'lerle çalışmanız gerekiyorsa, önce her sayfayı bir görüntüye dönüştürün.

## Adım 6 – Tanıma İşlemini Çalıştırma  

Şimdi motor, pikselleri okuyup metne dönüştürmeye çalışır.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Bu adım neden yavaş olabilir:** OCR CPU yoğun bir işlemdir, özellikle yüksek çözünürlüklü görüntülerde. Performans bir sorun ise, tanımadan önce görüntüyü küçültmeyi düşünün.

## Adım 7 – Çıkarılan Metni Çıktı Olarak Verme  

Son olarak, **görüntüden metin çıkarma** işlemini yapıp konsola yazdırıyoruz.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Programı çalıştırdığınızda `japan_doc.png` içindeki Japonca karakterler görüntülenmelidir. Her şey doğru ayarlandıysa, konsolda temiz bir Unicode metin bloğu göreceksiniz.

### Beklenen Çıktı

```
これはサンプルの日本語テキストです。
```

(Gerçek çıktınız görüntünün içeriğine bağlı olacaktır.)

## Yaygın Tuzaklar ve Nasıl Önlenir  

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|-------|
| **Dil dosyası eksik** | `AutoDownloadResources` false olduğu için motor dosyayı getiremez. | `ResourcesPath`'in `jpn.traineddata` dosyasını içeren klasöre işaret ettiğini doğrulayın. |
| **Yanlış görüntü yolu** | `ImageStream.FromFile` bir `FileNotFoundException` fırlatır. | Mutlak yollar kullanın veya çalışma dizininin doğru ayarlandığından emin olun. |
| **Desteklenmeyen görüntü formatı** | Aspose yalnızca belirli formatları okur. | `FromFile`'ı çağırmadan önce görüntünüzü PNG veya JPEG'e dönüştürün. |
| **Büyük görüntülerde bellek yetersizliği** | OCR tüm görüntüyü belleğe yükler. | Görüntüyü yeniden boyutlandırın veya parçalayın, ya da işlemin bellek limitini artırın. |

## Örneği Genişletme  

- **Toplu işleme:** Bir dizindeki görüntüler üzerinde döngü oluşturun, aynı tanıma kodunu çağırın ve her sonucu ayrı bir `.txt` dosyasına yazın.  
- **Farklı diller:** İlgili kaynak dosyalarını yerleştirdikten sonra `Language.Japanese` ifadesini `Language.English` (veya başka bir dil) ile değiştirin.  
- **Özel ön işleme:** OCR'dan önce Aspose.Imaging kullanarak görüntüyü eğriltme düzeltmesi yapın veya kontrastı artırın, böylece doğruluk artar.

## Sonuç  

Artık Aspose OCR için C#'ta **OCR'ı nasıl devre dışı bırakacağınızı** ve tamamen çevrim dışı çalıştıracağınızı biliyorsunuz. `AutoDownloadResources`'ı `false` olarak ayarlayarak, motoru yerel bir kaynak klasörüne yönlendirerek ve doğru şekilde **OCR için görüntüyü yükleyerek**, internete hiç dokunmadan güvenilir bir şekilde **görüntüden metin çıkarabilirsiniz**. Bu yaklaşım, güvenli ortamlar, CI pipeline'ları veya ağ erişiminin sınırlı olduğu herhangi bir senaryo için idealdir.

Bir sonraki adıma hazır mısınız? Taranmış PDF'lerin tamamını işleyin, farklı dil paketleriyle deney yapın veya OCR sonucunu aranabilir bir veritabanına entegre edin. Bugün oluşturduğunuz çevrim dışı yapı, herhangi bir şirket içi belge işleme akışı için sağlam bir temel oluşturur.

Kodlamanın tadını çıkarın ve herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}