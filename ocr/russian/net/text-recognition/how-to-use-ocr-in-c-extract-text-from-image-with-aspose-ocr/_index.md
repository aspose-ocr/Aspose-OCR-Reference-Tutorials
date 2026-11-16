---
category: general
date: 2026-02-24
description: Как использовать OCR в C# для извлечения текста из файлов изображений.
  Узнайте, как преобразовать PNG в текст, асинхронно читать изображения и справляться
  с распространёнными подводными камнями.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: ru
og_description: Как использовать OCR в C# для извлечения текста из изображений. Это
  руководство демонстрирует пошаговое асинхронное OCR с Aspose, охватывая конвертацию,
  обработку ошибок и лучшие практики.
og_title: Как использовать OCR в C# – Полное руководство
tags:
- OCR
- C#
- Aspose
title: Как использовать OCR в C# — извлечение текста из изображения с помощью Aspose
  OCR
url: /ru/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – Извлечение текста из изображения

Когда‑нибудь задавались вопросом, **как использовать OCR**, чтобы извлечь текст из изображения без ручного ввода? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно *извлечь текст из изображения* файлов, таких как PNG, а обычный способ копировать‑вставлять просто не работает.  

В этом руководстве мы пройдем полный асинхронный процесс, который **преобразует PNG в текст** с помощью библиотеки Aspose.OCR. К концу вы точно будете знать, как читать файлы изображений, обрабатывать ошибки и интегрировать результат в свои приложения.  

Мы охватим всё: от настройки пакета NuGet до тонкой настройки OCR‑движка для повышения точности, а также добавим советы, что делать, когда изображение не идеально чёткое. Не нужно бегать по ссылкам в документации — всё, что нужно, находится здесь.

## Что понадобится

- .NET 6.0 или новее (код работает также на .NET Core и .NET Framework)  
- Visual Studio 2022 (или любой другой предпочитаемый IDE)  
- Пакет NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)  
- Файл изображения (PNG, JPG, BMP), который вы хотите обработать — назовём его `input.png`

Вот и всё. Если у вас отмечены все пункты, вы готовы приступать.

![Диаграмма, показывающая рабочий процесс OCR – как использовать OCR для извлечения текста из изображения](/images/ocr-workflow.png)

## Шаг 1: Установите Aspose.OCR и добавьте пространства имён

