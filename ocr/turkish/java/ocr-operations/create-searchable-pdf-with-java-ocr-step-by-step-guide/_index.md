---
category: general
date: 2026-04-29
description: Java OCR kullanarak taranmış dosyalardan aranabilir PDF oluşturun. Taranmış
  PDF'yi nasıl dönüştüreceğinizi, taranmış belgeleri nasıl işleyeceğinizi ve aranabilir
  PDF'yi hızlı bir şekilde nasıl oluşturacağınızı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- java pdf ocr
- process scanned documents
- make searchable pdf
language: tr
og_description: Java OCR kullanarak aranabilir PDF oluşturun. Bu kılavuz, taranmış
  PDF'yi nasıl dönüştüreceğinizi, taranmış belgeleri nasıl işleyebileceğinizi ve aranabilir
  PDF'yi verimli bir şekilde nasıl oluşturacağınızı gösterir.
og_title: Java OCR ile aranabilir PDF oluşturma – Tam Kılavuz
tags:
- PDF
- OCR
- Java
title: Java OCR ile Aranabilir PDF Oluşturma – Adım Adım Kılavuz
url: /tr/java/ocr-operations/create-searchable-pdf-with-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR ile Arama Yapılabilir PDF Oluşturma – Adım Adım Kılavuz

Hiç **arama yapılabilir PDF** oluşturmanız gerektiğinde, taranmış görüntüler yığınıyla ne yapacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici, kağıt arşivleri dijitalleştirirken bu engelle karşılaşıyor. İyi haber şu ki, birkaç satır Java ve Aspose OCR ile **taran PDF'yi** tamamen arama yapılabilir bir belgeye dakikalar içinde **dönüştürebilirsiniz**.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: kütüphaneyi kurmaktan, kaynak dosyanıza işaret etmeye, performans ayarlarını ince ayar yapmaya, son olarak çıktının gerçekten *arama yapılabilir* olduğunu doğrulamaya kadar. Sonunda **taran belgeleri** toplu olarak nasıl **işleyeceğinizi** ve **arama yapılabilir PDF** dosyalarını herhangi bir PDF görüntüleyicinin arama işleviyle uyumlu şekilde nasıl oluşturacağınızı öğreneceksiniz.

## Öğrenecekleriniz

* Aspose OCR for Java paketini nasıl kurup içe aktaracağınızı.  
* Taran bir kaynaktan **arama yapılabilir PDF** oluşturmak için gereken tam kodu.  
* GPU hızlandırması ve paralel iş parçacıklarını etkinleştirmenin büyük toplu işler için dakikalar kazandırmasını.  
* Karışık görüntü/metin sayfaları içeren PDF'ler veya GPU'su olmayan makinelerde çalıştırma gibi kenar durumlarını ele alma ipuçları.  

Önceden OCR deneyimi gerekmez; sadece temel bir Java kurulumunuz ve kağıdı arama yapılabilir metne dönüştürme merakınız yeterli.

---

## Arama Yapılabilir PDF Oluşturma – Genel Bakış

Kodlara geçmeden önce çözdüğümüz problemi netleştirelim. *Taran PDF* aslında bir dizi görüntüdür; ekranda gördüğünüz metin gerçek karakterler değildir, bu yüzden normal bir “bul” işlemi hiçbir şey döndürmez. Her sayfada OCR (Optik Karakter Tanıma) çalıştırarak, orijinal görüntüyü korurken gizli bir metin katmanı ekleriz—bu da PDF'yi *arama yapılabilir* kılar.

Bunu, PDF'nize “görebilen bir beyin” eklemek gibi düşünün. Aspose OCR kütüphanesi ağır işi yapar: bitmap'i analiz eder, Unicode karakterleri çıkarır ve bunları PDF yapısına geri yazar.

## Taran PDF'yi Dönüştür – Ortamınızı Hazırlayın

### 1. Aspose OCR bağımlılığını ekleyin

Maven kullanıyorsanız, aşağıdaki snippet'i `pom.xml` dosyanıza ekleyin. (Gradle kullanıcıları koordinatları buna göre uyarlayabilir.)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Pro tip:** Her zaman en yeni kararlı sürümü kullanın; yeni sürümler performans artışı ve daha iyi dil desteği getirir.

### 2. Java sürümünü doğrulayın

