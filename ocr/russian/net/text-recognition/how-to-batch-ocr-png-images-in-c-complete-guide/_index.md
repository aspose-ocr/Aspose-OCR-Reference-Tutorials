---
category: general
date: 2026-03-17
description: Как быстро выполнять пакетный OCR PNG‑изображений в C#. Узнайте, как
  извлекать текст из PNG‑файлов, конвертировать PNG в текст и считывать изображения
  из каталога с помощью простого скрипта.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: ru
og_description: Как пакетно выполнять OCR PNG‑изображений в C# с пошаговым кодом.
  Извлекать текст из PNG‑файлов, конвертировать PNG в текст и без труда считывать
  изображения из каталога.
og_title: Как пакетно выполнять OCR PNG‑изображений в C# – Полное руководство
tags:
- OCR
- C#
- Image Processing
title: Как пакетно выполнять OCR PNG‑изображений в C# – Полное руководство
url: /ru/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как пакетно выполнять OCR PNG‑изображений в C# – Полное руководство

Когда‑нибудь задумывались **как пакетно выполнять OCR** папки, полной скриншотов, без ручного открытия каждого файла? Вы не одиноки — разработчики постоянно спрашивают, как пакетно выполнять OCR больших коллекций PNG, особенно когда цель — извлечь текст из PNG‑файлов для последующего анализа.  

В этом руководстве мы пройдемся по готовому к запуску примеру на C#, который **извлекает текст из PNG**‑файлов, **преобразует PNG в текст** и покажет лучший способ **читать изображения из каталога**. К концу вы получите один скрипт, который создаст файл `.txt` рядом с каждым изображением, экономя часы ручного копирования‑вставки.

## Что вы получите

- Инициализируете OCR‑движок один раз и будете переиспользовать его для всей партии.  
- Сканируете каждый `*.png` в заданной папке без написания собственного цикла.  
- Записываете каждый результат OCR в отдельный текстовый файл, сохраняя оригинальное имя файла.  
- Обрабатываете типичные граничные случаи, такие как пустые папки или файлы не‑изображения, без сбоев.

### Предпосылки

- .NET 6.0 или новее (код работает и на .NET Core, и на .NET Framework).  
- OCR‑библиотека, предоставляющая типы `OcrEngine`, `ImageStream` и `OcrResult` (например, вымышленный SDK **FastOCR**, используемый в фрагментах).  
- Базовые знания C# — никаких продвинутых шаблонов не требуется.

---

## Как пакетно выполнять OCR PNG‑изображений – Обзор

Ниже приведена **полная, готовая к запуску программа**. Скопируйте‑вставьте её в новый консольный проект, замените пути‑заполнители и нажмите **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Ожидаемый вывод:** Для каждого `image01.png` вы найдете `image01.txt` с распознанными символами. Консоль будет выводить каждый файл по мере его записи.

![Диаграмма пакетного OCR](how-to-batch-ocr-diagram.png "Диаграмма, иллюстрирующая пакетный OCR PNG изображений с использованием C#")

---

## Пошаговое объяснение

### 1. Инициализация OCR‑движка — ядро процесса  

Строка `var ocrEngine = new OcrEngine();` создаёт единственный экземпляр движка, который будет переиспользован для всей партии. Переиспользование движка **критически важно**, потому что большинство OCR‑библиотек выделяют тяжёлые ресурсы (например, языковые модели) при создании. Инициализация один раз резко повышает производительность — особенно при десятках и сотнях PNG‑файлов.

> **Pro tip:** Если нужен язык, отличный от английского, задайте `ocrEngine.Config.Language = Language.Spanish;` (или любой поддерживаемый enum).  

### 2. Чтение изображений из каталога — поиск каждого PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` делает ровно то, что обещает вторичное ключевое слово *read images from directory*. Он возвращает массив абсолютных путей, которые мы позже передаём OCR‑движку.  

