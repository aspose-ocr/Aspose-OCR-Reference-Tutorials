---
category: general
date: 2026-06-19
description: Как использовать Aspose OCR в C# для извлечения текста из изображений,
  выполнения OCR на изображениях и распознавания текста со сканов — пошаговое руководство.
draft: false
keywords:
- how to use aspose
- extract text from images
- run ocr on images
- recognize text from scans
language: ru
og_description: Как использовать Aspose OCR в C# для извлечения текста из изображений,
  выполнения OCR на изображениях и распознавания текста со сканов — полное руководство.
og_title: Как использовать Aspose OCR в C# — извлечение текста из изображений
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use Aspose OCR in C# to extract text from images, run OCR on
    images, and recognize text from scans – step‑by‑step guide.
  headline: How to Use Aspose OCR in C# – Extract Text from Images
  type: TechArticle
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Как использовать Aspose OCR в C# — извлечение текста из изображений
url: /ru/net/text-recognition/how-to-use-aspose-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать Aspose OCR в C# – извлечение текста из изображений

Когда‑то задумывались **как использовать Aspose**, чтобы вытащить слова из фотографии документа? Вы не первый, кто ломает голову над этим. В этом руководстве мы пройдём практический, сквозной пример, показывающий, как именно извлекать текст из изображений, выполнять OCR над изображениями пакетно и даже распознавать текст со сканов всего несколькими строками C#.

Мы начнём с настройки движка Aspose OCR, затем передадим ему список JPEG‑файлов и, наконец, выведем каждый результат в консоль. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой .NET‑проект — без загадочных шагов и недостающих ссылок.

## Что вам понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

* .NET 6.0 SDK или новее (код работает как на .NET Core, так и на .NET Framework)  
* Действительный пакет **Aspose.OCR** из NuGet (бесплатный пробный ключ можно получить на сайте Aspose)  
* Папка, содержащая несколько отсканированных изображений или фотографий текста (подойдут JPEG или PNG)  
* Любая любимая IDE — Visual Studio, Rider или даже VS Code.

И всё. Никаких тяжёлых OCR‑библиотек, никаких внешних консольных утилит. Только Aspose и пара строк кода.

## Шаг 1: Установите пакет Aspose.OCR из NuGet

Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Эта команда скачает последнюю версию (на июнь 2026 года это 22.9) и добавит ссылку в ваш `.csproj`. Если предпочитаете UI Visual Studio, щёлкните правой кнопкой **Dependencies → Manage NuGet Packages** и найдите “Aspose.OCR”.

> **Совет:** Следите за датой истечения лицензии; бесплатный пробный период длится 30 дней, после чего понадобится коммерческий ключ.

## Шаг 2: Настройте OCR‑движок – «Как использовать Aspose» начинается здесь

Пакет установлен, теперь создадим OCR‑движок и укажем, какой язык искать. В большинстве случаев достаточно английского, но Aspose поддерживает более 70 языков.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.Collections.Generic;

// Configure the OCR engine to use English language
var ocrConfig = new OcrEngineConfig { Language = Language.English };
using var ocrEngine = new OcrEngine(ocrConfig);
```

Зачем оборачивать `OcrEngine` в оператор `using`? Потому что он реализует `IDisposable`. Освобождение ресурсов удаляет нативные (неуправляемые) ресурсы, которые движок выделяет внутри — это необходимо в продакшн‑службе, обрабатывающей десятки файлов в минуту.

## Шаг 3: Сформируйте список путей к изображениям – подготовка к **Run OCR on Images**

Следующий шаг — простой `List<string>`, указывающий на каждую картинку, которую нужно обработать. Список можно собрать вручную (как показано ниже) или сформировать динамически с помощью `Directory.GetFiles`.

```csharp
// Prepare a list of image file paths to be processed
var imagePaths = new List<string>
{
    @"C:\Scans\page1.jpg",
    @"C:\Scans\page2.jpg",
    @"C:\Scans\page3.jpg"
};
```

Если ваши изображения находятся в подпапке относительно исполняемого файла, просто добавьте `Path.Combine`. Главное, чтобы порядок списка сохранялся — Aspose вернёт результаты в той же последовательности, что упрощает сопоставление вывода и ввода.

## Шаг 4: **Run OCR on Images** одним пакетом

Aspose OCR проявляет себя, когда требуется обработать множество файлов одновременно. Метод `ProcessBatch` принимает только что построенный список и возвращает `IList<OcrResult>`, где каждый элемент содержит распознанный текст, оценки уверенности и даже ограничивающие рамки, если они понадобятся позже.

```csharp
// Run OCR on the entire batch and obtain results in the same order
IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);
```

Под капотом Aspose порождает нативные потоки для ускорения работы, поэтому вы получаете почти линейное масштабирование по ядрам CPU. Для огромных нагрузок можно настроить свойство `OcrEngineConfig.ThreadCount`, но автоматическое определение по умолчанию хорошо работает в большинстве настольных сценариев.

## Шаг 5: Выведите **Recognized Text from Scans** – проверьте результат

Наконец, пройдемся по результатам и выведем каждый блок текста. Мы также отобразим оригинальное имя файла, чтобы вы могли увидеть, какому скану соответствует вывод.

```csharp
// Iterate through the results and display the recognized text for each image
for (int i = 0; i < ocrResults.Count; i++)
{
    System.Console.WriteLine($"--- Result for {imagePaths[i]} ---");
    System.Console.WriteLine(ocrResults[i].Text);
}
```

При запуске программы консоль покажет примерно следующее:

```
--- Result for C:\Scans\page1.jpg ---
Invoice #12345
Date: 06/15/2026
Total: $1,250.00

