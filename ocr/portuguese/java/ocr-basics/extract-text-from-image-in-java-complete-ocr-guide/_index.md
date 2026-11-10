---
category: general
date: 2026-07-21
description: Extrair texto de uma imagem usando Java OCR. Aprenda como converter PNG
  em texto, ler texto de PNG, carregar a imagem para OCR e executar OCR na imagem
  em apenas alguns passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: pt
lastmod: 2026-07-21
og_description: Extrair texto de imagem com Java. Este guia mostra como converter
  PNG em texto, ler texto de PNG, carregar imagem para OCR e realizar OCR em imagem
  de forma eficiente.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Extrair Texto de Imagem em Java – Tutorial de OCR Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extrair Texto de Imagem em Java – Guia Completo de OCR
url: /pt/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em Java – Guia Completo de OCR

Já precisou **extrair texto de imagem** mas não tinha certeza de qual biblioteca Java escolher? Você não está sozinho. Seja digitalizando recibos, escaneando PDFs ou construindo um arquivo pesquisável, extrair texto de um PNG é um ponto de dor diário para muitos desenvolvedores.

Neste tutorial, percorreremos uma solução prática que permite **converter PNG em texto**, **ler texto de PNG**, **carregar imagem para OCR** e **executar OCR em imagem** — tudo com algumas linhas de código Java limpo. Ao final, você terá um programa executável que pode ser inserido em qualquer projeto.

## O que você vai construir

Vamos criar um pequeno aplicativo console Java que:

1. Carrega um arquivo PNG do disco.  
2. Envia a imagem para um motor OCR (Tess4J, um wrapper Java para o Tesseract).  
3. Imprime o texto reconhecido no console.

Sem serviços externos, sem mágica — apenas Java puro e um motor OCR de código aberto.

## Pré-requisitos

- **Java 17** ou superior (o código compila com versões mais antigas, mas o Java 17 oferece os recursos mais recentes da linguagem).  
- **Maven** ou **Gradle** para gerenciamento de dependências.  
- Um PNG de exemplo chamado `sample.png` colocado em uma pasta que você possa referenciar (por exemplo, `src/main/resources`).  
- Familiaridade básica com o método `main` do Java e tratamento de exceções.

Se algum desses itens lhe for desconhecido, não se preocupe — cada passo inclui um breve resumo.

## Etapa 1: Configurar o Projeto e Adicionar a Biblioteca OCR

Primeiro, crie um novo projeto Maven (ou Gradle, se preferir). Adicione a dependência Tess4J, que inclui os binários do Tesseract para você.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Dica profissional:** Se você estiver usando Gradle, a linha equivalente é `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Adicionar esta biblioteca fornece a classe `Tesseract`, que lida com a parte pesada de **executar OCR em dados de imagem**.

## Etapa 2: Carregar Imagem para OCR

Agora precisamos **carregar imagem para OCR**. O Tess4J trabalha com `java.awt.image.BufferedImage`, então leremos o PNG usando `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

O método acima isola de forma limpa a lógica de **carregar imagem para OCR**, facilitando o teste do restante do código. Observe o comentário — ele reflete o trecho original enquanto o expande para maior clareza.

## Etapa 3: Executar OCR em Imagem

Com a imagem na memória, agora podemos **executar OCR em imagem**. A instância `Tesseract` é nosso motor; configuraremos para usar os dados de idioma padrão em inglês que vêm com o Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Aqui mesclamos as “Etapa 1” e “Etapa 4” originais em um único método, porque o objeto `Tesseract` é barato de criar e queremos que o código permaneça compacto. O comentário ainda faz referência às etapas originais para rastreabilidade.

## Etapa 4: Juntar Tudo – Método main

Finalmente, juntamos tudo em `main`. É aqui que você **lerá texto de PNG** e verá o resultado impresso no console.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Quando você executar `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (ou o equivalente no Gradle), deverá ver algo como:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Essa saída prova que você conseguiu **extrair texto de imagem**, **converter PNG em texto** e **ler texto de PNG** em um único programa organizado.

## Lidando com Casos de Borda Comuns

### Imagens de Baixa Qualidade

Se o PNG estiver borrado ou com baixo contraste, a precisão do OCR diminui. Uma solução rápida é pré‑processar a imagem:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Suporte a Múltiplos Idiomas

O Tess4J pode lidar com vários idiomas. Basta baixar o arquivo `.traineddata` apropriado e apontar `tesseract.setLanguage("spa")` para espanhol, por exemplo.

### PDFs Grandes ou Imagens Multi‑Página

Se precisar **extrair texto de imagem** de arquivos dentro de um PDF, divida cada página em PNGs primeiro (usando PDFBox) e então alimente cada PNG à mesma rotina de OCR.

## Exemplo Completo Funcional (Todo o Código em Um Só Lugar)

Abaixo está a classe Java completa, pronta para executar. Copie‑e cole em `src/main/java/com/example/ocrdemo/OcrDemo.java` e está pronto para usar.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Executar a classe imprime o resultado do OCR, confirmando que você executou **OCR em imagem** com sucesso e transformou seu PNG em texto editável.

## Recapitulação & Próximos Passos

Começamos **extraindo texto de imagem** usando uma configuração Java leve. Agora você sabe como **carregar imagem para OCR**, **executar OCR em imagem** e **ler texto de PNG** — blocos de construção essenciais para qualquer pipeline de digitalização de documentos.

Quer ir além? Experimente estas ideias:

- **Processamento em lote:** Percorra um diretório de PNGs e grave cada resultado em um arquivo `.txt`.  
- **Integração com banco de dados:** Armazene as strings extraídas junto com metadados para arquivos pesquisáveis.  
- **Combinar com NLP:** Alimente a saída do OCR em um modelo de análise de sentimento para obter insights rápidos.  

Cada uma dessas extensões se baseia nos mesmos conceitos centrais que abordamos, então você está pronto para experimentar.

*Feliz codificação! Se você encontrar algum problema

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completo e funcional com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem Java com Aspose.OCR Modo Detectar Áreas](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [imagem para texto java: Converter Imagem em Texto com Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Como fazer OCR de Texto de Imagem com Idioma usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}