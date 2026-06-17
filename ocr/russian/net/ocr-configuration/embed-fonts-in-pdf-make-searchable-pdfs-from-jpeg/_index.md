---
category: general
date: 2026-03-05
description: Встраивание шрифтов в PDF при конвертации JPEG в поисковый PDF с помощью
  Aspose OCR. Узнайте, как распознавать текст из JPEG и встраивать шрифты для соответствия
  PDF/A‑2b.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: ru
og_description: Встраивание шрифтов в PDF при преобразовании JPEG в поисковый PDF.
  Это пошаговое руководство показывает, как распознавать текст из JPEG и создавать
  файлы, соответствующие стандарту PDF/A‑2b.
og_title: Встраивание шрифтов в PDF – создание PDF с поиском из JPEG
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: Встраивание шрифтов в PDF — создание поисковых PDF из JPEG
url: /ru/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов в PDF – создание поисковых PDF из JPEG

Когда‑нибудь вам нужно было **встраивать шрифты в PDF** файлы, созданные из отсканированных изображений? Вы не одиноки. Большинство разработчиков сталкиваются с проблемой, когда полученный PDF выглядит нормально на их компьютере, но при открытии где‑то ещё отображается отсутствие текста, потому что шрифты не были встроены.  

Хорошие новости? С помощью Aspose OCR вы можете **распознавать текст из JPEG**, встроить необходимые шрифты и вывести полностью поисковый документ PDF/A‑2b всего за несколько строк кода на C#. В этом руководстве мы пройдем каждый шаг — почему каждый параметр важен, как избежать распространенных ошибок и как должен выглядеть конечный PDF.

К концу этого руководства вы сможете **преобразовать изображение в поисковый PDF**, правильно встраивать шрифты и понять, как **выполнять OCR на изображениях** программно.

---

## Что понадобится

