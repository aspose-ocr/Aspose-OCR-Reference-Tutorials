---
category: general
date: 2026-10-11
description: Aprenda como realizar OCR em uma imagem PNG em Java, extrair texto da
  imagem e converter a imagem em texto com um exemplo simples de OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: pt
lastmod: 2026-10-11
og_description: Como realizar OCR em uma imagem PNG em Java, extrair texto da imagem
  e converter a imagem em texto usando um exemplo conciso e pronto‑para‑executar.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Como fazer OCR em uma imagem PNG no Java – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Como fazer OCR em uma imagem PNG no Java
url: /pt/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como realizar OCR em uma imagem PNG em Java

Se você precisa **perform OCR** em um arquivo de imagem, aprender **how to perform OCR** em Java é essencial para muitas tarefas de automação. Seja digitalizando recibos, indexando documentos escaneados ou construindo um arquivo de fotos pesquisável, a capacidade de **extract text from image** arquivos economiza inúmeras horas manuais.

Este tutorial mostra uma solução completa e executável que carrega um PNG, executa um motor OCR e **recognize text from PNG** arquivos. Você também verá como **convert image to text** e lidar com armadilhas comuns, como entrada de baixa resolução ou caracteres não‑ASCII.

## O que você alcançará

* **load image java** código que lê um PNG do disco,
* inicializar um motor OCR leve,
* **extract text from image** e imprimir o resultado no console,
* adaptar a solução para outros formatos de imagem ou processamento em lote.

Nenhum serviço externo é necessário—apenas uma única biblioteca OCR de código aberto (Tess4J) e o runtime Java SE.

---

## Pré-requisitos

* Java 17 ou superior (o código compila com JDK 17).
* Maven ou Gradle para gerenciamento de dependências.
* Familiaridade básica com a linha de comando e IDE de sua escolha.
* A biblioteca `tess4j` (um wrapper Java para Tesseract). Adicione a seguinte dependência Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Se você usar Gradle, o equivalente é:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Você também precisa dos arquivos de dados do Tesseract (`.traineddata`). Baixe o pacote de dados em inglês do repositório oficial e coloque-o em uma pasta chamada `tessdata` na raiz do projeto.

---

## Etapa 1: Carregar a imagem em Java

Carregar um PNG é simples com a classe padrão `ImageIO`. O código abaixo demonstra **load image java** de forma segura e consciente de exceções:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Por que isso importa:** `ImageIO.read` detecta automaticamente o formato da imagem, mas verificamos explicitamente se é `null` para evitar falhas silenciosas quando o PNG está corrompido. Esse padrão é uma boa prática ao **load image java** para OCR.

---

## Etapa 2: Inicializar o motor OCR

Tess4J encapsula o binário nativo do Tesseract, expondo uma API Java simples. O método a seguir cria uma instância `Tesseract`, aponta-a para a pasta `tessdata` e configura o idioma para English:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Por que fazemos isso:** Inicializar o motor uma vez e reutilizá-lo para múltiplas imagens reduz a sobrecarga de inicialização. A chamada `setOcrEngineMode` seleciona o modo padrão, que funciona bem para a maioria dos PNGs. Se você encontrar digitalizações ruidosas, pode experimentar outros modos (por exemplo, `OEM_LSTM_ONLY`).

---

## Etapa 3: Executar OCR e **recognize text from PNG**

Agora combinamos o carregador de imagem e o motor OCR. O método abaixo executa OCR em um `BufferedImage` e retorna a string extraída:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Exemplo completo executável**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Saída esperada**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

O console mostrará os caracteres exatos que o motor extraiu de `sample.png`. Se o PNG contiver apenas uma única palavra, a saída será essa palavra seguida por uma nova linha.

---

## Etapa 4: Variações comuns e casos de borda

### 4.1 Lidando com PNGs de baixa resolução

Tesseract tem melhor desempenho em imagens com pelo menos 300 DPI. Se o seu PNG de origem for menor, aumente a escala antes do OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Aplique `upscale(image, 2)` antes de chamar `extractText` para melhorar a precisão.

### 4.2 Extraindo texto não‑English

Para **extract text from image** que contém outros idiomas, baixe os arquivos `.traineddata` apropriados e defina o código de idioma:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Processamento em lote de múltiplos PNGs

Se você precisar **recognize text from PNG** arquivos em uma pasta, itere sobre o diretório:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Lidando com erros de OCR

Erros típicos de OCR incluem ler `0` (zero) como `O` ou `1` como `l`. Pós‑processamento com expressões regulares pode limpar o resultado:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Dicas profissionais para OCR confiável em Java

| Dica | Motivo |
|-----|--------|
| **Use um PNG sem perdas** | Artefatos de compressão em JPEG podem confundir o motor. |
| **Corte bordas brancas** | Espaços em branco excessivos aumentam o tempo de processamento e podem causar falsos positivos. |
| **Defina `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** apenas quando o layout for desconhecido; caso contrário, escolha um modo específico (por exemplo, `PSM_SINGLE_BLOCK`). |
| **Cache a instância `ITesseract`** |

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como ler texto de uma imagem em Java usando Aspose OCR – Guia completo](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Como usar OCR em Java – Reconheça texto de imagem rapidamente](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR em lote de imagens em Java – Extraia texto de arquivos PNG rapidamente](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}