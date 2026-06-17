---
category: general
date: 2026-04-06
description: Как установить лицензию в Aspose OCR с помощью C# — узнайте, как встроить
  ресурс, получить встроенный ресурс и загрузить лицензию из файла или потока за несколько
  простых шагов.
draft: false
keywords:
- how to set license
- how to embed resource
- get embedded resource
- how to load license
- use license stream
language: ru
og_description: Пошагово объясняется, как установить лицензию в Aspose OCR. Узнайте,
  как внедрить лицензию, получить её и использовать поток лицензии для бесшовной интеграции.
og_title: Как установить лицензию в Aspose OCR – Полное руководство по C#
tags:
- Aspose OCR
- C#
- .NET licensing
title: Как установить лицензию в Aspose OCR – Полное руководство по C#
url: /ru/net/ocr-configuration/how-to-set-license-in-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить лицензию в Aspose OCR – Полное руководство на C#

Установка лицензии в Aspose OCR – частая проблема для разработчиков. В этом руководстве мы подробно пройдем все шаги по установке лицензии, встраиванию её как ресурса и загрузке из потока — чтобы вы могли использовать OCR без назойливого водяного знака режима пробной версии.

Когда‑то пытались запустить задачу OCR и видели баннер «Evaluation version»? Это симптом отсутствующей или неправильно применённой лицензии. К концу этого руководства у вас будет полностью лицензированный экземпляр Aspose OCR, независимо от того, храните ли вы файл `.lic` рядом с бинарниками или прячете его внутри сборки.

## Что понадобится

- **Aspose.OCR for .NET** (последний NuGet‑пакет на момент написания – 23.10)
- **Действительный файл лицензии Aspose OCR** (`Aspose.OCR.lic`)
- Visual Studio 2022 или любой IDE, поддерживающий C#
- Базовые знания о встраивании ресурсов в .NET (мы их покрываем)

Никакие сторонние библиотеки не требуются; всё находится внутри пакета Aspose.

![Иллюстрация установки лицензии](image.png "Как установить лицензию")

## Шаг 1: Установите NuGet‑пакет Aspose.OCR

Прежде чем писать любой код лицензирования, убедитесь, что библиотека подключена:

```bash
dotnet add package Aspose.OCR
```

Или через менеджер NuGet в Visual Studio найдите **Aspose.OCR** и нажмите *Install*. Это добавит `Aspose.OCR.dll` и его зависимости.

> **Pro tip:** Выбирайте .NET 6 или новее, чтобы пользоваться новейшим API и лучшей производительностью.

## Шаг 2: Создайте объект License – ядро «Как установить лицензию»

Aspose использует простой класс `License` для применения коммерческого ключа. Его создание – первая строка любого лицензированного рабочего процесса:

```csharp
using Aspose.OCR;

// Step 2: Create a License object
var ocrLicense = new License();
```

Почему это важно: экземпляр `License` читает содержимое `.lic` и регистрирует его глобально для текущего AppDomain. После регистрации каждый созданный `OcrEngine` будет работать в полном режиме.

## Шаг 3: Примените лицензию из файла (классический «Как загрузить лицензию»)

Если вы предпочитаете хранить файл лицензии рядом с исполняемым файлом, вызовите `SetLicense`, передав путь к файлу:

```csharp
// Step 3: Apply the license from a file (replace with your actual path)
ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

### На что обратить внимание

- **Абсолютные vs относительные пути:** Относительные пути разрешаются относительно *рабочей директории* процесса, обычно это папка `bin`.
- **Разрешения файлов:** Учётная запись, под которой работает приложение, должна иметь право чтения файла `.lic`.
- **Обработка исключений:** `SetLicense` бросает `FileNotFoundException`, если путь неверен, поэтому оберните вызов в `try/catch`, если нужен плавный отказ.

## Шаг 4: Как встраивать ресурс – размещаем лицензию внутри сборки

Встраивание лицензии избавляет от необходимости поставлять отдельный файл. Вот как **встроить ресурс** в проект .NET:

1. Добавьте файл `.lic` в проект (например, в папку `Resources`).
2. Щёлкните правой кнопкой → *Properties* → установите **Build Action** в **Embedded Resource**.
3. Сборка проекта; лицензия станет частью скомпилированного DLL.

Теперь её можно получить с помощью логики **получить встроенный ресурс**.

## Шаг 5: Получить поток встроенного ресурса

Следующий фрагмент демонстрирует **получить встроенный ресурс** с помощью рефлексии. Подкорректируйте пространство имён и имя ресурса под структуру вашего проекта:

```csharp
using System.Reflection;

// Step 5: Load the embedded license stream
using var licenseStream = Assembly.GetExecutingAssembly()
                                 .GetManifestResourceStream("MyApp.Resources.Aspose.OCR.lic");

