---
category: general
date: 2026-05-28
description: Создайте PDF с возможностью поиска, используя Aspose OCR в C#. Узнайте,
  как выполнять OCR для PDF, распознавать текст в PDF и преобразовать отсканированный
  PDF с OCR в PDF, доступный для поиска.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: ru
og_description: Создайте поисковый PDF с помощью Aspose OCR на C#. Следуйте этому
  пошаговому руководству, чтобы выполнить OCR в PDF, распознать текст в PDF и работать
  со сканированными PDF‑файлами, обработанными OCR.
og_title: Создайте PDF с возможностью поиска с помощью Aspose OCR – выполните OCR
  в PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Создайте PDF с поисковым текстом с помощью Aspose OCR – выполните OCR в PDF
url: /ru/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF с помощью Aspose OCR – Запуск OCR на PDF

Когда‑нибудь вам нужно было **создать поисковый PDF** из стопки отсканированных документов? Вы не одиноки. Во многих офисных процессах единственное, что стоит между вами и полностью‑поисковым архивом, — несколько строк кода, которые выполняют OCR на страницах PDF.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который покажет вам точно, как **создать поисковый PDF** с использованием библиотеки Aspose OCR для .NET. К концу вы будете знать, как *выполнять OCR на PDF*, *распознавать текст PDF* файлов и преобразовать *OCR‑отсканированный PDF* в поисковую версию без каких‑либо сторонних сервисов.

> **Требования** – Недавний .NET SDK (рекомендовано 6.0+), действующая лицензия Aspose.OCR для .NET (или временный ключ оценки) и PDF, который вы хотите обработать.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## Что покрывает это руководство

- Настройка библиотеки Aspose OCR в проекте C#.
- Загрузка исходного PDF (любое количество страниц).
- Конфигурация движка для вывода **searchable PDF**.
- Запуск процесса OCR и сохранение результата.
- Советы по работе с многостраничными документами, выбором языка и распространёнными подводными камнями.

Если вы выполните каждый шаг, у вас получится файл, который можно открыть в Adobe Reader, нажать **Ctrl + F** и мгновенно искать любое слово, присутствующее в оригинальном скане.

---

## Шаг 1: Установить Aspose OCR для .NET

Перед написанием кода добавьте пакет NuGet в ваш проект:

```bash
dotnet add package Aspose.OCR
```

> **Совет:** Используйте флаг `--version`, чтобы зафиксировать последнюю стабильную версию (например, `Aspose.OCR 23.10`). Это обеспечивает совместимость с .NET 6 и новее.

---

## Шаг 2: Создать экземпляр OCR Engine

Сердцем процесса является `OcrEngine`. Считайте его мозгом, который читает изображения и выводит текст. Инициализировать его просто:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

---

## Шаг 3: Загрузить исходный PDF (Запуск OCR на PDF)

Aspose OCR может принимать PDF напрямую; он извлекает каждую страницу как изображение внутри. Замените путь‑заполнитель на расположение вашего отсканированного документа:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Почему это работает:** Метод `ImageStream.FromFile` автоматически определяет формат PDF и подготавливает растровое представление для OCR. Дополнительный шаг конвертации не требуется.

---

## Шаг 4: Настроить формат вывода и язык

Здесь мы говорим Aspose, что нам нужно получить. Установка `OutputFormat` в `SearchablePdf` инструктирует движок встраивать распознанный текст за оригинальными изображениями страниц, создавая **searchable PDF**. Вы также можете выбрать язык для повышения точности — по умолчанию английский, но можно переключить на французский, немецкий и т.д.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Если необходимо обработать двуязычный документ, вы можете комбинировать языки, используя флаги перечисления `Language`.

---

## Шаг 5: Запустить процесс OCR – Распознать текст PDF

