---
category: general
date: 2026-05-25
description: Converta TIFF em texto usando Aspose.OCR em C#. Aprenda a conversão em
  lote de imagens para texto e extraia texto de arquivos TIFF de forma eficiente.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: pt
og_description: Converta TIFF em texto com Aspose.OCR. Este guia mostra a conversão
  em lote de imagem para texto e como extrair texto de arquivos TIFF em poucas linhas
  de C#.
og_title: Converter TIFF para Texto em C# – Guia Completo de OCR em Lote
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: Converter TIFF para Texto em C# – Guia Completo de OCR em Lote
url: /pt/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter TIFF para Texto em C# – Guia Completo de OCR em Lote

Já precisou **converter TIFF para texto** mas não sabia por onde começar? Você não está sozinho — muitos desenvolvedores tropeçam no OCR em lote ao lidar com documentos escaneados. Neste tutorial vamos percorrer uma solução prática que **extrai texto de arquivos TIFF** usando Aspose.OCR, e faremos isso em paralelo para que pastas grandes terminem em segundos.

Também abordaremos as melhores práticas de **conversão em lote de imagem para texto**, então ao final você terá um trecho reutilizável que transforma um diretório inteiro de imagens escaneadas em arquivos *.txt* organizados — perfeito para indexação, busca ou alimentação de análises posteriores.

## O que você vai precisar

- **.NET 6.0** ou superior (o código também compila no .NET Framework)  
- Pacote NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)  
- Uma pasta contendo um ou mais arquivos *.tif* (o clássico formato de escaneamento TIFF)  
- Seu IDE favorito (Visual Studio, VS Code, Rider — o que preferir)

É só isso. Sem serviços externos, sem chaves de API, apenas C# puro e Aspose.

![Screenshot of a TIFF file being processed and the resulting text file](/images/ocr-result.png "OCR result showing converted TIFF to text output")

*(Alt text: Screenshot showing converted TIFF to text output on screen)*

## Etapa 1: Configurar o Motor OCR – Converter TIFF para Texto

Primeiro de tudo, precisamos de uma instância `OcrEngine` que saiba que deve ler caracteres em inglês. O motor é o coração da conversão; configurá‑lo corretamente garante resultados confiáveis.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Por que isso importa:*  
Aspose.OCR suporta dezenas de idiomas. Se você estiver lidando com escaneamentos multilíngues, basta mudar `OcrLanguage.English` para o valor enum apropriado. Deixar o idioma indefinido força o motor ao modo de auto‑detecção, que pode ser mais lento e menos preciso.

## Etapa 2: Coletar Todos os Arquivos TIFF – Extrair Texto de TIFF de Forma Eficiente

Em seguida, buscamos cada arquivo *.tif* de uma pasta que você especificar. Usar `Directory.GetFiles` nos fornece um array limpo que podemos passar ao processador em lote.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Dica de especialista:* O sinalizador `SearchOption.AllDirectories` pode ser usado se seus escaneamentos estiverem aninhados em subpastas. Apenas lembre‑se de que recursão mais profunda pode aumentar o uso de memória durante a etapa em lote.

## Etapa 3: Executar OCR em Paralelo – Conversão em Lote de Imagem para Texto

Agora vem a parte divertida. Aspose.OCR fornece o helper estático `BatchOcr.RecognizeAll` que aceita um array de caminhos de arquivo, um motor e uma sugestão de `parallelism`. Vamos iniciar quatro threads, o que em um laptop quad‑core moderno oferece quase aceleração linear.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Por que paralelismo?*  
Processar um lote de TIFFs de alta resolução pode ser intensivo para a CPU. Ao distribuir o trabalho entre várias threads mantemos todos os núcleos ocupados, reduzindo drasticamente o tempo total. Se você executar isso em um servidor com mais núcleos, aumente o valor de `parallelism` conforme necessário.

## Etapa 4: Gravar a Saída – Converter Imagens Escaneadas em Arquivos TXT

Por fim, percorremos o dicionário e gravamos cada trecho de texto em um arquivo *.txt* que compartilha o nome base original. Este é o momento em que **convert scanned images txt** se torna realidade.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### O que o código faz, em português simples

1. **Cria** um motor OCR configurado para inglês.  
2. **Coleta** todos os arquivos TIFF da pasta de destino.  
3. **Executa** `BatchOcr.RecognizeAll` com quatro threads, transformando cada imagem em uma string.  
4. **Percorre** os resultados, substituindo a extensão `.tif` por `.txt` e gravando a string no disco.

Esse é todo o fluxo de **converter TIFF para texto** em menos de 50 linhas de código.

## Lidando com Casos de Borda – Quando as Coisas Não Saem Como Esperado

- **TIFFs ausentes ou corrompidos** – `BatchOcr` lançará uma `OcrException`. Envolva a chamada em um `try / catch` se precisar de degradação graciosa.  
- **Documentos não‑inglês** – altere `OcrLanguage.English` para `OcrLanguage.Spanish`, `OcrLanguage.French`, etc., ou use `OcrLanguage.AutoDetect`.  
- **Imagens muito grandes** – considere reduzir o DPI antes do OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) para economizar memória, embora possa perder alguma precisão.  
- **Codificação da saída** – se precisar de uma página de códigos específica (ex.: Windows‑1252), passe-a para `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## Dicas Profissionais para Conversões em Lote Robustas

- **Registre falhas**: crie uma `List<string> failedFiles` e adicione qualquer arquivo que lançar exceção; escreva a lista em um log após o loop.  
- **Reutilize o motor**: a mesma instância `OcrEngine` pode ser reutilizada em vários arquivos; não a instancie dentro do loop.  
- **Valide o resultado**: um rápido `if (string.IsNullOrWhiteSpace(extractedText))` pode sinalizar escaneamentos em branco ou ilegíveis.  
- **Combine com PDF**: se sua fonte for um PDF multipágina, converta cada página para TIFF primeiro (Aspose.PDF faz isso) e então execute este lote.

## Próximos Passos – Indo Além da Conversão Simples

Agora que você pode **extrair texto de arquivos TIFF** em massa, talvez queira:

- Alimentar os arquivos *.txt* em um índice de busca (Elasticsearch, Azure Cognitive Search).  
- Executar detecção de idioma em cada resultado para encaminhar documentos a pipelines específicos por localidade.  
- Gerar PDFs pesquisáveis sobrepondo o texto OCR nas imagens originais (Aspose.PDF novamente).  

Todos esses cenários se baseiam na mesma ideia central: **conversão em lote de imagem para texto** é um bloco de construção para sistemas maiores de processamento de documentos.

---

### Conclusão

Você acabou de aprender como **converter TIFF para texto** usando Aspose.OCR, processar uma pasta inteira em paralelo e salvar cada resultado como um arquivo *.txt* limpo. A solução é leve, totalmente configurável e pronta para produção — seja digitalizando faturas legadas, arquivando contratos escaneados ou alimentando um motor de busca textual.

Teste, ajuste o paralelismo e comece a alimentar esses novos arquivos de texto ao fluxo de trabalho que precisar. Boa OCR!

---


## Tutoriais Relacionados

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}