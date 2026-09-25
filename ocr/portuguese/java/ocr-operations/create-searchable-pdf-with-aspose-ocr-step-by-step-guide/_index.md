---
category: general
date: 2026-01-02
description: Crie PDF pesquisável a partir de um PDF de imagem digitalizada usando
  Aspose OCR. Aprenda a definir o idioma do OCR, incorporar uma camada de texto ao
  PDF e aplicar opções de alta compressão ao PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: pt
og_description: Crie PDFs pesquisáveis rapidamente. Este guia mostra como converter
  PDFs de imagens escaneadas, incorporar uma camada de texto, definir o idioma de
  OCR e habilitar alta compressão de PDF.
og_title: Crie PDF pesquisável com Aspose OCR – Guia completo
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Criar PDF pesquisável com Aspose OCR – Guia passo a passo
url: /pt/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável – Tutorial de programação completo

Já precisou **criar PDF pesquisável** a partir de imagens digitalizadas, mas não sabia por onde começar? Você não está sozinho. Em muitos fluxos de trabalho com muitos documentos, um PDF simples contendo apenas imagens é um beco sem saída para busca e indexação.  

A boa notícia é que, com o Aspose OCR, você pode **converter PDF de imagem digitalizada** em um documento totalmente pesquisável em apenas algumas linhas de Java. Este tutorial orienta você em cada passo — inicializando o motor OCR, configurando as definições de PDF de alta compressão, incorporando uma camada de texto oculta e até escolhendo o idioma OCR correto.

Ao final deste guia, você terá um programa executável que produz um PDF pesquisável, um arquivo que pode ser inserido em qualquer mecanismo de busca ou sistema de gerenciamento de documentos sem problemas.

---

## Criar PDF pesquisável – Visão geral

Antes de mergulharmos no código, vamos esclarecer o que realmente significa “criar PDF pesquisável”. Um PDF pesquisável contém duas camadas paralelas:

1. **Camada visual** – a imagem digitalizada original (ou página renderizada).  
2. **Camada de texto** – caracteres invisíveis, porém legíveis por máquina, extraídos pelo OCR.

Quando você abre esse PDF no Adobe Reader e seleciona texto, na verdade está interagindo com a camada de texto oculta, não com a imagem. Essa abordagem de dupla camada é o que permite a funcionalidade de **incorporar camada de texto PDF**.

---

## Converter PDF de imagem digitalizada usando Aspose OCR

A primeira coisa que você precisa é uma imagem digitalizada (PNG, JPEG, TIFF) que deseja transformar em PDF. O Aspose OCR pode ler essa imagem, executar OCR e passar o resultado para um gravador de PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Por que isso funciona:**  
- `setCreateSearchablePdf(true)` indica ao Aspose que gere a camada de texto oculta, atendendo ao requisito de **incorporar camada de texto pdf**.  
- `setCompressionLevel(9)` coloca o arquivo na faixa de **pdf de alta compressão**, reduzindo o tamanho final sem sacrificar a precisão do OCR.  
- O argumento `RecognitionLanguage.ENGLISH` demonstra como **definir o idioma OCR**; você pode trocá-lo por francês, alemão, etc., dependendo do material de origem.

---

## Configurações de PDF de alta compressão

PDFs digitalizados grandes podem rapidamente inflar para centenas de megabytes. O Aspose oferece uma API de compressão simples que funciona no nível do PDF. O método `setCompressionLevel` aceita valores de 0 (sem compressão) a 9 (compressão máxima).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Algumas dicas:

- **Use formatos de imagem sem perdas** (PNG) para digitalizações com muito texto; JPEG é melhor para fotos.  
- **Habilite a subconfiguração de fontes** se você incorporar fontes personalizadas — o Aspose faz isso automaticamente ao criar um PDF pesquisável.  
- **Teste o tamanho da saída** após cada alteração; às vezes, uma compressão nível‑8 oferece uma redução de tamanho de 10 % com perda de qualidade insignificante comparada ao nível 9.

---

## Incorporar camada de texto PDF para pesquisabilidade

Se você omitir a chamada `setCreateSearchablePdf(true)`, o arquivo resultante parecerá correto, mas você não poderá pesquisar seu conteúdo. A camada de texto oculta é criada ao mapear cada caractere reconhecido para sua localização na página.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**O que observar:**  

- **Documentos multilíngues** – pode ser necessário executar OCR duas vezes, uma por idioma, e então mesclar as camadas de texto.  
- **Layouts complexos** (tabelas, múltiplas colunas) – o Aspose faz um trabalho razoável, mas verifique novamente a saída com um visualizador de PDF que mostre texto oculto (por exemplo, o modo “Editar PDF” do Adobe Acrobat).

---

## Definir idioma OCR para reconhecimento preciso

A precisão do motor OCR depende do idioma que você indica como esperado. O Aspose vem com um conjunto de idiomas embutidos, e você também pode adicionar pacotes de idiomas personalizados.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Quando mudar o idioma:**  

- Documentos contêm **scripts não latinos** (Cirílico, Árabe) – altere para o `RecognitionLanguage` apropriado.  
- Páginas com múltiplos idiomas – você pode chamar `recognizeImageAndSave` duas vezes, cada vez com um idioma diferente, e então mesclar os PDFs.

---

## Executando o exemplo completo

Abaixo está o programa completo, pronto para ser executado. Substitua os caminhos de placeholder pelos locais reais dos arquivos, garanta que o JAR do Aspose OCR esteja no seu classpath e execute.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Saída esperada:** Quando você executa o programa, o console imprime:

```
Searchable PDF created.
```

Abra `searchable.pdf` em qualquer visualizador de PDF, tente selecionar texto e você verá a camada invisível em ação. Você criou com sucesso **PDF pesquisável** a partir de uma imagem digitalizada.

![exemplo de criação de pdf pesquisável](image-placeholder.png "exemplo de criação de pdf pesquisável")

*A captura de tela acima (placeholder) normalmente mostraria o visualizador de PDF com texto selecionável sobre uma página digitalizada.*

---

## Conclusão

Cobremos tudo o que você precisa para **criar arquivos PDF pesquisáveis** usando o Aspose OCR:

- Inicialize o motor OCR.  
- **Converta PDF de imagem digitalizada** fornecendo um PNG/JPEG para `recognizeImageAndSave`.  
- Use `setCreateSearchablePdf(true)` para **incorporar camada de texto PDF**.  
- Aplique `setCompressionLevel(9)` para um **PDF de alta compressão** que permanece leve.  
- Escolha o `RecognitionLanguage` correto para **definir o idioma OCR** e obter a máxima precisão.

A partir daqui, você pode experimentar processamento em lote, diferentes idiomas ou até combinar várias páginas digitalizadas em um único PDF pesquisável. O mesmo padrão funciona para outros idiomas como espanhol ou japonês — basta trocar o enum `RecognitionLanguage`.

Sinta‑se à vontade para deixar um comentário se encontrar algum problema, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}