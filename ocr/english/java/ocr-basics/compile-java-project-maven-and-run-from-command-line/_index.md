---
category: general
date: 2026-10-18
description: Compile java project maven and run from command line using Maven clean,
  compile, and exec commands. Learn how to build and run java app efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: en
lastmod: 2026-10-18
og_description: Compile java project maven and run from command line with a step‑by‑step
  guide. Master maven clean compile run to build and run java app.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Compile java project maven – run from command line
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
title: Compile java project maven and run from command line
url: /java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compile java project maven and run from command line

If you need to **compile java project maven** and launch the resulting class directly from a terminal, this guide shows you exactly how. By the end of the tutorial you’ll be able to clean old artifacts, compile the source code, and **execute java class command line** using a single Maven command chain.

The tutorial covers everything you need to know to **build and run java app** with Maven, including required plugins, common pitfalls, and tips for Windows‑ and Unix‑based shells. No external documentation is necessary—just follow the steps below.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit (JDK) 8 or newer installed and `JAVA_HOME` set.
* Apache Maven 3.6+ available on your `PATH`.
* A Maven project that contains a `pom.xml` and a Java class with a `public static void main(String[] args)` method (for this example the class is `com.aspose.ocr.examples.SimpleOcrDemo`).

## Compile java project maven

The first step is to remove any previously compiled classes and other build artifacts. Running `mvn clean` guarantees a fresh start and prevents stale bytecode from causing runtime errors.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Why clean?* Maven stores compiled classes in `target/`. If you skip the clean phase, old `.class` files may remain and hide compilation problems, especially after refactoring package names.

## Execute java class command line

After cleaning, compile the source files. Maven’s `compile` phase translates all `src/main/java` sources into bytecode and places the results in `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

You now have a **maven compile source code** output ready for execution. The next command runs the compiled class without needing a separate JAR.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

The `exec:java` goal of the **maven clean compile run** plugin launches the specified class directly from the compiled output directory. This is the quickest way to **execute java class command line** during development.

### Expected output

When the demo runs successfully you should see something similar to:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

If you receive a `ClassNotFoundException`, double‑check the fully‑qualified class name and ensure it resides under `src/main/java`.

## Maven clean compile run workflow

Putting the three commands together yields a compact, repeatable workflow:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Why chain them?* Combining the phases eliminates the need to press **Enter** three times and reduces the chance of forgetting a step. Maven will execute the phases in the order they appear, guaranteeing a clean build before execution.

### Tips for a smoother workflow

| Tip | Description |
|-----|-------------|
| **Use a profile** | Define a Maven profile that bundles `clean`, `compile`, and `exec:java` so you can run `mvn demo` instead of typing the full chain. |
| **Add JVM options** | Pass `-Dexec.args="-Xmx512m"` to increase heap size for memory‑intensive apps. |
| **Cross‑platform** | On Windows use `mvn.cmd` while Unix shells use `mvn`. The same command works in both environments. |

## Build and run java app with Maven

If you prefer a distributable artifact, you can let Maven package your compiled classes into a runnable JAR and then execute it with the standard `java -jar` command:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

This approach is useful when you need to **build and run java app** on a server where Maven isn’t installed. However, for rapid development the **maven clean compile run** sequence is faster because it skips the packaging step.

## Maven compile source code – common pitfalls

Even though the commands are straightforward, developers often encounter the following issues:

1. **Missing `exec-maven-plugin`**  
   If Maven cannot find the `exec:java` goal, add the plugin to your `pom.xml`:

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
   Maven compiles to `target/classes`. If you manually move files or change the default output directory, the `exec:java` goal may not locate your class. Keep the default layout unless you have a specific reason to change it.

3. **Using the wrong JDK version**  
   Maven inherits the JDK from `JAVA_HOME`. Compiling with JDK 11 source code while running on JDK 8 will cause `UnsupportedClassVersionError`. Verify the JDK version with `java -version` and `mvn -v`.

4. **Shell quoting problems**  
   On Unix, wrap the `-Dexec.mainClass` value in single quotes if it contains special characters:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   On Windows, double quotes work fine.

By addressing these points you can reliably **execute java class command line** in any environment.

## Pro tip: automate with a script

For teams that frequently rebuild the demo, create a small shell or batch script:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Make it executable (`chmod +x run-demo.sh`) and run `./run-demo.sh`. This eliminates typing errors and ensures every developer follows the exact **maven clean compile run** sequence.

## Conclusion

You now know how to **compile java project maven** and instantly **execute java class command line** using Maven’s clean, compile, and exec goals. The step‑by‑step workflow guarantees a fresh build, eliminates stale artifacts, and lets you **build and run java app** with a single command line.  

Next, you might explore:

* Adding the **shade plugin** to produce an uber‑JAR for deployment.  
* Configuring Maven profiles for different environments (dev, test, prod).  
* Integrating unit tests with `mvn test` before the compile step.

Experiment with these variations to fit the workflow into your own projects, and you’ll have a robust, repeatable build pipeline that works across Windows, macOS, and Linux. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}