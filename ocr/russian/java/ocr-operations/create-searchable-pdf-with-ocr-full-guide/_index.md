---
category: general
date: 2026-06-22
description: Создайте PDF с возможностью поиска с помощью OCR в Java. Узнайте, как
  отключить сжатие и быстро преобразовать отсканированный PDF‑изображение в PDF с
  возможностью поиска.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: ru
og_description: Создайте PDF с возможностью поиска с помощью OCR в Java. Это руководство
  показывает, как отключить сжатие, преобразовать отсканированный PDF‑изображение
  и создать PDF без сжатия.
og_title: Создание PDF с поиском с помощью OCR – Полный учебник по Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Создание PDF с поиском (OCR) – Полное руководство
url: /ru/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF с OCR – Полное руководство

Когда‑нибудь вам нужно было **create searchable PDF** из пакета отсканированных изображений, но вы не знали, какие настройки изменить? Вы не одиноки — большинство разработчиков сталкиваются с тем же, когда результат оказывается огромным, нечитаемым куском.  

В этом руководстве мы пройдем чистый, сквозной пример, который покажет, как **create searchable PDF** с помощью Java OCR‑движка, **convert scanned image PDF**, и, что особенно важно, **how to disable compression**, чтобы полученный файл сохранял оригинальные размеры. К концу вы получите готовый к запуску фрагмент кода и твердое понимание, почему каждая настройка имеет значение.

## Что вы узнаете

* Как настроить OCR‑движок для **ocr to searchable pdf**.  
* Причина отключения сжатия PDF и как получить **pdf without compression**.  
* Полная Java‑программа, которая берёт отсканированное изображение, выполняет OCR и сохраняет **searchable PDF**.  
* Советы по работе с особенностями, такими как многостраничные сканы или источники низкого разрешения.  

**Prerequisites** — установлен Java 8+, совместимый OCR SDK (в примере используется ABBYY FineReader Engine API, но концепции применимы к любой библиотеке, предоставляющей `setOutputFormat` и `setPdfCompression`). IDE, например IntelliJ IDEA или Eclipse, упростит работу, но подойдёт и простой текстовый редактор.

---

![Создание поискового PDF workflow](image-placeholder.png "Диаграмма, показывающая процесс создания поискового PDF из отсканированных изображений до финального PDF")

## Step 1: Set the OCR Engine to **Create Searchable PDF**

Первое, что нужно сообщить OCR‑движку, — какой тип вывода вы ожидаете. По умолчанию многие SDK выводят простой текст или растровый PDF, который не является поисковым. Переключение формата делает всю тяжёлую работу за вас.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Why this matters*: Флаг `PDF_SEARCHABLE` инструктирует движок внедрить невидимый слой текста под отсканированным изображением. Поисковые инструменты затем могут индексировать документ, заставляя его вести себя как любой нативный PDF, открываемый в Adobe Reader.

## Step 2: Disable Compression – **How to Disable Compression** Properly

Если пропустить этот шаг, движок будет сжимать каждую страницу для экономии места, но сжатие может размыть мелкие детали — особенно проблематично, когда позже нужно извлекать изображения высокого разрешения.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro tip**: Отключение сжатия необходимо, когда вы планируете архивировать юридические документы или медицинские сканы, где каждый пиксель важен. Полученный файл может быть больше, но вы сохраняете оригинальные размеры и чёткость.

## Step 3: Perform OCR and Get the Resulting Document

Теперь, когда движок знает, что выводить и как обрабатывать изображения, вы можете запустить распознавание. Вызов возвращает объект `PdfDocument`, готовый к сохранению или дальнейшей обработке.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*What’s happening under the hood?* Движок обрабатывает каждую входную страницу, выполняет распознавание символов и накладывает скрытый текстовый слой на изображение. Если у вас несколько страниц, они автоматически конкатенируются.

## Step 4: Save the **Searchable PDF** to Disk

