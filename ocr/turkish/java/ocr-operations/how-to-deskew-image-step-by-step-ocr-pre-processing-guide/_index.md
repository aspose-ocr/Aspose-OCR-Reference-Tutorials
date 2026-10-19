---
category: general
date: 2026-02-19
description: OCR için görüntünün eğriliğini düzeltmeyi ve gürültüyü kaldırmayı öğrenin.
  Bu öğreticide metin görüntüsünü tanıma, görüntü döndürmesini düzeltme ve Aspose
  OCR ile görüntü OCR ön işleme nasıl yapılacağını gösterir.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: tr
og_description: Görüntüyü eğriltmeyi düzeltmek ve gürültüyü temizlemek, metin görüntüsünü
  hızlıca tanımanıza olanak sağlar. Bu kılavuzu izleyerek görüntü döndürmeyi düzeltin
  ve Aspose ile OCR ön işleme yapın.
og_title: Resmi Nasıl Düzeltiriz – Tam OCR Ön İşleme Eğitimi
tags:
- OCR
- Java
- Image Processing
title: Görüntüyü Eğri Düzeltme — Adım Adım OCR Ön İşleme Rehberi
url: /tr/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Eğikliği Düzeltme — Tam OCR Ön İşleme Eğitimi

Bir OCR motoruna beslemeden önce **görüntüyü eğikliği düzeltme** işlemini nasıl yapacağınızı hiç merak ettiniz mi? Belki bir grup makbuzu taradınız ve sayfalar hafifçe yana yatmış gibi görünüyor ya da tarama rastgele noktalara sahip. Bu yaygın bir sorun—eğik ve gürültülü fotoğraflar metin tanıma sürecini zorlaştırır.  

İyi haber? Aspose.OCR kullanarak sadece birkaç Java satırıyla görüntüyü döndürmeyi (image rotation) düzeltebilir ve gürültüyü (how to remove noise) temizleyebilirsiniz. Bu rehberde, gürültülü‑döndürülmüş bir PNG'yi yüklemek, eğikliği düzeltme + medyan gürültü giderme uygulamak ve **metin tanıma** yapıp sonucu yazdırmak için tüm akışı adım adım inceleyeceğiz. Sonunda, herhangi bir Java projesine ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- **Java 17** veya daha yeni (kod eski sürümlerle de derlenebilir, ancak 17 ideal).  
- **Aspose.OCR for Java** – en yeni JAR dosyasını Maven Central'dan (`com.aspose:aspose-ocr`) alabilirsiniz.  
- Döndürülmüş ve gürültülü bir görüntü dosyası (ör. `noisy-rotated.png`).  
- Basit bir IDE (IntelliJ, Eclipse veya hatta VS Code).  

Karmaşık derleme araçlarına gerek yok; basit bir `javac` + `java` çalıştırması yeterli.

---

## Adım 1 – OCR Motoru Örneğini Oluşturma  

İlk yaptığınız şey bir `OcrEngine` başlatmak. Bu, karakterleri sizin için okuyacak beyin gibi düşünülebilir.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **İpucu:** Birçok görüntü işliyorsanız motoru singleton olarak tutun; iç tamponları yeniden kullanır ve hızı artırır.

## Adım 2 – Eğikliği Düzeltme ve Medyan Gürültü Giderme (How to Remove Noise) Özelliğini Etkinleştirme

Şimdi motoru **görüntü döndürmeyi düzeltme** ve **gürültüyü nasıl kaldırılır** işlemlerini yapması için ayarlıyoruz. Her iki filtre de isteğe bağlıdır, ancak birlikte kullanıldıklarında doğruluğu büyük ölçüde artırırlar.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Neden medyan gürültü giderme? Kenarları (karakterleri tanımlayan çizgileri) korurken izole pikseları siler—temiz OCR için tam da ihtiyacınız olan şey budur.

## Adım 3 – İşlenecek Görüntüyü Yükleme  

Burada motoru temizlenmesi gereken dosyaya yönlendiriyoruz. `ImageStream.fromFile` PNG'yi belleğe okur.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Görüntünüz uzak bir sunucuda ise, bunun yerine bir `InputStream` sağlayın—Aspose bunu sorunsuz yönetir.

