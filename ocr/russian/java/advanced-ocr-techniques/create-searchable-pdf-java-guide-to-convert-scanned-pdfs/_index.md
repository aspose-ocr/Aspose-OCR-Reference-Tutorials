---
category: general
date: 2026-02-22
description: Создайте поисковый PDF из отсканированного PDF с помощью Aspose OCR на
  Java. Узнайте, как конвертировать отсканированный PDF, сжимать изображения PDF и
  эффективно распознавать текст OCR в PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: ru
og_description: Создайте PDF с возможностью поиска из отсканированного PDF с помощью
  Aspose OCR в Java. Этот пошаговый учебник показывает, как преобразовать отсканированный
  PDF, сжать изображения PDF и выполнить OCR‑распознавание PDF.
og_title: Создание PDF с поиском – руководство Java по конвертации отсканированных
  PDF
tags:
- Java
- OCR
- PDF
- Aspose
title: Создание PDF с возможностью поиска – Руководство Java по конвертации отсканированных
  PDF
url: /ru/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF – Руководство Java по конвертации отсканированных PDF

Когда‑нибудь вам нужно было **создать поисковый PDF** из кучи отсканированных документов? Это распространённая проблема — ваши PDF выглядят нормально, но нельзя воспользоваться *Ctrl + F* для поиска. Хорошая новость? С несколькими строками кода на Java и Aspose OCR вы можете превратить такие PDF, содержащие только изображения, в полностью поисковые файлы, **конвертировать отсканированный PDF** в текст и даже уменьшить размер результата, **сжимая изображения PDF**.  

В этом руководстве мы пройдем полный, исполняемый пример, объясним, почему каждое настройка важна, и покажем, как подправить процесс для крайних случаев, таких как многостраничные сканы или изображения низкого разрешения. К концу вы получите надёжный, готовый к продакшну фрагмент кода, который **recognize pdf ocr** надёжно и создаёт аккуратный поисковый документ.

---

## Что понадобится

- **Java 17** (или любой современный JDK; API не зависит от JDK)  
- **Aspose.OCR for Java** библиотека — её можно получить из Maven Central (`com.aspose:aspose-ocr`)  
- Отсканированный PDF (только изображения), который вы хотите сделать поисковым  
- IDE или текстовый редактор, с которым вам удобно работать (IntelliJ, VS Code, Eclipse…)

Никаких тяжёлых фреймворков, никаких внешних сервисов — только чистый Java и один сторонний JAR.  

---

![пример создания поискового pdf](placeholder-image.png "Иллюстрация поискового PDF, созданного из отсканированного документа")

*Текст альтернативного изображения:* **create searchable pdf** иллюстрация, показывающая «до‑и‑после» отсканированного PDF, преобразованного в поисковый текст.

---

## Шаг 1 – Инициализация OCR‑движка  

Первое, что нужно сделать, — создать экземпляр `OcrEngine`. Считайте его мозгом, который будет анализировать каждый битмап внутри PDF и выдавать символы Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

**Pro tip:** Если вы планируете обрабатывать много PDF подряд, переиспользуйте один и тот же `OcrEngine`, а не создавайте новый каждый раз. Это экономит несколько миллисекунд и уменьшает нагрузку на память.

---

## Шаг 2 – Настройка OCR‑опций, специфичных для PDF  

Aspose позволяет точно настроить, как будет построен результирующий PDF. Три настройки ниже оказывают наибольшее влияние на **compress pdf images**, одновременно сохраняя возможность поиска.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** — 300 dpi является оптимальным; более низкие значения ускоряют процесс, но могут пропустить мелкие шрифты.  
- **CompressImages** — активирует без потерь PNG‑сжатие; поисковый PDF остаётся чётким, но легче.  
- **EmbedOriginalImages** — без этого флага движок удалит оригинальный растр, оставив только невидимый текст. Сохранение изображения гарантирует, что PDF будет выглядеть точно как скан, что требуется многим отделам комплаенса.

---

## Шаг 3 – Загрузка вашего отсканированного PDF в `OcrInput`  

Aspose читает исходный файл через обёртку `OcrInput`. Вы можете добавить несколько файлов, но в этом демо мы сосредоточимся на единственном **image PDF**.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

