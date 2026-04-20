---
category: general
date: 2026-02-11
description: Создайте PDF с возможностью поиска из JPG‑изображения с помощью Aspose
  OCR в C#. Узнайте, как быстро преобразовать изображение в PDF и извлечь текст.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text from jpg
- how to extract text from image
language: ru
og_description: Создайте PDF с возможностью поиска из изображения JPG с помощью Aspose
  OCR в C#. Следуйте этому пошаговому руководству, чтобы преобразовать изображение
  в PDF и извлечь текст.
og_title: Создать PDF с поисковым текстом из изображения с помощью Aspose OCR в C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Создание PDF с возможностью поиска из изображения с помощью Aspose OCR в C#
url: /ru/net/text-recognition/create-searchable-pdf-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из изображения с помощью Aspose OCR на C#

Когда‑нибудь вам нужно было **создать поисковый PDF** из отсканированной фотографии, но вы не знали, с чего начать? Вы не одиноки — разработчики постоянно спрашивают: «Как превратить JPG в PDF, который действительно можно искать?» Хорошая новость в том, что Aspose OCR делает весь процесс простым как раз два пальца. В этом руководстве мы покажем, как **конвертировать изображение в PDF**, извлечь текст и получить поисковый документ, который можно отправить кому угодно.

Мы рассмотрим всё — от установки библиотеки до обработки крайних случаев, таких как большие файлы или отсутствие шрифтов. К концу вы сможете ответить на вопрос *«как извлечь текст из изображения»* без запуска отдельного OCR‑инструмента. Готовы? Погружаемся.

## Что понадобится

- **.NET 6.0** или новее (код также работает на .NET Framework 4.6+).  
- **Действительная лицензия Aspose.OCR** (можно начать с бесплатного временного ключа).  
- Файл изображения (JPG, PNG, BMP…), который вы хотите превратить в поисковый PDF.  
- Visual Studio, VS Code или любой другой редактор C# по вашему выбору.

Никакие другие сторонние пакеты не требуются — Aspose OCR включает всё, включая компоненты генерации PDF.

## Шаг 1: Установите Aspose.OCR через NuGet

Первое, что нужно сделать, — добавить пакет Aspose OCR в ваш проект. Откройте терминал в папке решения и выполните:

```bash
dotnet add package Aspose.OCR
```

> **Совет:** Если вы используете Visual Studio, щёлкните правой кнопкой по проекту → *Manage NuGet Packages* → найдите *Aspose.OCR* и нажмите **Install**. Это загрузит последнюю стабильную версию (в данный момент 23.10), поддерживающую автоматическую загрузку ресурсов сразу же.

Почему это важно: пакет содержит как OCR‑движок, так и PDF‑писатель, поэтому вам не придётся управлять несколькими библиотеками.

## Шаг 2: Настройте OCR‑движок (автоматическая загрузка ресурсов)

Aspose OCR может загружать файлы языковых данных «на лету», что означает, что вам не нужно поставлять огромные *.dat* файлы вместе с приложением. Вот как включить эту возможность:

```csharp
using Aspose.OCR;

// Create the OCR engine and turn on automatic resource download
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true // <-- ensures language packs are fetched when needed
};
```

Если пропустить этот флаг, движок выбросит *ResourceNotFoundException* при первой обработке изображения, требующего языкового пакета, который вы не включили. Включение занимает одну небольшую строку кода, но избавит вас от множества проблем в дальнейшем.

## Шаг 3: Определите пути ввода и вывода

Вам нужно указать движку, где находится исходное изображение и куда сохранять PDF. Абсолютные пути работают везде, но для быстрой проверки подойдут относительные.

```csharp
// Replace these with your actual file locations
string inputImagePath  = @"C:\MyImages\sample.jpg";
string outputPdfPath   = @"C:\MyOutputs\searchable.pdf";
```

> **Внимание:** Если папка для `outputPdfPath` не существует, `RecognizeToPdf` выбросит *DirectoryNotFoundException*. Убедитесь, что создали каталог заранее или используйте `Directory.CreateDirectory(Path.GetDirectoryName(outputPdfPath))`.

## Шаг 4: Распознать текст и создать поисковый PDF

Теперь происходит магия. Метод `RecognizeToPdf` делает две вещи за один вызов: запускает OCR на изображении и встраивает распознанный текст в PDF, который можно искать.

```csharp
// Perform OCR and write a searchable PDF
int recognizedWordCount = ocrEngine.RecognizeToPdf(inputImagePath, outputPdfPath);
```

Метод возвращает количество слов, которые удалось распознать, что удобно для логирования или проверок. Если возвращаемое значение равно нулю, вы, вероятно, передали движку пустое изображение или язык не поддерживается.

### Почему использовать `RecognizeToPdf`, а не отдельные шаги?

Можно вызвать `Recognize`, чтобы получить обычный текст, а затем создать PDF самостоятельно с помощью другой библиотеки. Такой подход работает, но удваивает код и вводит проблемы синхронизации (например, выравнивание текстовых блоков с оригинальным изображением). `RecognizeToPdf` гарантирует визуальную точность оригинального скана, накладывая невидимый слой текста сверху — именно то, что нужно для **поискового PDF**.

