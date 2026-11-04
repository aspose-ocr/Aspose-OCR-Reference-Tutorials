---
category: general
date: 2026-04-01
description: Создайте PDF с возможностью поиска в C# с использованием Aspose OCR —
  узнайте, как конвертировать отсканированный PDF, добавить OCR в PDF и включить ускорение
  с помощью GPU для быстрых результатов.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: ru
og_description: Быстро создавайте поисковый PDF в C# — конвертируйте отсканированные
  PDF, добавляйте OCR в PDF и включайте ускорение GPU для высокопроизводительной обработки.
og_title: Создайте PDF с возможностью поиска с помощью Aspose OCR на C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Создание PDF с возможностью поиска с помощью Aspose OCR на C#
url: /ru/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF с помощью Aspose OCR на C#

Когда‑то вам нужно **создать поисковый PDF** из кучи отсканированных документов? Вы не одиноки — многие команды сталкиваются с задачей преобразования PDF‑файлов, содержащих только изображения, в документы, по которым можно искать текст. Хорошая новость: с Aspose OCR вы можете **преобразовать отсканированный PDF** в полностью поисковый вариант всего в несколько строк кода на C#. В этом руководстве мы пройдем весь процесс, от добавления OCR в PDF до **включения ускорения на GPU** для повышения скорости.

Мы также покажем, как **конвертировать pdf в searchable** формат, обсудим, зачем может понадобиться **add OCR to PDF**, и дадим практические советы по работе с большими партиями файлов. К концу вы получите готовое консольное приложение, которое генерирует поисковый PDF, готовый к загрузке в любую систему управления документами.

---

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть следующее:

- **.NET 6.0** или новее (API также работает с .NET Framework, но .NET 6+ — оптимальный вариант).
- NuGet‑пакет **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).
- Отсканированный PDF‑файл (только изображения), который будет использоваться в качестве входных данных.
- Необязательно: машина с поддержкой GPU и установленным CUDA®, если вы хотите **enable GPU acceleration**.

И всё — без тяжёлых OCR‑движков и внешних сервисов. Всё работает локально.

---

## Создание поискового PDF — пошаговый обзор

Ниже представлена высокоуровневая схема, которой мы будем следовать:

1. **Инициализировать OCR‑движок** — указать Aspose, какие языки искать и использовать ли GPU.
2. **Указать движку ваш отсканированный PDF** — задать пути входного и выходного файлов.
3. **Запустить конвертацию** — Aspose выполнит всю работу и запишет поисковый PDF.
4. **Проверить результат** — открыть полученный файл и выполнить поиск текста.

Каждый шаг выделен в отдельный раздел, так что вы можете выбрать только те части, которые вам нужны.

---

## Преобразование отсканированного PDF в поисковый PDF

Первое, что нужно сделать — создать экземпляр `OcrEngine`. Этот объект является «рабочей лошадкой», которая читает растровые изображения внутри вашего PDF и извлекает из них текст.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Почему это работает:** `ConvertToSearchablePdf` читает каждую страницу, выполняет OCR над растровым содержимым и затем встраивает невидимый слой текста позади оригинального изображения. Результат выглядит точно так же, как исходный отсканированный документ, но теперь вы можете копировать, выделять и искать текст.

---

## Добавление OCR в PDF с помощью Aspose

Если у вас уже есть PDF и вы просто хотите **add OCR to PDF** без полной конвертации файла, можно вызвать тот же метод — Aspose рассматривает эту операцию как «добавление OCR». Приведённый выше код уже делает это, но ниже показан быстрый вариант, демонстрирующий обработку нескольких файлов в цикле:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Совет:** Храните один экземпляр `OcrEngine` для всей партии. Повторное создание объекта каждый раз добавляет лишние накладные расходы, особенно когда вы **enable GPU acceleration**.

---

## Включение ускорения на GPU для более быстрой OCR

Ускорение на GPU может сэкономить минуты при обработке большой партии. Aspose OCR использует NVIDIA CUDA под капотом, поэтому достаточно переключить булевый флаг:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Когда использовать:** Если вы обрабатываете PDF‑файлы размером более 10 МБ или более нескольких десятков файлов, GPU обычно даёт прирост скорости 2‑3×. На обычном ноутбуке без CUDA‑совместимого GPU оставьте значение `false` — библиотека автоматически переключится на процессор.

**Типичная ошибка:** Забыл установить правильную версию драйвера CUDA, что приводит к исключению времени выполнения (`CudaException`). Убедитесь, что ваш драйвер соответствует версии, ожидаемой Aspose (см. примечания к выпуску на странице NuGet).

---

## Полный рабочий пример (все шаги вместе)

Ниже — полностью автономное консольное приложение, которое можно скопировать в новый .NET‑проект. В нём есть комментарии, обработка ошибок и финальный шаг проверки, выводящий количество обработанных страниц.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Ожидаемый вывод**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Откройте `output.pdf` в любом PDF‑просмотрщике и попробуйте ввести слово, которое присутствует на отсканированных изображениях. Если текст подсвечивается, вы успешно **create searchable pdf**.

---

## Распространённые проблемы и профессиональные советы

| Проблема | Почему происходит | Как исправить / избежать |
|----------|-------------------|--------------------------|
| **GPU не обнаружен** | Отсутствует или несовместим драйвер CUDA. | Установите драйвер версии, указанной в примечаниях к выпуску Aspose; при необходимости задайте `UseGpuAcceleration = false` как запасной вариант. |
| **Неправильный язык** | По умолчанию OCR использует английский; другие языки требуют явного указания. | Установите `Language = Language.Spanish` (или любой поддерживаемый enum) перед конвертацией. |
| **Большие PDF вызывают OutOfMemory** | Движок загружает целые страницы в память. | Обрабатывайте PDF частями, используя `ocrEngine.PageRange = new PageRange(1, 5)` для каждой порции. |
| **Файл вывода повреждён** | Папка назначения недоступна для записи. | Запустите приложение с повышенными правами или выберите путь, в который можно писать. |
| **Текстовый слой не ищется** | Просмотрщик кеширует старую версию. | Обновите (refresh) PDF‑просмотрщик или откройте файл заново. |

**Профессиональный совет:** При работе с миксом отсканированных и «нативных» PDF проверяйте флаг `HasText` каждой страницы (`PdfPageInfo.HasText`) перед запуском OCR. Это экономит процессорное время и предотвращает двойной OCR на уже поисковых страницах.

---

## Программная проверка результата (опционально)

Если нужно автоматизировать проверку, Aspose.PDF может извлечь скрытый текст:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Этот фрагмент доказывает, что вы действительно **convert pdf to searchable** формат, а не просто наложили изображение.

---

## Пример изображения

![Create searchable PDF output example](https://example.com/images/searchable-pdf.png "Create searchable PDF using Aspose OCR")

*Alt text:* **create searchable pdf** пример, показывающий до (скан) и после (поисковый) вид.

---

## Следующие шаги и смежные темы

- **Пакетная обработка:** Оберните цикл из раздела «Add OCR to PDF» в Windows Service или Azure Function для ночных задач.
- **Расширенная поддержка языков:** Исследуйте `ocrEngine.Language = Language.Multilingual` для документов, содержащих смешанные скрипты.
- **Очистка после OCR:** Используйте `TextFragmentAbsorber` из Aspose.PDF для исправления типичных ошибок OCR (например, «0» vs «O»).
- **Безопасность**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}