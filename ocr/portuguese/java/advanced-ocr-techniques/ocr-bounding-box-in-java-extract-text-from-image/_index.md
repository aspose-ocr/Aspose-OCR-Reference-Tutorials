---
category: general
date: 2026-06-16
description: O tutorial de caixa delimitadora OCR em Java mostra como extrair texto
  de uma imagem, ler texto de uma imagem e obter a pontuação de confiança OCR para
  arquivos JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: pt
og_description: A caixa delimitadora de OCR em Java permite reconhecer texto de arquivos
  JPG, extrair texto da imagem e visualizar as pontuações de confiança do OCR — tudo
  em um exemplo de código simples.
og_title: Caixa delimitadora de OCR em Java – Extrair texto da imagem
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Caixa delimitadora de OCR em Java – Extrair texto da imagem
url: /pt/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Caixa Delimitadora OCR em Java – Extrair Texto de Imagem

Já se perguntou como obter a **ocr bounding box** para cada trecho de texto em uma imagem Java? Neste tutorial vamos mostrar como **extract text from image**, **read text from image** e até ver a **ocr confidence score** enquanto você **recognize text from jpg**. A resposta curta? Algumas linhas de código usando uma biblioteca OCR moderna, mais uma explicação sobre por que cada chamada importa.

Abaixo você encontrará um exemplo completo, pronto‑para‑executar, uma análise passo‑a‑passo e algumas dicas práticas que pode copiar direto para seu próprio projeto. Ao final, você será capaz de gerar algo como:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## O que Você Precisará

- **Java 11** ou superior (a sintaxe abaixo usa a palavra‑chave `var` por brevidade, mas você pode removê‑la para JDKs mais antigos).  
- Uma biblioteca OCR que ofereça uma API Java – para este guia usaremos **[Tesseract4J](https://github.com/nguyenq/tess4j)**, um wrapper leve ao redor do popular motor Tesseract.  
- Uma imagem JPEG (`.jpg`) que contenha texto impresso e nítido.  
- Sua IDE favorita (IntelliJ IDEA, Eclipse, VS Code…) – qualquer serve.

Se estiver faltando a biblioteca, basta adicionar esta dependência Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Agora vamos mergulhar.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## Caixa Delimitadora OCR: Configurando o Motor

A primeira coisa que você tem que fazer é criar uma instância do motor OCR. Pense nisso como ligar o scanner que mais tarde lerá os pixels.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Por que isso importa:**  
Sem definir o `datapath`, o Tesseract não saberá onde estão os pacotes de idioma, e você receberá um erro enigmático “Failed loading language”. A chamada `setLanguage` é opcional se você precisar apenas do pacote padrão em inglês, mas ser explícito torna o código mais claro para futuros leitores.

## Carregue a Imagem que Você Deseja Processar

Em seguida, alimente o motor com o JPEG que você deseja analisar. A biblioteca aceita um `File` ou `BufferedImage`; usaremos um `File` por simplicidade.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Dica profissional:**  
Se sua imagem estiver em resources (por exemplo, dentro de um JAR), use `getResourceAsStream` e envolva‑a com `ImageIO.read`. Dessa forma o tutorial funciona tanto localmente quanto em um aplicativo empacotado.

## Execute o Reconhecimento OCR

Agora pedimos ao motor que leia a imagem. O resultado é uma string de texto simples, mas também queremos a **ocr confidence score** e a **ocr bounding box** para cada linha.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Por que usamos `getWords` em vez do simples `doOCR`:**  
`doOCR` fornece a string bruta mas descarta informações espaciais. Ao chamar `getWords` com `RIL_WORD` (ou `RIL_TEXTLINE` se preferir caixas ao nível de linha), recuperamos uma lista de objetos `Word` que carregam o texto, a confiança e o retângulo delimitador. Esse é o coração do recurso **ocr bounding box**.

## Entendendo a Saída

Executar o trecho acima contra um JPEG limpo gera uma saída semelhante a:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Texto** – os caracteres reconhecidos.  
- **Confiança** – um valor de ponto flutuante entre 0 e 1; quanto maior, mais certa está a engine.  
- **Caixa** – o retângulo que envolve a palavra nas coordenadas de pixel (x, y, largura, altura).  

Agora você pode **read text from image** e também saber exatamente onde cada trecho está na tela — perfeito para realçar, recortar ou alimentar pipelines de NLP posteriores.

## Casos de Borda e Armadilhas Comuns

| Situação | O que observar | Correção / Solução |
|-----------|-------------------|-------------------|
| Imagem borrada ou de baixo contraste | Pontuações de confiança caem drasticamente (geralmente abaixo de 0,6). | Pré‑processar com OpenCV: aumentar contraste, aplicar limiarização. |
| JPEG contém texto rotacionado | Caixas delimitadoras aparecem distorcidas ou ausentes. | Use `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` para que o Tesseract detecte automaticamente a orientação. |
| Imagens grandes causam OutOfMemoryError | Heap Java enche ao carregar imagens grandes. | Reduza a escala da imagem antes do OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Você precisa de caixas ao nível de linha em vez de palavra | `RIL_WORD` retorna caixas por palavra. | Mude para `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Caracteres não‑ingleses aparecem como � | Dados de idioma não carregados. | Baixe o arquivo `.traineddata` apropriado e aponte `setDatapath` para sua pasta. |

Abordar esses problemas cedo economiza horas de depuração depois.

## Exemplo Completo Funcional (Todas as Etapas em Um Arquivo)

A seguir está uma classe Java autônoma que você pode copiar‑colar para a pasta `src/main/java` e executar com `mvn exec:java`. Ela reúne tudo que discutimos.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo‑a‑passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem Java com Aspose.OCR Modo Detectar Áreas](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extrair Imagens de Texto – Conceitos Básicos de OCR com Aspose.OCR para Java](/ocr/english/java/ocr-basics/)
- [Como fazer OCR de Texto em Imagem com Idioma Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}