Сначала подключите библиотеку к вашему проекту. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.OCR
```

Затем, в начале вашего C# файла, добавьте необходимые пространства имён:

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **Pro tip:** Если вы используете минимальные API .NET 6, вы можете разместить эти `using` директивы в глобальном файле, чтобы не повторять их в разных классах.

### Почему это важно

Пространство имён `Aspose.OCR` предоставляет доступ к `OcrEngine` — основному классу, который действительно читает изображение. Без него вам пришлось бы писать собственный код анализа пикселей — огромный кроличий хвост. Добавление пространств имён делает код аккуратным и сообщает компилятору, где искать используемые типы.

## Шаг 2: Создайте асинхронный OCR‑движок

Мы обернём вызов OCR в `async` метод, чтобы ваш UI оставался отзывчивым, а серверный код мог масштабироваться. Вот каркас консольного приложения:

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Объяснение

- **`OcrEngine ocrEngine = new OcrEngine();`** – Создаёт экземпляр движка с настройками по умолчанию. Позже вы можете настроить язык, режим обнаружения или фильтры предобработки.  
- **`await ocrEngine.RecognizeImageAsync(...)`** – Асинхронный метод возвращает `Task<OcrResult>`. Ожидание освобождает поток, пока OCR работает в фоне.  
- **`ocrResult.Text`** – Текстовое представление всего, что движок смог прочитать. Это суть *как извлечь текст* из изображения.

## Шаг 3: Точная настройка движка для лучшей точности

Стандартный OCR хорошо работает с чистыми, контрастными изображениями, но в реальных условиях часто требуется небольшая помощь. Вы можете изменить несколько свойств перед вызовом `RecognizeImageAsync`:

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### Когда использовать эти настройки

- **Сканы низкого качества** – Включите `ImagePreprocessingOptions.Auto`, чтобы Aspose очистил шум.  
- **Многоязычные PDF** – Измените `Language` на `OcrLanguage.French` или комбинируйте языки с помощью битовой маски.  
- **Поля форм** – Ограничьте `Characters` цифрами или заглавными буквами, чтобы уменьшить количество ложных срабатываний.

## Шаг 4: Обрабатывайте ошибки корректно

OCR не волшебство; он может не сработать, если файл отсутствует, повреждён или в неподдерживаемом формате. Оберните асинхронный вызов в блок try/catch:

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### Почему это помогает

Предоставление понятных сообщений об ошибках ускоряет отладку и улучшает опыт конечного пользователя. Вместо общего сбоя вы получаете полезное сообщение, которое подсказывает, проверять ли путь, формат файла или конфигурацию OCR‑движка.

## Шаг 5: Соберите всё вместе — полностью рабочий пример

Ниже представлен полностью готовый к запуску консольный пример, демонстрирующий **как использовать OCR**, применяющий предобработку и обрабатывающий ошибки. Скопируйте его в новый `.csproj` и нажмите F5.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**Ожидаемый вывод** (при условии, что `input.png` содержит фразу “Hello World”):

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

Если изображение размыто, вы можете увидеть лишние символы или пропущенные слова — здесь в игру вступают параметры предобработки из Шага 3.

## Шаг 6: Расширение решения — из PNG в PDF или текстовые файлы

Иногда требуется **преобразовать PNG в текст**, а затем сохранить результат в `.txt` или встроить его в PDF‑отчёт. Вот быстрый фрагмент, который записывает вывод OCR в файл:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

Или, если вы генерируете PDF с помощью Aspose.PDF:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

Эти расширения показывают, как **как читать данные изображения** может питать последующие процессы — генерацию отчётов, индексацию поиска или даже подачу в языковую модель.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| *Какие форматы изображений поддерживаются?* | Aspose.OCR поддерживает PNG, JPEG, BMP, TIFF и GIF. Если у вас PDF, сначала извлеките его страницы как изображения. |
| *Могу ли я обрабатывать несколько изображений параллельно?* | Да — оберните каждый вызов `RecognizeImageAsync` в отдельную задачу и используйте `Task.WhenAll`. Просто следите за потреблением памяти. |
| *Что делать, если OCR возвращает пустой текст?* | Проверьте качество изображения: низкий контраст или повернутый текст часто приводят к провалу. Включите `ImagePreprocessingOptions.Deskew` или вручную поверните изображение перед OCR. |
| *Есть ли ограничение на размер изображения?* | Большие изображения (>10 МП) могут вызвать `OutOfMemoryException`. Снизьте их до разумного разрешения (например, 300 DPI) перед распознаванием. |
| *Нужна ли лицензия для Aspose.OCR?* | Режим разработки работает с временной лицензией, но для продакшна понадобится приобретённая лицензия, чтобы убрать водяные знаки оценки. |

## Советы по производительности

- **Повторно используйте экземпляр `OcrEngine`** для пакетной обработки; создание нового движка для каждого изображения добавляет накладные расходы.  
- **Отключайте неиспользуемые языки** для ускорения обнаружения — каждый дополнительный язык добавляет небольшие затраты на обработку.  
- **Запускайте OCR в фоновом потоке** (как показано), чтобы UI‑потоки оставались отзывчивыми в настольных или веб‑приложениях.

## Заключение

Мы рассмотрели **как использовать OCR** в C# от начала до конца: установка Aspose.OCR, написание асинхронного метода, настройка параметров для шумных изображений, обработка ошибок и сохранение результатов. Теперь у вас есть надёжный способ *извлекать текст из изображений*, *преобразовывать PNG в текст* и даже передавать этот текст в другие процессы, такие как генерация PDF.  

Готовы к следующему вызову? Попробуйте передать вывод OCR в индексируемый Azure Cognitive Search, или поэкспериментировать с многоязычным OCR, добавив `OcrLanguage.Spanish | OcrLanguage.French` в движок. Возможности безграничны, когда вы знаете **как программно читать данные изображения**.  

*Если этот гид оказался полезным, поставьте звёздочку на GitHub, поделитесь им с коллегами или оставьте комментарий ниже со своими приёмами OCR. Счастливого кодинга!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}