Теперь происходит основная работа. Метод `Recognize` сканирует каждую страницу, извлекает глифы и создает внутренний поток PDF, содержащий как оригинальное изображение, так и невидимый слой текста. Это шаг, где мы *распознаем текст PDF*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Распространённый вопрос:** *Что если PDF содержит 200 страниц?*  
> Движок обрабатывает страницы последовательно и потоково выводит результаты, поэтому потребление памяти остаётся умеренным. Однако для чрезвычайно больших файлов вы можете увеличить параметр `MemoryLimit` в `ocrEngine.Configuration`.

---

## Шаг 6: Сохранить поисковый PDF

Наконец, запишите результат на диск. Метод `Save` сохраняет внутренний поток в новый файл, который можно открыть любым просмотрщиком PDF.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Запустите программу (`dotnet run`) и наблюдайте, как консоль подтверждает создание файла. Откройте `handbook_searchable.pdf` и попробуйте поискать слово, которое, как вы знаете, присутствует в оригинальном скане — вы должны увидеть совпадения мгновенно.

---

## Обработка граничных случаев и продвинутые сценарии

### Несколько языков (OCR‑отсканированный PDF)

Если ваш исходный PDF содержит как английский, так и испанский текст, объедините языки:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

### PDF, защищённые паролем

При работе с защищёнными PDF предоставьте пароль перед вызовом `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Если пароль неверен, `Recognize` бросает `InvalidPasswordException`; перехватив её, вы можете запросить у пользователя правильный пароль.

### Управление качеством изображения

Более высокое DPI дает лучшие результаты OCR, но потребляет больше памяти. Отрегулируйте DPI, если замечаете искажённые символы:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Лицензия vs. режим оценки

В режиме оценки на каждой странице появляется водяной знак. Чтобы убрать его, примените вашу лицензию до любого вызова OCR:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Профессиональные советы для продакшн‑использования

- **Пакетная обработка:** Оберните основную логику в цикл `foreach`, который проходит по списку PDF‑файлов. Освобождайте `OcrEngine` после каждого файла, чтобы освободить нативные ресурсы.
- **Логирование:** Используйте `ocrEngine.Configuration.Logger` для захвата подробной статистики OCR (например, распознанные символы в секунду). Это бесценно при отладке низкой точности.
- **Тонкая настройка производительности:** Для многопоточных серверов создавайте отдельные объекты `OcrEngine` для каждого потока; библиотека потокобезопасна, когда каждый экземпляр изолирован.
- **Обработка ошибок:** Всегда оборачивайте `Recognize` и `Save` в блоки `try/catch`. Типичные исключения включают `FileNotFoundException`, `OutOfMemoryException` и `UnsupportedFormatException`.

---

## Полный рабочий пример (готовый к копированию и вставке)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Ожидаемый вывод** (консоль):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Откройте полученный файл, нажмите **Ctrl + F**, и вы сможете найти любое слово, которое присутствовало в оригинальных отсканированных страницах. Это магия преобразования *OCR‑отсканированного PDF* в **searchable PDF**.

---

## Заключение

Мы только что продемонстрировали, как **создать поисковый PDF** с помощью Aspose OCR для .NET, охватив всё от установки пакета до работы с многоязычными и защищёнными паролем PDF. Следуя этим шагам, вы сможете надёжно *выполнять OCR на PDF* документах, *распознавать текст PDF* и преобразовать любой *OCR‑отсканированный PDF* в полностью поисковый ресурс.

### Что дальше?

- Изучите API **aspose ocr pdf** подробнее: извлечение простого текста, экспорт в DOCX или массовое создание поисковых PDF.
- Скомбинируйте вывод поискового PDF с Aspose.PDF для добавления закладок или водяных знаков.
- Экспериментируйте с различными настройками DPI или пользовательскими словарями OCR для специфических шрифтов.

Не стесняйтесь изменять пример, интегрировать его в ваш конвейер управления документами или задавать вопросы в комментариях. Приятного кодинга и наслаждайтесь превращением нечитаемых сканов в поисковое золото!

## Связанные руководства

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Cómo hacer OCR a PDF en .NET con Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [كيفية إجراء OCR لملف PDF في .NET باستخدام Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}