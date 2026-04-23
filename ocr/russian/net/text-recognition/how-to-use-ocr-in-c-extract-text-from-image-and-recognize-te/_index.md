---
category: general
date: 2026-02-13
description: Как использовать OCR в C# для извлечения текста из изображения, распознавания
  текста на фотографии или JPG и выполнения OCR на изображении без интернета.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: ru
og_description: Как использовать OCR в C# для извлечения текста из изображения, распознавания
  текста на фотографии и выполнения OCR на изображении с полным, готовым к запуску
  примером.
og_title: Как использовать OCR в C# – извлечение текста из изображения
tags:
- OCR
- C#
- Image Processing
title: Как использовать OCR в C# – извлекать текст из изображения и распознавать текст
  на фотографии
url: /ru/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

"Вы можете". But maybe keep as is? The instruction: translate all text content. So translate "You might" to Russian: "Вы можете". But it's incomplete; keep as is.

Then closing shortcodes.

Also need to translate the "Pro tip" block.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – Извлечение текста из изображения и распознавание текста на фотографии

Когда‑нибудь задумывались **как использовать OCR**, чтобы вытянуть слова из скриншота, отсканированного чека или случайного фото, сделанного на телефоне? Вы не одиноки. Во многих реальных приложениях нам нужно превращать картинки в поисковый текст, а делать это локально — без ненадёжного интернет‑соединения — может ощущаться как головоломка.

Именно поэтому это руководство показывает пошаговый способ **извлечения текста из изображения** с помощью OCR‑движка на C#, а также охватывает, как **распознавать текст с фотографии**, **распознавать текст из JPG** и **запускать OCR на изображении**, находящемся прямо на вашем диске. К концу вы получите полностью готовую к копированию программу, работающую сразу из коробки.

## Что вы узнаете

- Как настроить OCR‑движок для упрощённого китайского (или любого другого языка, который вы подключите).  
- Точный код, необходимый для **загрузки ресурсов** из локальной папки — без сетевых запросов.  
- Как **распознавать текст с фотографии** файлов, таких как JPEG, PNG или BMP.  
- Советы по обработке типичных проблем, таких как отсутствие файлов модели или неподдерживаемые форматы изображений.  
- Полный, готовый к запуску пример, который можно вставить в Visual Studio и сразу увидеть результаты.

### Требования

- .NET 6.0 или новее (API, используемое здесь, ориентировано на .NET Standard 2.0, так что работают и более старые версии).  
- Базовое знакомство с C# и Visual Studio (или любой другой IDE).  
- Библиотека OCR, которую вы используете (в примере предполагается вымышленный класс `OcrEngine`, поставляемый с языковыми моделями).  
- Папка, содержащая необходимые файлы языковой модели — по сути «мозг», который движок использует для чтения китайских иероглифов.

> **Pro tip:** Если у вас ещё нет файлов китайской модели, скачайте их один раз с сайта поставщика и поместите в папку вроде `C:\OcrResources`. Движку больше никогда не понадобится выход в интернет.

---

![Диаграмма, показывающая процесс OCR на фотографии](path/to/ocr-diagram.png "Диаграмма, показывающая процесс OCR на фотографии")

## Как использовать OCR: настройка движка

Первое, что вам нужно, — это экземпляр OCR‑движка, сконфигурированный под нужный язык. В этом руководстве мы нацелены на **упрощённый китайский**, но заменив `OcrLanguage.ChineseSimplified` на `OcrLanguage.English` (или любое другое значение enum), вы измените язык всего в одну строку.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Почему это важно:**  
Установка свойства `Language` сообщает движку, какой набор символов ожидать. `ResourceFolder` — это место, где движок ищет веса нейронных сетей и словари языка — по сути банковскую память мозга. Если указать неправильную папку, движок бросит `FileNotFoundException`, и вы застрянете.

## Извлечение текста из изображения – загрузка ресурсов