## Шаг 5: Проверьте результат

Быстрое сообщение в консоли подтверждает, что всё прошло успешно:

```csharp
Console.WriteLine($"PDF saved to {outputPdfPath}. Words recognized: {recognizedWordCount}");
```

Откройте полученный файл в любом PDF‑просмотрщике (Adobe Reader, Edge, Chrome). Попробуйте ввести слово, которое точно есть на оригинальном изображении — если документ перейдёт к этому месту, вы успешно создали поисковый PDF.

### Крайние случаи и советы

| Situation | What to Do |
|-----------|------------|
| **Huge image ( > 10 MB )** | Увеличьте лимит памяти `OcrEngine`: `ocrEngine.MemoryLimit = 1024; // MB` |
| **Multiple pages** | Передайте список путей к изображениям в перегрузку `RecognizeToPdf`, принимающую `IEnumerable<string>` |
| **Non‑Latin script** | Установите `ocrEngine.Language = OcrLanguage.Arabic;` (или любой поддерживаемый язык) перед вызовом `RecognizeToPdf` |
| **License not set** | Бесплатная пробная версия добавляет водяной знак. Зарегистрируйте лицензию с помощью `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

## Полный рабочий пример

Ниже приведено автономное консольное приложение, которое вы можете скопировать в `Program.cs`. Оно включает все обсуждённые части, а также обработку ошибок.

```csharp
using System;
using System.IO;
using Aspose.OCR;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Optional: Load your Aspose OCR license (remove for trial)
            // var license = new License();
            // license.SetLicense(@"C:\Path\To\Aspose.OCR.lic");

            // 2️⃣ Initialize the OCR engine with automatic resource download
            var ocrEngine = new OcrEngine
            {
                AutomaticResourceDownload = true,
                // Uncomment to boost memory for huge images
                // MemoryLimit = 1024 // in MB
            };

            // 3️⃣ Define file locations (adjust to your environment)
            string inputImagePath = @"YOUR_DIRECTORY/input.jpg";
            string outputPdfPath  = @"YOUR_DIRECTORY/output.pdf";

            // Ensure output directory exists
            Directory.CreateDirectory(Path.GetDirectoryName(outputPdfPath)!);

            try
            {
                // 4️⃣ Perform OCR and create searchable PDF
                int wordCount = ocrEngine.RecognizeToPdf(inputImagePath, outputPdfPath);

                // 5️⃣ Inform the user
                Console.WriteLine($"✅ PDF saved to {outputPdfPath}. Words recognized: {wordCount}");
            }
            catch (Exception ex)
            {
                // Friendly error output
                Console.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

Сохраните, соберите и запустите (`dotnet run`). Если всё настроено правильно, вы увидите сообщение ✅ и новый поисковый PDF в `YOUR_DIRECTORY`.

![Пример создания поискового PDF](/images/searchable-pdf.png "Создание поискового PDF из изображения с помощью Aspose OCR")

## Часто задаваемые вопросы

**Q: Работает ли это также с файлами PNG или BMP?**  
A: Абсолютно. `RecognizeToPdf` принимает любой растровый формат, поддерживаемый Aspose.OCR. Просто укажите `inputImagePath` на нужный файл.

**Q: Насколько точен OCR?**  
A: Точность зависит от качества изображения, языка и шрифта. Для лучших результатов используйте разрешение не менее 300 dpi и хороший контраст. Вы также можете настроить `ocrEngine.Settings` (например, `ocrEngine.Settings.DetectSkew = true`) для улучшения результатов.

**Q: Могу ли я добавить собственный водяной знак после создания PDF?**  
A: Да. После завершения `RecognizeToPdf` вы можете открыть PDF с помощью Aspose.PDF и добавить слой водяного знака. Это отдельный урок, но процесс прост.

## Заключение

Мы прошли весь процесс **создания поискового PDF** из изображения с помощью Aspose OCR на C#. От установки пакета NuGet до обработки больших файлов и многоязычных сценариев, теперь у вас есть надёжное, готовое к продакшену решение, которое можно внедрить в любой .NET‑проект.

Если вам нужно **конвертировать изображение в PDF** пакетно, просто передайте список путей к файлам в перегрузку `RecognizeToPdf(IEnumerable<string>, string)`. Хотите **ocr image to pdf** «на лету» в веб‑API? Оберните тот же код в контроллер ASP.NET и передавайте PDF клиенту в потоковом виде. А когда понадобится **recognize text from jpg** для последующего анализа, просто вызовите `ocrEngine.Recognize(inputImagePath)` перед генерацией PDF.

Не стесняйтесь экспериментировать — менять язык, настраивать лимиты памяти или объединять несколько изображений в один документ. Возможностей бесконечно много, а Aspose OCR скрывает всю тяжёлую работу за чистым, легко читаемым кодом.

Есть дополнительные вопросы по извлечению текста или конвертации форматов? Оставляйте комментарий, и удачной разработки!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}