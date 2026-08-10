---
category: general
date: 2026-02-22
description: Crie PDF pesquisável a partir de um PDF escaneado usando Aspose OCR em
  Java. Aprenda a converter PDF escaneado, compactar imagens de PDF e reconhecer OCR
  de PDF de forma eficiente.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: pt
og_description: Criar PDF pesquisável a partir de um PDF escaneado usando Aspose OCR
  em Java. Este tutorial passo a passo mostra como converter PDF escaneado, compactar
  imagens de PDF e reconhecer OCR em PDF.
og_title: Criar PDF pesquisável – Guia Java para converter PDFs digitalizados
tags:
- Java
- OCR
- PDF
- Aspose
title: Criar PDF pesquisável – Guia Java para converter PDFs escaneados
url: /pt/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável – Guia Java para Converter PDFs Escaneados

Já precisou **criar PDF pesquisável** a partir de uma pilha de documentos escaneados? É uma dor de cabeça comum — seus PDFs parecem bons, mas você não consegue usar *Ctrl + F* para encontrar nada. A boa notícia? Com algumas linhas de Java e Aspose OCR você pode transformar esses PDFs apenas de imagem em arquivos totalmente pesquisáveis, **converter PDF escaneado** em texto e ainda reduzir o resultado ao **compactar imagens PDF**.  

Neste tutorial percorreremos um exemplo completo e executável, explicaremos por que cada configuração importa e mostraremos como ajustar o processo para casos extremos, como digitalizações de várias páginas ou imagens de baixa resolução. Ao final, você terá um trecho sólido, pronto para produção, que **recognize pdf ocr** de forma confiável e produz um documento pesquisável bem formatado.

---

## O que você precisará

- **Java 17** (ou qualquer JDK recente; a API é independente de JDK)  
- Biblioteca **Aspose.OCR for Java** – você pode obtê-la no Maven Central (`com.aspose:aspose-ocr`)  
- Um PDF escaneado (apenas imagem) que você deseja tornar pesquisável  
- Uma IDE ou editor de texto com o qual se sinta confortável (IntelliJ, VS Code, Eclipse…)

Não há frameworks pesados, nem serviços externos — apenas Java puro e um único JAR de terceiros.  

---

![exemplo de pdf pesquisável](placeholder-image.png "Ilustração de um PDF pesquisável criado a partir de um documento escaneado")

*Texto alternativo da imagem:* **create searchable pdf** ilustração mostrando antes‑e‑depois de um PDF escaneado transformado em texto pesquisável.

---

## Etapa 1 – Inicializar o Motor OCR  

A primeira coisa que você deve fazer é iniciar uma instância de `OcrEngine`. Pense nele como o cérebro que analisará cada bitmap dentro do PDF e gerará caracteres Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Dica profissional:** Se você planeja processar muitos PDFs consecutivamente, reutilize o mesmo `OcrEngine` em vez de criar um novo a cada vez. Isso economiza alguns milissegundos e reduz o consumo de memória.

---

## Etapa 2 – Configurar Opções OCR Específicas para PDF  

A Aspose permite ajustar finamente como o PDF de saída é construído. As três configurações abaixo são as mais impactantes para **compress pdf images** enquanto preservam a capacidade de pesquisa.  

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi é um ponto ideal; valores menores aceleram o processo, mas podem perder fontes pequenas.  
- **CompressImages** – ativa compressão PNG sem perdas nos bastidores; o PDF pesquisável permanece nítido e mais leve.  
- **EmbedOriginalImages** – sem essa flag o motor descartaria o raster original, deixando apenas texto invisível. Manter a imagem garante que o PDF tenha exatamente a aparência da digitalização, o que muitas equipes de conformidade exigem.

---

## Etapa 3 – Carregar seu PDF escaneado em um `OcrInput`  

A Aspose lê o arquivo de origem através de um wrapper `OcrInput`. Você pode adicionar vários arquivos, mas para esta demonstração focamos em um único **image PDF**.  

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Por que não passar apenas um `File`?** Usar `OcrInput` oferece a flexibilidade de concatenar vários PDFs ou até mesmo misturar arquivos de imagem (PNG, JPEG) antes do OCR. É o padrão recomendado quando você **convert scanned pdf** que pode estar dividido em várias fontes.

