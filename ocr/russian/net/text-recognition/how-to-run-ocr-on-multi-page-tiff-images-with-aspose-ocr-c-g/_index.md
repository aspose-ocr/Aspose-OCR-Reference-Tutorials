---
category: general
date: 2026-02-11
description: Узнайте, как выполнять OCR для многостраничного TIFF в C# с помощью Aspose
  OCR. Преобразуйте TIFF в текст, извлекайте текст из TIFF и быстро распознавайте
  текст с изображения.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: ru
og_description: Как выполнить OCR на многостраничном TIFF с помощью Aspose OCR в C#.
  Пошаговое руководство по преобразованию TIFF в текст, извлечению текста из TIFF
  и распознаванию текста на изображении.
og_title: Как выполнить OCR на многостраничных TIFF‑изображениях – Полный учебник
  C#
tags:
- OCR
- C#
- Aspose
- TIFF
title: Как выполнить OCR для многостраничных TIFF‑изображений с помощью Aspose OCR
  – руководство на C#
url: /ru/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

Conclusion" translate.

Paragraph translate, keep **how to run OCR**, **extract text from TIFF**, **convert TIFF to text**, **recognize text from image** unchanged.

Next paragraph about next step, combine... translate, keep **perform OCR on image** maybe unchanged.

Next final paragraph about comments, GitHub. Translate.

Then closing shortcodes.

Make sure to keep all shortcodes exactly.

Now produce final output.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR на многостраничных TIFF‑изображениях с Aspose OCR

Когда‑нибудь задавались вопросом **how to run OCR** на отсканированном TIFF, содержащем несколько страниц? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда им нужно извлечь поисковый текст из старых документов. Хорошая новость? С Aspose OCR вы можете распознавать текст из файлов‑изображений всего несколькими строками кода C#, и получите простой конкатенированный текст, готовый для индексации или дальнейшей обработки.

В этом руководстве мы пройдем весь процесс: от установки пакета Aspose OCR, загрузки многостраничного TIFF, до преобразования TIFF в текст и окончательного отображения извлечённого содержимого. К концу вы сможете **extract text from TIFF** файлы, **recognize text from image** источники и даже автоматизировать процесс для десятков файлов в пакетной задаче. Никакой магии, только чёткие практические шаги.

## Что вы узнаете

- Как настроить движок Aspose OCR для распознавания английского языка.  
- Точный код, необходимый для **convert TIFF to text** с использованием класса `OcrEngine`.  
- Советы по работе с многостраничными изображениями и обеспечению правильного разделения страниц.  
- Распространённые подводные камни (например, отсутствие нативных зависимостей) и как их избежать.  