Наконец, запишите PDF из памяти в файл. Выберите место, где у вас есть права записи, и дайте файлу осмысленное имя.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Когда вы откроете `searchable.pdf` в просмотрщике, заметите, что можно выделять и искать текст, хотя видимое содержимое остаётся оригинальным отсканированным изображением.

### Full Working Example

Ниже представлен автономный Java‑класс, объединяющий все четыре шага. Смело копируйте‑вставляйте, корректируйте путь к входному файлу и запускайте как есть.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Expected output** — После запуска программы в консоли появится сообщение выше, а файл `searchable.pdf` появится в `YOUR_DIRECTORY`. Открывая его в любом PDF‑читалке, вы сможете:

* Выделять текст.  
* Использовать встроенный поиск (Ctrl + F) для нахождения слов.  
* При необходимости экспортировать скрытый текстовый слой.  

---

## Why Disable Compression? Understanding **PDF Without Compression**

Возможно, вы задаётесь вопросом: «Разве сжатие не всегда полезно?» Ответ более сложный:

| Situation | Keep Compression (`NORMAL`) | Disable Compression (`NONE`) |
|-----------|-----------------------------|------------------------------|
| Archival of legal contracts | ❌ May alter pixel fidelity | ✅ Guarantees original look |
| Large batch of low‑resolution scans | ✅ Saves storage | ❌ Increases size without benefit |
| Need for OCR accuracy on tiny fonts | ❌ Blurs fine details | ✅ Preserves every stroke |

Кратко, **how to disable compression** — это компромисс между объёмом хранения и точностью. Для большинства рабочих процессов с поисковыми PDF, где цель — поиск текста, а не печать изображений, отключение сжатия является самым надёжным вариантом.

## Converting a **Scanned Image PDF** Directly

Иногда у вас уже есть PDF, содержащий отсканированные изображения («PDF только с изображениями»). Чтобы **convert scanned image pdf** в поисковую версию, можно передать весь PDF движку вместо отдельных изображений:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Те же флаги конфигурации (`PDF_SEARCHABLE` и `PdfCompression.NONE`) применяются, поэтому вы получаете **pdf without compression**, даже начиная с PDF‑контейнера.

## Common Pitfalls & How to Avoid Them

* **Forgot to set the output format** — Движок по умолчанию создаёт растровый PDF, который не является поисковым. Всегда вызывайте `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` перед `recognizeToPdf()`.  
* **Running out of memory on large batches** — Загружайте и обрабатывайте страницы порциями или используйте потоковый API, если ваш SDK его поддерживает.  
* **Incorrect file paths** — Используйте абсолютные пути или убедитесь, что рабочий каталог установлен правильно; иначе `pdf.save()` бросит `IOException`.  
* **License not activated** — Большинство коммерческих OCR SDK требуют действующей лицензии; при её отсутствии движок бросит исключение времени выполнения.  

---

## Conclusion

Теперь у вас есть полное, готовое к запуску решение, показывающее **how to create searchable PDF** из отсканированных изображений, как **convert scanned image PDF**, и точно **how to disable compression** для получения **pdf without compression**. Ключевые шаги:

1. Установите формат вывода в `PDF_SEARCHABLE`.  
2. Отключите сжатие PDF с помощью `PdfCompression.NONE`.  
3. Запустите OCR и получите `PdfDocument`.  
4. Сохраните файл на диск.

Отсюда вы можете экспериментировать со шрифтами, добавлять водяные знаки или пакетно обрабатывать целые папки. Если вам интересно добавить языковые пакеты OCR, работать с многостраничными TIFF‑файлами или интегрировать этот процесс в веб‑службу, смотрите наши будущие руководства «OCR language selection in Java» и «Streaming OCR for large document sets».

Есть вопросы или обнаружили проблему? Оставьте комментарий ниже — приятного кодинга и наслаждайтесь новыми поисковыми PDF!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Распознавание текста PDF – OCR операции с Aspose.OCR для Java](/ocr/english/java/ocr-operations/)
- [OCR распознавание PDF‑документов в Aspose.OCR для Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Конвертация изображений в PDF C# – Сохранить многостраничный OCR‑результат](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}