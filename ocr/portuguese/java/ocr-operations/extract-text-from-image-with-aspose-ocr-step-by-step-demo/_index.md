---
category: general
date: 2026-02-14
description: Extrair texto de imagem usando Aspose OCR. Aprenda como carregar a imagem
  para OCR, ler texto de um retângulo e seguir este tutorial de Aspose OCR em minutos.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: pt
og_description: Extraia texto de imagens instantaneamente. Este guia mostra como carregar
  a imagem para OCR, ler texto de um retângulo e concluir um tutorial de Aspose OCR.
og_title: Extrair texto de imagem com Aspose OCR – Guia rápido
tags:
- Aspose
- OCR
- Java
title: Extrair Texto de Imagem com Aspose OCR – Demonstração Passo a Passo
url: /pt/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem com Aspose OCR – Demo Passo a Passo

Já precisou **extrair texto de uma imagem** mas não sabia por onde começar? Você não está sozinho—muitos desenvolvedores encontram essa barreira ao lidar com a digitalização de recibos ou verificação de documentos de identidade. A boa notícia? Com o Aspose OCR você pode carregar uma imagem, definir a região exata onde o texto está e obter os caracteres em poucas linhas de código.

Neste **tutorial de aspose ocr** vamos percorrer tudo que você precisa: carregar a imagem para OCR, definir um retângulo que indica ao motor onde procurar e, por fim, ler o texto extraído. Ao final, você terá um programa Java executável que imprime o texto da ROI no console—sem mistério, apenas uma solução clara e funcional.

## O Que Você Precisa

Antes de mergulharmos, certifique‑se de que tem o básico pronto:

| Pré‑requisito | Por que é importante |
|--------------|----------------------|
| **Java JDK 8+** | O Aspose OCR é distribuído como uma biblioteca Java; qualquer JDK moderno serve. |
| **Aspose.OCR for Java** (download no site da Aspose ou adicione via Maven) | Fornece as classes `OcrEngine`, `ImageStream` e relacionadas. |
| **Um arquivo de imagem** (ex.: `receipt.jpg`) que contenha texto legível | Apontaremos o motor para um retângulo dentro desse arquivo. |
| **IDE ou editor** (IntelliJ, Eclipse, VS Code…) | Facilita a compilação e execução rápida do exemplo. |

Se você usa Maven, adicione esta dependência ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Dica de especialista:** O número da versão acima está atualizado até fevereiro 2026. Atualizar para a versão mais recente garante correções de bugs e melhorias de desempenho.

## Etapa 1 – Inicializar o Motor OCR

Primeiro passo: você precisa de uma instância de `OcrEngine`. Pense nele como o cérebro que analisará os pixels.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Por que criá‑lo desta forma? O Aspose separa o motor (que contém as configurações) dos dados da imagem, permitindo que você reutilize o mesmo motor para várias imagens, se desejar.

## Etapa 2 – Carregar a Imagem para OCR

Agora realmente **carregamos a imagem para OCR**. O auxiliar `ImageStream.fromFile` lê o arquivo para um stream que o Aspose entende.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Se o arquivo não for encontrado, o motor lançará uma exceção, então pode ser interessante envolver isso em um bloco try‑catch no código de produção. Para este demo deixamos a exceção subir—mantém o exemplo mais limpo.

## Etapa 3 – Definir o Retângulo (Ler Texto do Retângulo)

É aqui que a parte **read text from rectangle** brilha. Você indica ao motor exatamente onde olhar, o que acelera o processamento e reduz falsos positivos.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Por que um retângulo?**  
> A maioria dos documentos tem layouts previsíveis—pense em um recibo onde o valor total sempre aparece próximo ao final. Ao focar nessa fatia, o motor OCR ignora gráficos irrelevantes e aumenta a precisão.

**Caso extremo:** Se o retângulo ultrapassar os limites da imagem, o Aspose o ajusta silenciosamente, mas você perderá dados. Uma verificação rápida pode evitar isso:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Etapa 4 – Processar a Imagem

Com tudo configurado, pedimos ao motor que faça a mágica.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

A chamada `process()` devolve um objeto `OcrResult` que contém o texto extraído, pontuações de confiança e até as caixas delimitadoras de cada palavra, caso precise delas depois.

## Etapa 5 – Exibir o Texto Extraído

Por fim, imprimimos o resultado. Em um aplicativo real você pode armazená‑lo em um banco de dados ou enviá‑lo a outro serviço, mas para este tutorial a saída no console já basta.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Saída esperada** (supondo que o retângulo capturou o valor total de um recibo):

```
ROI text:
$12.34
```

Se a ROI estiver vazia ou a imagem borrada, você verá uma string vazia ou caracteres incompreensíveis. Ajuste o retângulo, melhore a qualidade da imagem ou habilite as opções de pré‑processamento do Aspose (ex.: `setAutoSkewCorrection(true)`).

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para ser executado. Copie‑e cole em um arquivo chamado `RoiDemo.java`, ajuste o caminho da imagem e execute `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Verificação do resultado:** Após a execução, compare a saída do console com o texto real dentro do retângulo. Se coincidirem, você extraiu texto de imagem com sucesso usando o Aspose OCR.

## Perguntas Frequentes & Dicas

### E se eu precisar processar várias ROIs na mesma imagem?
Crie um novo `Rectangle` para cada área, chame `setRegionOfInterest` novamente e execute `process()` outra vez. O motor reutiliza os mesmos dados da imagem, mantendo o desempenho ágil.

### Como o Aspose lida com diferentes idiomas ou fontes?
Você pode mudar o modelo de idioma via `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Para scripts não latinos, carregue o pacote de idioma apropriado (disponível na página de download da Aspose).

### A biblioteca suporta entrada em PDF?
Sim—o Aspose OCR aceita streams de PDF diretamente. Basta substituir `ImageStream.fromFile` por `ImageStream.fromPdfFile("doc.pdf")` e, opcionalmente, especificar o número da página.

### Posso melhorar a precisão em digitalizações de baixa qualidade?
Habilite o pré‑processamento:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

Essas opções limpam ruído e alinham o texto antes do reconhecimento.

## Conclusão

Acabamos de percorrer um **tutorial de aspose ocr** completo que demonstra como **extrair texto de imagem**, **carregar imagem para OCR** e **ler texto do retângulo** usando Java. Os passos chave são: inicializar o motor, fornecer uma imagem, definir a região de interesse, processar e, finalmente, imprimir o resultado.

A partir daqui você pode explorar:

* **Processamento em lote** – iterar sobre uma pasta de recibos e armazenar cada total em um banco de dados.  
* **Detecção dinâmica de ROI** – usar bibliotecas de processamento de imagem (OpenCV) para localizar blocos de texto automaticamente.  
* **Pós‑processamento** – aplicar expressões regulares ou correspondência aproximada para corrigir peculiaridades do OCR.

Experimente essas ideias, ajuste o retângulo conforme seus documentos e você terá um pipeline robusto de extração de texto em pouco tempo. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}