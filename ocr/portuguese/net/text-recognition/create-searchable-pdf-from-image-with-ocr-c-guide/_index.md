---
category: general
date: 2026-03-18
description: Crie PDF pesquisável usando Aspose OCR em C#. Converta a imagem em PDF,
  adicione a camada de texto OCR e grave os bytes do PDF em um arquivo em alguns passos
  simples.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: pt
og_description: Crie PDF pesquisável rapidamente com Aspose OCR em C#. Aprenda como
  converter imagem em PDF, adicionar camada de texto OCR e gravar os bytes do PDF
  em um arquivo.
og_title: Criar PDF pesquisável a partir de imagem – Guia rápido de OCR em C#
tags:
- OCR
- PDF
- C#
- Aspose
title: Criar PDF pesquisável a partir de imagem com OCR – Guia C#
url: /pt/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem com OCR – Guia C#

Já precisou **criar PDF pesquisável** a partir de uma foto escaneada? Com o Aspose OCR você pode fazer isso em poucas linhas, sem bibliotecas pesadas. Neste tutorial vamos **converter imagem para PDF**, adicionar uma **camada de texto OCR** por cima e, finalmente, **escrever os bytes do PDF em um arquivo**, para que você obtenha um documento PDF/A‑2b compatível com padrões que seus usuários realmente podem pesquisar.

Se você está se perguntando por que se preocupar com um PDF pesquisável em vez de um arquivo apenas de imagem, pense na experiência do usuário: um PDF pesquisável permite que as pessoas copiem, selecionem e indexem o texto — ótimo para arquivos, documentos legais ou qualquer fluxo de trabalho que precise extrair texto posteriormente. Vamos começar.

## O que você precisará

- .NET 6 ou posterior (o código também funciona no .NET Framework 4.7+)
- Um pacote NuGet Aspose.OCR (`Aspose.OCR` versão 23.10 ou mais recente)
- Uma imagem raster (`.png`, `.jpg`, etc.) que você deseja transformar em um PDF pesquisável
- Um conhecimento básico de C# — nada avançado, apenas o essencial

É isso. Sem ferramentas externas, sem conversores adicionais. Todo o processamento pesado é feito pelo motor Aspose OCR.

## Criar PDF pesquisável – Visão geral

Antes de mergulharmos no código, vamos delinear o processo:

1. **Instanciar** o motor OCR – este objeto sabe como ler texto a partir de imagens.  
2. **Carregar** a imagem de origem – vamos fornecer um `ImageStream` ao motor.  
3. **Configurar** as opções de salvamento PDF/A‑2b – isso indica ao Aspose que incorpore o texto reconhecido como uma camada oculta.  
4. **Executar** o OCR e **capturar** os bytes do PDF resultante.  
5. **Escrever** esses bytes no disco, produzindo o arquivo PDF pesquisável final.

Cada um desses passos corresponde a uma ou duas linhas de C#, fazendo com que todo o fluxo pareça um pequeno script em vez de um projeto enorme.

## Etapa 1: Converter imagem para PDF – Carregar a imagem

Primeiro de tudo: precisamos fornecer ao motor OCR algo para ler. O helper `ImageStream.FromFile` carrega o arquivo em um stream que o Aspose pode processar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Dica profissional:** Mantenha a resolução da sua imagem em 300 dpi ou superior; a precisão do OCR cai drasticamente em digitalizações de baixa resolução.

## Etapa 2: Reconhecer texto da imagem e adicionar camada de texto OCR

Agora criamos o motor OCR e instruímos que reconheça o texto. A mágica acontece quando combinamos o resultado do reconhecimento com `PdfSaveOptions` que têm `IncludeTextLayer = true`. Essa flag força o Aspose a incorporar os caracteres extraídos como uma camada de texto invisível, que é o que torna o PDF pesquisável.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Por que PDF/A‑2b? É um formato de arquivamento padrão ISO que garante preservação a longo prazo e, importante para nós, obriga o PDF a conter uma camada de texto pesquisável. Se você não precisar de conformidade de arquivamento, pode remover `PdfCompliance` completamente, mas mantê-lo não custa nada.

## Etapa 3: Escrever bytes do PDF em arquivo – Salvar o resultado

Com o motor pronto e as opções definidas, executamos o reconhecimento e imediatamente pedimos ao Aspose que nos forneça o PDF como um `byte[]`. Em seguida, gravamos esses bytes no disco usando `File.WriteAllBytes`. Simples, porém poderoso.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Essa linha `Console.WriteLine` é opcional, mas fornece feedback instantâneo quando você executa o programa a partir de um terminal.

## Exemplo completo em funcionamento

Juntando tudo, aqui está o programa completo, pronto para ser executado. Copie e cole em um novo projeto de console, substitua `YOUR_DIRECTORY` por um caminho real e pressione **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Saída esperada

- Um arquivo chamado `output.pdf` aparece na pasta que você especificou.  
- Abra‑o no Adobe Acrobat Reader ou em qualquer visualizador de PDF e tente selecionar texto — se você puder copiar palavras, você criou com sucesso um **PDF pesquisável**.  
- O documento também passará nas ferramentas de validação PDF/A‑2b porque usamos a flag de conformidade correta.

## Perguntas comuns e casos extremos

**E se minha imagem contiver várias páginas?**  
Envolva cada página em seu próprio `ImageStream` e alimente‑as sequencialmente ao `OcrEngine`. O Aspose concatenará automaticamente as páginas em um único PDF.

**Posso mudar o idioma do OCR?**  
Claro. Defina `ocrEngine.Language = Language.English;` (ou qualquer idioma suportado) antes de chamar `Recognize`.

**E quanto ao uso de memória para arquivos enormes?**  
Se você estiver processando digitalizações em escala de gigabytes, considere transmitir o resultado diretamente para um `FileStream` em vez de manter todo o `byte[]` na memória:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Preciso de uma licença?**  
A Aspose oferece um teste gratuito sem marca d'água. Para uso em produção, adquira uma licença para remover o banner de avaliação e desbloquear todos os recursos.

## Dicas para melhorar a precisão do OCR

- **Pré‑processar** a imagem: corrigir inclinação, remover ruído e aumentar o contraste.  
- **Usar formatos sem perdas** como PNG; artefatos de compressão JPEG podem confundir o motor.  
- **Evitar fundos coloridos**; um fundo branco simples produz os melhores resultados.

## Próximos passos

Agora que você pode **criar PDF pesquisável**, talvez queira:

- **Processar em lote** uma pasta de imagens usando `Directory.GetFiles`.  
- **Extrair o texto oculto** posteriormente com as APIs `PdfDocument` para indexação.  
- **Combinar OCR com assinaturas digitais** para criar arquivos à prova de adulteração.  

Todos esses se baseiam no mesmo padrão central que abordamos: carregar, reconhecer, configurar, salvar.

---

*Pronto para transformar seus arquivos escaneados em PDFs pesquisáveis? Pegue o código, aponte para suas imagens e deixe o Aspose fazer o trabalho pesado. Boa codificação!*

![Exemplo de PDF pesquisável](/images/create-searchable-pdf.png "Ilustração de um PDF pesquisável gerado a partir de uma imagem")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}