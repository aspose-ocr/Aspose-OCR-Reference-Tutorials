---
category: general
date: 2026-11-17
description: Aprenda como realizar OCR em uma imagem em Java e extrair texto de fotos
  usando um exemplo de código simples. Inclui dicas de leitura de imagem em Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: pt
lastmod: 2026-11-17
og_description: Como realizar OCR em uma imagem em Java e extrair texto rapidamente.
  Siga este guia para ler imagens em Java e converter a imagem em texto com um exemplo
  pronto para executar.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Como realizar OCR em uma imagem em Java – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Como fazer OCR em uma imagem em Java – guia passo a passo
url: /pt/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como realizar OCR em uma imagem em Java – guia passo a passo

Se você precisa **how to perform OCR** em uma foto, este tutorial mostra uma solução completa e executável em Java. Você verá como ler um arquivo de imagem, configurar um motor OCR e extrair o texto que o motor reconhece.

Trabalhar com documentos escaneados, recibos ou capturas de tela costuma exigir a conversão do conteúdo visual em texto pesquisável. Este guia conduz você por cada etapa, desde o carregamento da imagem até a impressão do texto extraído, e também aborda armadilhas comuns, como formatos de arquivo não suportados e resultados nulos.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* Java Development Kit (JDK) 8 ou mais recente instalado.
* Uma ferramenta de build (Maven ou Gradle) para obter a biblioteca OCR.
* Um arquivo de imagem (JPEG, PNG, BMP) que você deseja processar.

O código usa a **OCR library from the `com.asprise.ocr` package** porque requer apenas um único JAR e funciona em todas as principais plataformas. Substitua‑a por outro provedor (Tesseract, Google Vision, etc.) trocando as instruções de importação e o código de inicialização do motor.

## Passo 1: Adicionar a dependência OCR

Se você usa Maven, adicione a seguinte dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Para Gradle, coloque esta linha em `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Essas linhas garantem que o código **read image Java** possa ser compilado e que o motor OCR esteja disponível em tempo de execução.

## Passo 2: Ler a imagem com Java

Ler um arquivo de imagem é a primeira etapa concreta em qualquer fluxo de trabalho **extract text image**. A classe nativa `ImageIO` do Java lida com a maioria dos formatos comuns.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Por que isso importa:** `ImageIO.read` retorna `null` para formatos não suportados ou arquivos corrompidos. O método acima registra o problema e devolve `null` para que a próxima etapa possa reagir de forma graciosa.

## Passo 3: Criar e configurar o motor OCR

O motor OCR precisa saber qual idioma reconhecer. Definir o idioma melhora a precisão drasticamente, especialmente para documentos que não são em inglês.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Por que isso importa:** Iniciar o motor é uma operação relativamente pesada, portanto você deve criá‑lo uma única vez e reutilizá‑lo para múltiplas imagens se sua aplicação processar lotes.

## Passo 4: Executar OCR e converter a imagem em texto

Agora que a imagem está carregada e o motor está pronto, você pode executar a etapa de reconhecimento. Este é o núcleo de **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Tratamento de casos extremos:** Se a imagem for `null`, o método devolve uma string vazia em vez de lançar uma `NullPointerException`. Isso torna o código circundante mais robusto ao lidar com arquivos fornecidos pelo usuário.

## Passo 5: Exibir o texto extraído

Finalmente, imprima o resultado no console ou encaminhe‑o para outro componente (por exemplo, um banco de dados ou um widget de UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Ao executar o programa com `java OcrDemo sample.jpg`, o console mostra os caracteres reconhecidos. Isso completa o ciclo **convert image to text**.

### Saída esperada

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Se a imagem não contiver caracteres legíveis, o programa imprime `(no text detected)`.

## Variações comuns e como adaptá‑las

| Variação | O que muda | Quando usar |
|-----------|--------------|-------------|
| **Different language** | Substitua `"eng"` por `"spa"` para espanhol, `"fra"` para francês, etc. | Documentos escritos em um idioma diferente do inglês |
| **Batch processing** | Percorra uma lista de caminhos de arquivos, reutilizando a mesma instância `Ocr`. | Grandes conjuntos de páginas escaneadas |
| **Higher accuracy** | Use `Ocr.SPEED_SLOW` ou habilite `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` para digitalizações apenas numéricas. | Quando a qualidade do OCR é crítica (por exemplo, números de fatura) |
| **Tesseract alternative** | Troque a importação para `net.sourceforge.tess4j.Tesseract` e ajuste o código de inicialização. | Projetos que já dependem do Tesseract |

## Dicas profissionais

* **Resize large images** antes de enviá‑las ao motor; a velocidade do OCR escala com a contagem de pixels.
* **Pre‑process** a imagem (tons de cinza, aumento de contraste) usando bibliotecas como OpenCV se a fonte for ruidosa.
* **Cache the OCR engine** se você o chamar muitas vezes em um curto período — iniciar e parar o motor gera sobrecarga.
* **Validate the result** com expressões regulares quando você espera um formato específico (por exemplo, datas, números de telefone).

## Conclusão

Agora você sabe **how to perform OCR** em uma imagem em Java, desde a leitura do arquivo até a exibição do texto extraído. O tutorial abordou as técnicas **read image Java**, **extract text image**, **convert image to text** e **image to text java**, e forneceu dicas práticas para cenários reais.  

A partir daqui você pode:

* Integrar a etapa OCR em um serviço web que receba uploads.
* Combinar a saída com um índice de busca para pesquisa full‑text em documentos escaneados.
* Explorar opções avançadas de OCR, como suporte multilíngue ou conjuntos de caracteres personalizados.

Boa codificação e aproveite para transformar imagens em texto pesquisável!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar OCR em Java – Extrair texto de imagem com correção ortográfica](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Converter imagem em texto em Java usando Aspose OCR – Guia completo](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [Como habilitar GPU para OCR em Java – Extrair texto de imagem](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}