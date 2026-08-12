---
category: general
date: 2026-02-22
description: Создайте PDF с возможностью поиска и извлеките текст из изображения с
  помощью Aspose OCR. Узнайте, как преобразовать изображение в PDF и получить обычный
  текст в одном руководстве.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: ru
og_description: Создайте PDF с возможностью поиска из отсканированных изображений
  с помощью Aspose OCR. В этом руководстве показано, как извлечь текст из изображения,
  вывести его в виде обычного текста и преобразовать изображение в PDF.
og_title: Создание PDF с возможностью поиска из изображений – Полный учебник по C#
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Создание поискового PDF из изображений в C# – пошаговое руководство
url: /ru/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Генерация поискового PDF из изображений на C# – Полный учебник

Когда‑то вам нужно было **создать поисковый PDF** из отсканированного изображения, но вы не знали, с чего начать? Вы не одиноки — большинство разработчиков сталкиваются с этим, когда впервые встречают OCR. Хорошая новость? С Aspose OCR вы можете **извлекать текст из изображения**, **получать обычный текст** и **конвертировать изображение в PDF** всего в несколько строк кода на C#.

В этом руководстве мы пройдем весь процесс, от загрузки PNG‑файла до сохранения поискового PDF и обычного текстового файла. К концу вы получите переиспользуемый фрагмент, который можно вставить в любой .NET‑проект. Без лишних слов, только то, что действительно работает.

## Что вы узнаете

- Как настроить **Aspose.OCR** в консольном приложении .NET.  
- Разницу между режимами **output plain text** и **searchable PDF**.  
- Как **extract text from image** и записать его в файл `.txt`.  
- Как **convert image to PDF**, сохраняющий оригинальный битмап и добавляющий скрытый слой текста.  
- Советы по обработке больших пакетов, типичные подводные камни и места, где можно настроить параметры для лучшей точности.

> **Prerequisites** – Вам нужен .NET 6+ (или .NET Framework 4.7+), Visual Studio 2022 (или любой редактор) и лицензия Aspose OCR (или бесплатная пробная версия). Другие сторонние библиотеки не требуются.

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## Шаг 1: Установите Aspose OCR и создайте движок

Первым делом — добавьте пакет NuGet в ваш проект:

```bash
dotnet add package Aspose.OCR
```

