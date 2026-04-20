---
category: general
date: 2026-02-16
description: Создайте PDF с возможностью поиска из изображения TIFF с помощью Aspose
  OCR. Узнайте, как преобразовать TIFF в PDF, выполнить OCR изображения в PDF и распознать
  текст с изображения на C#.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- ocr image to pdf
- recognize text from image
- convert scanned image pdf
language: ru
og_description: Быстро создавайте поисковые PDF. В этом руководстве показано, как
  преобразовать TIFF в PDF, выполнить OCR изображения в PDF и распознать текст с изображения
  с помощью Aspose OCR.
og_title: Создать поисковый PDF из TIFF – Руководство Aspose OCR
tags:
- Aspose OCR
- C#
- PDF/A
- Document Processing
title: Создание PDF с поисковым текстом из TIFF – пошаговое руководство Aspose OCR
url: /ru/net/text-recognition/create-searchable-pdf-from-tiff-aspose-ocr-step-by-step-guid/
---

exactly.

Let's construct final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из TIFF – пошаговое руководство Aspose OCR

Когда‑нибудь вам нужно было **create searchable PDF** из отсканированного TIFF, но вы не знали, какая библиотека справится с задачей? Вы не одиноки. Во многих проектах офис‑автоматизации мы получаем кучу файлов TIFF, которые выглядят как картинки, а не как текст. Хорошая новость? С Aspose OCR вы можете **convert tiff to pdf**, выполнить OCR на изображении и получить PDF/A‑2b, полностью поисковый.

В этом руководстве мы пройдем полный, готовый к запуску пример на C#, который показывает, как **create searchable PDF** файлы, почему каждый шаг важен и на какие подводные камни стоит обратить внимание. К концу вы сможете **recognize text from image** файлы, **OCR image to pdf**, и даже **convert scanned image pdf** документы, соответствующие архивным стандартам.

## Что вы узнаете

- Как установить и подключить пакет Aspose OCR NuGet.  
- Точный код, необходимый для **create searchable PDF** из файла TIFF.  
- Почему загрузка правильной языковой модели критична для точного OCR.  
- Советы по работе с большими сканами, многостраничными TIFF и соответствию PDF/A.  
- Где найти полученный файл и как проверить, что текст действительно поисковый.

