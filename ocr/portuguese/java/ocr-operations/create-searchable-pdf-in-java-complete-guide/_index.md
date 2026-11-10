---
category: general
date: 2026-07-05
description: Crie PDF pesquisável em Java usando Aspose OCR. Aprenda como comprimir
  imagens em PDF, converter imagem escaneada em PDF e desativar a incorporação de
  fontes no PDF para arquivos menores.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: pt
og_description: Crie PDF pesquisável em Java com Aspose OCR. Este tutorial mostra
  como compactar imagens em PDF, converter imagem escaneada em PDF e desativar a incorporação
  de fontes no PDF.
og_title: Criar PDF pesquisável em Java – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Criar PDF pesquisável em Java – Guia completo
url: /pt/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável em Java – Guia Completo

Já precisou **criar PDF pesquisável** a partir de um documento escaneado, mas ficou travado na parte “como‑faço‑isso”? Você não está sozinho. Em muitos projetos, transformar um TIFF ou JPEG em um PDF que realmente possa ser pesquisado é um recurso *essencial*, especialmente quando você também quer **compactar imagens em PDF** para manter os tamanhos de arquivo manejáveis.  

Neste tutorial vamos percorrer um exemplo prático usando Aspose OCR para Java. Ao final, você saberá exatamente como **converter imagem escaneada para PDF**, ajustar a configuração de **compactar imagens em PDF** e até **desativar incorporação de fontes PDF** para reduzir alguns kilobytes a mais. Sem enrolação — apenas uma solução completa e executável que você pode inserir no seu código hoje mesmo.

## O que você vai aprender

- Configurar o motor Aspose OCR em um projeto Java.  
- Executar OCR em um TIFF (ou qualquer imagem raster).  
- Configurar `PdfSaveOptions` para **compactar imagens em PDF** e **desativar incorporação de fontes PDF**.  
- Salvar o resultado como um **PDF pesquisável** que você pode indexar ou buscar instantaneamente.  

**Pré‑requisitos**  
- Java 8 ou superior instalado.  
- Maven ou Gradle para gerenciamento de dependências (mostraremos o trecho Maven).  
- Um arquivo de imagem escaneada (TIFF, PNG ou JPEG) pronto para ser processado.  

Se você tem tudo isso, vamos mergulhar.

![Criar fluxo de trabalho de PDF pesquisável – Conversão de OCR Java para PDF](/images/create-searchable-pdf-workflow.png "Diagrama mostrando as etapas para criar PDF pesquisável com Aspose OCR")

## Etapa 1: Adicionar a dependência Aspose OCR

Primeiro, importe a biblioteca Aspose OCR para o seu projeto. Com Maven, adicione isto ao seu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Se preferir Gradle, o equivalente é:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Dica de especialista:** Fique de olho nas notas de versão da Aspose; versões mais recentes costumam trazer melhorias de desempenho para a precisão do OCR.

## Etapa 2: Inicializar o motor OCR

Criar um motor OCR é tão simples quanto instanciar `OcrEngine`. Esse objeto cuidará de tudo, desde o carregamento da imagem até a extração de texto.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Por que precisamos de um motor dedicado? A Aspose separa o processamento pesado (pré‑processamento de imagem, modelos de linguagem) do resto da sua aplicação, permitindo reutilizar o mesmo `engine` em vários arquivos sem precisar reinicializar recursos pesados.

## Etapa 3: Executar OCR na imagem escaneada

Agora alimentamos o motor com um arquivo escaneado. O método `recognizeImage` devolve um `RecognitionResult` que contém o texto extraído e informações de layout.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **E se a imagem não for um TIFF?**  
> O Aspose OCR detecta automaticamente formatos raster comuns, então você pode apontá‑lo para um JPEG, PNG ou BMP sem mudar o código.

## Etapa 4: Configurar opções de salvamento PDF (Compactar imagens e desativar incorporação de fontes)

