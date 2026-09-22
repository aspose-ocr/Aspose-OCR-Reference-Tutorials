---
category: general
date: 2026-02-09
description: Aspose OCR ile OCR'ı hızlıca nasıl kullanılır, görüntüden metin tanıma
  ve PNG'den metin çıkarma, mod ve GPU bellek sınırı ayarlanarak.
draft: false
keywords:
- how to use ocr
- recognize text from image
- extract text from png
- how to set mode
- set gpu memory limit
language: tr
og_description: OCR'yi verimli bir şekilde nasıl kullanılır – görüntüden metin tanımayı,
  PNG'den metin çıkarmayı, modu ayarlamayı ve Java'da GPU bellek sınırını kontrol
  etmeyi öğrenin.
og_title: Java'da GPU Hızlandırmalı OCR Nasıl Kullanılır
tags:
- OCR
- Java
- GPU
- Aspose
title: Java'da GPU Hızlandırmalı OCR Nasıl Kullanılır – Adım Adım Rehber
url: /tr/java/advanced-ocr-techniques/how-to-use-ocr-with-gpu-acceleration-in-java-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da GPU Hızlandırmalı OCR Kullanımı – Tam Programlama Öğreticisi

Milyon satır kod yazmadan bir resimden metin çıkarmak için **OCR nasıl kullanılır** diye hiç merak ettiniz mi? Yalnız değilsiniz. Birçok projede—fatura tarama, fiş işleme veya sadece eski belgeleri dijitalleştirme—geliştiriciler **görüntüden metin tanıma** için güvenilir bir yola ihtiyaç duyar, özellikle temiz, yüksek çözünürlüklü grafikler içeren PNG dosyalarına.  

İyi haber? Aspose OCR bu işi çocuk oyuncağı haline getiriyor ve birkaç yapılandırma ayarıyla ağır işi GPU’ya devredebilirsiniz. Bu öğreticide tüm süreci adım adım inceleyeceğiz: PNG dosyasını yüklemek, GPU işleme için **modu ayarlamak**, **GPU bellek limitini belirlemek** ve sonunda çıkarılan metni yazdırmak. Sonunda ihtiyacınız olan tam çalışan bir Java programına sahip olacaksınız.

## Öğrenecekleriniz

- Aspose OCR for Java’ı nasıl kurup içe aktaracağınızı.
- Kütüphaneyi kullanarak **görüntüden metin tanıma** nasıl yapılır.
- **PNG’den metin çıkarma** nasıl verimli yapılır.
- **Modu ayarlama** GPU’ya ve **GPU bellek limitini belirleme** ile bellek kullanımını kontrol etme.
- Gerçek dünyada karşılaşılan yaygın tuzaklar ve ipuçları.

### Önkoşullar

- Java 8 veya daha yeni bir sürüm (kod JDK 11 ile de derlenir).
- GPU hızlandırması istiyorsanız CUDA uyumlu bir sürücüye sahip NVIDIA GPU.
- Aspose OCR for Java JAR (Aspose sitesinden indirin veya Maven/Gradle ile ekleyin).
- Referans alabileceğiniz bir örnek PNG resmi (ör. `sample1.png`) bir klasöre yerleştirilmiş olmalı.

---

## OCR Kullanımı – GPU Modunu Etkinleştirme

İlk yapmanız gereken, Aspose OCR’a CPU yerine GPU’da çalışmasını istediğinizi söylemek. İşte **modu ayarlama** anahtar kelimesinin devreye girdiği yer.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Grab the configuration object
OcrEngineConfiguration config = ocrEngine.getConfiguration();

// Step 3: Switch processing mode to GPU
config.setProcessingMode(ProcessingMode.GPU);   // requires a CUDA‑compatible driver

// (Optional) Step 4: Limit GPU memory usage to 1024 MB
config.setGpuMemoryLimit(1024);                 // set gpu memory limit (MB)
```

**Neden önemli:**  
GPU işleme, büyük toplular veya yüksek çözünürlüklü görüntüler için dramatik derecede daha hızlı olabilir, ancak video belleğini de tüketir. `setGpuMemoryLimit` çağrısı, uygulamanızın tüm GPU’yu ele geçirmesini engeller; bu, aynı cihazda başka işler (ör. bir UI veya makine öğrenimi modeli) çalıştırıldığında kritik öneme sahiptir.

## Aspose OCR Kullanarak Görüntüden Metin Tanıma

Motor yapılandırıldıktan sonra, okumak istediğimiz dosyayı ona göstermek gerekir. Bu, **görüntüden metin tanıma**nın temelidir.

```java
// Step 5: Define the image to be processed
ImageRecognitionResult imageInfo = new ImageRecognitionResult();
imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

// Step 6: Run the OCR operation
RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);
```

**Arka planda ne oluyor?**  
Aspose OCR PNG’yi yükler, ön‑işleme (ikilileştirme, eğrilik düzeltme vb.) yapar ve ardından OCR sinir ağını GPU’da çalıştırır. Sonuç nesnesi ham metni ve her satır için güven skorlarını içerir.

## GPU Bellek Limitiyle PNG’den Metin Çıkarma

Tanıma işleminden sonra, düz metni çıkarmak çok basittir, ancak birçok geliştirici çıktıyı doğrulamayı unutur. İşte **PNG’den metin çıkarma**yı güvenli bir şekilde yapıp ekrana yazdırma yöntemi.

```java
// Step 7: Output the recognized text
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Beklenen çıktı (örnek):**