### Требования

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6.0 или новее (любой современный .NET runtime) | Aspose OCR поставляет бинарники для .NET Standard 2.0+, которые работают везде от .NET Core до .NET Framework. |
| Visual Studio 2022 (или VS Code с расширением C#) | Предоставляет IntelliSense и упрощённое управление NuGet. |
| Действующая лицензия Aspose OCR (или бесплатный оценочный ключ) | Бесплатная пробная версия ограничивает количество страниц; лицензия удаляет водяной знак и включает вывод PDF/A‑2b. |
| Файл TIFF, который нужно обработать (например, `input.tif`) | Это исходное изображение, которое мы превратим в **searchable PDF**. |

> **Pro tip:** Если вы работаете с многостраничными TIFF, Aspose OCR автоматически будет рассматривать каждую страницу как отдельное изображение — дополнительный код не нужен.

---

## Шаг 1: Установите пакет Aspose OCR NuGet

Сначала добавьте библиотеку в ваш проект. Откройте консоль диспетчера пакетов и выполните:

```powershell
Install-Package Aspose.OCR
```

Или, если вам удобнее графический интерфейс, найдите “Aspose.OCR” в **NuGet Package Manager** и нажмите **Install**. Это загрузит все необходимые DLL, включая языковые модели, которые понадобятся позже.

> **Почему этот шаг?** Без пакета класс `OcrEngine` не существует, и вы получите ошибки компиляции. Подход через NuGet гарантирует, что у вас правильная версия (в настоящее время 23.12) и автоматически подтягивает все транзитивные зависимости.

---

## Шаг 2: Инициализируйте OCR Engine

Создание экземпляра движка – первая реальная строка кода, которую вы напишете. Думайте о `OcrEngine` как о мозге, который делает всю тяжёлую работу.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine – this object will manage the entire pipeline
OcrEngine ocrEngine = new OcrEngine();
```

> **Что происходит?** Конструктор инициализирует внутренние буферы и подготавливает движок к загрузке языковой модели. Если пропустить этот шаг, последующие вызовы вроде `LoadLanguage` выбросят `NullReferenceException`.

---

## Шаг 3: Загрузите английскую языковую модель (или любую другую)

Точность OCR зависит от загруженной языковой модели. Для большинства западных документов достаточно английского, но Aspose поддерживает десятки языков.

```csharp
// Load English language data – essential for recognizing Latin characters
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **Почему загружать модель?** Движку нужна статистическая репрезентация форм символов. Без неё вы получите бессмыслицу или пустой результат. Если нужно **recognize text from image** на французском, замените `LanguageModel.English` на `LanguageModel.French`.

---

## Шаг 4: Укажите изображение TIFF и создайте PDF/A‑2b

Теперь указываем движку наш исходный файл. Вспомогательный метод `ImageStream.FromFile` читает TIFF (одностраничный или многостраничный) в память.

```csharp
// Step 4: Assign the TIFF image to the engine
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

// Run OCR and produce a PDF/A‑2b document – this is the searchable PDF we want
PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);
```

> **Что делает этот метод?** `RecognizePdfA` под капотом выполняет три действия:  
> 1️⃣ Выполняет OCR на каждой странице TIFF.  
> 2️⃣ Встраивает распознанный текст как невидимый слой.  
> 3️⃣ Оборачивает всё в контейнер PDF/A‑2b, который является ISO‑стандартом для долгосрочного хранения.  

Если нужен простой PDF без архивных требований, можно вызвать `ocrEngine.RecognizePdf()` вместо этого. Но для большинства корпоративных сценариев PDF/A‑2b – самый надёжный выбор.

---

## Шаг 5: Сохраните поисковый PDF на диск

Наконец, запишите результат в файл. Метод `Save` принимает путь и выполняет всю работу ввода‑вывода.

```csharp
// Save the generated searchable PDF to your output folder
searchablePdf.Save("YOUR_DIRECTORY/output.pdf");
```

Когда вы откроете `output.pdf` в Adobe Reader, сможете ввести слово в поле поиска и мгновенно найти его — хотя исходный файл был лишь картинкой. Это магия рабочих процессов **create searchable PDF**.

---

## Конвертация TIFF в PDF – краткое резюме

Ниже приведена полная, готовая к запуску программа, объединяющая всё вместе. Смело копируйте‑вставляйте её в консольное приложение и нажимайте **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the desired language model (English in this case)
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 3️⃣ Point the engine at the TIFF you want to convert
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

        // 4️⃣ Recognize the image and produce a PDF/A‑2b (searchable PDF)
        PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);

        // 5️⃣ Persist the result to disk
        searchablePdf.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ Searchable PDF created successfully!");
    }
}
```

**Ожидаемый результат:** `output.pdf` появляется в `YOUR_DIRECTORY`. Откройте его, выберите инструмент текста, и вы увидите выделяемый, поисковый текст, наложенный на оригинальное растровое изображение.

---

## OCR изображение в PDF – обработка граничных случаев

### Многостраничные TIFF

Если ваш исходный файл содержит более одной страницы, Aspose OCR автоматически обрабатывает каждую страницу и добавляет соответствующую страницу в PDF. Дополнительный цикл не требуется.

### Большие файлы и управление памятью

Для сканов гигабайтного масштаба рассмотрите возможность включения **streaming mode**:

```csharp
ocrEngine.Image = ImageStream.FromFile("large.tif", useMemoryCache: false);
```

Это заставляет движок читать куски с диска вместо загрузки всего изображения в ОЗУ — отлично подходит для серверных пакетных задач.

### Разные форматы вывода

Иногда нужен не PDF/A‑2b, а простой PDF. Поменяйте вызов:

```csharp
PdfResult plainPdf = ocrEngine.RecognizePdf();
plainPdf.Save("plain.pdf");
```

Или, если нужен только чистый текст (без PDF), используйте:

```csharp
string extractedText = ocrEngine.RecognizeText();
System.IO.File.WriteAllText("text.txt", extractedText);
```

Эти варианты решают задачу **convert scanned image pdf**, когда downstream‑системы принимают только обычные PDF.

---

## Профессиональные советы для надёжного OCR

- **DPI matters:** Сканирование с разрешением 300 DPI и выше даёт лучшие результаты распознавания. Ниже 200 DPI точность заметно падает.  
- **Pre‑processing:** Если TIFF шумный, выполните `ocrEngine.Image = ImageProcessor.Deskew(...).Apply(ocrEngine.Image);` перед распознаванием.  
- **Licensing:** Не забудьте установить лицензию в начале приложения (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`). Без этого в выводе будет водяной знак “Evaluation”.  
- **Batch processing:** Оберните основную логику в `foreach` цикл по каталогу TIFF, чтобы **convert tiff to pdf** пакетно.

---

## Часто задаваемые вопросы

**Q: Работает ли это на Linux?**  
A: Абсолютно. Aspose OCR ориентирован на .NET Standard, поэтому тот же бинарник можно запускать в Windows, Linux или macOS с .NET 6 runtime.

**Q: Что делать, если нужно распознавать язык, отличный от английского?**  
A: Просто замените `LanguageModel.English` на нужный enum, например `LanguageModel.Spanish`. Можно также загрузить несколько языков одновременно для смешанных документов.

**Q: Можно ли встроить пользовательский шрифт в PDF/A?**  
A: Да. Используйте `ocrEngine.Options.PdfOptions.Font = PdfFont.CreateFont("path/to/font.ttf");` перед вызовом `RecognizePdfA`.

## Заключение

Мы рассмотрели всё, что нужно для **create searchable PDF** файлов из изображений TIFF с помощью Aspose OCR. От установки пакета NuGet, загрузки правильной языковой модели, до генерации PDF/A‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}