--- Result for C:\Scans\page2.jpg ---
Terms and Conditions
...
```

Вот и всё — **how to use Aspose** превращает стопку отсканированных PDF‑ов или JPEG‑ов в поисковый, редактируемый текст.

![How to Use Aspose OCR example output](image-placeholder.png "How to Use Aspose OCR example output")

*Текст alt изображения: “Пример вывода Aspose OCR, показывающий распознанный текст со сканов.”*

## Необязательно: Тонкая настройка точности – когда **Extract Text from Images** требует ускорения

Если замечаете пропущенные символы или искажённые слова, попробуйте следующие настройки:

| Setting | What it does | When to use it |
|---------|--------------|----------------|
| `ocrConfig.DetectOrientation = true` | Автоматически вращает изображения, находящиеся в боковом положении | Сканированные книги часто в портретной ориентации |
| `ocrConfig.Preprocess = true` | Применяет улучшение контраста и шумоподавление | Низкокачественные фотографии, снятые телефоном |
| `ocrConfig.CharacterWhitelist = "0123456789"` | Ограничивает распознавание только цифрами | Извлечение сумм счетов или серийных номеров |
| `ocrEngine.SetPageSegmentationMode(PageSegMode.SingleBlock)` | Рассматривает всю страницу как один блок текста | Когда макет простой и важна скорость |

Экспериментируйте с этими флагами, пока оценки уверенности (доступные через `ocrResults[i].Confidence`) не поднимутся выше 0.9. Помните: чем лучше исходное изображение, тем лучше результат OCR — небольшая предобработка в Photoshop или ImageMagick может сэкономить часы отладки.

## Полный рабочий пример – готовый к копированию

Ниже представлена полная программа, которую можно сразу собрать и запустить. Просто замените пути к файлам на свои.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine (how to use Aspose OCR)
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,
            DetectOrientation = true,          // optional: auto‑rotate
            Preprocess = true                  // optional: improve low‑quality scans
        };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 2️⃣ List of image files (run OCR on images)
        var imagePaths = new List<string>
        {
            @"C:\Scans\page1.jpg",
            @"C:\Scans\page2.jpg",
            @"C:\Scans\page3.jpg"
        };

        // 3️⃣ Process the batch (extract text from images)
        IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);

        // 4️⃣ Show the results (recognize text from scans)
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Result for {imagePaths[i]} ---");
            Console.WriteLine(ocrResults[i].Text);
            Console.WriteLine($"Confidence: {ocrResults[i].Confidence:P2}");
            Console.WriteLine(); // blank line for readability
        }
    }
}
```

Соберите с помощью `dotnet run` и наблюдайте, как консоль заполняется чистым, поисковым текстом. Это весь **how to use aspose** процесс в менее чем 50 строк кода.

## Распространённые подводные камни и их решения

* **NullReferenceException на `ocrResults[i]`** — обычно означает, что движок не смог открыть файл (неверный путь, неподдерживаемый формат). Проверьте расширение файла и права доступа.  
* **Неправильные символы** — если видите символы “�”, изображение, вероятно, сохранено в кодировке, отличной от UTF‑8. Сконвертируйте изображение в без‑потерьный PNG или включите `ocrConfig.Preprocess`.  
* **Узкое место в производительности** — для пакетов более 100 изображений рассмотрите параллельную обработку с `Parallel.ForEach` и отдельным экземпляром `OcrEngine` на каждый поток. Aspose потокобезопасен, если каждый поток владеет своим движком.

## Следующие шаги – углубляемся

Теперь, когда вы освоили основы **how to use Aspose** для OCR, можно исследовать:

* **Экспорт в поисковый PDF** — используйте `Aspose.Pdf`, чтобы внедрить распознанный текст обратно в PDF‑файл, превращая скан в действительно поисковый артефакт.  
* **Интеграция с Azure Functions** — автоматически запускайте OCR, когда новое изображение появляется в контейнере Azure Blob.  
* **Комбинация с AI‑моделями** — передавайте извлечённый текст в ChatGPT или Claude для суммирования, извлечения сущностей или перевода.

Во всех этих темах естественно встречаются наши вторичные ключевые фразы — **extract text from images**, **run OCR on images**, и **recognize text from scans** — так вы будете постоянно видеть те же паттерны, расширяя свои навыки.

## Заключение

Мы прошли полный, готовый к продакшн пример, отвечающий на вопрос **how to use Aspose** для извлечения текста из изображений, пакетного OCR и распознавания текста со сканов с минимальным объёмом кода. Настроив движок, подготовив список путей, обработав пакет и выведя результаты, вы получили надёжную основу для любого проекта автоматизации документов.

Попробуйте, поиграйте с настройками, и скоро вы будете превращать горы бумажных документов в поисковые данные.


## Что изучать дальше?


В следующих руководствах рассматриваются тесно связанные темы, построенные на техниках, продемонстрированных в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}