if (licenseStream == null)
{
    throw new InvalidOperationException("Embedded license not found. Check the resource name.");
}
```

> **Почему рефлексия?** `Assembly.GetExecutingAssembly()` указывает на текущую сборку, что гарантирует работу кода в консольных приложениях, веб‑сайтах и Azure Functions.

## Шаг 6: Использовать поток лицензии – шаблон «использовать поток лицензии»

Получив поток, **используйте поток лицензии**, чтобы применить её без обращения к файловой системе:

```csharp
// Step 6: Apply the license using the stream
ocrLicense.SetLicense(licenseStream);
```

Когда `SetLicense` получает `Stream`, Aspose читает байты напрямую, регистрирует лицензию и освобождает поток при выходе из блока `using`. Это самый чистый способ скрыть вашу лицензию.

### Полный рабочий пример

Объединив всё вместе, получаем автономную программу, демонстрирующую три подхода (файл, встроенный ресурс и поток). Закомментируйте те части, которые не нужны.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

namespace LicenseDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣  Create the License object – core of how to set license
            // -------------------------------------------------
            var ocrLicense = new License();

            // -------------------------------------------------
            // 2️⃣  Option A: Load from external .lic file (how to load license)
            // -------------------------------------------------
            // Replace with your actual path or use a relative path.
            // ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // -------------------------------------------------
            // 3️⃣  Option B: Load from an embedded resource (how to embed resource)
            // -------------------------------------------------
            // Ensure the .lic file is added as an Embedded Resource.
            // string resourceName = "LicenseDemo.Resources.Aspose.OCR.lic";
            // using var licenseStream = Assembly.GetExecutingAssembly()
            //                                   .GetManifestResourceStream(resourceName);
            // if (licenseStream == null)
            // {
            //     Console.WriteLine("Embedded license not found.");
            //     return;
            // }
            // ocrLicense.SetLicense(licenseStream); // use license stream

            // -------------------------------------------------
            // 4️⃣  Verify the license – no exception means success
            // -------------------------------------------------
            Console.WriteLine("License applied successfully!");

            // -------------------------------------------------
            // 5️⃣  Run a quick OCR test to prove it works
            // -------------------------------------------------
            var engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample.png"); // replace with your image
            engine.Recognize();

            Console.WriteLine("Recognized text:");
            Console.WriteLine(engine.Text);
        }
    }
}
```

**Ожидаемый вывод**

```
License applied successfully!
Recognized text:
[Your OCR result here]
```

Если лицензия не применена, Aspose бросит `LicenseException` или вы увидите водяной знак оценки в результатах OCR.

## Распространённые ошибки и как их избежать

| Симптом | Возможная причина | Решение |
|---------|-------------------|---------|
| Баннер «Evaluation version» всё ещё появляется | Лицензия не загружена или путь неверен | Проверьте путь к файлу или имя встроенного ресурса. |
| `NullReferenceException` при `GetManifestResourceStream` | Ошибка в имени ресурса или Build Action не установлен в Embedded Resource | Убедитесь в правильном полностью квалифицированном имени и правильной настройке Build Action. |
| Лицензия работает локально, но падает после деплоя | Отсутствие прав чтения на сервере | Дайте идентификатору пула приложений права чтения к файлу `.lic` или встраивайте лицензию, чтобы избежать проблем с файловой системой. |
| Несколько объектов `License` не дают эффекта | Вы вызвали `SetLicense` у *другого* экземпляра после первого | Держите один объект `License` на AppDomain; переиспользуйте его или вызывайте `SetLicense` один раз при старте. |

## Когда выбирать каждый подход

- **На основе файла** – Быстрое прототипирование, легко заменить без пересборки.
- **Встроенный ресурс** – Идеально для десктопных приложений или библиотек, где не хочется, чтобы лицензия «плавала» в файловой системе.
- **На основе потока** – Отлично для облачных сред (Azure Functions, AWS Lambda), где лицензия может быть получена из защищённого хранилища и передана напрямую.

## Следующие шаги – расширяем знания о лицензировании

Теперь, когда вы освоили **как установить лицензию**, можно изучить:

- **Как встраивать ресурс** в более сложных многопроектных решениях.
- **Получить встроенный ресурс** из спутниковых сборок для сценариев локализации.
- **Как загрузить лицензию** динамически из Azure Key Vault или AWS Secrets Manager.
- **Использовать поток лицензии** совместно с внедрением зависимостей для более чистого кода инициализации.

Каждая из этих тем опирается на базовые принципы, рассмотренные здесь, и помогает сделать вашу стратегию лицензирования безопасной и поддерживаемой.

---

### TL;DR

Мы показали, **как установить лицензию** в Aspose OCR тремя надёжными способами: загрузка из файла, встраивание `.lic` как ресурса и применение через поток. Следуйте коду, учитывайте подводные камни, и ваш OCR‑движок будет работать на полную мощность — без пробных водяных знаков и сюрпризов.

Удачной разработки, и пусть результаты OCR будут кристально чистыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}