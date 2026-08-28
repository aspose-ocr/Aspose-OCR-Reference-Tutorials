---
category: general
date: 2026-01-04
description: Создайте быстро ищущийся PDF из отсканированного PDF. Узнайте, как конвертировать
  отсканированный PDF, добавить OCR в PDF и отрегулировать качество изображения с
  помощью Aspose OCR на C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: ru
og_description: Быстро создайте поисковый PDF из отсканированного PDF. Следуйте этому
  пошаговому руководству, чтобы преобразовать отсканированный PDF, добавить OCR в
  PDF и настроить качество изображения.
og_title: Создать поисковый PDF из отсканированных файлов с помощью Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Создать PDF с поиском из отсканированных файлов с помощью Aspose OCR
url: /ru/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из отсканированных файлов с помощью Aspose OCR

Когда‑то вам нужно **создать поисковый PDF** из кучи отсканированных документов, но вы не знаете, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при построении конвейеров управления документами. Хорошая новость: с Aspose OCR вы можете **конвертировать отсканированный PDF**, добавить OCR и настроить качество изображения всего в нескольких строках C#.

В этом руководстве мы пройдем весь процесс, от загрузки отсканированного PDF до сохранения полностью поискового варианта. К концу вы точно будете знать **как использовать OCR** с Aspose, почему важна каждая настройка и что менять, если что‑то пойдёт не так. Никаких расплывчатых ссылок — только готовый, исполняемый пример, который можно сразу вставить в ваш проект.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 или новее (код также работает с .NET Core и .NET Framework)
- Действительная лицензия Aspose OCR (бесплатная пробная версия подходит для тестов)
- Входной PDF с именем `input.pdf`, расположенный в папке, к которой вы имеете доступ
- Visual Studio 2022 или любой другой редактор C#

И всё. Если что‑то из перечисленного вам незнакомо, сделайте паузу и установите недостающий компонент — больше ничего не требуется.

