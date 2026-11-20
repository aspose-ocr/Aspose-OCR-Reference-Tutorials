---
category: general
date: 2026-05-31
description: Reconheça texto de imagens rapidamente usando Aspose OCR Java. Aprenda
  como extrair texto de arquivos PNG e definir o idioma do OCR para obter resultados
  ideais.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: pt
og_description: reconheça texto de imagens de forma eficiente com Aspose OCR Java.
  Este tutorial mostra como extrair texto de arquivos png e definir o idioma OCR para
  processamento em lote.
og_title: reconhecer texto de imagens – Aspose OCR Java Paralelo em lote
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Reconheça texto de imagens com Aspose OCR – Guia de Lote Paralelo em Java
url: /pt/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagens – Tutorial de Lote Paralelo Aspose OCR Java

Já se perguntou como **reconhecer texto de imagens** de forma que não trave sua UI? Talvez você tenha uma pasta cheia de digitalizações, capturas de tela ou até mesmo uma mistura de arquivos PNG e JPEG, e precise do texto o mais rápido possível. A boa notícia? Com o Aspose OCR para Java você pode criar um lote multithread que **extrai texto de png** (e outros formatos) enquanto toma seu café.

Neste guia vamos percorrer um exemplo completo, pronto‑para‑executar, que mostra como **definir o idioma do OCR**, disparar quatro workers paralelos e imprimir os resultados. Ao final, você terá um modelo sólido que pode ser inserido em qualquer projeto Java — sem frescuras, apenas o código que você precisa.

## O que você aprenderá

- Como aplicar uma licença do Aspose OCR para não ser limitado pelas restrições de avaliação.  
- Os passos exatos para **reconhecer texto de imagens** em paralelo, aumentando o rendimento em máquinas com múltiplos núcleos.  
- Por que e como **definir o idioma do OCR** (francês no demo) para melhorar a precisão.  
- Uma forma prática de **extrair texto de png** arquivos, mas a mesma lógica funciona para JPG, TIFF, BMP, etc.  

**Pré‑requisitos** – você precisará do Java 8 ou superior, Maven ou Gradle para obter a biblioteca Aspose OCR, e um arquivo de licença válido do Aspose OCR (`Aspose.OCR.Java.lic`). Nenhum truque especial de IDE é necessário; qualquer editor que compile Java serve.

---

## Etapa 1: Adicionar a dependência do Aspose OCR

Primeiro, certifique‑se de que o JAR do Aspose OCR está no seu classpath. Se estiver usando Maven, adicione:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Para Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Dica profissional:** Fique de olho nas notas de versão do Aspose; elas costumam adicionar pacotes de idiomas ou ajustes de desempenho que podem reduzir segundos nas execuções de lote.

## Etapa 2: Aplicar a licença do Aspose OCR

Sem uma licença a biblioteca roda em modo demo e inserirá marcas d'água na saída. Carregue seu arquivo de licença uma única vez, de preferência na inicialização da aplicação.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Chamar `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` garante que toda chamada subsequente de **reconhecer texto de imagens** seja executada sem restrições.

## Etapa 3: Preparar a lista de imagens

Você pode alimentar o processador de lote com qualquer coleção de caminhos de arquivo. Abaixo demonstramos **extrair texto de png** junto com arquivos JPEG e TIFF — basta substituir os caminhos pelo seu diretório.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **Por que uma List?** O `OcrBatchProcessor` espera um `List<String>` para poder dividir o trabalho entre as threads automaticamente.

## Etapa 4: Configurar e executar o Processador de Lote Paralelo

Agora vem o coração do tutorial: criar um `OcrBatchProcessor`, definir quantas threads serão iniciadas e **definir o idioma do OCR** para francês (mude para `OcrLanguage.ENGLISH` ou qualquer idioma suportado conforme necessário).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Como funciona

- **Contagem de Threads** – O processador cria um pool de threads do tamanho que você especificar. Em um laptop quad‑core, `4` costuma ser um ponto ideal; aumente para servidores com mais núcleos.  
- **Configuração de Idioma** – Ao chamar `setLanguage(OcrLanguage.FRENCH)`, instruímos o motor OCR a favorecer seu dicionário para caracteres franceses, o que melhora drasticamente a precisão em documentos não‑inglês.  
- **Reconhecimento em Lote** – O método `recognize` itera internamente sobre a lista fornecida, distribui o trabalho e devolve um `List<OcrResult>` preservando a ordem original. Essa é a maneira mais direta de **reconhecer texto de imagens** sem precisar escrever seu próprio código de gerenciamento de threads.

## Etapa 5: Verificar a saída

Ao executar o programa, você deverá ver algo como:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

Se o arquivo francês (`doc1.png`) contiver texto em francês, a etapa **definir o idioma do OCR** terá ajudado a capturar corretamente os caracteres acentuados. Para arquivos PNG, isso demonstra uma forma limpa de **extrair texto de png** enquanto trata outros formatos no mesmo lote.

---

## Tratamento de Casos de Borda Comuns

### 1️⃣ Imagens ausentes ou corrompidas

Se um caminho de imagem for inválido, o `OcrBatchProcessor` lança uma `IOException`. Envolva a chamada em um bloco try‑catch, registre o arquivo problemático e continue com o restante do lote.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ Múltiplos idiomas em um único lote

Quando você tem documentos em vários idiomas, pode:

- Executar lotes separados, cada um com seu próprio `setLanguage`.  
- Ou deixar o idioma não definido (`OcrLanguage.AUTO_DETECT`) e deixar o Aspose adivinhar, embora a precisão possa cair.

### 3️⃣ Restrições de memória

Processar imagens muito grandes (ex.: >10 MB) pode inflar o uso de heap. Redimensione as imagens previamente ou aumente a flag `-Xmx` da JVM se encontrar `OutOfMemoryError`.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ Personalizando as configurações do OCR

Além do idioma, você pode ajustar velocidade vs. precisão:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

Escolher `ACCURATE` é mais lento, mas produz resultados melhores para digitalizações ruidosas.

---

## Exemplo Completo (Todos os Arquivos)

Abaixo está o conjunto completo de arquivos‑fonte que você precisa. Copie‑os para um projeto Maven, ajuste o caminho da licença e o diretório de imagens, então execute `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Execute-o, e você verá o texto extraído de cada arquivo impresso no console — exatamente o que você precisa ao construir arquivos pesquisáveis, automação de entrada de dados ou ferramentas de acessibilidade.

---

## Conclusão

Acabamos de cobrir um padrão completo e pronto para produção para **reconhecer texto de imagens** usando o Aspose OCR para Java. Ao configurar o processador de lote, você pode **extrair texto de png** (e outros formatos) em paralelo, e a capacidade de **definir o idioma do OCR** garante a maior precisão possível para cargas de trabalho multilíngues.

Próximos passos? Experimente trocar o idioma para `OcrLanguage.SPANISH` ou teste `OcrRecognitionMode.ACCURATE` em digitalizações mais difíceis. Você também pode integrar os resultados a um banco de dados, enviá‑los para um índice de busca ou canalizá‑los para uma API de tradução.

Tem um cenário complicado — como OCR em PDFs ou em imagens armazenadas na nuvem? Esses são extensões naturais do que construímos hoje. Mergulhe, ajuste as configurações e deixe o motor OCR fazer o trabalho pesado.

Feliz codificação, e que sua extração de texto seja rápida e precisa!

## O que você deve aprender a seguir?

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}