Прежде чем движок сможет что‑то прочитать, необходимо загрузить файлы модели в память. Этот шаг **критически важен**, потому что он избавляет от сетевого запроса каждый раз, когда вы обрабатываете изображение.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Что может пойти не так?**  
Если путь к папке неверен или файлы повреждены, `LoadResources()` вызовет исключение. Блок `try/catch`, показанный выше, демонстрирует корректную обработку ошибок — то, что часто требуется в продакшене.

## Распознавание текста с фотографии – запуск OCR

Теперь самая интересная часть: передать файл изображения движку и получить распознанный текст. Это ядро сценариев **запуска OCR на изображении**, независимо от того, JPEG это, PNG или даже BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Метод `RecognizeImage` возвращает `RecognitionResult` (или как его называют в вашем SDK), который обычно содержит:

- `Text` — простая текстовая транскрипция.  
- `Confidence` — числовой показатель, указывающий, насколько уверенно движок распознал каждую строку.  
- `BoundingBoxes` — необязательные координаты, где каждое слово расположено на картинке.

**Почему может быть важна уверенность:**  
Если вы создаёте инструмент автоматизации ввода данных, можно задать порог (например, 0.85) и попросить пользователя подтвердить строки с низкой уверенностью. Это значительно повышает общую точность.

## Распознавание текста из JPG – обработка разных форматов

Многие разработчики считают, что OCR работает только с PNG, но современные движки без проблем обрабатывают **JPG** файлы. Единственное «подводное камень» — сжатие JPEG может добавить артефакты, сбивающие модель с толку.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Если у вас нет вспомогательной функции `DenoiseAndDeskew`, многие библиотеки (например, OpenCvSharp) предоставляют такие функции. Главное: **запускать OCR на изображении** после небольшой очистки, если файл получен со сканера или камеры телефона.

## Запуск OCR на изображении – советы, крайние случаи и лучшие практики

### 1. Управление памятью
Загрузка больших языковых моделей может потреблять сотни мегабайт. Освобождайте движок, когда он больше не нужен:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Пакетная обработка
Если нужно обработать десятки фотографий, загрузите ресурсы один раз, а затем выполните цикл:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Сценарии с несколькими языками
Можно переключать языки «на лету», переустанавливая `ocrEngine.Language` и вызывая `LoadResources()` снова. Только учитывайте дополнительное время загрузки.

### 4. Обработка пустых результатов
Иногда движок возвращает пустую строку. Это обычно означает, что изображение слишком размыто или цвет текста сливается с фоном. Быстрая проверка:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Соображения безопасности
Никогда не передавайте файлы, загруженные пользователем, напрямую в OCR‑движок без проверки. Как минимум, проверяйте расширение и размер файла, а также рассматривайте сканирование на наличие вредоносного кода.

## Полный рабочий пример

Ниже представлен единый, автономный программный файл, который можно скопировать в новый проект консольного приложения. Он демонстрирует **как использовать OCR**, **извлекать текст из изображения**, **распознавать текст с фотографии**, **распознавать текст из JPG** и **запускать OCR на изображении** — всё в одном месте.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Ожидаемый вывод (пример):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Ваш реальный текст будет отличаться в зависимости от содержимого изображения, но вы должны увидеть блок Unicode‑символов, выведенный в консоль вместе с процентом уверенности.

## Заключение

Мы прошли весь процесс **использования OCR** в C# от начала до конца — настройка движка, загрузка языковых ресурсов и, наконец, **распознавание текста с фотографии** или **из JPG** без обращения к интернету. Следуя этим шагам, вы сможете **извлекать текст из изображения**, **запускать OCR на изображении** и справляться с типичными подводными камнями, которые часто сбивают новичков.

Готовы к следующему вызову? Попробуйте передать движку страницу PDF, преобразованную в изображение, или поэкспериментировать с другим языковым пакетом, чтобы увидеть, как меняются показатели уверенности. Вы можете

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}