**Почему бы не передать просто `File`?** Использование `OcrInput` даёт гибкость объединять несколько PDF или даже смешивать файлы изображений (PNG, JPEG) перед OCR. Это рекомендуемый подход, когда вы **convert scanned pdf**, который может быть разбит на несколько источников.

---

## Шаг 4 – Выполнение OCR и получение поискового PDF в виде массива байтов  

Теперь происходит магия. Движок анализирует каждую страницу, запускает свой OCR‑движок и создаёт новый PDF, содержащий как оригинальное изображение, так и скрытый слой текста.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Если вам нужен сырой текст для других целей (например, индексация), вы также можете вызвать `ocrEngine.recognize(ocrInput)`, который возвращает `String`. Но для цели **create searchable pdf** массив байтов — это то, что вы запишете на диск.

---

## Шаг 5 – Сохранение поискового PDF на диск  

Наконец, запишите массив байтов в файл. NIO в Java делает это однострочником.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Когда вы откроете `searchable_output.pdf` в Adobe Acrobat или любом современном просмотрщике, вы заметите, что теперь можно выделять, копировать и искать текст — именно то, что обещает трансформация **image pdf to text**.

---

## Конвертация отсканированного PDF в текст с помощью OCR (опционально)

Иногда вам нужен только извлечённый простой текст, а не новый PDF. Вы можете переиспользовать тот же движок:

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Этот фрагмент демонстрирует, насколько просто выполнить **recognize pdf ocr** для последующей обработки, такой как заполнение поискового индекса или проведение анализа естественного языка.

---

## Сжатие изображений PDF для уменьшения файлов  

Если ваши исходные сканы огромные (например, цветные сканы 600 dpi), полученный поисковый PDF всё равно может быть громоздким. Помимо флага `setCompressImages(true)`, вы можете вручную уменьшить масштаб перед OCR:

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

Снижение DPI уменьшит размер файла примерно вдвое, но проверьте читаемость — некоторые шрифты становятся нечитаемыми ниже 150 dpi. Компромисс между **compress pdf images** и точностью OCR — это то, что вам придётся решить, исходя из ограничений по хранению.

---

## Пояснение настроек Recognize PDF OCR  

| Настройка                | Влияние на результат                         | Типичный сценарий использования                                   |
|--------------------------|----------------------------------------------|-------------------------------------------------------------------|
| `setOutputDpi(int)`      | Контролирует разрешение растра вывода OCR    | Архивы высокого качества (300 dpi) против лёгких веб‑PDF (150 dpi) |
| `setCompressImages`      | Включает PNG‑сжатие                          | Когда нужно отправлять PDF по электронной почте или хранить в облаке |
| `setEmbedOriginalImages` | Сохраняет оригинальный скан видимым          | Юридические или комплаенс‑документы, которые должны сохранять оригинальный вид |
| `setLanguage` (optional) | Принудительно задаёт языковую модель (например, "eng") | Многоязычные корпуса, где автоматическое определение по умолчанию может ошибаться |

Понимание этих «ручек» помогает вам **recognize pdf ocr** более интеллектуально и избегать ловушки «размытого текста».

---

## Image PDF в текст — распространённые подводные камни и как их избежать  

1. **Сканы низкого разрешения** — точность OCR резко падает ниже 150 dpi. Увеличьте масштаб исходного изображения перед передачей в Aspose или запросите более высокое DPI у сканера.  
2. **Повернутые страницы** — если страницы отсканированы боком, включите авто‑поворот: `pdfOcrOptions.setAutoRotate(true);`.  
3. **Зашифрованные PDF** — движок не может читать файлы, защищённые паролем; сначала расшифруйте их, используя `PdfDocument` из Aspose.PDF.  
4. **Смешанные растр и текст** — некоторые PDF уже содержат скрытый слой текста. Повторный запуск OCR может дублировать текст. Используйте `PdfOcrOptions.setSkipExistingText(true);`, чтобы сохранить оригинальный слой.  

Устранение этих проблем гарантирует, что ваш конвейер **create searchable pdf** будет надёжным для реальных наборов документов.

---

## Полный рабочий пример (Все шаги в одном файле)

Ниже приведён полный Java‑класс, который вы можете скопировать и вставить в свою IDE. Замените `YOUR_DIRECTORY` на реальный путь к папке.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}