Aspose OCR, Java 8 ve üzerini gerektirir. Terminalinizde `java -version` komutunu çalıştırın—eğer 1.8 veya daha yeni bir sürüm görüyorsanız, hazırsınız demektir.

---

## Java PDF OCR – Dönüştürücüyü yapılandırma

Kütüphane artık sınıf yolunda olduğuna göre, **arama yapılabilir PDF** oluşturacak Java programını yazmaya başlayabiliriz. Aşağıda her bölümün satır satır açıklaması yer alıyor.

### Adım 1: Kaynak ve hedef yollarını tanımlayın

```java
// Step 1: Specify the input scanned PDF and the output searchable PDF
String sourcePdfPath = "YOUR_DIRECTORY/input.pdf";
String searchablePdfPath = "YOUR_DIRECTORY/searchable_output.pdf";
```

*Why?* OCR motorunun yalnızca görüntü PDF'sini (`sourcePdfPath`) nereden okuyacağını ve gizli metin katmanını içeren yeni dosyayı (`searchablePdfPath`) nereye yazacağını bilmesi gerekir. Yolları proje köküne göre mutlak ya da göreli tutun; dosya sistemini şaşırtabilecek boşluklar veya özel karakterlerden kaçının.

### Adım 2: Dönüştürücüyü örnekleyin

```java
// Step 2: Create the OCR converter and assign source/destination files
PdfOcrConverter ocrConverter = new PdfOcrConverter();
ocrConverter.setSourcePdf(sourcePdfPath);
ocrConverter.setDestinationPdf(searchablePdfPath);
```

`PdfOcrConverter`, OCR boru hattını yöneten çekirdek sınıftır. `setSourcePdf` ve `setDestinationPdf` çağrılarıyla giriş ve çıkışı bağlarız. Bu çağrılardan birini atlamanız durumunda kütüphane çalışma zamanında bir `IllegalArgumentException` fırlatır—bu yüzden satırları iki kez kontrol edin.

### Adım 3: (İsteğe Bağlı) GPU ve çoklu iş parçacığı ile performansı artırın

```java
// Step 3: (Optional) Enable GPU acceleration and set parallel processing
ocrConverter.getProcessingSettings().setUseGpu(true);
ocrConverter.getProcessingSettings().setMaxParallelThreads(4);
```

*Why enable GPU?* Uyumlu bir NVIDIA GPU'suna sahipseniz, OCR motoru piksel‑ağır işleri grafik kartına devrederek işleme süresini büyük ölçüde kısar—genellikle büyük PDF'lerde %30‑50  azalma sağlar.  

*Why set parallel threads?* Her sayfa bağımsız işlenir, bu yüzden dönüştürücüye birden fazla iş parçacığı vermek, birkaç sayfayı aynı anda işlemeye olanak tanır. `4` sayısı tipik bir quad‑core dizüstü bilgisayarda iyi çalışır; donanımınıza göre artırıp azaltabilirsiniz.

> **Edge case:** Sunucunuzda GPU yoksa `setUseGpu(false)` bırakın (ya da çağrıyı tamamen kaldırın). Dönüştürücü, hata vermeden CPU‑only moda geri dönecektir.

### Adım 4: Dönüştürmeyi çalıştırın

```java
// Step 4: Run the conversion to produce a searchable PDF
ocrConverter.convert();
```

Bu tek satır ağır işi yapar: her sayfayı okur, OCR çalıştırır, gizli bir metin akışı oluşturur ve sonunda çıktıyı PDF olarak yazar. Metot, iş bitene kadar bloklanır, bu yüzden ardından bir onay mesajı ekleyebilirsiniz.

### Adım 5: Kullanıcıyı bilgilendirin

```java
// Step 5: Inform the user where the searchable PDF was saved
System.out.println("Searchable PDF created at: " + searchablePdfPath);
```

Komut satırı demosu için basit bir `println` yeterlidir, ancak gerçek bir uygulamada yolu loglamak ya da bir servis metodundan döndürmek isteyebilirsiniz.

---

## Taran belgeleri işleyin – Programı çalıştırın

Aşağıdaki tam kodu `PdfToSearchablePdf.java` olarak kaydedin, derleyin ve terminalden çalıştırın. İşaret ettiğiniz `input.pdf` gerçekten taranmış görüntüler içeriyorsa, OCR motorunun tanıyacak bir şeyleri olacaktır; aksi takdirde hiçbir şey tanınmayacaktır.

