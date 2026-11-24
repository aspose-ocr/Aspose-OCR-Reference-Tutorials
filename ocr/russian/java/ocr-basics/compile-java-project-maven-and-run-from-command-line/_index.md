---
category: general
date: 2026-10-18
description: Скомпилируйте Maven‑проект Java и запустите его из командной строки,
  используя команды Maven clean, compile и exec. Узнайте, как эффективно собрать и
  запустить Java‑приложение.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: ru
lastmod: 2026-10-18
og_description: Скомпилируйте Java‑проект с Maven и запустите его из командной строки
  по пошаговому руководству. Овладейте командами Maven clean, compile и run для сборки
  и запуска Java‑приложения.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Скомпилировать Java‑проект Maven — запуск из командной строки
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: Скомпилировать Java‑проект Maven и запустить из командной строки
url: /ru/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Скомпилировать java‑проект Maven и запустить из командной строки

Если вам нужно **compile java project maven** и запустить полученный класс напрямую из терминала, это руководство покажет, как это сделать. К концу урока вы сможете очистить старые артефакты, скомпилировать исходный код и **execute java class command line** с помощью одной цепочки команд Maven.

В этом руководстве изложено всё, что нужно знать, чтобы **build and run java app** с Maven, включая необходимые плагины, распространённые подводные камни и советы для оболочек Windows‑ и Unix‑based shells. Внешняя документация не требуется — просто следуйте приведённым ниже шагам.

## Предварительные требования

* Java Development Kit (JDK) 8 или новее, установленный и с установленной переменной `JAVA_HOME`.
* Apache Maven 3.6+ доступный в вашем `PATH`.
* Maven‑проект, содержащий `pom.xml` и Java‑класс с методом `public static void main(String[] args)` (для этого примера класс — `com.aspose.ocr.examples.SimpleOcrDemo`).

## Компиляция java проекта maven

Первый шаг — удалить все ранее скомпилированные классы и другие артефакты сборки. Выполнение `mvn clean` гарантирует чистый старт и предотвращает возникновение ошибок выполнения из‑за устаревшего байт‑кода.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Почему clean?* Maven сохраняет скомпилированные классы в `target/`. Если пропустить фазу clean, старые файлы `.class` могут остаться и скрыть проблемы компиляции, особенно после рефакторинга имён пакетов.

## Выполнение java класса из командной строки

После очистки скомпилируйте исходные файлы. Фаза `compile` Maven переводит все источники из `src/main/java` в байт‑код и помещает результаты в `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Теперь у вас есть вывод **maven compile source code**, готовый к выполнению. Следующая команда запускает скомпилированный класс без необходимости отдельного JAR‑файла.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Цель `exec:java` плагина **maven clean compile run** запускает указанный класс напрямую из каталога скомпилированных файлов. Это самый быстрый способ **execute java class command line** во время разработки.

### Ожидаемый вывод

Когда демонстрация выполнится успешно, вы должны увидеть что‑то похожее на:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Если вы получаете `ClassNotFoundException`, дважды проверьте полностью квалифицированное имя класса и убедитесь, что он находится в `src/main/java`.

## Рабочий процесс Maven clean compile run

Объединение трёх команд в одну дает компактный, повторяемый рабочий процесс:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Почему объединять их?* Сочетание фаз устраняет необходимость нажимать **Enter** три раза и уменьшает риск забыть шаг. Maven выполнит фазы в указанном порядке, гарантируя чистую сборку перед запуском.

### Советы для более гладкого рабочего процесса

| Совет | Описание |
|-----|-------------|
| **Use a profile** | Определите профиль Maven, который объединяет `clean`, `compile` и `exec:java`, чтобы вы могли выполнить `mvn demo` вместо ввода полной цепочки. |
| **Add JVM options** | Передайте `-Dexec.args="-Xmx512m"` для увеличения размера кучи в приложениях, требующих много памяти. |
| **Cross‑platform** | В Windows используйте `mvn.cmd`, а в Unix‑оболочках — `mvn`. Та же команда работает в обеих средах. |

## Сборка и запуск java приложения с Maven

Если вы предпочитаете распространяемый артефакт, можете позволить Maven упаковать скомпилированные классы в исполняемый JAR, а затем запустить его стандартной командой `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Этот подход полезен, когда нужно **build and run java app** на сервере, где Maven не установлен. Однако для быстрой разработки последовательность **maven clean compile run** быстрее, так как пропускает шаг упаковки.

## Maven compile source code — распространённые подводные камни

Несмотря на простоту команд, разработчики часто сталкиваются со следующими проблемами:

1. **Missing `exec-maven-plugin`**  
   Если Maven не может найти цель `exec:java`, добавьте плагин в ваш `pom.xml`:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Incorrect classpath**  
   Maven компилирует в `target/classes`. Если вы вручную перемещаете файлы или меняете каталог вывода по умолчанию, цель `exec:java` может не найти ваш класс. Сохраняйте стандартную структуру, если нет особой причины её менять.

3. **Using the wrong JDK version**  
   Maven наследует JDK из `JAVA_HOME`. Компиляция исходного кода JDK 11 при запуске на JDK 8 вызовет `UnsupportedClassVersionError`. Проверьте версию JDK с помощью `java -version` и `mvn -v`.

4. **Shell quoting problems**  
   В Unix оберните значение `-Dexec.mainClass` в одинарные кавычки, если оно содержит специальные символы:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   В Windows двойные кавычки работают без проблем.

Учитывая эти моменты, вы сможете надёжно **execute java class command line** в любой среде.

## Профессиональный совет: автоматизировать с помощью скрипта

Для команд, которые часто пересобирают демонстрацию, создайте небольшой shell‑ или batch‑скрипт:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Сделайте его исполняемым (`chmod +x run-demo.sh`) и запустите `./run-demo.sh`. Это устраняет ошибки ввода и гарантирует, что каждый разработчик следует точной последовательности **maven clean compile run**.

## Заключение

Теперь вы знаете, как **compile java project maven** и мгновенно **execute java class command line** с помощью целей clean, compile и exec Maven. Пошаговый рабочий процесс гарантирует чистую сборку, устраняет устаревшие артефакты и позволяет **build and run java app** одной командой.

Далее вы можете изучить:

* Добавление **shade plugin** для создания uber‑JAR для развертывания.  
* Настройку профилей Maven для разных окружений (dev, test, prod).  
* Интеграцию модульных тестов с `mvn test` перед шагом компиляции.

Экспериментируйте с этими вариантами, чтобы адаптировать процесс к своим проектам, и у вас будет надёжный, повторяемый конвейер сборки, работающий в Windows, macOS и Linux. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, опираясь на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}