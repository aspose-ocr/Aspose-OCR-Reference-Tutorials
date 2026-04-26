---
category: general
date: 2026-04-26
description: Создайте поисковый PDF из отсканированного изображения с помощью Aspose
  OCR в C#. Узнайте, как быстро преобразовать отсканированное изображение, извлечь
  текст и сгенерировать поисковый PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: ru
og_description: Создайте поисковый PDF из отсканированного изображения с помощью Aspose
  OCR. Пошаговый код на C# для конвертации, извлечения текста и генерации поискового
  PDF.
og_title: Создание поискового PDF из отсканированного изображения – руководство по
  C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Создание PDF с возможностью поиска из отсканированного изображения – руководство
  по C#
url: /ru/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из отсканированного изображения – Руководство C#  

Когда‑нибудь вам нужно было **создать поисковый PDF** из бумажных контрактов, чеков или старых архивов? Вы не одиноки — большинство разработчиков сталкиваются с этой проблемой, когда клиент передаёт кучу сканов TIFF и ожидает готовый поисковый PDF.  

В этом руководстве мы покажем вам точно **как выполнить OCR документа** и превратить отсканированное изображение в **поисковый PDF** с помощью Aspose OCR для .NET. К концу вы сможете **конвертировать отсканированные изображения**, **извлекать текст из изображения** и даже обрабатывать многостраничные TIFF без усилий.

## Что понадобится

* .NET 6.0 или новее (API работает с .NET Core, .NET Framework и .NET 5+).  
* Действующая лицензия Aspose OCR или вы согласны с водяным знаком в оценочной версии.  
* Пакет NuGet `Aspose.OCR`, установленный (`dotnet add package Aspose.OCR`).  
* Пример файла TIFF (например, `contract_scan.tif`), который вы хотите превратить в поисковый PDF.

Вот и всё — никаких дополнительных библиотек, без сложных настроек. Готовы? Поехали.

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## Шаг 1 – Инициализация OCR‑движка (Создание поискового PDF)

Первое, что нужно: создать экземпляр `OcrEngine`. Этот объект — основной исполнитель, который читает bitmap, определяет символы и возвращает вам текст.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Зачем задавать язык?**  
Если оставить значение по умолчанию, Aspose будет пробовать все языковые пакеты, что замедляет процесс. Указание `Language.Latin` заставляет движок сосредоточиться на латинском алфавите, давая ускорение и более точные результаты для контрактов на английском языке.

## Шаг 2 – Загрузка отсканированного изображения (Конвертация отсканированного изображения)

Теперь передаём движку изображение, которое нужно обработать. Aspose может читать путь к файлу, поток или даже `byte[]`. Для простоты мы используем `ImageStream.FromFile`.

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Если вам когда‑нибудь понадобится **конвертировать TIFF в PDF**, имейте в виду, что многостраничные TIFF обрабатываются автоматически — каждый кадр становится отдельной страницей PDF.

## Шаг 3 – Запуск OCR и получение текста (Извлечение текста из изображения)

Запуск OCR так же прост, как вызов `Recognize`. Движок вернёт `RecognitionResult`, содержащий простой текст, оценки уверенности и информацию о разметке.

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Полезный совет:** Если вам нужен только текст (без PDF), можно остановиться здесь и записать `extractedText` в файл `.txt`. Но чаще всего наша цель — поисковый PDF, поэтому продолжаем.

## Шаг 4 – Сохранение как поискового PDF (Создание поискового PDF)

Aspose делает последний шаг тривиальным: просто вызовите `Save` с `SaveFormat.PdfSearchable`. Под капотом библиотека встраивает извлечённый текст как невидимый слой, сохраняя оригинальный вид изображения.

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Когда вы откроете `contract_searchable.pdf` в любом PDF‑просмотрщике, сможете выделять, копировать и искать текст — именно то, что клиент ожидает от «поискового PDF».

## Обработка многостраничных TIFF (Конвертация TIFF в PDF)

Если исходный файл содержит несколько страниц, Aspose автоматически будет рассматривать каждый кадр как отдельную страницу. Дополнительные циклы не требуются. Тем не менее, вы можете захотеть контролировать DPI или качество изображения для каждой страницы:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

После установки этих параметров повторите **Шаг 2** для каждого кадра, либо просто укажите `ImageStream.FromFile` на многостраничный TIFF и позвольте Aspose выполнить всю работу.

## Распространённые проблемы и их решение

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| Текст искажен или отсутствует | Установлен неверный язык | Установите `ocrEngine.Language` на правильный языковой пакет (например, `Language.German`). |
| PDF огромный (10 МБ для одностраничного скана) | Сжатие изображения по умолчанию низкое | Настройте `ocrEngine.ImageProcessingOptions.Compression` на `Jpeg` и задайте разумное значение `Quality` (0‑100). |
| OCR работает очень медленно | Используется автоматическое определение языка по умолчанию | Явно задайте ожидаемый язык. |
| Отсутствует поисковый слой | Сохранено с `SaveFormat.Pdf` вместо `PdfSearchable` | Используйте `PdfSearchable`. |

## Полный пример от начала до конца

Объединив всё вместе, представляем готовое к запуску консольное приложение, которое вы можете скопировать и вставить в Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Что вы увидите:**  
* Окно консоли, выводящее фрагмент распознанного текста.  
* Файл `contract_searchable.pdf`, находящийся рядом с оригинальным TIFF. Откройте его, нажмите **Ctrl + F** и найдите любое слово, которое было в исходном скане — вуаля, работает.

## Следующие шаги и связанные темы

* **Как выполнять OCR документов** пакетно — оберните код выше в цикл `foreach` и обработайте всю папку.  
* **Конвертировать отсканированные изображения** в форматы, отличные от TIFF (PNG, JPEG) — тот же API работает; просто измените расширение файла.  
* **Извлекать текст из изображения** для дальнейшего анализа — передайте `result.Text` в конвейер обработки естественного языка.  
* **Оптимизировать размер PDF** — изучите `PdfSaveOptions` для дальнейшего сжатия изображений или встраивания шрифтов только при необходимости.  

Экспериментируя с этими идеями, вы быстро станете специалистом, к которому обращаются за любой задачей «превратить скан в поисковый PDF».

---

### Кратко

Теперь вы знаете, как **создавать поисковые PDF** из отсканированных изображений с помощью Aspose OCR в C#. Процесс таков: инициализировать движок, загрузить изображение, выполнить OCR и сохранить с `PdfSearchable`. Настраивайте параметры языка, DPI и сжатия для обработки граничных случаев, и вы готовы **конвертировать отсканированные изображения**, **извлекать текст из изображения** и даже **конвертировать TIFF в PDF** в масштабе. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}