É aqui que as palavras‑chave secundárias entram em ação. Diremos ao Aspose para **compactar imagens em PDF** e para **desativar incorporação de fontes PDF**. Ambas as configurações reduzem o tamanho final do arquivo — útil quando você está enviando dezenas de documentos.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Por que compactar imagens?**  
Páginas escaneadas costumam ser de alta resolução; compactá‑las para 80 % de qualidade pode reduzir um PDF de 10 páginas de 12 MB para menos de 3 MB sem perda visual perceptível.

**Por que desativar incorporação de fontes?**  
Se o motor OCR usar fontes padrão do sistema (como Arial ou Times New Roman), incorporá‑las é redundante. Desativá‑las reduz ainda mais o tamanho do arquivo, especialmente em lotes grandes.

## Etapa 5: Salvar o resultado OCR como PDF pesquisável

A etapa final junta tudo: a imagem original, a camada de texto extraído e as opções PDF que configuramos.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Ao abrir `document.pdf` no Adobe Reader ou em qualquer visualizador moderno, você verá a imagem escaneada original **mais** uma camada de texto invisível. Digitar uma palavra na caixa de busca destacará as ocorrências — exatamente o que “criar PDF pesquisável” promete.

### Saída esperada

Executar o programa com um TIFF válido gera algo como:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Abra o PDF, pressione `Ctrl+F`, digite uma palavra que apareça na página escaneada e veja o cursor pular para o local correto. Esse é o sinal de um fluxo **criar PDF pesquisável** bem‑sucedido.

## Armadilhas comuns & como evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **PDF em branco** | `PdfSaveOptions` não foi passado para `saveAsSearchablePdf`. | Certifique‑se de chamar a sobrecarga que aceita `PdfSaveOptions`. |
| **Caracteres estranhos** | Idioma do OCR não definido (padrão é Inglês). | Use `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` antes de `recognizeImage`. |
| **Tamanho de arquivo enorme** | `setCompressImages(false)` ou `setEmbedFonts(true)`. | Mantenha ambas as flags conforme mostrado acima. |
| **Distorção da imagem** | `setImageQuality` definido muito baixo (<50). | Use valores entre 70‑90 para um bom compromisso. |

## Expandindo o exemplo

Agora que você pode **converter imagem escaneada para PDF** e controlar o tamanho, talvez queira:

- **Processar em lote** uma pasta de escaneamentos com um simples loop `for(File f : folder.listFiles())`.  
- Adicionar **marcas d'água** usando Aspose PDF (`PdfDocument.addWatermarkText`).  
- Exportar o texto OCR para um **arquivo .txt** simples para sistemas de indexação (`result.getText().writeToFile("doc.txt")`).  

Todas essas extensões reutilizam a mesma instância de `OcrEngine`, mantendo o uso de memória baixo.

## Código completo, pronto‑para‑executar

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Copie‑e‑cole isso no seu IDE, substitua `YOUR_DIRECTORY` por um caminho real e execute. Se tudo estiver configurado corretamente, você terá um **PDF pesquisável** que também é leve graças à compactação de imagens e à desativação da incorporação de fontes.

## Conclusão

Acabamos de cobrir tudo o que você precisa para **criar PDF pesquisável** em Java usando Aspose OCR. Desde a inicialização do motor, execução do OCR, ajuste de **compactar imagens em PDF** e **desativar incorporação de fontes PDF**, até a gravação final do documento pesquisável — cada passo foi explicado com o *porquê* por trás dele.  

Pronto para o próximo desafio? Experimente adicionar pacotes de idioma ao OCR, processar pastas inteiras em lote ou sobrepor PDFs com anotações. Os fundamentos que você acabou de dominar tornarão essas extensões muito mais simples.

Tem dúvidas ou quer compartilhar suas próprias dicas? Deixe um comentário abaixo e feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Reconhecer texto em PDF – Operações OCR com Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [OCR reconhecendo documentos PDF em Aspose.OCR para Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Como fazer OCR em PDF no .NET com Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}