```
Recognized text:
Invoice #12345
Date: 2026-02-09
Total: $1,250.00
Thank you for your business!
```

Görüntü gürültü içeriyorsa veya alışılmadık fontlar varsa bozuk karakterler görebilirsiniz. Bu durumda ön‑işleme seçeneklerini ayarlamayı düşünün (ör. `config.setLanguage(Language.ENGLISH)` veya `config.setAutoSkewCorrection(true)`).

## Tam, Çalıştırılabilir Örnek

Aşağıda her şeyi bir araya getiren tam Java programı yer alıyor. `GpuExample.java` adlı bir dosyaya kopyalayıp yapıştırın, görüntü yolunu ayarlayın ve `javac`/`java` ya da IDE’nizle çalıştırın.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.configuration.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the image to be processed
        ImageRecognitionResult imageInfo = new ImageRecognitionResult();
        imageInfo.setImagePath("YOUR_DIRECTORY/sample1.png");

        // Step 2: Create the OCR engine and enable GPU processing
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration config = ocrEngine.getConfiguration();

        // Step 3: Set processing mode to GPU (requires CUDA driver)
        config.setProcessingMode(ProcessingMode.GPU);

        // Step 4 (optional): Limit GPU memory usage to 1024 MB
        config.setGpuMemoryLimit(1024);

        // Step 5: Perform recognition
        RecognitionResult ocrResult = ocrEngine.recognize(imageInfo);

        // Step 6: Print the extracted text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Programı çalıştırma**

```bash
javac -cp "path/to/aspose-ocr.jar" GpuExample.java
java -cp ".:path/to/aspose-ocr.jar" GpuExample
```

JAR’ın sınıf yolunda (classpath) olduğundan emin olun; aksi takdirde `ClassNotFoundException` alırsınız.

## Pro İpuçları & Yaygın Tuzaklar

- **GPU sürücü versiyonu:** `ProcessingMode.GPU` bayrağı, CUDA sürücüsü eksik ya da uyumsuzsa bir istisna fırlatır. `nvidia-smi` ile kontrol edin.
- **Bellek bütçelemesi:** Aynı anda çok sayıda görüntü işliyorsanız, `setGpuMemoryLimit` değerini artırın veya işleri sırayla çalıştırarak bellek taşması hatalarını önleyin.
- **Görüntü formatı:** PNG harika çalışırken, yüksek sıkıştırmalı JPEG’ler tanıma hatalarına yol açabilir. OCR öncesi kayıpsız PNG’ye dönüştürmeyi düşünün.
- **Dil desteği:** Varsayılan olarak Aspose OCR İngilizce kabul eder. Başka diller için `config.setLanguage(Language.SPANISH)` (veya uygun enum) çağrısını `recognize` öncesinde yapın.
- **Performans testi:** GPU ve CPU ile çalıştırarak (`System.nanoTime()`) hızlı bir benchmark yapın; hız artışının ek karmaşıklığı hak edip etmediğini doğrulayın.

## Sık Sorulan Sorular

**Bu macOS veya Linux’da çalışır mı?**  
Evet—Aspose OCR platformlar arasıdır. Sadece CUDA uyumlu bir GPU ve işletim sisteminiz için doğru sürücünün kurulu olduğundan emin olun.

**GPU’m yoksa ne yapmalıyım?**  
`setProcessingMode(ProcessingMode.GPU)` satırını tamamen çıkarabilirsiniz; motor otomatik olarak CPU moduna geçer.

**PDF’leri doğrudan işleyebilir miyim?**  
Aspose OCR raster görüntülere odaklanır. PDF’ler için önce her sayfayı bir görüntüye (ör. Aspose PDF kullanarak) dönüştürün, ardından PNG’leri OCR akışına besleyin.

## Sonuç

Özetle, Aspose ile Java’da **OCR nasıl kullanılır** sorusu üç net adıma indirgenir: motoru yapılandırmak (**modu ayarlama** ve **GPU bellek limitini belirleme** dahil), PNG’nizi göstermek ve çıkan metni okumak. Yukarıdaki kod parçacığı, herhangi bir Java projesine ekleyebileceğiniz tam işlevsel, uçtan uca bir çözümdür.

Artık **görüntüden metin tanıma** ve **PNG’den metin çıkarma** konusunda uzmanlaştığınıza göre, iş akışını genişletebilirsiniz: klasörleri toplu işleyin, sonuçları bir veritabanına kaydedin veya metni sonraki NLP boru hatlarına besleyin. Tek sınır hayal gücünüz—sadece GPU belleği ve sürücü uyumluluğuna dikkat etmeyi unutmayın.

OCR, GPU hızlandırması veya Aspose özellikleri hakkında daha fazla sorunuz mu var? Yorum bırakın ya da resmi Aspose OCR dokümantasyonunda daha derin özelleştirme seçeneklerini keşfedin. İyi kodlamalar! 🚀

![how to use ocr diagram](https://example.com/images/ocr-gpu-diagram.png "how to use ocr diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}