---
date: 2026-04-29
description: Узнайте, как конвертировать изображения в PDF на C# с помощью Aspose.OCR,
  сохранять многостраничные результаты OCR в виде документов и извлекать текст из
  изображений на C#.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: Преобразовать изображения в PDF C# – Сохранить многостраничный результат
  OCR
second_title: Aspose.OCR .NET API
title: Конвертировать изображения в PDF на C# – Сохранить многостраничный результат
  OCR
url: /ru/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование изображений в PDF C# – Сохранение многостраничного результата OCR

## Введение

В этом руководстве вы узнаете, как **convert images to PDF C#** с помощью мощной библиотеки **Aspose.OCR** для .NET. Независимо от того, нужно ли вам **convert scanned TIFF files to searchable PDFs**, извлекать текст из изображений для анализа данных или создавать книгу Excel из пакета фотографий, это руководство проведёт вас через каждый шаг с понятными объяснениями, практическими советами и рекомендациями по лучшим практикам.

## Быстрые ответы
- **What does this tutorial cover?** Преобразование нескольких изображений в PDF, Docx, Text и Xlsx с использованием Aspose.OCR в C# и сохранение результата OCR в виде многостраничного документа.  
- **Which output formats are supported?** Docx, Text, Pdf и Xlsx (вы также можете напрямую выводить PDF).  
- **Do I need a license?** Бесплатная пробная версия подходит для оценки; для продакшн требуется постоянная лицензия.  
- **What .NET versions are compatible?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Can I extract text while converting?** Да — используйте результаты OCR для получения поискового текста перед сохранением.  

## Что такое “convert images to PDF C#”?

Преобразование изображений в PDF в C# означает программное взятие одного или нескольких файлов bitmap (PNG, JPEG, TIFF и т.д.) и создание PDF‑документа, сохраняющего визуальное расположение, при желании встраивая поисковый текст с помощью OCR. Aspose.OCR предоставляет **c# ocr library**, которая обрабатывает процесс от начала до конца, включая поддержку многостраничных документов и прямое сохранение в популярные офисные форматы.

## Почему использовать Aspose.OCR для этой задачи?

- **High‑accuracy OCR** поддерживает десятки языков.  
- **Multipage processing** – загрузите целую папку изображений и получите один поисковый PDF.  
- **Direct export** в Docx, Text, Pdf и Xlsx без необходимости второго шага конвертации.  
- **Pure .NET** – без нативных зависимостей, работает на Windows, Linux и облачных средах выполнения.  

## Предварительные требования

1. Установите Aspose.OCR для .NET. Вы можете скачать его [здесь](https://releases.aspose.com/ocr/net/).  
2. Получите бесплатную пробную версию или приобретённую лицензию – пробную версию можно получить [здесь](https://releases.aspose.com/), а купить — [здесь](https://purchase.aspose.com/buy).  
3. Ознакомьтесь с официальной [documentation](https://reference.aspose.com/ocr/net/), чтобы познакомиться с API.  
4. Присоединитесь к сообществу на [support forums](https://forum.aspose.com/c/ocr/16) для получения помощи при возникновении проблем.  

Теперь, когда всё готово, давайте начнём кодировать.

## Импорт пространств имён

Начните с добавления необходимых пространств имён в ваш файл C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Эти импорты дают вам доступ к коллекциям, работе с файлами, LINQ и классам Aspose OCR.

## Шаг 1: Установите каталог документов

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Замените `"Your Document Directory"` на абсолютный или относительный путь, где находятся ваши исходные изображения и куда вы хотите сохранять выходные файлы.

## Шаг 2: Инициализировать Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Создание объекта `AsposeOcr` даёт вам доступ ко всем операциям OCR, включая рабочий процесс **convert images to PDF C#**.

## Шаг 3: Распознать изображения

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Метод `RecognizeMultipleImages` обрабатывает каждый файл в списке и возвращает коллекцию `RecognitionResult`. Вы можете передать любое количество изображений, что идеально подходит для сценариев **convert scanned images to PDF**.

## Шаг 4: Сохранить результаты в предпочтительных форматах

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Выберите формат, который лучше всего подходит для вашего последующего рабочего процесса:

- **Docx** – редактируемый документ Word с поисковым текстом.  
- **Text** – извлечение простого текста для быстрого анализа данных (**extract text from images**).  
- **Pdf** – классический вывод PDF, идеален для архивирования.  
- **Xlsx** – представление в виде таблицы для табличных данных (**convert images to xlsx**).

## Как convert images to PDF C# – пошаговое резюме

1. **Prepare the folder** с изображениями, которые вы хотите конвертировать.  
2. **Create an `AsposeOcr` instance** для доступа к функциям OCR.  
3. **Call `RecognizeMultipleImages`** чтобы получить результаты OCR для каждого файла.  
4. **Save the multipage result** используя `SaveMultipageDocument` в нужном вам формате.

## Распространённые сценарии использования

- **Digital archiving:** Преобразовать отсканированные бумажные контракты в поисковые PDF.  
- **Data entry automation:** Извлекать текст из чеков или счетов и передавать его в базу данных.  
- **Batch processing:** Обрабатывать тысячи изображений в одной задаче с минимальным кодом.  
- **Generate PDF from TIFF:** Идеально подходит для сканированных документов высокого разрешения, которым необходимо сохранять оригинал.

## Устранение неполадок и советы

- **Large image sets:** Обрабатывайте изображения небольшими партиями, чтобы избежать всплесков памяти.  
- **Image quality:** Убедитесь, что изображения имеют минимум 300 dpi для оптимальной точности OCR.  
- **License errors:** Убедитесь, что ваш файл лицензии правильно загружен перед вызовом методов OCR.  
- **Empty results:** Если изображение не может быть прочитано, соответствующий `RecognitionResult` будет иметь пустое свойство `Text` — проверьте на null или пустые строки перед сохранением.  

## Часто задаваемые вопросы

**Q: Can I convert images to PDF C# without using OCR?**  
A: Да, вы можете использовать Aspose.PDF или другие библиотеки для чистого преобразования изображений в PDF, но OCR добавляет поисковый текст, который делает PDF гораздо более полезным.

**Q: How do I extract text from images C# after conversion?**  
A: Список `result`, возвращаемый `RecognizeMultipleImages`, содержит свойство `Text` для каждой страницы. Вы можете записать эти строки в файл `.txt` или обрабатывать их напрямую в вашем приложении.

**Q: Is it possible to set custom page margins or orientation?**  
A: При сохранении в PDF или Docx вы можете изменить макет документа через API Aspose.Words или Aspose.PDF перед вызовом `SaveMultipageDocument`.

**Q: What happens if an image cannot be read?**  
A: OCR‑движок возвращает пустой `RecognitionResult` для этой страницы; вы можете обнаружить это и пропустить или записать проблемный файл в журнал.

**Q: Does the API support cloud deployment?**  
A: Да, библиотека работает на любой среде выполнения .NET, включая Azure Functions и AWS Lambda, при условии, что среда соответствует требованиям к версии.

## Заключение

Теперь у вас есть полный, готовый к продакшн рабочий процесс для **convert images to PDF C#**, извлечения поискового текста и даже генерации файлов Word, простого текста или Excel из пакета изображений. Не стесняйтесь экспериментировать с различными форматами вывода, настраивать параметры OCR для конкретных языков или интегрировать код в более крупные конвейеры обработки документов.

---

**Last Updated:** 2026-04-29  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}