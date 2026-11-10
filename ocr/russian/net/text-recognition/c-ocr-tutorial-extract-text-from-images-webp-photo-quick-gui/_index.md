---
category: general
date: 2026-03-17
description: c# OCR tutorial – узнайте, как извлекать текст из файлов изображений,
  читать текст с фотографий WebP и преобразовывать изображение в текст с помощью простого
  OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: ru
og_description: Учебник по OCR на C# показывает, как извлекать текст из файлов изображений,
  считывать текст с фотографий в формате WebP и преобразовывать изображение в текст
  с помощью нескольких строк кода.
og_title: c# OCR руководство – Извлечение текста из изображений за несколько минут
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR учебник: извлечение текста из изображений (WebP, фото) – краткое руководство'
url: /ru/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Извлечение текста из изображений (WebP, фото)

Когда‑то вам нужно **извлечь текст из файлов изображений**, но вы не знали, с чего начать в C#? Возможно, у вас есть скриншот в формате WebP, JPEG‑чек или отсканированная страница PDF, и вы просто хотите получить содержащиеся в ней слова. В этом **c# OCR tutorial** мы пройдемся по полностью готовому к запуску примеру, который читает текст с фотографии, обрабатывает WebP и другие современные форматы и преобразует изображение в обычный текст — всё в паре строк кода.

**Что вы получите?** Вы сможете превратить любую картинку с текстом в поисковые строки, загрузить их в базы данных или передать в последующие AI‑конвейеры. Никакой магии, только надёжный OCR‑движок, несколько .NET‑API и понятные объяснения «почему» каждого шага.

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

- **.NET 6 SDK** (или новее). Приведённый ниже код компилируется с .NET 6+ и работает в Windows, Linux или macOS.
- **Visual Studio 2022** или любой другой редактор (VS Code тоже подойдёт).
- Пакет NuGet **`Microsoft.Windows.SDK.Contracts`** (предоставляет `Windows.Media.Ocr`). Установите его с помощью:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Файл изображения, который вы хотите обработать — для этого урока мы будем использовать **WebP**‑фото `photo.webp`, размещённое в папке `YOUR_DIRECTORY`.

> Pro tip: Если вы работаете на платформе, отличной от Windows, можете заменить `OcrEngine` на кроссплатформенную библиотеку, например **Tesseract**. Остальной код останется практически без изменений.

## Шаг 1: Создание проекта C# OCR Tutorial

Сначала создайте новое консольное приложение. Откройте терминал и выполните:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Добавьте требуемый пакет (как показано выше) и откройте проект в вашей IDE. Эта заготовка даёт чистый старт для **c# OCR tutorial**.

## Шаг 2: Подключение пространств имён и подготовка изображения

Нужны несколько директив `using`, чтобы компилятор знал, где искать `OcrEngine`, `SoftwareBitmap` и вспомогательные функции загрузки изображений.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Почему именно эти пространства имён?**  
> `Windows.Media.Ocr` содержит класс `OcrEngine`, который непосредственно выполняет распознавание. `Windows.Graphics.Imaging` позволяет декодировать изображение (включая WebP) в `SoftwareBitmap`, понятный движку. Помощники из `System.IO` и `Windows.Storage.Streams` упрощают загрузку файлов.

Теперь загрузим изображение. Встроенный декодер умеет работать с WebP, HEIF, PNG, JPEG и другими форматами, так что вы можете **читать текст из WebP** без дополнительных плагинов.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Особый случай:** Если ваше изображение уже чёрно‑белое, шаг конвертации можно пропустить. Преобразование в градации серого даёт небольшое ускорение и часто улучшает распознавание шумных фотографий.

## Шаг 3: Запуск OCR‑движка – распознавание текста с фотографии

Это ядро **c# OCR tutorial**. Мы создаём экземпляр `OcrEngine`, передаём ему bitmap и получаем распознанный текст.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Что происходит?**  
- `TryCreateFromUserProfileLanguages()` выбирает язык(и), указанные в профиле пользователя Windows, что обычно покрывает английский, испанский и т.д. Если нужен конкретный язык, используйте `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` выполняет тяжёлую работу в фоновом потоке и возвращает `OcrResult`, содержащий сырую строку, ограничивающие рамки слов и оценки уверенности.  
- В конце мы выводим `ocrResult.Text`, получая результат **convert image to text**, который можно передать дальше.

## Шаг 4: Полный, готовый к запуску пример

Объединив всё вместе, получаем автономную программу, которую можно скопировать в `Program.cs`. Она компилируется, запускается и выводит текст, извлечённый из `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Ожидаемый вывод

Если `photo.webp` содержит предложение «Hello, world! This is a test.», вы увидите примерно следующее:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Точные переносы строк зависят от разметки исходного изображения, но результат **extract text from image** всегда будет обычной строкой, с которой можно работать дальше.

## Часто задаваемые вопросы и особые случаи

### Работает ли это с другими форматами изображений?

Однозначно. Декодер (`BitmapDecoder`) автоматически определяет JPEG, PNG, BMP, GIF, **WebP**, HEIF и прочие форматы. Поэтому вы можете **читать текст из WebP**, JPEG или даже TIFF без изменения кода.

### Что делать, если OCR‑движок возвращает низкую уверенность?

Можно проанализировать `ocrResult.Lines` и каждый `OcrWord` на предмет `ConfidenceScore`. Если оценка ниже порога (например, 0.6), рассмотрите:

- Предобработку изображения (увеличить контраст, резкость, исправить наклон).  
- Использование изображения более высокого разрешения.  
- Переход на специализированную библиотеку, такую как **Tesseract**, для поддержки нескольких языков.

### Как обрабатывать несколько языков в одном изображении?

Создайте отдельные экземпляры `OcrEngine` для каждого языка и запускайте их последовательно, либо используйте библиотеку, поддерживающую смешанное определение языков. Для встроенного движка можно передать объект `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Можно ли запускать это на Linux/macOS?

API `Windows.Media.Ocr` доступен только в Windows. На других платформах замените раздел OCR на **Tesseract** (через `Tesseract.Net.SDK`). Код загрузки и предобработки остаётся тем же, так что остальная часть этого **c# OCR tutorial** применима.

## Pro Tips для повышения точности

- **Измените размер** больших изображений до максимум 2000 px по самой длинной стороне — OCR‑движки работают быстрее с умеренными размерами.  
- **Уменьшите шум** простым гауссовым размазыванием, если фото зернистое.  
- **Исправьте наклон** bitmap, если текст не полностью горизонтален; `SoftwareBitmap` можно повернуть перед передачей в `OcrEngine`.  
- **Кешируйте** объект `OcrEngine`, если обрабатываете множество изображений пакетно; повторное создание добавляет накладные расходы.

## Сопутствующие темы для изучения

- **Convert image to text** с помощью **Tesseract** для кроссплатформенных проектов.  
- **Extract text from PDF** путём рендеринга каждой страницы в изображение.  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}