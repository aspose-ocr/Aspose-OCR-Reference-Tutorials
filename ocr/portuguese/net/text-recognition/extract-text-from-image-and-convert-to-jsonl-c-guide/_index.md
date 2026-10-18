---
category: general
date: 2026-01-02
description: Extrair texto de imagem usando Aspose OCR em C#. Aprenda como converter
  imagem para o formato JSONL de forma rápida e confiável.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: pt
og_description: Extraia texto de imagem com Aspose OCR e converta para o formato JSONL.
  Tutorial completo passo a passo em C# para desenvolvedores.
og_title: Extrair Texto de Imagem – Converter para JSONL em C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Extrair Texto de Imagem e Converter para JSONL – Guia C#
url: /pt/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem e Converter para JSONL – Tutorial Completo em C#

Já precisou **extrair texto de imagem** mas não tinha certeza de qual biblioteca forneceria uma saída limpa e estruturada? Você não está sozinho. Em muitos projetos de processamento de recibos ou digitalização de documentos, o gargalo é transformar um bitmap em texto pesquisável *e* em um formato legível por máquina.  

Boa notícia? Com o Aspose OCR você pode **extrair texto de imagem** e, com algumas linhas de código, **converter imagem para JSONL** para análises posteriores. Este guia leva você por todo o processo, desde carregar um PNG até escrever um arquivo JSON‑Lines que pode ser transmitido para um pipeline de dados.

> **Dica:** Se você já está usando .NET 6 ou superior, o mesmo código funciona sem nenhuma configuração adicional.

## Pré-requisitos — O Que Você Precisa

- **SDK .NET 6** (ou qualquer versão recente do .NET)
- **Aspose.OCR** Pacote NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** para serialização  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Uma imagem de exemplo (por exemplo, `receipt.png`) colocada em uma pasta que você pode referenciar.
- Uma IDE ou editor de sua escolha—Visual Studio, VS Code, Rider, etc.

Sem configuração pesada, sem serviços externos, apenas alguns pacotes NuGet.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: texto extraído de imagem usando C# com Aspose OCR*

## Etapa 1: Carregar a Imagem que Você Deseja Processar  

A primeira coisa que você faz quando quer **extrair texto de imagem** é fornecer ao motor OCR um bitmap. Usar `System.Drawing.Bitmap` é simples e funciona para a maioria dos formatos raster.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Por que isso importa:** Carregar a imagem como um `Bitmap` dá ao motor OCR acesso direto aos pixels, o que melhora a velocidade e a precisão do reconhecimento em comparação com o streaming de bytes brutos.

## Etapa 2: Configurar o Aspose OCR para Saída JSON‑Lines  

Aspose OCR permite especificar idioma, formato de saída e alguns ajustes de desempenho. Aqui solicitamos **JSON‑Lines** (um objeto JSON por linha) porque é perfeito para processamento linha a linha posteriormente.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Dica profissional:** Se precisar de recibos multilíngues, defina `Language = Language.Multilingual` ou passe um array de valores `Language`.

## Etapa 3: Executar o OCR e Capturar o Resultado  

Agora realmente **extraímos texto de imagem**. O método `Recognize` retorna um objeto `OcrResult` que contém uma coleção de objetos `OcrLine`, cada um representando uma linha de texto reconhecido junto com sua caixa delimitadora.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

Neste ponto `ocrResult.Lines` contém tudo que você precisa — texto bruto, pontuações de confiança e coordenadas.

## Etapa 4: Serializar as Linhas para JSON‑Lines  

Transformaremos a coleção em uma string JSON bem identada. Embora JSON‑Lines normalmente seja compacto, adicionar identação facilita a inspeção do arquivo durante o desenvolvimento.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

A variável resultante `jsonLines` fica mais ou menos assim (cortada para brevidade):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Cada linha termina com um caractere de nova linha, fornecendo um verdadeiro **JSONL** (JSON‑Lines) file.

## Etapa 5: Gravar o JSON‑Lines no Disco  

Finalmente, persistimos a saída para que outros serviços — como Spark, Logstash ou um simples script Bash — possam consumi‑la linha a linha.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Ao abrir `receipt.jsonl` você verá um objeto JSON por linha, pronto para streaming.

## Etapa 6: Verificar a Exportação  

Uma verificação rápida de sanidade economiza horas de depuração depois. Vamos ler as primeiras linhas de volta e imprimi‑las no console.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Saída típica do console:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Se você vir algo semelhante, parabéns — você **extraiu texto de imagem** e **converteu imagem para JSONL** com sucesso.

## Armadilhas Comuns & Como Evitá‑las  

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Saída em branco** | Caminho da imagem incorreto ou arquivo não legível. | Use `File.Exists(imagePath)` antes de criar o bitmap. |
| **Pontuações de confiança baixas** | Imagem está borrada ou tem baixo contraste. | Pré‑processar a imagem (ex., `Bitmap.RotateFlip`, `Graphics.Clear`) ou aumentar DPI. |
| **Idioma incorreto** | OCR padrão é Inglês, mas o recibo está em outro idioma. | Defina `options.Language = Language.Spanish` (ou enum apropriado). |
| **JSONL aparece como um único array JSON** | Você usou `Formatting.None` sem tratamento de nova linha. | Garanta que cada objeto serializado termine com `Environment.NewLine`. |

## Exemplo Completo de Funcionamento  

Abaixo está o programa completo, pronto para ser executado. Cole-o em um projeto de console e pressione **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Resultado esperado:** Um arquivo `receipt.jsonl` contendo um objeto JSON por linha, cada um com os campos `Text`, `Confidence` e `BoundingBox`. Agora você pode alimentar esse arquivo em qualquer pipeline de análise que consuma JSONL.

## Próximos Passos – Indo Além do OCR Básico  

- **Processamento em lote:** Envolva a lógica acima em um loop `foreach` para lidar com pastas inteiras de recibos.  
- **Paralelismo:** Use `Parallel.ForEach` para aceleração multi‑core ao lidar com milhares de imagens.  
- **Pós‑processamento:** Remova linhas de baixa confiança (`Confidence < 0.9`) antes de armazenar.  
- **Integração:** Envie o JSONL diretamente para Azure Blob Storage ou AWS S3 com os respectivos SDKs.  
- **Formatos alternativos:** Altere `OutputFormat` para `PlainText` ou `Xml` se seu sistema posterior preferir esses.  

## Conclusão  

Agora você tem uma solução sólida, de ponta a ponta, para **extrair texto de imagem** e **converter imagem para JSONL** usando Aspose OCR em C#. O tutorial cobriu tudo, desde carregar o bitmap até verificar a saída, além de várias dicas práticas para manter seu pipeline robusto.

Experimente com seus próprios recibos, faturas ou formulários digitalizados — veja o motor OCR transformar pixels em dados pesquisáveis e estruturados por linha em segundos. Se encontrar casos extremos (ex., digitalizações inclinadas ou texto multilíngue), revisite a seção *RecognitionOptions* e ajuste idioma ou etapas de pré‑processamento.

Boa codificação, e que seus pipelines de dados estejam sempre limpos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}