```java
import com.aspose.ocr.*;

public class PdfToSearchablePdf {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the input scanned PDF and the output searchable PDF
        String sourcePdfPath = "YOUR_DIRECTORY/input.pdf";
        String searchablePdfPath = "YOUR_DIRECTORY/searchable_output.pdf";

        // Step 2: Create the OCR converter and assign source/destination files
        PdfOcrConverter ocrConverter = new PdfOcrConverter();
        ocrConverter.setSourcePdf(sourcePdfPath);
        ocrConverter.setDestinationPdf(searchablePdfPath);

        // Step 3: (Optional) Enable GPU acceleration and set parallel processing
        ocrConverter.getProcessingSettings().setUseGpu(true);
        ocrConverter.getProcessingSettings().setMaxParallelThreads(4);

        // Step 4: Run the conversion to produce a searchable PDF
        ocrConverter.convert();

        // Step 5: Inform the user where the searchable PDF was saved
        System.out.println("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Beklenen çıktı** (her şey doğru kurulduysa):

```
Searchable PDF created at: YOUR_DIRECTORY/searchable_output.pdf
```

`searchable_output.pdf` dosyasını Adobe Reader’da açın, **Ctrl + F** tuşlarına basın ve taranmış sayfalarda bulunan bir kelimeyi aramayı deneyin. OCR başarılıysa, vurgulama eşleşen konuma atlayacaktır—görünür sayfa hâlâ bir görüntü olsa da.

---

## Arama Yapılabilir PDF Oluştur – Sonucu Doğrulama

### Hızlı kontrol

1. Oluşturulan PDF'yi metin aramasını destekleyen herhangi bir görüntüleyicide açın.  
2. *Bul* özelliğini kullanarak, orijinal taranmış sayfalardan birinde kesinlikle bulunan bir ifadeyi arayın.  
3. İfade vurgulanıyorsa, **arama yapılabilir PDF** oluşturmayı başarıyla tamamlamışsınız demektir.

### Programatik doğrulama (isteğe bağlı)

Toplu bir işlem hattı kuruyorsanız, gizli metin katmanının varlığını programatik olarak doğrulamak isteyebilirsiniz:

```java
import com.aspose.pdf.*;

Document doc = new Document(searchablePdfPath);
boolean hasText = doc.getPages().get_Item(1).getParagraphs().size() > 0;
System.out.println("Text layer present? " + hasText);
```

`true` sonucu, OCR adımının metin içeriği eklediği anlamına gelir; `false` ise bir şeylerin ters gittiğini gösterir—belki kaynak PDF'de görüntü yoktur ya da OCR motoru sessizce başarısız olmuştur.

---

## Yaygın tuzaklar ve nasıl kaçınılır

| Problem | Neden olur | Çözüm |
|---------|------------|------|
| **Empty output PDF** | Kaynak dosya taranmış bir görüntü değil (zaten metin içeriyor) | Gerçek bir taranmış PDF kullandığınızdan emin olun; aksi takdirde dönüştürücü OCR yapılacak bir şey bulamaz. |
| **Out‑of‑memory error** on huge PDFs | Varsayılan bellek tahsisi çok büyük belgeler için yetersiz | JVM heap'ini artırın (`-Xmx2g` veya daha yüksek) ya da `PdfOcrConverter.setPageRange` kullanarak dosyayı parçalar halinde işleyin. |
| **GPU not detected** | NVIDIA sürücüleri eksik veya GPU uyumsuz | Ya doğru sürücüleri kurun ya da `setUseGpu(false)` ayarlayın. |
| **Incorrect language detection** | OCR varsayılan olarak İngilizce; belgeniz başka bir dilde | `ocrConverter.getProcessingSettings().setLanguage("fr")` gibi uygun ISO kodunu çağırın. |

## Sonraki adımlar: ölçeklendirme ve gelişmiş özellikler

Şimdi tek bir dosyada **taran PDF'yi dönüştürebildiğinize** göre şu genişletmeleri düşünün:

* **Batch processing** – PDF dizininde döngü oluşturun, başlangıç maliyetini azaltmak için tek bir `PdfOcrConverter` örneğini yeniden kullanın.  
* **Custom OCR settings** – DPI ayarlayın, gürültü azaltmayı etkinleştirin, veya

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}