Теперь можно создать OCR‑движок и указать, с каким языком мы работаем. Английский используется по умолчанию, но вы можете переключиться на французский, испанский и т.д., изменив перечисление `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Почему это важно:** Движок хранит всю конфигурацию — язык, формат вывода и необязательные флаги предобработки. Установив её один раз и переиспользуя, вы избегаете накладных расходов на создание нового экземпляра для каждого файла.

## Шаг 2: Извлеките текст и сохраните как обычный текст

Если вам нужны только сырые символы, переключите движок в `OutputFormat.Text`. Это заставит Aspose OCR полностью отказаться от генерации PDF и вернуть строку.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Pro tip:** `plainTextResult.Text` уже удаляет разрывы строк, принадлежащие разметке OCR. Если вам нужно сохранить оригинальные отступы, смотрите `plainTextResult.TextBlocks`.

### Ожидаемый результат

Откройте `output.txt`, и вы увидите что‑то вроде:

```
Hello, world!
This is a sample scanned document.
```

Это часть **output plain text** учебника — быстро, легковесно и идеально для последующей обработки (например, индексации).

## Шаг 3: Переключитесь в режим поискового PDF

Теперь создадим **searchable PDF**. Движок внедрит оригинальный битмап и наложит под него сгенерированный OCR‑текст, делая документ поисковым в любом PDF‑просмотрщике.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Почему мы повторно распознаём:** OCR‑движок кэширует последнее изображение, но формат вывода определяет, какие данные он возвращает. Переключение формата заставляет выполнить новый проход, включающий скрытый слой текста.

### Как выглядит PDF

Откройте `output.pdf` в Adobe Reader или любом другом просмотрщике и попробуйте выделить текст. Вы сможете копировать, искать и выделять содержимое, хотя визуально отображается оригинальный битмап. Это и есть суть **convert scanned image pdf**.

## Шаг 4: Обработка нескольких файлов (опционально)

В реальных проектах редко обрабатывают одно изображение. Ниже простой цикл, который обрабатывает каждый PNG в папке, создавая соответствующие файлы `.txt` и `.pdf`.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Примечание о граничных случаях:** Большие изображения могут исчерпать память. Если вы получаете `OutOfMemoryException`, рассмотрите уменьшение размера с помощью `Image.Resize` перед распознаванием или обрабатывайте файлы небольшими партиями.

## Шаг 5: Точная настройка точности OCR

Aspose OCR предоставляет несколько параметров, которые можно настроить:

| Setting | What it does | When to use |
|---------|--------------|-------------|
| `ocrEngine.PageSegmentationMode` | Управляет тем, как движок делит изображение на текстовые блоки. | Полезно для макетов с несколькими колонками. |
| `ocrEngine.Deskew` | Автоматически выравнивает слегка наклонённые страницы. | Сканированные документы, не идеально отсканированные. |
| `ocrEngine.RemoveNoise` | Пытается очистить пятна и фоновые артефакты. | Низкокачественные сканы или факсимильные страницы. |

Пример:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Включение этих опций может увеличить время обработки, но улучшение качества **extract text from image** зачастую того стоит.

## Шаг 6: Программная проверка результата

Иногда нужно убедиться, что PDF действительно содержит поисковый текст (например, в автоматических тестах). Самая простая проверка — убедиться, что массив байтов PDF не пуст и длина `RawData` превышает размер изображения.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Для более глубокой валидации можно воспользоваться PDF‑библиотекой (например, iTextSharp), извлечь поток текста и сравнить его с `plainTextResult.Text`.

## Распространённые подводные камни и как их избежать

- **Отсутствие лицензии** – Без действующей лицензии Aspose работает в режиме оценки, добавляя водяной знак в PDF. Зарегистрируйте лицензию сразу (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Неправильный путь** – Жёстко прописанные абсолютные пути работают только на вашей машине. Используйте `Path.Combine` с `AppDomain.CurrentDomain.BaseDirectory` для переносимости.  
- **Неподдерживаемые форматы изображений** – GIF и TIFF с несколькими кадрами требуют особой обработки (`Image.LoadMultiPage`). Конвертируйте их в PNG/JPEG, если нужен только первый кадр.  
- **Узкие места производительности** – Создание `OcrEngine` внутри цикла дорого. Держите один экземпляр и меняйте только `OutputFormat`, как показано выше.

## Итоги

Мы прошли весь рабочий процесс **generate searchable PDF** из отсканированного изображения с помощью Aspose OCR:

1. Установили пакет NuGet и создали `OcrEngine`.  
2. Установили `OutputFormat.Text` для **output plain text** и записали его в файл `.txt`.  
3. Переключились на `OutputFormat.SearchablePdf` для **convert image to PDF** с невидимым слоем текста.  
4. Сохранили PDF‑байты и при желании обработали каталог в пакетном режиме.  
5. Точно настроили точность с помощью deskew, удаления шума и параметров сегментации страниц.  

Всё это укладывается в компактную, самодостаточную программу, которую можно скопировать‑вставить в Visual Studio.

## Что попробовать дальше?

- **Пакетная обработка** с пользовательским интерфейсом (WinForms или WPF), чтобы пользователи могли перетаскивать файлы.  
- **Определение языка** — Aspose OCR умеет автоматически определять язык; попробуйте `ocrEngine.Language = Language.AutoDetect`.  
- **Последующая обработка** — Передайте извлечённый текст в поисковый индекс (ElasticSearch, Azure Cognitive Search) для мгновенного поиска по документам.  
- **Альтернативные форматы вывода** — Используйте `OutputFormat.Hocr` для HTML‑результатов OCR, удобно для веб‑превью.

Экспериментируйте с различными разрешениями изображений, цветовыми режимами и настройками OCR. Чем больше вы играете, тем лучше понимаете компромиссы между скоростью и точностью.

---

**Happy coding!** Если столкнётесь с какими‑либо нюансами, оставьте комментарий ниже или ознакомьтесь с документацией Aspose OCR для более глубокого погружения. Ваш следующий проект — будь то обработка счетов, архивирование или построение поисковой базы знаний — теперь стал гораздо проще.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}