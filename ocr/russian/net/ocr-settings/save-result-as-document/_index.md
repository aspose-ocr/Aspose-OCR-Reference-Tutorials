---
date: 2026-06-29
description: Узнайте, как сохранять результаты OCR с помощью Aspose.OCR for .NET —
  пошаговое руководство по сохранению вывода OCR, конвертации изображения в поисковый
  PDF, извлечению текста из PNG и экспорту в DOCX, TXT, PDF или XLSX.
keywords:
- how to save ocr
- image to searchable pdf
- extract text from png
- create searchable pdf
- ocr result to txt
linktitle: Как сохранить результат OCR в документ
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  headline: How to Save OCR Result as Document
  type: TechArticle
- description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  name: How to Save OCR Result as Document
  steps:
  - name: Initialize Aspose.OCR
    text: AsposeOcr is the primary class that performs OCR operations. Set the path
      to your working directory and create an instance of the OCR engine.
  - name: Recognize Image
    text: RecognitionResult holds the text and layout information extracted from the
      image. Pass the image file (e.g., a PNG) to the recognizer. This is where we
      **recognize text images** and turn them into a `RecognitionResult`.
  - name: Save Result in Different Formats
    text: Now we export the recognized text. Choose the format that fits your workflow—whether
      you need to **convert image to searchable pdf**, **extract text from png**,
      or generate a spreadsheet.
  - name: Display Success Message
    text: A simple console message confirms that the process completed without errors.
  type: HowTo
- questions:
  - answer: It refers to persisting the text recognized from an image into a file
      format like DOCX, PDF, etc.
    question: What does “how to save ocr” mean?
  - answer: DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.
    question: Which formats can I export to?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—save the OCR result as PDF to get a searchable PDF document.
    question: Can I convert image to PDF directly?
  - answer: Absolutely; you can **extract text from PNG** images with the same API.
    question: Is PNG supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Как сохранить результат OCR в документ
url: /ru/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить результат OCR в документ

## Введение

В этом руководстве вы узнаете **как сохранить OCR**‑результат, используя Aspose.OCR для .NET. Мы пройдём процесс распознавания текста на изображении, а затем преобразуем этот текст в популярные форматы документов, такие как DOCX, TXT, PDF и XLSX. К концу вы сможете автоматизировать извлечение данных из изображений и сохранять их в виде поисковых, редактируемых файлов — идеально для архивирования, отчётности или последующей обработки.

## Быстрые ответы
- **Что означает «как сохранить OCR»?** Это относится к сохранению распознанного из изображения текста в файл формата DOCX, PDF и т.д.  
- **В какие форматы можно экспортировать?** Поддерживаются DOCX, TXT, PDF и XLSX «из коробки».  
- **Нужна ли лицензия?** Для оценки доступна бесплатная пробная версия; для использования в продакшене требуется коммерческая лицензия.  
- **Можно ли напрямую конвертировать изображение в PDF?** Да — сохраните результат OCR как PDF, чтобы получить поисковый PDF‑документ.  
- **Поддерживается ли PNG?** Абсолютно; вы можете **извлекать текст из PNG**‑изображений тем же API.

## Что такое OCR и почему сохранять результаты в документы?

OCR (Optical Character Recognition) преобразует печатный или рукописный текст на изображениях в машинно‑читаемые строки. Сохранение этих строк в виде документов позволяет создавать **поисковые PDF**, заполнять электронные таблицы, генерировать редактируемые отчёты или архивировать простые текстовые журналы. Aspose.OCR может превратить отсканированное изображение в **поисковый PDF** за один шаг, устраняя необходимость в отдельных инструментах создания PDF.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- Aspose.OCR для .NET установлен. Вы можете скачать его **[здесь](https://releases.aspose.com/ocr/net/)**.  
- Папка на вашем компьютере, в которой будут храниться исходные изображения и выходные документы. Обновите переменную `dataDir` в коде, указав путь к этой папке.

## Импорт пространств имён

Нужны несколько пространств имён .NET для доступа к файловому вводу‑выводу и классам Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Шаг 1: Инициализация Aspose.OCR

AsposeOcr — основной класс, выполняющий операции OCR. Укажите путь к рабочему каталогу и создайте экземпляр OCR‑движка.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Шаг 2: Распознавание изображения

RecognitionResult содержит текст и информацию о макете, извлечённые из изображения. Передайте файл изображения (например, PNG) распознавателю. Здесь мы **распознаём текстовые изображения** и преобразуем их в `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Шаг 3: Сохранение результата в разных форматах

Теперь экспортируем распознанный текст. Выберите формат, соответствующий вашему рабочему процессу — будь то **конвертация изображения в поисковый PDF**, **извлечение текста из PNG** или создание электронной таблицы.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Шаг 4: Вывод сообщения об успехе

Простое сообщение в консоли подтверждает, что процесс завершён без ошибок.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Распространённые ошибки и советы

- **Пути к файлам:** Всегда используйте абсолютные пути или убедитесь, что `dataDir` заканчивается разделителем пути (`\` или `/`).  
- **Качество изображения:** Изображения с более высоким разрешением повышают точность; рассмотрите предварительную обработку (выравнивание, шумоподавление) для лучших результатов.  
- **Режим лицензии:** В режиме оценки вывод может содержать водяной знак; примените действующую лицензию, чтобы убрать его.

## Часто задаваемые вопросы

**В1. Совместим ли Aspose.OCR с различными форматами изображений?**  
ОТВ: Да, Aspose.OCR поддерживает более 30 форматов изображений, включая PNG, JPEG, TIFF, BMP и GIF, обеспечивая гибкость ваших OCR‑задач.

**В2: Можно ли настроить параметры распознавания для повышения точности?**  
ОТВ: Абсолютно! Aspose.OCR предоставляет `RecognitionSettings` для тонкой настройки процесса OCR в соответствии с вашими требованиями.

**В3: Доступна ли бесплатная пробная версия?**  
ОТВ: Да, вы можете начать с бесплатной пробной версии **[здесь](https://releases.aspose.com/)**.

**В4: Как получить временную лицензию для Aspose.OCR?**  
ОТВ: Временные лицензии можно получить **[здесь](https://purchase.aspose.com/temporary-license/)**.

**В5: Где можно получить помощь или связаться с сообществом?**  
ОТВ: Присоединяйтесь к сообществу Aspose.OCR на **[форуме Aspose](https://forum.aspose.com/c/ocr/16)** для поддержки и обсуждений.

---

**Последнее обновление:** 2026-06-29  
**Тестировано с:** Aspose.OCR 24.11 для .NET  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Похожие руководства

- [Извлечение текста из изображения с помощью Aspose.OCR .NET](/ocr/net/image-and-drawing-recognition/)
- [Конвертация изображений в PDF C# – Сохранение многостраничного результата OCR](/ocr/net/ocr-optimization/save-multipage-result-as-document/)
- [Извлечение текстовых изображений – Параметры OCR](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}