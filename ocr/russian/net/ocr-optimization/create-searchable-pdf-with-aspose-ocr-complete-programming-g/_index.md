---
category: general
date: 2026-05-21
description: Создайте PDF с возможностью поиска, используя Aspose OCR, улучшая точность
  распознавания, и узнайте, как загрузить изображение для OCR в C#. Пошаговое руководство.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: ru
og_description: Создайте PDF с поисковым текстом с помощью Aspose OCR. Узнайте, как
  улучшить точность OCR и загрузить изображение для OCR в одном готовом к запуску
  примере.
og_title: Создайте поисковый PDF с помощью Aspose OCR – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Создание PDF с возможностью поиска с помощью Aspose OCR – Полное руководство
  по программированию
url: /ru/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF с помощью Aspose OCR – Полное руководство по программированию

Когда‑то вам нужно **создать поисковый PDF** из отсканированного изображения, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда впервые берутся за проекты OCR. Хорошая новость в том, что Aspose OCR делает весь процесс — загрузку изображения, улучшение качества картинки для лучших результатов и, наконец, сохранение поискового PDF — довольно простым.

В этом руководстве мы пройдем полный пример от начала до конца, который не только покажет, как **создать поисковый PDF**, но и продемонстрирует, как **повысить точность OCR** и правильный способ **загрузки изображения для OCR**. К концу вы получите готовое консольное приложение C#, которое выводит поисковый PDF с вложенным оригинальным изображением.

## Что вы узнаете

- Настройка Aspose OCR (включая необязательное ускорение GPU)  
- Конфигурация движка для французского (или любого другого языка) с целью **повысить точность OCR**  
- Правильная **загрузка изображения для OCR** с использованием `ImageStream`  
- Создание конвейера фильтров для очистки изображения перед распознаванием  
- Сохранение результата в виде поискового PDF с вложенным исходным изображением  

Никаких внешних зависимостей, кроме Aspose OCR, не требуется, а код работает на .NET 6+ (или .NET Framework 4.6+). Поехали.

---

![Пример поискового PDF, сгенерированного Aspose OCR – пример создания поискового PDF](images/searchable-pdf-sample.png "пример создания поискового PDF")

## Шаг 1: Создание поискового PDF – включение GPU и установка пути к ресурсам  

Если у вас есть совместимый GPU, его включение может значительно ускорить распознавание. Даже если вы пропустите этот шаг, остальной код будет работать нормально.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Почему это важно:** Ускорение GPU уменьшает задержку при обработке больших пакетов, а установка пути к ресурсам гарантирует, что движок сможет работать без подключения к интернету — идеально для CI‑конвейеров или изолированных сред.

> **Совет:** Если вы работаете на безголовом сервере, убедитесь, что драйверы CUDA соответствуют версии, поставляемой с Aspose OCR; несовпадение версий может вызвать тихие сбои.

## Шаг 2: Повышение точности OCR – выбор правильного языка  

Выбор корректной языковой модели — быстрый способ улучшить точность. Здесь мы выбираем французский, но можете заменить `OcrLanguage.French` на любой поддерживаемый язык.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Почему это важно:** Языко‑специфичные словари помогают движку разрешать неоднозначные символы (например, «œ» vs «oe»). Если пропустить этот шаг, движок по умолчанию использует английский, что может резко снизить **повышение точности OCR** для неанглийских текстов.

## Шаг 3: Загрузка изображения для OCR – использование ImageStream  

Теперь мы **загружаем изображение для OCR**. Помощник `ImageStream.FromFile` абстрагирует работу с необработанным битмапом и поддерживает большинство распространённых форматов (JPG, PNG, TIFF).

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Почему это важно:** Такая загрузка гарантирует, что Aspose получит изображение в формате, который он может эффективно обработать. Если попытаться передать сырой `Bitmap` напрямую, могут возникнуть проблемы с управлением памятью при работе с большими файлами.

## Шаг 4: Создание конвейера фильтров изображения для повышения точности  

Чистое изображение — половина успеха. Ниже представленный конвейер исправляет наклон картинки и удаляет фоновой шум — два классических виновника, подрывающих **повышение точности OCR**.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Почему это важно:** Выравнивание (deskew) гарантирует, что строки текста находятся горизонтально, а шумоподавление уменьшает количество ложных «объектов» символов. При особенно плохих сканах можно добавить дополнительные фильтры (например, `ContrastFilter`).

## Шаг 5: Выполнение распознавания OCR  

После предобработки изображения мы наконец позволяем движку выполнить свою магию.

```csharp
ocrEngine.Recognize();
```

Эта единственная строка запускает модель глубокого обучения, лежащую в основе Aspose OCR. Она заполняет `ocrEngine.Text` обычным текстом и также готовит вывод в PDF.

> **Текст выглядит нечитаемым?** Проверьте настройку языка из Шага 2 и рассмотрите возможность добавления `BinarizeFilter` в конвейер.

## Шаг 6: Сохранение результата в виде поискового PDF  

Последний шаг — сохранить **поисковый PDF**, где извлечённый текст находится за оригинальным изображением — именно то, что нужно для юридических документов или архивов.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Почему это важно:** `EmbedOriginalImage = true` сохраняет визуальную точность скана, одновременно позволяя искать текст. Если установить `false`, PDF будет содержать только извлечённый текст, что может быть полезно для лёгких архивов.

### Необязательно: Вывод распознанного текста и JSON  

Если хотите посмотреть «сырой» вывод, эти строки выводят обычный текст и структурированный JSON‑payload.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Ожидаемый вывод:** После запуска программы в консоли появятся французские предложения, а затем объект JSON с координатами ограничивающих рамок, оценками уверенности и метаданными языка.

---

## Полный рабочий пример (готовый к копированию)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Запустите программу, укажите `YOUR_DIRECTORY` на папку, содержащую `input.jpg` и ресурсы Aspose OCR, и вы получите `output.pdf` рядом с ними.

---

## Заключение

Теперь у вас есть надёжный, готовый к продакшену рецепт для **создания поисковых PDF** с помощью Aspose OCR, а также знания о том, как **повысить точность OCR** и правильно **загружать изображение для OCR**. Конвейер — GPU (опционально) → выбор языка → загрузка изображения → цепочка фильтров → распознавание → сохранение PDF — покрывает каждый ключевой шаг, так что вы сможете адаптировать его под другие языки, большие партии или разные форматы вывода.

Что дальше? Попробуйте заменить `PdfSaveOptions` на `DocxSaveOptions`, чтобы генерировать поисковые документы Word, поэкспериментируйте с дополнительными фильтрами, такими как `ContrastFilter`, или интегрируйте этот код в ASP.NET Core API для генерации PDF «на лету». Возможности безграничны, а благодаря этой основе вы готовы к любой задаче, связанной с OCR.

Есть вопросы или возникли трудности? Оставляйте комментарий, и удачной разработки!

## Связанные руководства

- [Как выполнить OCR PDF в .NET с помощью Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Как извлечь таблицу из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Как выполнить OCR текста изображения с указанием языка, используя Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}