---
category: general
date: 2026-05-28
description: Как выполнять OCR в ASP.NET Core — научитесь загружать изображение, извлекать
  текст из изображения и эффективно обрабатывать загрузку файлов.
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: ru
og_description: Как выполнить OCR в ASP.NET Core. Узнайте пошагово, как загрузить
  изображение, извлечь текст из изображения и обработать загрузку файлов с помощью
  Aspose OCR.
og_title: Как выполнить OCR в ASP.NET Core – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: Как выполнить OCR в ASP.NET Core – Полное руководство
url: /ru/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в ASP.NET Core – Полное руководство

Когда‑нибудь задавались вопросом **как выполнять OCR** внутри современного веб‑API, не теряя волосы? Вы не одиноки. Разработчикам постоянно нужно позволять пользователям загружать изображение — возможно, чек, скан паспорта или рукописную заметку — и получать необработанный текст в формате JSON.  

В этом руководстве мы пройдем полный, готовый к продакшну, решение, которое показывает **как загружать файл**, проверяет его, запускает Aspose OCR и, наконец, **извлекает текст из изображения**. К концу у вас будет готовый к вставке контроллер, который можно добавить в любой проект ASP.NET Core.

## Что вы построите

- Контроллер `OcrController`, принимающий загрузки multipart/form‑data
- Проверка того, что файл действительно существует и не пустой
- Асинхронная обработка OCR с использованием движка Aspose OCR
- Чистый JSON‑ответ, содержащий распознанный текст

Никаких внешних сервисов, никакой скрытой магии — только чистый C# код, который можно запускать локально.

## Предварительные требования (Что нужно перед началом)

| Требование | Почему это важно |
|-------------|----------------|
| .NET 6 SDK or later | ASP.NET Core 6+ предоставляет нам возможности минимального API и поддержку async. |
| Visual Studio 2022 (or VS Code) | IDE упрощает отладку, но любой редактор подойдет. |
| Aspose.OCR NuGet package (`dotnet add package Aspose.OCR`) | Движок, который действительно выполняет OCR. |
| Basic knowledge of ASP.NET Core MVC | Мы будем использовать `ControllerBase` и атрибуты маршрутизации. |

Если у вас есть всё это, отлично — давайте начнём.

## Шаг 1: Настройка проекта и установка Aspose OCR

Откройте терминал и создайте новый проект веб‑API:

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Эта единственная команда подтягивает библиотеку OCR и все её зависимости. Больше ничего настраивать не нужно; Aspose работает сразу из коробки с распространёнными форматами изображений.

## Шаг 2: Добавление OCR‑контроллера (Ядро **как выполнять OCR**)

Создайте новый файл `Controllers/OcrController.cs` и вставьте в него следующий код. Это полный, готовый к запуску пример — без недостающих частей.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### Почему это работает