---

## Etapa 4 – Executar OCR e Obter um PDF Pesquisável como um Array de Bytes  

Agora a mágica acontece. O motor analisa cada página, executa seu OCR e cria um novo PDF que contém tanto a imagem original quanto uma camada de texto oculto.  

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Se você precisar do texto bruto para outros fins (por exemplo, indexação), também pode chamar `ocrEngine.recognize(ocrInput)`, que retorna uma `String`. Mas para o objetivo de **create searchable pdf**, o array de bytes é o que você gravará no disco.

---

## Etapa 5 – Salvar o PDF Pesquisável no Disco  

Finalmente, escreva o array de bytes em um arquivo. O NIO do Java torna isso uma única linha.  

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Ao abrir `searchable_output.pdf` no Adobe Acrobat ou em qualquer visualizador moderno, você perceberá que agora pode selecionar, copiar e pesquisar o texto — exatamente o que a transformação **image pdf to text** promete.

---

## Converter PDF Escaneado em Texto com OCR (Opcional)

Às vezes você só precisa do texto simples extraído, não de um novo PDF. Você pode reutilizar o mesmo motor:  

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Este trecho demonstra como é fácil **recognize pdf ocr** para processamento posterior, como alimentar um índice de busca ou realizar análise de linguagem natural.

---

## Compactar Imagens PDF para Arquivos Menores  

Se suas digitalizações de origem são enormes (por exemplo, escaneamentos coloridos de 600 dpi), o PDF pesquisável resultante ainda pode ser volumoso. Além da flag `setCompressImages(true)`, você pode reduzir manualmente a resolução antes do OCR:  

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

Reduzir o DPI diminuirá o tamanho do arquivo aproximadamente à metade, mas teste a legibilidade — algumas fontes ficam ilegíveis abaixo de 150 dpi. O trade‑off entre **compress pdf images** e a precisão do OCR é algo que você decidirá com base nas restrições de armazenamento.

---

## Configurações de OCR de PDF Explicadas  

| Configuração                | Efeito na Saída                         | Caso de Uso Típico                                   |
|-----------------------------|------------------------------------------|------------------------------------------------------|
| `setOutputDpi(int)`         | Controla a resolução raster da saída OCR | Arquivos de alta qualidade (300 dpi) vs. PDFs leves para web (150 dpi) |
| `setCompressImages`         | Habilita compressão PNG                  | Quando você precisa enviar PDFs por e‑mail ou armazenar na nuvem |
| `setEmbedOriginalImages`    | Mantém a digitalização original visível  | Documentos legais ou de conformidade que devem preservar a aparência original |
| `setLanguage` (optional)    | Força o modelo de idioma (ex.: "eng")    | Corpora multilíngues onde a detecção automática padrão pode falhar |

---

## PDF de Imagem para Texto – Armadilhas Comuns e Como Evitá‑las  

1. **Low‑resolution scans** – A precisão do OCR cai drasticamente abaixo de 150 dpi. Aumente a resolução da fonte antes de enviá‑la ao Aspose, ou solicite um DPI maior ao scanner.  
2. **Rotated pages** – Se as páginas foram escaneadas de lado, habilite a rotação automática: `pdfOcrOptions.setAutoRotate(true);`.  
3. **Encrypted PDFs** – O motor não pode ler arquivos protegidos por senha; descriptografe primeiro usando `PdfDocument` do Aspose.PDF.  
4. **Mixed raster and text** – Alguns PDFs já contêm uma camada de texto oculto. Executar OCR novamente pode duplicar o texto. Use `PdfOcrOptions.setSkipExistingText(true);` para preservar a camada original.  

Abordar essas questões garante que seu pipeline de **create searchable pdf** seja robusto em coleções de documentos do mundo real.

---

## Exemplo Completo Funcional (Todas as Etapas em Um Arquivo)

Abaixo está a classe Java completa que você pode copiar‑colar em sua IDE. Substitua `YOUR_DIRECTORY` pelo caminho real da pasta.  

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Inicializar o motor OCR
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configurar opções OCR específicas para PDF
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Carregar o PDF escaneado (apenas imagem) em um objeto OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- seu arquivo de origem

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}