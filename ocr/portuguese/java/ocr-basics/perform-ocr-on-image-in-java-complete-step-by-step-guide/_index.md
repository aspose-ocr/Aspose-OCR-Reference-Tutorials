---
category: general
date: 2026-06-16
description: Aprenda como realizar OCR em arquivos de imagem em Java. Este tutorial
  aborda o reconhecimento de texto a partir de PNG, a extração de texto de imagens,
  a conversão de imagem em texto e o carregamento de imagens para OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: pt
og_description: Execute OCR em imagem usando Java. Este guia mostra como reconhecer
  texto de PNG, extrair texto de imagem e converter imagem em texto com um exemplo
  pronto‑para‑executar.
og_title: Realizar OCR em Imagem no Java – Tutorial Completo de Programação
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Realize OCR em Imagem no Java – Guia Completo Passo a Passo
url: /pt/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem em Java – Guia Completo Passo a Passo

Já precisou **perform OCR on image** arquivos mas não tinha certeza de qual biblioteca Java escolher? Você não está sozinho. Seja construindo um scanner de recibos, um arquivador de documentos, ou apenas curioso sobre transformar imagens em texto pesquisável, aprender como **perform OCR on image** com Java é uma habilidade útil.

Neste tutorial vamos percorrer tudo que você precisa para **perform OCR on image** arquivos: carregar a imagem, configurar o motor, reconhecer o texto e, finalmente, imprimir o resultado. Ao final, você será capaz de **recognize text from PNG** arquivos, **extract text from image** fontes, e **convert image to text** com apenas algumas linhas de código.

## Pré-requisitos

- Java 17 ou superior (o código compila com qualquer JDK recente)
- Maven instalado (ou sua ferramenta de build favorita)
- Familiaridade básica com a sintaxe Java
- Um arquivo PNG que você queira testar (vamos chamá-lo de `hello.png`)

> **Dica profissional:** Se você não tem um PNG à mão, crie um tirando uma captura de tela de qualquer texto e salvando‑o como `hello.png` em uma pasta chamada `resources`.

## O Que Vamos Construir

1. **Loads image for OCR** – lê um PNG do disco.
2. **Performs OCR on image** – usa o motor Tesseract via Tess4J.
3. **Extracts text from image** – retorna uma `String` com o conteúdo reconhecido.
4. Imprime o resultado no console.

Vamos mergulhar.

## Etapa 1: Configurar o Projeto e Adicionar Tess4J

Primeiro, crie um novo projeto Maven (ou Gradle se preferir). Adicione a dependência Tess4J, que encapsula o popular motor Tesseract OCR.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Por que Tess4J?** É mantido ativamente, funciona em várias plataformas e fornece uma API Java limpa para tarefas de **perform OCR on image**.

## Etapa 2: Preparar a Lógica de Carregamento de Imagem

Agora vamos escrever um método auxiliar que **load image for OCR**. O método usa o `ImageIO` do Java para ler um PNG em um `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Observe que o nome do método reflete claramente a intenção de **load image for OCR**, tornando o código auto‑documentado.

## Etapa 3: Configurar o Motor OCR para **Perform OCR on Image**

Com a imagem em mãos, criamos uma instância `Tesseract`, habilitamos a detecção automática de idioma e chamamos `doOCR`. Este é o núcleo de como **perform OCR on image** dados.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Por que habilitar a detecção automática?** Isso permite que o motor escolha o melhor modelo de idioma para a imagem, o que é especialmente útil quando você **convert image to text** de fontes que misturam inglês e outros scripts.

## Etapa 4: Juntar Tudo – A Aplicação Principal

Aqui está o ponto de entrada que **recognize text from PNG**, **extract text from image**, e finalmente imprime o resultado. Este é o exemplo completo e executável.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Saída Esperada

Se `hello.png` contiver a frase “Hello, OCR world!”, o console exibirá algo como:

```
=== Recognized Text ===
Hello, OCR world!
```

A saída exata pode variar ligeiramente dependendo da qualidade da imagem, mas você deve ver o texto que colocou no PNG.

## Etapa 5: Lidando com Casos de Borda Comuns

### 5.1 Lidando com Imagens de Baixa Resolução

Se o PNG de origem estiver borrado, a precisão do OCR diminui. Uma solução rápida é ampliar a imagem antes de enviá‑la ao motor:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Chame `upscale(image, 2)` antes de `engine.recognize(image)` para melhorar os resultados.

### 5.2 Documentos Multilíngues

Se você espera texto em francês ou alemão, basta adicionar os códigos de idioma ao `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

O motor então tentará **extract text from image** usando os modelos de idioma combinados.

### 5.3 Ignorando Páginas Vazias

Às vezes uma página PDF escaneada é renderizada como um PNG em branco. Detectar uma imagem vazia economiza tempo de processamento:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Etapa 6: Empacotar e Executar a Aplicação

1. **Compilar:** `mvn clean compile`
2. **Executar:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Certifique‑se de que a pasta `tessdata` (contendo arquivos de idioma) esteja ao lado do JAR compilado ou especifique seu caminho absoluto em `OcrEngine`.

## Conclusão

Agora você tem um padrão sólido e pronto para produção para **perform OCR on image** arquivos usando Java. De **loading image for OCR** a **recognize text from PNG**, cobrimos como **extract text from image**, **convert image to text**, e lidar com cenários difíceis como digitalizações de baixa resolução ou conteúdo multilíngue.

Em seguida, você pode explorar:

- **Batch processing** – percorrer um diretório de PNGs e gravar cada resultado em um arquivo `.txt`.
- **PDF generation** – incorporar o texto extraído de volta em PDFs pesquisáveis.
- **Cloud OCR services** – comparar o desempenho local do Tesseract com APIs como Google Vision ou Azure Cognitive Services.

Sinta‑se à vontade para experimentar, ajustar os parâmetros e compartilhar suas descobertas. Feliz codificação, e que suas imagens sempre se transformem em texto limpo e pesquisável! 

![Diagrama mostrando o fluxo de trabalho OCR para perform OCR on image](https://example.com/ocr-workflow.png "exemplo de perform OCR on image")

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [reconhecer texto em imagem com Aspose OCR – Tutorial Completo de OCR Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Converter Imagem para Texto em Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extrair Texto de Imagem Java com Aspose.OCR Modo Detectar Áreas](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}