- **`[FromForm] IFormFile`** сообщает ASP.NET Core привязать часть multipart‑файла к `uploadedFile`. Это классический способ **обработки загрузки файлов** в веб‑API.
- Условие `if` гарантирует, что мы **обрабатываем ошибки загрузки файлов** корректно, возвращая 400 Bad Request, если клиент забыл отправить файл.
- `using var fileStream = uploadedFile.OpenReadStream();` открывает *только‑для‑чтения* поток, что важно для больших файлов — нет необходимости загружать всё изображение в память сразу.
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` передаёт поток напрямую в Aspose OCR, поддерживая лёгкий конвейер.
- `await ocrEngine.RecognizeAsync();` выполняет тяжёлую работу в фоновом потоке, поэтому наш API остаётся отзывчивым. Это суть **как выполнять OCR** асинхронно.
- Наконец, мы оборачиваем результат в JSON‑объект (`{ extractedText }`) — идеально для использования на фронтенде.

## Шаг 3: Настройка ограничения размера запроса (Опционально, но удобно)

Если вы ожидаете сканы высокого разрешения, увеличьте размер запроса по умолчанию. Добавьте следующее в `Program.cs`:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

Теперь API не будет падать при изображении чека размером 10 МБ. Настройте лимит в соответствии с вашими потребностями.

## Шаг 4: Тестирование эндпоинта с помощью cURL или Postman

Вот быстрый cURL‑команд, который можно выполнить в терминале:

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

Вы должны увидеть JSON‑полезную нагрузку, похожую на:

```json
{
  "extractedText": "Sample text that was on the image."
}
```

Если изображение не содержит распознаваемых символов, строка будет пустой — ничего не падает, просто пустой результат. Это хороший граничный случай, который стоит учитывать.

## Шаг 5: Визуальное подтверждение (Опциональное изображение)

Ниже — заглушка‑скриншот, демонстрирующая JSON‑ответ, который вы получите после успешного OCR‑запроса.

![Как выполнить OCR результат – скриншот JSON‑ответа, показывающий извлечённый текст](/images/ocr-result.png)

*Alt text:* **скриншот результата OCR, показывающий извлечённый текст из изображения**

## Распространённые подводные камни и профессиональные советы

| Подводный камень | Решение |
|------------------|----------|
| **Неподдерживаемый формат изображения** (например, TIFF с несколькими страницами) | Сначала конвертируйте в PNG/JPEG или используйте `ImageConverter` от Aspose перед передачей в `OcrEngine`. |
| **Большие файлы вызывают нагрузку на память** | Передавайте файл как поток, как показано; избегайте `IFormFile.CopyToAsync` в `MemoryStream`. |
| **OCR возвращает искажённый текст** | Убедитесь, что изображение имеет высокий контраст и правильно ориентировано. При необходимости предварительно обработайте с помощью `ocrEngine.Preprocess()`. |
| **Несколько одновременных запросов** | Aspose OCR потокобезопасен, но при ограниченной памяти сервера может потребоваться ограничить количество одновременных запросов с помощью семафора. |

## Расширение примера: массовая загрузка и параллельная обработка

Если вам нужно **обрабатывать загрузку файлов** для нескольких изображений одновременно, измените сигнатуру действия, чтобы принимать список:

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

Теперь вы можете **массово загружать OCR изображений** — отлично подходит для сканирования папки чеков за один раз.

## Соображения безопасности

- **Проверяйте расширения файлов** (`.png`, `.jpg`, `.jpeg`) перед обработкой, чтобы избежать вредоносных загрузок.
- **Сканируйте на вирусы**, если ваш API доступен из интернета; интегрируйте сервис, например ClamAV.
- **Ограничивайте частоту запросов** к эндпоинту, чтобы предотвратить атаки отказа в обслуживании.

## Ожидаемый вывод и как проверить

Когда вы обращаетесь к эндпоинту `/ocr/upload` с чётким изображением, содержащим слово «Hello», ответ должен быть:

```json
{
  "extractedText": "Hello"
}
```

Вы можете быстро проверить, открыв инструменты разработчика браузера → вкладка Network, или посмотрев вывод cURL.

## Итоги — Что мы рассмотрели

- Настроили проект ASP.NET Core и добавили пакет NuGet Aspose OCR.
- Реализовали чистый контроллер, демонстрирующий **как выполнять OCR**, **обрабатывать загрузку файлов** и **извлекать текст из изображения**.
- Обсудили обработку ошибок, оптимизацию производительности и лучшие практики безопасности.
- Предоставили готовый к запуску пример кода и вариант массовой загрузки.

## Что дальше?

- **Добавьте поддержку языков**: Aspose OCR можно настроить для разных языков (`ocrEngine.Language = Language.English;`).
- **Интегрируйте с базой данных**: Сохраняйте извлечённый текст вместе с метаданными для последующего поиска.
- **UI на фронтенде**: Создайте простую страницу на React или Blazor, позволяющую пользователям перетаскивать изображения и мгновенно видеть результат OCR.

Не стесняйтесь экспериментировать — заменять OCR‑движок, пробовать разные шаги предобработки изображений или подключать результат к последующей AI‑модели. Возможности безграничны, когда вы знаете **как выполнять OCR** в современном стеке .NET.

Удачной разработки, и пусть ваш текст всегда будет читаемым!

## Похожие руководства

- [Как выполнить OCR изображения – Выполнить OCR на изображении в распознавании изображений](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Как использовать Aspose для распознавания изображения из потока в распознавании изображений OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Как установить пороговое значение в распознавании изображений OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}