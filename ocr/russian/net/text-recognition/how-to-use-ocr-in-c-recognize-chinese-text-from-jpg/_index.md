---
category: general
date: 2026-05-25
description: Как использовать OCR в C# для извлечения текста из файлов изображений.
  Узнайте, как распознавать китайские символы из JPG с помощью Aspose.OCR за несколько
  простых шагов.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: ru
og_description: Как использовать OCR в C# для извлечения текста из файлов изображений.
  Это руководство показывает, как распознавать китайские символы из JPG с помощью
  Aspose.OCR.
og_title: Как использовать OCR в C# – распознавание китайского текста из JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Как использовать OCR в C# — распознавать китайский текст из JPG
url: /ru/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в C# – распознавание китайского текста из JPG

Когда‑нибудь задумывались **как использовать OCR**, чтобы извлечь слова из фотографии, сделанной на телефон? Вы не одиноки. Во многих реальных проектах — подумайте о сканерах чеков, приложениях‑переводчиках или автоматическом вводе данных — вам понадобится **извлекать текст из изображения** быстро и надёжно.

В этом руководстве мы пройдём через полностью готовый пример, который **распознаёт текст из JPG**‑файлов и даже справляется с сложным случаем **распознавания китайских иероглифов** с помощью языкового пакета **OCR Chinese Simplified**. К концу вы получите автономное консольное приложение, выводящее обнаруженную строку в консоль, без дополнительных ручных загрузок.

> **Краткое замечание:** Код работает с Aspose.OCR ≥ 23.7, который автоматически загружает языковые ресурсы при первом использовании. Если у вас более старая версия, потребуется добавить язык вручную.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- .NET 6.0 SDK или новее (пример ориентирован на .NET 6, но .NET 5 тоже подойдёт)
- Последняя версия Visual Studio 2022 или VS Code с расширением C#
- Интернет‑соединение для первой загрузки языка
- JPG‑изображение, содержащее упрощённый китайский текст (назовём его `chinese_sign.jpg`)

И всё — без тяжёлых OCR‑движков, без нативных DLL. Достаточно нескольких команд NuGet и пары строк кода.

## Шаг 1: Установите Aspose.OCR через NuGet

Во‑первых, нам нужна библиотека OCR. Откройте терминал в папке проекта и выполните:

```bash
dotnet add package Aspose.OCR
```

Или, если предпочитаете UI Visual Studio, щёлкните правой кнопкой **Dependencies → Manage NuGet Packages**, найдите “Aspose.OCR” и нажмите **Install**.

> **Совет:** Держите пакеты в актуальном состоянии. Новые языковые пакеты и оптимизации появляются в каждом минорном релизе.

## Шаг 2: Создайте новый консольный проект (если ещё не сделали)

Если вы начинаете с нуля, создайте новое консольное приложение:

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

Теперь у вас есть файл `Program.cs`, готовый для кода OCR.

## Шаг 3: Напишите код OCR – распознавание упрощённого китайского из JPG

Откройте `Program.cs` и замените его содержимое следующим кодом. Каждая строка прокомментирована, чтобы вы видели *почему* мы делаем тот или иной шаг, а не только *что* делаем.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Что происходит «под капотом»?

- **`OcrEngine.Language`** указывает Aspose, какой словарь использовать. Выбирая `ChineseSimplified`, мы инструктируем движок искать пакет упрощённого китайского языка.
- **Первичная загрузка**: Когда вызывается `Recognize`, SDK обращается к CDN Aspose, скачивает ≈6 МБ языковой файл, кэширует его локально и затем продолжает OCR. Последующие вызовы мгновенны.
- **`Image.FromFile`** работает с любым растровым форматом, который .NET умеет декодировать — JPG, PNG, BMP — так что вы можете **извлекать текст из изображения** файлов разных типов, а не только JPG.

## Шаг 4: Запустите приложение и проверьте вывод

Соберите и запустите:

```bash
dotnet run
```

Вы должны увидеть что‑то вроде:

```
=== Recognized Text ===
欢迎光临
```

Если консоль выводит мусор или пустую строку, проверьте следующее:

1. Изображение действительно содержит чёткие, контрастные китайские символы.
2. Путь к файлу правильный (нет лишних пробелов или отсутствующих расширений).
3. Ваш компьютер может достичь `https://download.aspose.com` для загрузки языкового пакета.

## Шаг 5: Обработка граничных случаев и типичных подводных камней

### 5.1 Работа с низкокачественными изображениями

Точность OCR падает, когда исходное изображение размыто, шумно или имеет плохое освещение. Быстрое решение — предобработать изображение:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 Запуск в безголовом окружении

Если вы развёртываете в Linux‑контейнере без GUI, убедитесь, что установлен пакет `libgdiplus` (необходимый для `System.Drawing`):

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 Кеширование языкового пакета вручную

Можно один раз скачать языковой файл и указать Aspose путь к нему через API `License`, что устраняет единовременный сетевой запрос. Это удобно для офлайн‑сценариев.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## Полный рабочий пример (всё в одном файле)

Ниже представлен *полный* код программы, который можно скопировать в `Program.cs`. Никаких скрытых частей, никаких внешних скриптов.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Ожидаемый вывод

Если JPG содержит фразу “欢迎光临”, консоль выведет:

```
=== Recognized Text ===
欢迎光临
```

Не стесняйтесь заменять изображение любым другим упрощённым китайским знаком, названием улицы или этикеткой продукта — движок постарается распознать всё как можно лучше.

## Заключение

Мы только что рассмотрели **как использовать OCR** в C# для **извлечения текста из изображения**, особенно решая задачу **распознавания китайских символов** в **JPG**. Благодаря загрузке языков «на лету» от Aspose.OCR вы можете держать развертывание лёгким, одновременно поддерживая **OCR Chinese Simplified** из коробки.

Что дальше? Попробуйте следующие идеи:

- **Пакетная обработка**: пройдитесь по папке с изображениями и запишите каждый результат в CSV.
- **Комбинация с API перевода**: передайте распознанную строку в Azure Translator для создания многоязычных приложений в реальном времени.
- **Исследуйте другие языки**: замените `OcrLanguage.ChineseSimplified` на `Japanese` или `Arabic` и посмотрите, как тот же код адаптируется.

Есть вопросы о настройке производительности, лицензировании или интеграции OCR в веб‑службу? Оставляйте комментарий ниже — happy coding! 

---

![Скриншот вывода консоли, показывающий, как использовать OCR в C# для распознавания китайского текста из JPG‑изображения](ocr-chinese-demo.png "вывод консоли OCR")

## Похожие руководства

- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Распознавание текста на изображении с Aspose OCR для нескольких языков](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Как извлечь текст из изображения, задав прямоугольники в OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}