## Adım 4 – OCR'ı Çalıştırma ve Tanınan Metni Yakalama  

Ön işleme etkinleştirildiğinde, motor artık düzeltilmiş görüntüyü okur. `recognize()` çağrısı, çıkarılan dizeyi içeren bir `RecognitionResult` döndürür.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Orijinal fotoğraf eğik ve grenli olsa bile, konsolda temiz ve okunabilir bir metin görmelisiniz.

## Adım 5 – Sonucu Doğrulama (What to Expect)

Her şey doğru çalıştığında, konsol aşağıdakine benzer bir çıktı verir:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Çıktı hâlâ bozuk karakterler içeriyorsa, şunları kontrol edin:

- Görüntü çözünürlüğü (≥ 300 dpi ideal).  
- Dosya yolunun doğru olduğundan emin olun.  
- Ek filtrelerin (`setContrastStretch` gibi) yardımcı olup olmayacağını değerlendirin.

---

## İsteğe Bağlı: Örnek Görüntü ile Görsel Doğrulama  

Aşağıda döndürülmüş, gürültülü bir makbuzun küçük bir ön izlemesi yer alıyor. Eğikliği fark edin—kodumuz sizin için bunu düzeltecek.

![görüntüyü eğikliği düzeltme örneği](deskew-demo.png "görüntüyü eğikliği düzeltme")

*Alt metin: görüntüyü eğikliği düzeltme – işleme öncesi ve sonrası.*

---

## Sık Sorulan Sorular

### Bu sadece PNG/JPEG mi, PDF'lerde de çalışır mı?  
Aspose.OCR PDF'leri doğrudan okuyabilir; sadece `ImageStream.fromFile` yerine `ImageStream.fromPdf` kullanmanız yeterlidir. Aynı ön işleme bayrakları geçerlidir, böylece hâlâ **görüntüyü eğikliği düzeltme** ve **gürültüyü nasıl kaldırılır** işlemlerini yaparsınız.

### Orijinal yönelimi sonraki adımlar için korumam gerekirse?  
Ön işleme başlamadan önce görüntüyü klonlayabilirsiniz:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Eğikliği manuel olarak ayarlayabilir miyim?  
Evet—`setDeskewAngle(double degrees)` otomatik algılama algoritmasını geçersiz kılar. Aşırı döndürmelerde otomatik algılama başarısız olduğunda faydalıdır.

### Medyan gürültü giderme, Gaussian bulanıklaştırmadan nasıl farklıdır?  
Medyan filtre, her pikseli komşularının medyanı ile değiştirir ve kenarları korur. Gaussian bulanıklaştırma her şeyi yumuşatır, karakter çizgilerini de bulanıklaştırabilir—bu yüzden OCR için medyan daha güvenlidir.

---

## Sonuç  

Bu eğitimde **görüntüyü eğikliği düzeltme** işlemini, **gürültüyü nasıl kaldırılır** yöntemini ve Aspose OCR’ın yerleşik ön işleme özellikleriyle **metin tanıma** nasıl yapılır gösterdik. `setDeskew(true)` ve `setMedianDenoise(true)` ayarlarını etkinleştirerek otomatik olarak **görüntü döndürmeyi düzeltme** ve nokta‑nokta gürültüyü temizleme işlemlerini gerçekleştirirsiniz; böylece dağınık bir taramayı temiz bir metin dizesine dönüştürmüş olursunuz.  

Deney yapmaktan çekinmeyin: farklı gürültü giderme stratejileri deneyin, PDF'leri besleyin veya bir döngü içinde birden çok görüntüyü işleyin. Motor → ön işleme → tanıma modeli her senaryo için aynı kalır ve bu da herhangi bir OCR hattı için sağlam bir temel oluşturur.

**İleri adımlar** olarak şunları inceleyebilirsiniz:

- **Toplu işleme** – bir klasördeki tüm görüntüler üzerinde döngü kurup her sonucu bir `.txt` dosyasına yazdırma.  
- **Dil paketleri** – İngilizce dışı metinlerde doğruluğu artırmak için belirli bir dil sözlüğü yükleme.  
- **Gelişmiş filtreler** – düşük kontrastlı taramalar için `setContrastStretch` veya `setBinarization` gibi seçenekler.  

Başka sorularınız mı var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}