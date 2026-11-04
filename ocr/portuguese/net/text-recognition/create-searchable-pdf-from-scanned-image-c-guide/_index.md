---
category: general
date: 2026-04-26
description: Crie PDF pesquisável a partir de uma imagem escaneada usando Aspose OCR
  em C#. Aprenda como converter a imagem escaneada, extrair texto e gerar um PDF pesquisável
  rapidamente.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: pt
og_description: Crie PDF pesquisável a partir de uma imagem escaneada usando Aspose
  OCR. Código C# passo a passo para converter, extrair texto e gerar um PDF pesquisável.
og_title: Crie PDF pesquisável a partir de imagem escaneada – Guia C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Criar PDF pesquisável a partir de imagem escaneada – Guia C#
url: /pt/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem escaneada – Guia C#

Já precisou **criar PDFs pesquisáveis** a partir de contratos em papel, recibos ou arquivos antigos? Você não está sozinho—a maioria dos desenvolvedores encontra esse obstáculo quando um cliente entrega uma pilha de escaneamentos TIFF e espera um PDF pesquisável como entrega final.  

Neste tutorial vamos mostrar exatamente **como fazer OCR em um documento** e transformar uma imagem escaneada em um **PDF pesquisável** com Aspose OCR para .NET. Ao final, você será capaz de **converter imagens escaneadas**, **extrair texto de imagens** e até lidar com TIFFs de várias páginas sem esforço.

## O que você precisará

* .NET 6.0 ou superior (a API funciona com .NET Core, .NET Framework e .NET 5+).  
* Uma licença válida do Aspose OCR ou você está satisfeito com a marca d'água de avaliação.  
* O pacote NuGet `Aspose.OCR` instalado (`dotnet add package Aspose.OCR`).  
* Um arquivo TIFF de exemplo (por exemplo, `contract_scan.tif`) que você deseja transformar em um PDF pesquisável.

É isso—sem bibliotecas extras, sem configurações complicadas. Pronto? Vamos lá.

![Criar exemplo de PDF pesquisável](create-searchable-pdf.png "criar exemplo de PDF pesquisável")

## Etapa 1 – Inicializar o mecanismo OCR (Criar PDF pesquisável)

Primeiro de tudo: você precisa de uma instância de `OcrEngine`. Esse objeto é o motor que lê o bitmap, identifica os caracteres e devolve o texto para você.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Por que definir o idioma?**  
Se você deixar o padrão, o Aspose tentará todos os pacotes de idioma, o que diminui a velocidade. Especificar `Language.Latin` indica ao motor que ele deve focar no alfabeto latino, proporcionando um ganho de desempenho e resultados mais precisos para contratos em inglês.

## Etapa 2 – Carregar sua imagem escaneada (Converter imagem escaneada)

Agora alimentamos o motor com a imagem que queremos processar. O Aspose pode ler um caminho de arquivo, um stream ou até um `byte[]`. Para simplificar, usaremos `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Se algum dia precisar **converter TIFF para PDF**, lembre-se de que TIFFs de várias páginas são tratados automaticamente—cada quadro se torna uma página PDF separada.

## Etapa 3 – Executar OCR e obter o texto (Extrair texto de imagem)

Executar OCR é tão simples quanto chamar `Recognize`. O motor retornará um `RecognitionResult` que contém o texto puro, pontuações de confiança e informações de layout.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Dica profissional:** Se você precisar apenas do texto (sem PDF), pode parar aqui e gravar `extractedText` em um arquivo `.txt`. Mas na maioria das vezes nosso objetivo é um PDF pesquisável, então continuaremos.

## Etapa 4 – Salvar como PDF pesquisável (Criar PDF pesquisável)

O Aspose torna a etapa final trivial: basta chamar `Save` com `SaveFormat.PdfSearchable`. Por baixo dos panos, a biblioteca incorpora o texto extraído como uma camada invisível enquanto preserva a aparência da imagem original.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Quando você abrir `contract_searchable.pdf` em qualquer visualizador de PDF, poderá selecionar, copiar e pesquisar o texto—exatamente o que o cliente espera de um “PDF pesquisável”.

## Manipulando TIFFs de várias páginas (Converter Tiff para PDF)

Se o seu arquivo de origem contém várias páginas, o Aspose tratará cada quadro como uma página separada automaticamente. Nenhum loop extra é necessário. Contudo, você pode querer controlar o DPI ou a qualidade da imagem para cada página:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Depois de definir essas opções, repita a **Etapa 2** para cada quadro, ou simplesmente aponte `ImageStream.FromFile` para o TIFF de várias páginas e deixe o Aspose fazer o trabalho pesado.

## Armadilhas comuns e como corrigi‑las

| Sintoma | Causa provável | Solução |
|---------|----------------|--------|
| Texto está embaralhado ou ausente | Idioma errado definido | Defina `ocrEngine.Language` para o pacote de idioma correto (ex.: `Language.German`). |
| PDF é muito grande (10 MB para um escaneamento de página única) | Compressão de imagem padrão está baixa | Ajuste `ocrEngine.ImageProcessingOptions.Compression` para `Jpeg` e defina um valor razoável de `Quality` (0‑100). |
| OCR executa muito lentamente | Uso da detecção automática de idioma `Auto` | Defina explicitamente o idioma esperado. |
| Nenhuma camada pesquisável aparece | Salvo com `SaveFormat.Pdf` em vez de `PdfSearchable` | Use `PdfSearchable`. |

## Exemplo completo de ponta a ponta

Juntando tudo, aqui está um aplicativo console pronto‑para‑executar que você pode copiar‑colar no Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**O que você verá:**  
* Uma janela de console que imprime um trecho do texto reconhecido por OCR.  
* Um arquivo `contract_searchable.pdf` ao lado do seu TIFF original. Abra-o, pressione **Ctrl + F** e procure por qualquer palavra que apareceu no escaneamento original—voilà, funciona.

## Próximos passos e tópicos relacionados

* **Como fazer OCR em lotes de documentos** – envolva o código acima em um loop `foreach` e processe uma pasta inteira.  
* **Converter formatos de imagem escaneada** diferentes de TIFF (PNG, JPEG) – a mesma API funciona; basta mudar a extensão do arquivo.  
* **Extrair texto de imagem** para análise adicional – alimente `result.Text` em um pipeline de processamento de linguagem natural.  
* **Otimizar tamanho de PDF** – explore `PdfSaveOptions` para comprimir ainda mais as imagens ou incorporar fontes somente quando necessário.  

Experimente essas ideias, e você rapidamente se tornará a pessoa de referência para qualquer solicitação de “transformar este escaneamento em um PDF pesquisável”.

---

### TL;DR

Agora você sabe como **criar PDFs pesquisáveis** a partir de imagens escaneadas usando Aspose OCR em C#. O processo é: inicializar o motor, carregar a imagem, executar OCR e salvar com `PdfSearchable`. Ajuste as configurações de idioma, DPI e compressão para lidar com casos extremos, e você está pronto para **converter imagens escaneadas**, **extrair texto de imagens**, e até **converter TIFF para PDF** em escala. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}