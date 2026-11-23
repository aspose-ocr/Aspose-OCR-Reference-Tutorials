---
category: general
date: 2026-07-05
description: Сжимайте изображения PDF при конвертации PNG в PDF с помощью Java. Изучите
  предварительную обработку изображений для OCR, распознавание текста из JPG и пакетное
  OCR в PDF в одном руководстве.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: ru
og_description: Сжимайте изображения PDF и конвертируйте PNG в PDF с помощью Java.
  Это руководство охватывает предварительную обработку изображений для OCR, распознавание
  текста в JPG и пакетное OCR в PDF.
og_title: Сжатие изображений PDF с помощью Java – Полное руководство по пакетному
  OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Сжатие изображений PDF с помощью Java – Полное руководство по пакетному OCR
  в PDF
url: /ru/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сжатие изображений PDF с помощью Java – Полное руководство по пакетному OCR в PDF

Когда‑то вам нужно было **сжать изображения PDF**, одновременно преобразуя папку PNG‑файлов в поисковые PDF? Вы не одиноки. Во многих автоматизационных конвейерах самая большая боль – это балансировать между качеством изображения, точностью OCR и конечным размером PDF — всё одновременно.  

В этом руководстве мы пройдём практическое решение, которое **преобразует PNG в PDF**, применяет **предобработку изображений для OCR**, а затем **сжимает изображения PDF**, чтобы полученный файл оставался лёгким. К концу вы узнаете, как **распознавать текст на JPG**‑файлах, настроить рабочий процесс **пакетного OCR в PDF** и поддерживать порядок в ваших PDF‑файлах.

## Что вы узнаете

- Как установить Aspose OCR для Java и применить лицензию.  
- Как настроить движок для многопоточности, ускорения с помощью GPU и коррекции орфографии.  
- Как построить переиспользуемый конвейер **предобработки изображений для OCR** (шумоподавление, контраст, бинаризация).  
- Как использовать **PdfSaveOptions** для **сжатия изображений PDF** без потери читаемости.  
- Как в цикле по каталогу **преобразовать PNG в PDF** и **распознавать текст JPG** пакетно.  
- Полную готовую к запуску программу на Java, которую можно вставить в любой проект.

> **Prerequisites**: Java 8+, Maven или Gradle, лицензия Aspose OCR для Java и папка с PNG/JPG‑изображениями, которые нужно обработать.

---

## Шаг 1: Примените лицензию Aspose OCR (необходимо для продакшна)

Прежде чем вы сможете вызывать любые OCR‑API, необходимо загрузить действующую лицензию; иначе вы будете ограничены условиями trial‑версии.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Почему это важно*: Лицензированный движок открывает поддержку GPU, повышенную точность и убирает водяные знаки, которые иначе раздували бы ваши PDF‑файлы.

---

## Шаг 2: Настройка OCR‑движка – потоки, GPU и коррекция орфографии

Быстрый OCR‑движок — фундамент любой задачи **пакетного OCR в PDF**. Мы запустим столько потоков, сколько может обработать процессор хоста, включим ускорение GPU (если у вас совместимая видеокарта) и усилим коррекцию орфографии, чтобы очистить ошибки OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: Если вы работаете на безголовом сервере без GPU, просто установите `gpu.setEnabled(false)` — код будет работать, лишь немного медленнее.

---

## Шаг 3: Построение конвейера предобработки изображений

Сырые сканы часто страдают от шума, низкого контраста или неравномерного освещения. **Предобработка изображений для OCR** значительно повышает коэффициент распознавания, особенно в сценариях **распознавания текста JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Почему мы цепляем их*: Шумоподавление в начале предотвращает усиление пятен бинaризатором; затем контраст делает символы более заметными; наконец, бинаризация даёт OCR‑движку чистое бинарное изображение.

---

## Шаг 4: Настройка параметров сохранения PDF – **Эффективное сжатие изображений PDF**

Aspose позволяет точно настроить вывод PDF. Мы включим сжатие изображений и зададим уровень качества, который балансирует размер и читаемость.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Результат*: Каждый поисковый PDF будет заметно меньше — идеально для архивирования или отправки по электронной почте.

---

## Шаг 5: Обработка папки – **Преобразовать PNG в PDF** и **распознавать текст JPG** в одном цикле

Теперь собираем всё вместе. Цикл проходит по входному каталогу, выполняет OCR для каждого PNG или JPG и записывает поисковый PDF в выходную папку. Имя PDF повторяет имя исходного изображения.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Ожидаемый вывод

Запуск программы выводит строку для каждого изображения, например:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Откройте любой полученный PDF в просмотрщике — вы увидите выделяемый, поисковый текст, а размер файла обычно **на 30‑50 % меньше**, чем у неплотно сжатого аналога.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если на сервере нет GPU?
Просто установите `gpuSettings.setEnabled(false)`. Остальная часть конвейера остаётся без изменений, и вы всё равно получаете многопоточную обработку на CPU.

### PDF‑файлы всё ещё слишком большие — можно ли ещё снизить качество?
Да. Отрегулируйте `options.setImageQuality(70)` или даже `50`. Более низкие значения уменьшают размер агрессивнее, но могут размыть мелкие глифы. Проверьте на репрезентативном образце.

### Как обрабатывать другие форматы изображений (TIFF, BMP)?
Добавьте расширения в лямбда‑фильтр:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Тот же конвейер предобработки работает для большинства растровых форматов.

### Можно ли оставить оригинальные цветные изображения вместо бинаризации?
Замените `.addBinarize()` на `.addGrayscale()` в билдере предобработчика, если вам нужно сохранять цвет для последующего анализа.

---

## Pro‑советы для продакшн‑готового пакетного OCR

- **Управление памятью**: Переиспользуйте один экземпляр `OcrEngine` (как показано), чтобы избежать накладных расходов на создание/уничтожение объектов для каждого изображения.  
- **Обработка ошибок**: Оберните блок обработки отдельного файла в `try/catch`, чтобы логировать сбои без прерывания всей партии.  
- **Логирование**: Используйте полноценный фреймворк логирования (SLF4J, Log4j) вместо `System.out.println` для масштабируемых решений.  
- **Параллелизм**: Для огромных папок рассмотрите обработку подпапок в параллельных потоках, но следите за конкуренцией за GPU.  
- **Безопасность**: Храните файл лицензии вне репозитория и защищайте его правами доступа файловой системы.

---

## Заключение

Мы продемонстрировали, как **сжать изображения PDF** одновременно с выполнением **пакетного OCR в PDF**, который **преобразует PNG в PDF**, **распознаёт текст JPG** и использует надёжный конвейер **предобработки изображений для OCR**. Полная Java‑программа автономна, работает на любой современной JDK и создаёт лёгкие поисковые PDF, готовые к архивированию или дальнейшему анализу.

Что дальше? Поэкспериментируйте с различными параметрами предобработки, попробуйте OCR‑языки, отличные от английского, или интегрируйте рабочий процесс в микросервис Spring Boot, который следит за каталогом и обрабатывает файлы «на лету». Основные концепции — загрузка лицензии, настройка движка, предобработка и сжатие PDF — остаются теми же, давая прочную основу для любого проекта, основанного на OCR.

Есть вопросы или хотите поделиться своими доработками? Оставляйте комментарий ниже, и удачной разработки!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Диаграмма пакетного OCR‑конвейера, показывающая входные изображения, предобработку, OCR‑движок и сжатый PDF‑вывод")

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}