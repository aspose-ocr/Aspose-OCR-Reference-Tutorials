---
category: general
date: 2026-05-25
description: Узнайте, как извлекать текст из изображения с помощью минимального API
  ASP.NET Core. Загружайте изображение через POST, считывайте multipart‑данные формы
  и выполняйте OCR изображения.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: ru
og_description: Извлеките текст из изображения с помощью минимального API ASP.NET
  Core. В этом руководстве показано, как загрузить изображение через POST, прочитать
  данные multipart/form-data и выполнить OCR изображения.
og_title: Извлечение текста из изображения в ASP.NET Core – пошагово
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Извлечение текста из изображения в ASP.NET Core Minimal API — Полное руководство
url: /ru/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в ASP.NET Core Minimal API – Полное руководство

Задумывались когда‑нибудь, как **извлечь текст из изображения** без борьбы с тяжёлыми фреймворками? Вы не одиноки. Многие разработчики нуждаются в быстром способе позволить пользователям загрузить картинку и получить обратно символы, будь то сканирование чеков, оцифровка рукописных заметок или наполнение поискового индекса.

В этом руководстве мы создадим крошечный ASP.NET Core Minimal API, который **загружает изображение через POST**, разбирает полезную нагрузку *multipart/form‑data* и затем **выполняет OCR на изображении** с помощью singleton‑объекта `OcrEngine`. К концу вы получите полностью рабочее приложение, которое можно добавить в любой проект .NET 8 и сразу начинать извлекать текст из изображения.

## Что вы построите

- Минимальное веб‑приложение, прослушивающее `/ocr`.
- Точка доступа, принимающая файл изображения, отправленный POST‑запросом `multipart/form-data`.
- Логика, читающая загруженный файл, передающая его OCR‑движку и возвращающая результат в виде простого текста.
- Необязательный фрагмент ускорения на GPU (закомментирован) для тех, у кого есть совместимая видеокарта.

**Требования**  
- .NET 8 SDK (или новее).  
- Базовое знакомство с C# и командной строкой.  
- Библиотека OCR, предоставляющая класс `OcrEngine` (в примере используется гипотетический пакет NuGet).  

Если всё это у вас есть, давайте начнём.

## Шаг 1: Настройка проекта и добавление OCR‑пакета

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Подсказка:** Держите зависимости в актуальном состоянии. Более новые версии часто дают прирост производительности, особенно для ускорения на GPU.

## Шаг 2: Регистрация singleton‑OCR‑движка (основной сервис)

Нам нужен один экземпляр `OcrEngine` для всего приложения — нет необходимости создавать новый движок для каждого запроса. Зарегистрируйте его в контейнере сервисов билдера.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Почему singleton?**  
Создание OCR‑движка может быть дорогим — представьте загрузку весов нейронной сети в память. Переиспользуя один и тот же экземпляр, мы экономим как CPU‑циклы, так и ОЗУ, что приводит к более быстрым откликам для каждого вызова `/ocr`.

## Шаг 3: Сборка приложения

Теперь мы материализуем объект `WebApplication`.

```csharp
var app = builder.Build();
```

Эта строка выглядит почти волшебно, но под капотом она настраивает маршрутизацию, middleware и DI‑контейнер, который мы только что сконфигурировали.

## Шаг 4: Определение POST‑эндпоинта – «Загрузка изображения через POST»

Это сердце руководства: эндпоинт, который **загружает изображение через POST**, читает multipart‑payload и передаёт данные OCR‑движку.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Разбор логики

| Шаг | Что происходит | Почему это важно |
|------|----------------|-------------------|
| **ReadFormAsync** | Разбирает входящий запрос *multipart/form-data*. | Без этого нельзя получить доступ к загруженным файлам. |
| **form.Files["image"]** | Получает файл, у которого имя поля формы `image`. | Обеспечивает предсказуемый контракт для вызывающих. |
| **Content‑type check** | Проверяет, что файл является изображением (например, `image/png`). | Предотвращает сбой OCR‑движка при обработке не‑изображений. |
| **Image.FromStream** | Преобразует поток байтов в объект `System.Drawing.Image`. | OCR‑библиотека ожидает объект `Image`, а не сырые байты. |
| **ocr.Recognize(img)** | Вызывает OCR‑движок для **распознавания текста из изображения**. | Это основной шаг **выполнения OCR на изображении**. |
| **Results.Text** | Возвращает ответ в виде простого текста. | Простой, удобный формат для downstream‑сервисов. |

## Шаг 5: Запуск API

Наконец, запустите веб‑сервер.

```csharp
app.Run();
```

Когда вы выполните `dotnet run`, API будет слушать `http://localhost:5000` (или любой выбранный вами порт). Вы можете протестировать его с помощью `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Ожидаемый вывод:** Консоль выведет распознанные символы, например:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Если изображение размыто или язык не поддерживается, OCR‑движок вернёт пустую строку или сообщение об ошибке — обрабатывайте такие случаи в продакшн‑коде.

## Пограничные случаи и лучшие практики

### 1. Большие файлы

Ограничение тела запроса по умолчанию — 30 МБ. Для более крупных сканов может потребоваться изменить его:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Асинхронный OCR

Некоторые OCR‑библиотеки предоставляют асинхронные методы (`RecognizeAsync`). Если ваша библиотека их поддерживает, замените `ocr.Recognize(img)` на `await ocr.RecognizeAsync(img)` и пометьте лямбда‑выражение как `async`.

### 3. Соображения безопасности

- **Проверяйте размер файла** перед загрузкой в память.
- **Очистите имя файла**, если вы когда‑либо будете записывать его на диск.
- **Ограничивайте частоту запросов** к эндпоинту, чтобы избежать атак отказа в обслуживании.

### 4. Ускорение на GPU

Если раскомментировать строку `engine.GpuDevice = new GpuDevice(0);` и ваше оборудование поддерживает CUDA или DirectML, вы заметите значительное ускорение, особенно на изображениях высокого разрешения.

## Полный рабочий пример

Ниже приведён полный `Program.cs`, который можно скопировать и вставить в новый проект Minimal API.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Сохраните, запустите `dotnet run`, и вы будете готовы **извлекать текст из изображения** по запросу.

## Заключение

Мы прошли через **полное, сквозное решение** для извлечения текста из изображения с использованием ASP.NET Core Minimal API. Начиная со scaffolding проекта, мы **зарегистрировали singleton‑OCR‑движок**, создали эндпоинт, который **загружает изображение через POST**, **чтёт multipart‑форму**, и, наконец, **выполняет OCR на изображении**, возвращая чистый простой текст.

Отсюда вы можете:

- Добавить JSON‑обёртки для более богатых ответов.  
- Подключить базу данных для хранения извлечённого текста.  
- Расширить поддержку нескольких языков (`OcrLanguage.Spanish` и др.).  

Паттерн хорошо масштабируется — просто добавьте тот же эндпоинт в более крупный микросервис или разместите его за API‑gateway.

Есть вопросы по работе с PDF, пакетной обработкой или настройкой GPU? Оставляйте комментарий, и счастливого кодинга!

## Похожие руководства

- [Извлечение текста из изображения с использованием Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Извлечение текста из изображения — оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)
- [Извлечение текста из изображения C# с выбором языка с помощью Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}