> **Почему не использовать `SearchOption.AllDirectories`?** Если ваши изображения находятся в подпапках, можно переключиться на `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Просто помните, что более глубокий поиск может захватить нежелательные файлы, поэтому фильтруйте их соответствующим образом.

### 3. Преобразование путей файлов в объекты ImageStream  

Большинство OCR‑SDK ожидают поток, а не простой путь. Выражение LINQ `Select(path => ImageStream.FromFile(path)).ToList()` формирует **список потоков**, который пакетный распознаватель может обработать за один вызов. Этот шаг также гарантирует, что файловые дескрипторы открываются лишь один раз, снижая нагрузку ввода‑вывода.

> **Edge case:** Если файл повреждён, `ImageStream.FromFile` может бросить исключение. Оберните преобразование в `try/catch`, если нужна устойчивость.

### 4. Распознавание текста во всей партии  

`ocrEngine.RecognizeBatch(imageStreams)` — это «sweet spot» для *how to batch OCR*. Вместо того чтобы перебирать каждое изображение и вызывать метод для одного изображения, мы передаём всю коллекцию движку. Внутри библиотека может параллелить работу, давая ускорение на многопроцессорных машинах.

> **Tip:** Если ваша OCR‑библиотека не предоставляет метод пакетного распознавания, аналогичную производительность можно достичь, используя `Parallel.ForEach` вокруг одиночного метода `Recognize`.

### 5. Запись каждого результата OCR — преобразование PNG в текст  

Последний цикл `for` записывает `ocrResults[i].Text` в файл `.txt`, имя которого повторяет оригинальный PNG. Это именно то, что описывает вторичное ключевое слово *convert PNG to text*. Вызов `Path.Combine` гарантирует, что папка вывода существует, и предотвращает ошибки обхода путей.

> **Common pitfall:** Если забыть создать выходную директорию заранее, возникнет `DirectoryNotFoundException`. Строка `Directory.CreateDirectory(outputFolder);` решает эту проблему заранее.

---

## Обработка реальных вариаций

| Ситуация | Что изменить | Почему |
|-----------|----------------|-----|
| **Пустая входная папка** | Оставить раннюю проверку `if (imagePaths.Length == 0)` | Предотвращает лишний вызов OCR и выводит дружелюбное сообщение |
| **Смешанные типы файлов** | Использовать `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Гарантирует обработку только PNG, удовлетворяя *extract text png* без ошибок |
| **Большие изображения ( > 5 МБ )** | Уменьшить размер перед передачей в OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (если API поддерживает) | Снижает нагрузку на память и часто улучшает точность распознавания |
| **Другой язык OCR** | Установить `ocrEngine.Config.Language = Language.French;` | Соответствует языку исходных изображений |

---

## Часто задаваемые вопросы (FAQ)

**В: Работает ли это с JPEG или TIFF файлами?**  
О: Основная логика остаётся той же; просто измените шаблон поиска на `"*.jpg"` или `"*.tif"` и убедитесь, что OCR‑библиотека умеет декодировать эти форматы.

**В: Как обработать тысячи изображений, не исчерпав память?**  
О: Замените пакетный вызов на потоковый подход — обрабатывайте, например, порциями по 50 изображений, затем освобождайте потоки перед загрузкой следующей порции.

**В: Мне нужен показатель уверенности OCR. Где его найти?**  
О: Большинство объектов `OcrResult` имеют свойство `Confidence`. Вы можете расширить шаг записи:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Итоги

Мы только что рассмотрели **как пакетно выполнять OCR** PNG‑изображений в C# от начала до конца. Инициализировав один движок, прочитав изображения из каталога, преобразовав их в потоки, распознав всю партию и записав каждый результат в текстовый файл, вы получили надёжный, готовый к продакшну шаблон для задач **extract text PNG**, **convert PNG to text** и **read images from directory**.

Что дальше? Попробуйте заменить поставщика OCR, добавить многопоточную пост‑обработку (например, проверку орфографии) или загрузить `.txt` файлы в поисковый индекс. Возможности безграничны, как только вы освоите пакетный рабочий процесс.

Есть свой вариант? Оставьте комментарий, и happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}