**Prerequisites** – вам понадобится .NET 6 или новее, Visual Studio (или любой редактор C#) и подключение к интернету для функции автоматической загрузки ресурсов. Всё, без дополнительных нативных библиотек, с которыми пришлось бы возиться.

---

## Шаг 1 – Установить пакет Aspose OCR NuGet

Прежде чем вы сможете **perform OCR on image** файлы, необходимо добавить библиотеку в ваш проект.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Если вы работаете в Visual Studio, вы также можете щёлкнуть правой кнопкой мыши по проекту → *Manage NuGet Packages* → поискать “Aspose.OCR” и нажать *Install*.

Пакет содержит всё необходимое, а при `AutomaticResourceDownload = true` движок автоматически загрузит языковые пакеты «на лету».

---

## Шаг 2 – Инициализировать OCR‑движок (How to Run OCR)

Теперь, когда пакет установлен, мы создаём и настраиваем экземпляр `OcrEngine`. Это сердце **how to run OCR** в нашем сценарии.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Why this matters:** Установка `Language` сообщает движку, какой набор символов ожидать, а `AutomaticResourceDownload` избавляет от необходимости вручную размещать языковые файлы на сервере. `OutputFormat` в виде `Text` даёт нам простую строку — идеальную для конвейеров **convert TIFF to text**.

---

## Шаг 3 – Загрузить многостраничный TIFF (Recognize Text from Image)

TIFF может содержать множество кадров, каждый из которых представляет отдельную страницу. Класс `System.Drawing.Image` абстрагирует это для нас.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **What if the file isn’t in the same folder?** Просто укажите полный абсолютный путь или используйте `Path.Combine` с `AppContext.BaseDirectory`.  
> **What about memory usage?** Оператор `using` освобождает изображение после обработки, предотвращая утечки — критично при пакетной обработке десятков больших TIFF‑файлов.

Вызов `Recognize` автоматически перебирает каждую страницу TIFF, объединяя результаты с переводами строк. Поэтому при выводе `ocrResult.Text` вы увидите разделение страниц.

---

## Шаг 4 – Полный рабочий пример (Все шаги в одном файле)

Ниже представлено полностью готовое консольное приложение. Скопируйте‑вставьте его в новый .NET‑консольный проект и нажмите **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected output** (сокращённо для наглядности):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Каждая страница выводится на отдельной строке, потому что `OcrOutputFormat.Text` вставляет перевод строки между кадрами. Если нужен иной разделитель, можно пост‑обработать `result.Text` с помощью `String.Replace`.

---

## Шаг 5 – Обработка распространённых граничных случаев

### 5.1 Большие TIFF‑файлы  
При работе с TIFF‑файлами гигабайтного размера загрузка всего файла в память может стать проблемой. Обходной путь — обрабатывать каждый кадр отдельно:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Документы не на английском  
Если нужно **recognize text from image** на испанском или французском, просто измените свойство `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose автоматически загрузит соответствующие языковые ресурсы.

### 5. Сохранение результата  
Часто требуется **convert TIFF to text** и сохранить результат в файл `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Вы также можете разбить вывод по страницам, используя `String.Split(Environment.NewLine)`, и записать каждый фрагмент в отдельный файл.

---

## Pro Tips & Gotchas

- **AutomaticResourceDownload** работает при первом запуске приложения; последующие запуски работают офлайн.  
- Если видите «мусорные» символы, проверьте настройку `Language`; несоответствующие языковые пакеты вызывают неправильное распознавание.  
- Для PDF‑файлов, преобразованных в TIFF, может потребоваться увеличить `ocrEngine.Dpi` (по умолчанию 300) для лучшей точности.  
- Всегда оборачивайте `Image.FromFile` в блок `using`; иначе файл будет заблокирован и его нельзя будет удалить или переместить позже.

---

## Frequently Asked Questions

**Q: Работает ли это с одностраничными TIFF?**  
**A:** Да, конечно. Движок обрабатывает одно‑кадровый TIFF так же, как и много‑кадровый; вы получите одну строку текста.

**Q: Можно ли обрабатывать PNG или JPEG так же?**  
**A:** Да — просто измените расширение файла. Метод `Recognize` принимает любой формат `System.Drawing.Image`.

**Q: Что если мне нужен результат OCR в виде PDF, а не простого текста?**  
**A:** Установите `OutputFormat = OcrOutputFormat.Pdf`, и `ocrResult` будет содержать массив байтов PDF, который можно записать на диск.

---

## Conclusion

Теперь у вас есть полное сквозное решение для **how to run OCR** на многостраничных TIFF‑файлах с помощью Aspose OCR в C#. Настроив движок, загрузив изображение и вызвав `Recognize`, вы сможете **extract text from TIFF**, **convert TIFF to text** и **recognize text from image** всего несколькими строками кода. Не стесняйтесь менять язык, формат вывода или обработку кадр за кадром, чтобы подстроить решение под свои задачи пакетной обработки.

Готовы к следующему шагу? Попробуйте сочетать этот подход с сервисом наблюдения за папкой, чтобы автоматически **perform OCR on image** файлы, как только они появятся в папке‑приёмнике, или интегрировать вывод в поисковый индекс для мгновенного полнотекстового поиска. Возможности безграничны, а представленный код — надёжный фундамент.

Если столкнётесь с проблемами, оставьте комментарий ниже или напишите мне на GitHub. Приятного кодинга и удачной трансформации упорных TIFF‑файлов в поисковый текст!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}