- **Aspose.OCR for .NET** (latest version, e.g., 23.10) – библиотека, которая делает всю тяжелую работу.
- Действительный **файл лицензии Aspose OCR** (`Aspose.OCR.lic`). Бесплатная пробная версия работает, но лицензированная версия удаляет водяные знаки оценки.
- JPEG‑изображение (`input.jpg`), содержащее печатный или набранный текст.
- Среда разработки .NET (Visual Studio, Rider или VS Code с расширением C#).

Дополнительные пакеты NuGet не требуются; движок OCR уже включает утилиты генерации PDF.

## Шаг 1: Настройка OCR‑движка и применение лицензии *(Встраивание шрифтов в PDF)*

Прежде чем запустить распознавание, необходимо создать экземпляр `OcrEngine` и указать, какую лицензию использовать. Пропуск шага с лицензией приведет к работе движка в режиме оценки, который добавляет наложение «Powered by Aspose» на каждую страницу.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Почему это важно:** Лицензия не только удаляет водяные знаки, но и открывает параметры соответствия PDF/A, которые нам понадобятся позже для встраивания шрифтов.

## Шаг 2: Загрузка JPEG‑изображения, которое нужно обработать *(Распознавание текста из JPEG)*

OCR‑движок работает со свойством `Image`, которое принимает `ImageStream`. Укажите путь к JPEG, который вы хотите преобразовать.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**Подсказка:** Если ваше изображение находится в потоке (например, загружено через API), вы можете использовать `ImageStream.FromStream(yourStream)` вместо `FromFile`.

## Шаг 3: Настройка параметров сохранения PDF для поискового PDF

Это ядро требования «встраивание шрифтов в PDF». Мы будем использовать `PdfSaveOptions` для:

1. Выбора **PDF/A‑2b** (широко принятый архивный стандарт).
2. **Встраивания всех используемых шрифтов**, чтобы PDF отображался одинаково везде.
3. Применения **без потерь сжатия Flate** для разумного размера файла.
4. Сохранения оригинального JPEG как фонового слоя, что сохраняет визуальную точность.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**Почему эти настройки?**  
- **PdfAStandard.PdfA2b** гарантирует долгосрочное сохранение и принудительно встраивает шрифты.  
- **EmbedFonts = true** — явный флаг, удовлетворяющий основной цели по ключевому слову.  
- **Compression.Flate** уменьшает размер без потери качества.  
- **RenderOriginalImage** сохраняет визуальный вид отсканированной страницы, а скрытый слой OCR обеспечивает поисковый текст.

## Шаг 4: Запуск OCR‑распознавания изображения *(Выполнение OCR на изображении)*

Когда всё готово, запустите распознавание. Движок проанализирует JPEG, извлечёт символы и внутренне создаст текстовый слой.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**Распространённый вопрос:** *Нужно ли указывать язык или словарь?*  
Если ваш документ не на английском, установите `ocrEngine.Language = OcrLanguage.French;` (или любой поддерживаемый язык) перед вызовом `Recognize()`. По умолчанию — английский.

## Шаг 5: Сохранение результата как поискового PDF с встроенными шрифтами

Наконец, запишите результат на диск. Метод `Save` принимает путь назначения и `PdfSaveOptions`, которые мы определили ранее.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

Когда вы откроете `output.pdf` в Adobe Acrobat или любом PDF‑просмотрщике, вы сможете:

- **Искать** любое слово, которое было в оригинальном JPEG.
- Не видеть **предупреждений о недостающих шрифтах** (благодаря `EmbedFonts = true`).
- Проверить, что файл соответствует **PDF/A‑2b** (File → Properties → PDF/A).

## Полный рабочий пример

Ниже представлен полный, готовый к запуску пример программы. Скопируйте и вставьте его в новый проект Console App, скорректируйте пути к файлам и нажмите **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**Ожидаемый вывод:**  
Консоль выводит сообщение об успехе, и `output.pdf` появляется в целевой папке. Открытие PDF и использование поисковой строки просмотрщика должно находить любое слово, присутствующее в `input.jpg`.

## Часто задаваемые вопросы и особые случаи

### 1. «Что если мой JPEG — многостраничный TIFF?»

Aspose OCR обрабатывает каждую страницу отдельно. Преобразуйте TIFF в серию JPEG (или используйте `ImageStream.FromFile` для каждой страницы) и выполните цикл OCR, добавляя каждый результат в один и тот же PDF, переиспользуя тот же экземпляр `OcrEngine`.

### 2. «Могу ли я контролировать DPI или предобработку изображения?»

Да. Перед вызовом `Recognize()` вы можете изменить разрешение изображения:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

Более высокое DPI часто дает лучшую точность распознавания, особенно для мелкого шрифта.

### 3. «Мой PDF всё ещё показывает недостающие шрифты в Adobe Reader — в чём проблема?»

Убедитесь, что вы выбираете **PDF/A‑2b** и что `EmbedFonts` установлен в `true`. Если вы вручную изменили `PdfAStandard` на `None`, шаг проверки PDF/A пропускается, и некоторые шрифты могут остаться не встроенными.

### 4. «Является ли слой OCR поисковым на мобильных устройствах?»

Абсолютно. Скрытый текстовый слой является частью спецификации PDF, поэтому любой PDF‑просмотрщик, поддерживающий извлечение текста (включая iOS Files, Android PDF Viewer и т.д.), позволит пользователям искать.

### 5. «Как обрабатывать языки с написанием справа налево, такие как арабский?»

Установите язык перед распознаванием:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

Aspose OCR автоматически переключает направление текста и встраивает соответствующие шрифты, когда `EmbedFonts` равно true.

## Профессиональные советы и распространённые подводные камни

- **Pro tip:** Если ваши исходные изображения — цветные фотографии, рассмотрите возможность преобразования их в градации серого сначала (`ocrEngine.Image.ConvertToGrayscale();`). Это уменьшает размер файла без ухудшения точности OCR.
- **Watch out for:** Использование бесплатной пробной лицензии с **большим** изображением может привести к усечению OCR‑текста движком. Перейдите на полную лицензию для производственных нагрузок.
- **Performance tip:** Переиспользование того же экземпляра `OcrEngine` для нескольких изображений избавляет от накладных расходов повторной загрузки OCR‑DLL.
- **Security note:** Файлы PDF/A‑2b по умолчанию **только для чтения**, что помогает предотвратить случайную инъекцию скриптов — приятный бонус для сред с высокими требованиями к соответствию.

## Заключение

Мы рассмотрели весь конвейер для **встраивания шрифтов в PDF** при **распознавании текста из JPEG** и создания **поискового PDF**, соответствующего стандарту PDF/A‑2b. Процесс сводится к:

1. Инициализировать `OcrEngine` и применить вашу лицензию.  
2. Загрузить JPEG‑изображение.  
3. Настроить `PdfSaveOptions` (встраивание шрифтов, PDF/A‑2b, сжатие).  
4. Запустить `Recognize()`.  
5. Сохранить с указанными параметрами.

Теперь вы можете интегрировать этот процесс в веб‑сервисы, настольные утилиты или пакетные задания, которым необходимо **преобразовать изображение в поисковый PDF** в реальном времени. Далее вы можете изучить **как создавать поисковые PDF** из многостраничных PDF или PDF, генерируемых

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}