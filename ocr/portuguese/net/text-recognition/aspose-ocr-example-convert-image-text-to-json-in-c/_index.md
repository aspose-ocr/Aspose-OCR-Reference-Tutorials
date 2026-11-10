---
category: general
date: 2026-04-17
description: Aprenda um exemplo de Aspose OCR para ler um arquivo de imagem em C#,
  extrair texto da imagem em C# e gravar um arquivo JSON em C#. Tutorial completo
  de OCR em C# passo a passo.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: pt
og_description: Domine um exemplo de Aspose OCR para ler uma imagem, extrair texto
  e gravar um arquivo JSON usando C#. Siga este conciso tutorial de OCR em C#.
og_title: exemplo de Aspose OCR – Converter texto de imagem para JSON em C#
tags:
- Aspose
- OCR
- C#
- JSON
title: exemplo Aspose OCR – Converter texto de imagem para JSON em C#
url: /pt/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# aspose ocr example – Converter Texto de Imagem para JSON em C#

Já precisou de um **aspose ocr example** que não só leia uma imagem, mas também gere um JSON organizado para processamento posterior? Você não está sozinho. Em muitos projetos—automação de faturas, digitalização de recibos ou até arquivamento simples de documentos—os desenvolvedores se deparam com a mesma barreira: “Como obtenho o resultado do OCR em um formato que minha API aceita?”  

A boa notícia? Com Aspose.OCR você pode fazer isso em poucas linhas, e eu vou mostrar exatamente como. Ao final deste guia você saberá como **read image file C#**, **extract text image C#**, e **write JSON file C#**—tudo encapsulado em um tutorial de OCR em C# limpo e reutilizável.

## O que você vai precisar

- .NET 6.0 ou superior (o código também compila com .NET Core)  
- Pacote NuGet Aspose.OCR for .NET (`Install-Package Aspose.OCR`)  
- Uma imagem (`input.jpg`) contendo texto claro e legível por máquina  
- Um editor de texto ou Visual Studio (qualquer IDE serve)  

Sem arquivos de configuração extras, sem mágica oculta—apenas o SDK e uma foto.

## Etapa 1 – Read image file C# com Aspose.OCR

Primeiro de tudo: você precisa fornecer ao motor OCR uma imagem válida. Aspose.OCR espera um objeto `OcrImage`, que pode ser criado diretamente a partir de um caminho de arquivo.

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*Por que isso importa:* Carregar a imagem antecipadamente permite validar a existência do arquivo e capturar problemas de formato antes que o motor comece a processar os pixels. Se o arquivo estiver ausente, `FromFile` lança uma exceção clara que pode ser tratada posteriormente.

## Etapa 2 – Initialize the Aspose OCR engine

Criar o motor é barato, mas você deve envolvê‑lo em uma instrução `using` para que os recursos sejam liberados prontamente.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Dica de especialista:* O motor padrão funciona bem para a maioria dos textos baseados em latim. Se precisar de outro idioma, você pode definir `ocrEngine.Language = Language.YourLanguage;` antes de chamar `Recognize`.

## Etapa 3 – Extract text image C# – Perform the recognition

Agora a parte pesada acontece. O método `Recognize` retorna um objeto `OcrResult` que contém o texto bruto, pontuações de confiança e caixas delimitadoras para cada palavra.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Você perceberá que `ocrResult.Text` contém a string simples, enquanto `ocrResult.Regions` fornece os dados posicionais caso você precise destacar palavras em uma UI.

## Etapa 4 – Write JSON file C# – Serialize the result

Serializar para JSON é simples com `System.Text.Json`. Vamos formatar a saída de forma legível.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Por que usamos `System.Text.Json`*: Ele já vem incluído no .NET, é rápido e não requer dependências extras. Se preferir Newtonsoft, o código muda apenas algumas linhas.

## Etapa 5 – Persist the JSON to disk

Por fim, escreva a string em um arquivo. Isso completa a parte **write json file c#**.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Saída JSON esperada (exemplo)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*Observação:* Os números exatos variarão conforme sua imagem, mas a estrutura permanece a mesma—perfeita para alimentar APIs, bancos de dados ou visualizadores front‑end.

## Tutorial completo de OCR em C# – Todas as etapas combinadas

Abaixo está o programa completo, pronto para copiar e colar, que une tudo. Sem peças faltando, sem atalhos “veja a documentação”.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### Executando o código

1. Substitua os dois caminhos `@"C:\MyProject\…"` pelos seus diretórios reais.  
2. Compile o projeto (`dotnet build`) e execute (`dotnet run`).  
3. Abra `output.json`—você deverá ver uma representação bem estruturada do texto da imagem.

## Perguntas Frequentes & Casos de Borda

**E se a minha imagem estiver borrada?**  
Aspose.OCR oferece opções de pré‑processamento como `ocrEngine.ImagePreprocessOptions.Deskew = true;`. Ative‑as antes de chamar `Recognize` para melhorar a precisão.

**Posso limitar a saída apenas ao texto puro?**  
Claro—basta serializar `ocrResult.Text` em vez do objeto completo:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**Preciso lidar com PDFs de várias páginas?**  
O exemplo foca em uma única imagem, mas você pode percorrer cada página, executar as mesmas etapas e agregar os resultados em um array JSON.

## Dicas Profissionais & Armadilhas

- **Caminhos de arquivo:** Use `Path.Combine` para evitar barras invertidas codificadas, especialmente se algum dia migrar para Linux.  
- **Memória:** Para lotes massivos, reutilize uma única instância de `OcrEngine` ao invés de criar uma nova para cada imagem.  
- **Tamanho do JSON:** Se precisar apenas do texto, descarte a propriedade `Regions` para manter a carga útil pequena.  
- **Verificação de versão:** Este tutorial foi testado com Aspose.OCR 23.9.0; versões mais recentes mantêm a mesma superfície de API, mas sempre confira as notas de lançamento para mudanças incompatíveis.

![Sample OCR JSON output – aspose ocr example](https://example.com/sample-ocr-json.png "aspose ocr example JSON preview")

## Conclusão

Percorremos um **aspose ocr example** completo que lê uma imagem, extrai seu texto e grava o resultado em um arquivo JSON usando puro C#. A solução é autônoma, pronta para produção e fácil de estender—seja para adicionar suporte a idiomas, ajustar limites de confiança ou alimentar o JSON em um serviço downstream.

Se você está buscando o próximo passo, experimente encadear este tutorial com um **C# OCR tutorial** que envie o JSON para o Azure Cognitive Search, ou experimente extrair tabelas de faturas. O céu é o limite quando você tem o JSON em mãos.

Tem alguma variação que gostaria de compartilhar? Deixe um comentário, faça um fork do repositório ou me chame no GitHub. Boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}