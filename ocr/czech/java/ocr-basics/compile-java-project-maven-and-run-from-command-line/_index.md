---
category: general
date: 2026-10-18
description: Zkompilujte Maven projekt v Javě a spusťte jej z příkazové řádky pomocí
  příkazů Maven clean, compile a exec. Naučte se, jak efektivně sestavit a spustit
  Java aplikaci.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: cs
lastmod: 2026-10-18
og_description: Zkompilujte Maven projekt v Javě a spusťte jej z příkazové řádky pomocí
  podrobného návodu krok za krokem. Ovládněte příkazy maven clean, compile a run pro
  sestavení a spuštění Java aplikace.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Kompilace Java projektu Maven – spuštění z příkazové řádky
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
title: Kompilovat Java projekt Maven a spustit z příkazové řádky
url: /cs/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kompilace Java projektu Maven a spuštění z příkazové řádky

Pokud potřebujete **compile java project maven** a spustit výslednou třídu přímo z terminálu, tento návod vám přesně ukáže, jak na to. Na konci tutoriálu budete schopni vyčistit staré artefakty, zkompilovat zdrojový kód a **execute java class command line** pomocí jediného řetězce Maven příkazů.

Tutoriál pokrývá vše, co potřebujete vědět k **build and run java app** s Maven, včetně požadovaných pluginů, běžných úskalí a tipů pro shelly na Windows i Unixu. Není potřeba žádná externí dokumentace – stačí postupovat podle níže uvedených kroků.

## Požadavky

* Java Development Kit (JDK) 8 nebo novější nainstalovaný a nastavený `JAVA_HOME`.
* Apache Maven 3.6+ dostupný ve vašem `PATH`.
* Maven projekt, který obsahuje `pom.xml` a Java třídu s metodou `public static void main(String[] args)` (pro tento příklad je třída `com.aspose.ocr.examples.SimpleOcrDemo`).

## Kompilace java projektu maven

Prvním krokem je odstranit všechny dříve zkompilované třídy a další artefakty sestavení. Spuštěním `mvn clean` zajistíte čistý start a zabráníte, aby zastaralý bytecode způsoboval chyby za běhu.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Proč čistit?* Maven ukládá zkompilované třídy do `target/`. Pokud vynecháte fázi clean, mohou v adresáři zůstat staré soubory `.class`, které skryjí problémy s kompilací, zejména po refaktorování názvů balíčků.

## Spuštění java třídy z příkazové řádky

Po vyčištění zkompilujte zdrojové soubory. Fáze `compile` v Maven přeloží všechny zdroje z `src/main/java` do bytecode a umístí výsledek do `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Nyní máte výstup **maven compile source code** připravený k provedení. Další příkaz spustí zkompilovanou třídu bez potřeby samostatného JAR souboru.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Cíl `exec:java` pluginu **maven clean compile run** spustí zadanou třídu přímo z adresáře s kompilovaným výstupem. To je nejrychlejší způsob, jak **execute java class command line** během vývoje.

### Očekávaný výstup

Když demo úspěšně proběhne, měli byste vidět něco podobného:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Pokud obdržíte `ClassNotFoundException`, dvakrát zkontrolujte plně kvalifikovaný název třídy a ujistěte se, že se nachází pod `src/main/java`.

## Pracovní postup Maven clean compile run

Spojením těchto tří příkazů získáte kompaktní, opakovatelný workflow:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Proč je řetězit?* Kombinace fází eliminuje potřebu stisknout **Enter** třikrát a snižuje riziko zapomenutí kroku. Maven provede fáze v pořadí, v jakém jsou uvedeny, a zajistí čisté sestavení před spuštěním.

### Tipy pro plynulejší workflow

| Tip | Description |
|-----|-------------|
| **Use a profile** | Definujte Maven profil, který zahrnuje `clean`, `compile` a `exec:java`, abyste mohli spustit `mvn demo` místo psaní celého řetězce. |
| **Add JVM options** | Předejte `-Dexec.args="-Xmx512m"` pro zvýšení velikosti haldy u aplikací náročných na paměť. |
| **Cross‑platform** | Na Windows použijte `mvn.cmd`, zatímco v Unixových shellech použijte `mvn`. Stejný příkaz funguje v obou prostředích. |

## Sestavení a spuštění java aplikace s Maven

Pokud dáváte přednost distribuovatelnému artefaktu, můžete nechat Maven zabalit vaše zkompilované třídy do spustitelného JAR a poté jej spustit standardním příkazem `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Tento přístup je užitečný, když potřebujete **build and run java app** na serveru, kde není Maven nainstalován. Pro rychlý vývoj je však sekvence **maven clean compile run** rychlejší, protože přeskočí krok balení.

## Maven compile source code – běžné úskalí

I když jsou příkazy jednoduché, vývojáři často narazí na následující problémy:

1. **Missing `exec-maven-plugin`**  
   Pokud Maven nemůže najít cíl `exec:java`, přidejte plugin do vašeho `pom.xml`:

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
   Maven kompiluje do `target/classes`. Pokud soubory ručně přesunete nebo změníte výchozí výstupní adresář, cíl `exec:java` nemusí najít vaši třídu. Zachovejte výchozí strukturu, pokud nemáte konkrétní důvod ji měnit.

3. **Using the wrong JDK version**  
   Maven dědí JDK z `JAVA_HOME`. Kompilace se zdrojovým kódem pro JDK 11 a spuštění na JDK 8 způsobí `UnsupportedClassVersionError`. Ověřte verzi JDK pomocí `java -version` a `mvn -v`.

4. **Shell quoting problems**  
   Na Unixu obalte hodnotu `-Dexec.mainClass` jednoduchými uvozovkami, pokud obsahuje speciální znaky:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Na Windows fungují dvojité uvozovky.

Řešením těchto bodů můžete spolehlivě **execute java class command line** v jakémkoli prostředí.

## Pro tip: automatizace pomocí skriptu

Pro týmy, které často přebudovávají demo, vytvořte malý shell nebo batch skript:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Udělejte jej spustitelným (`chmod +x run-demo.sh`) a spusťte `./run-demo.sh`. Tím se eliminují chyby při psaní a zajistí, že každý vývojář používá přesnou sekvenci **maven clean compile run**.

## Závěr

Nyní víte, jak **compile java project maven** a okamžitě **execute java class command line** pomocí Maven cílů clean, compile a exec. Tento krok‑za‑krokem workflow zajišťuje čisté sestavení, eliminuje zastaralé artefakty a umožňuje **build and run java app** jedním příkazem.

Další kroky, které můžete prozkoumat:

* Přidání **shade plugin** pro vytvoření uber‑JAR pro nasazení.  
* Konfigurace Maven profilů pro různé prostředí (dev, test, prod).  
* Integrace unit testů pomocí `mvn test` před krokem kompilace.

Experimentujte s těmito variantami, aby workflow zapadl do vašich projektů, a získáte robustní, opakovatelný build pipeline, který funguje na Windows, macOS i Linuxu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}