## Шаг 1: Инициализация OCR‑движка и загрузка отсканированного PDF  
**(Здесь мы **добавляем OCR в PDF** впервые.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Зачем нужен этот шаг?*  
`OcrEngine` — сердце Aspose OCR. Загрузка PDF сообщает движку, где искать растровые изображения, которые он будет анализировать. Если пропустить этот шаг, нечего будет конвертировать, и последующие операции вызовут исключение.

> **Совет:** Если ваш PDF защищён паролем, используйте `ocrEngine.LoadPdf(path, password)`, чтобы избежать ошибки во время выполнения.

## Шаг 2: Установка основного и дополнительных языков  
**(Мы **конвертируем отсканированный PDF** на английском, французском и немецком.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Почему язык важен?*  
Точность OCR зависит от ожидаемого набора символов. Указав английский как основной язык и добавив французский/немецкий, движок сможет правильно распознавать акцентированные символы и специальные глифы. Пропуск этой настройки часто приводит к «мусорному» тексту.

## Шаг 3: Настройка качества изображения — тонкая настройка вывода PDF  
**(Здесь мы **регулируем качество изображения** для баланса между размером файла и читаемостью.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Зачем менять `ImageQuality`?*  
Большее значение (90‑100) сохраняет чёткость, что критично для точности OCR, но одновременно увеличивает размер файла. Если вы архивируете миллионы страниц, уменьшите его до 70‑80 — получите более лёгкий PDF без значительной потери читаемости.

## Шаг 4: Сохранение результата как поискового PDF  
**(Теперь мы наконец **создаём поисковый PDF**, который можно индексировать.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Что происходит на самом деле?*  
Aspose OCR извлекает текстовый слой с каждой страницы и внедряет его позади оригинального изображения. Визуально PDF остаётся тем же, но теперь можно выделять, копировать и искать текст — огромный плюс для последующих процессов.

## Шаг 5: Проверка результата (необязательно, но рекомендуется)  
Легко предположить, что всё прошло успешно, но быстрая проверка спасёт от проблем позже.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Откройте файл, попробуйте выделить слово или нажмите `Ctrl+F` и введите фразу, которую знаете в оригинальном скане. Если текст выделяется, вы успешно **создали поисковый PDF**.

## Распространённые граничные случаи и способы их решения  

| Ситуация | Почему происходит | Быстрое решение |
|-----------|-------------------|-----------------|
| **Страницы разного разрешения** (некоторые 150 dpi, другие 300 dpi) | Качество OCR меняется от страницы к странице, что приводит к неравномерной поисковости. | Установите `ocrEngine.Config.Dpi = 300;` перед загрузкой, чтобы принудительно увеличить разрешение, или предварительно обработайте изображения с помощью `ImageProcessor` для нормализации DPI. |
| **Зашифрованный PDF** | Aspose OCR не может читать файл без пароля. | Передайте пароль в `LoadPdf`, как показано выше. |
| **Большие PDF (>500 MB)** | Потребление памяти резко возрастает, вызывая `OutOfMemoryException`. | Обрабатывайте документ частями: `ocrEngine.SplitPdfIntoPages();` затем OCR каждой страницы отдельно и объединяйте результаты. |
| **Не‑латинские символы** (например, кириллица) | Язык не добавлен, поэтому символы превращаются в «?». | Добавьте `Language.Russian` (или любой нужный язык) в `AdditionalLanguages`. |
| **Слишком низкое качество изображения** | Текст становится размытым, OCR не справляется. | Увеличьте `ImageQuality` или используйте `pdfOptions.Dpi = 300;` для внедрения изображений более высокого разрешения. |

## Полный готовый к запуску пример  

Ниже представлен полностью готовый к копированию в новое консольное приложение код. В нём реализованы все шаги, обработка ошибок и комментарии для ясности.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Ожидаемый вывод:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

После открытия `output.pdf` вы сможете выделять и искать любой текст, присутствующий в оригинальном скане.

---

## Часто задаваемые вопросы (FAQ)

**В: Работает ли это с PDF, содержащими как отсканированные изображения, так и нативный текст?**  
О: Да. Aspose OCR добавляет скрытый текстовый слой только там, где это необходимо, оставляя существующий текст нетронутым.

**В: Можно ли пакетно обрабатывать папку с PDF?**  
О: Да. Оберните приведённый выше код в цикл `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` и скорректируйте путь вывода.

**В: Как ещё уменьшить конечный размер PDF?**  
О: Понизьте `ImageQuality` до 70‑80, включите `Compress` или задайте `pdfOptions.Dpi = 150` для даунсемплинга изображений перед внедрением.

**В: Есть ли способ извлечь OCR‑текст без создания PDF?**  
О: Вызовите `ocrEngine.ExtractText();` после загрузки PDF. Метод вернёт строку обычного текста, которую можно сохранить или проиндексировать.

---

## Итоги  

Мы только что рассмотрели **как использовать OCR** с Aspose для **создания поискового PDF** из отсканированного документа, показали, как **конвертировать отсканированный PDF**, продемонстрировали **добавление OCR в PDF** и объяснили, как **регулировать качество изображения** для оптимального результата. Полный пример кода готов к запуску, а таблица с решением проблем поможет вам двигаться вперёд, когда возникнут непредвиденные ситуации.

Что дальше? Попробуйте поэкспериментировать с:

- Разными языковыми пакетами для многоязычных архивов
- Пользовательской предобработкой изображений (выравнивание, удаление шумов) через `ImageProcessor`
- Интеграцией поискового PDF в конвейер SharePoint или ElasticSearch

Не стесняйтесь оставить комментарий, если столкнётесь с проблемой или обнаружите интересный приём. Приятного кодинга и наслаждайтесь мгновенно поисковыми PDF! 

![Create searchable PDF flowchart showing OCR engine → language config → PDF save options → searchable PDF output](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}