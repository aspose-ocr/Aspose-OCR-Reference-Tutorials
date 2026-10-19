---
date: 2026-05-24
description: Узнайте, как улучшить OCR, задав разрешённые символы с помощью Aspose.OCR
  для .NET, обеспечивая точное распознавание цифр и более быструю обработку. Следуйте
  пошаговому руководству.
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: Как улучшить OCR – задать разрешённые символы с помощью Aspose.OCR для
  .NET
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Как улучшить OCR – задать разрешённые символы с помощью Aspose.OCR для .NET
url: /ru/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как улучшить OCR – установить разрешённые символы с Aspose.OCR для .NET

В этом руководстве вы узнаете **как улучшить результаты OCR** путем **указания разрешённых символов** при использовании Aspose.OCR для .NET. Ограничение OCR‑движка известным белым списком — например, только цифрами — повышает точность, сокращает время обработки и устраняет нежелательные символы. Независимо от того, извлекаете ли вы серийные номера, идентификаторы счетов или показания счётчиков, нижеописанные шаги позволят вам применить эту технику за несколько минут.

## Быстрые ответы
- **Что делает “указание разрешённых символов OCR”?** Ограничивает OCR заранее определённым белым списком, резко повышая точность для целевых наборов данных.  
- **Какие символы я могу разрешить?** Любую комбинацию, которую вам нужно — цифры (`0‑9`), заглавные буквы, пользовательские символы или смесь, например “ABC‑123”.  
- **Зачем ограничивать символы?** Белый список уменьшает количество ложных распознаваний до 70 % и ускоряет обработку в среднем на 30 %.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; для продакшн‑развёртываний требуется коммерческая лицензия.  
- **Какие версии .NET поддерживаются?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Можно ли комбинировать это с языковыми пакетами?** Да — сочетайте белый список с языковым пакетом для обработки многоязычных строк цифр.

## Что такое “указание разрешённых символов OCR”?

**Прямой ответ:** Указание разрешённых символов сообщает Aspose.OCR игнорировать любые визуальные шаблоны, не соответствующие перечисленным вами символам, поэтому движок возвращает только результаты из этого белого списка. Такой целенаправленный подход устраняет шум, повышает коэффициенты уверенности и снижает объём пост‑обработки. Кроме того, он ускоряет процесс распознавания.

## Почему использовать Aspose.OCR для распознавания изображений с цифрами?

**Прямой ответ:** Встроенная функция `AllowedCharacters` в Aspose.OCR позволяет распознавать изображения, содержащие только цифры, одной строкой кода, обеспечивая до 95 % точности при сканировании низкого разрешения без дополнительной логики фильтрации. Библиотека поддерживает более 30 языков, обрабатывает пакеты из 500 изображений менее чем за 2 секунды на страницу и полностью работает офлайн, что делает её идеальной для высокопроизводительных локальных сценариев, таких как считывание показаний счётчиков или извлечение идентификаторов счетов.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

- Базовый опыт разработки на .NET.  
- Библиотека **Aspose.OCR for .NET** — скачайте её с официального сайта **[здесь](https://releases.aspose.com/ocr/net/)**.  
- Visual Studio 2019+ (или любой совместимый .NET IDE).  

## Импорт пространств имён

Следующие пространства имён дают доступ к OCR‑движку и его настройкам:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Как улучшить OCR, указав разрешённые символы?

`AsposeOcr` — основной класс OCR‑движка, предоставляемый библиотекой Aspose.OCR.  
`RecognizeLine` обрабатывает одну строку текста из изображения и возвращает распознанную строку.

**Прямой ответ:** Загрузите изображение, создайте экземпляр `AsposeOcr` с белым списком только цифр (`"0123456789"`), вызовите `RecognizeLine` (или `Recognize` для многострочного распознавания) и прочитайте свойство `Text` из результата. Этот трёхшаговый процесс выдаёт чистые числовые строки менее чем за секунду для типичных изображений 300 dpi.

### Шаг 1: Установите путь к папке с изображениями

Определите папку, содержащую образцы изображений, которые вы хотите обработать.

```csharp
string dataDir = "Your Document Directory";
```

### Шаг 2: Инициализируйте Aspose.OCR с белым списком только цифр

`AllowedCharacters` — свойство, задающее белый список символов, которые OCR‑движок может распознавать.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Шаг 3: Распознайте одну строку, содержащую цифры

Метод `RecognizeLine` сканирует изображение и возвращает лучшую строку, соответствующую белому списку.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Шаг 4: Выведите распознанные цифры

Запишите результат в консоль (или журнал), чтобы мгновенно проверить вывод.

```csharp
Console.WriteLine(result);
```

### Шаг 5: Используйте `RecognitionSettings` для более тонкой настройки

`RecognitionSettings` позволяет настраивать параметры OCR, такие как DPI, языковые пакеты и режим обработки.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Шаг 6: Отобразите результат второго случая

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Шаг 7: Подтвердите успешное выполнение

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Следуя этим шагам, вы узнали **как улучшить точность OCR**, ограничив набор символов, и теперь можете надёжно извлекать числовые строки из изображений с помощью Aspose.OCR для .NET.

## Распространённые подводные камни и устранение неполадок

- **Пустой результат:** Убедитесь, что изображение имеет чёткий контраст и минимум фонового шума; рекомендуется минимум 300 dpi.  
- **Неожиданные символы:** Проверьте строку белого списка; лишние пробелы или невидимые символы нарушат фильтр.  
- **Файл не найден:** Убедитесь, что `dataDir` указывает на правильную папку и имя файла соответствует регистрозависимой файловой системе.  
- **Задержка производительности:** Для больших пакетов переиспользуйте один экземпляр `AsposeOcr` вместо создания нового для каждого изображения.

## Часто задаваемые вопросы

### В1: Подходит ли Aspose.OCR для .NET как новичкам, так и опытным разработчикам?
**О:** Абсолютно. API предлагает однострочную настройку для быстрых задач и расширенные `RecognitionSettings` для продвинутых пользователей, охватывая все уровни навыков.

### В2: Могу ли я распознавать символы на нескольких языках, используя белый список разрешённых символов?
**О:** Да. Загрузите соответствующий языковой пакет (например, `ocrEngine.LoadLanguage("en")`) и комбинируйте его с белым списком вроде `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` для обработки многоязычных цифровых строк.

### В3: Как часто обновляется Aspose.OCR для .NET?
**О:** Новые версии выпускаются примерно каждые 6‑8 недель, добавляя поддержку языков, улучшения производительности и исправления ошибок. Последние детали см. в [документации](https://reference.aspose.com/ocr/net/).

### В4: Доступна ли бесплатная пробная версия?
**О:** Да — скачайте **[бесплатную пробную версию](https://releases.aspose.com/)**, чтобы оценить все функции без лицензии. Для продакшн‑использования требуется коммерческая лицензия.

### В5: Где я могу получить помощь от сообщества или официальную поддержку?
**О:** Присоединяйтесь к активному сообществу на **[форуме Aspose.OCR](https://forum.aspose.com/c/ocr/16)**, где можно задавать вопросы, делиться фрагментами кода и получать рекомендации от инженеров Aspose.

---

**Последнее обновление:** 2026-05-24  
**Тестировано с:** Aspose.OCR 24.11 для .NET  
**Автор:** Aspose

## Связанные руководства

- [Настройки распознавания OCR‑изображений — указание игнорируемых символов](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Предобработка изображения OCR с фильтрами Aspose.OCR для .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [Как установить пороговое значение в распознавании OCR‑изображений](/ocr/net/ocr-settings/set-threshold-value/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}