---
category: general
date: 2026-03-18
description: Extrair tabela de imagem usando Aspose OCR em C#. Aprenda como converter
  a tabela para JSON, obter o JSON da tabela e extrair texto da imagem em minutos.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: pt
og_description: Extraia tabela de imagem usando Aspose OCR em C#. Aprenda a converter
  a tabela para JSON, obter o JSON da tabela e extrair texto da imagem rapidamente.
og_title: Extrair Tabela de Imagem com Aspose OCR – Guia Completo em C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: Extrair Tabela de Imagem com Aspose OCR – Guia Completo em C#
url: /pt/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Tabela de Imagem – Guia Completo em C#

Já precisou **extrair tabela de imagem** mas não sabia qual biblioteca faria isso sem uma montanha de parsing manual? Você não está sozinho. Em muitos projetos de processamento de faturas ou digitalização de recibos, o ponto crítico é transformar um bitmap ruidoso em uma tabela estruturada que seu sistema downstream possa consumir.  

A boa notícia? Com Aspose OCR você pode **converter tabela para JSON** em poucas linhas, e ainda obtém o texto puro de toda a imagem, então **extrair texto de imagem** é um bônus. Neste tutorial vamos percorrer todo o fluxo – desde o carregamento da imagem até obter uma representação JSON organizada da tabela detectada.

> **Quick win:** Ao final você terá um aplicativo console C# executável que imprime tanto o texto OCR bruto quanto uma string JSON que pode ser enviada diretamente para um banco de dados ou uma API.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- .NET 6.0 SDK (ou qualquer versão recente do .NET) instalado.  
- Uma licença válida do Aspose OCR ou um teste gratuito (a biblioteca funciona sem licença, mas adiciona marca d'água).  
- Uma imagem que realmente contenha uma tabela – por exemplo `invoice_table.png`.  
- Visual Studio 2022, VS Code ou qualquer editor de sua preferência.

Nenhum pacote NuGet extra além de `Aspose.OCR` é necessário.

## Etapa 1: Configurar o Projeto e Instalar Aspose OCR

Primeiro, crie um novo projeto console e adicione a biblioteca OCR.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Se você estiver usando um proxy corporativo, adicione a flag `--no-restore` e execute `dotnet restore` depois, configurando as variáveis de ambiente apropriadas.

## Etapa 2: Inicializar o OCR Engine e Habilitar Reconhecimento de Tabelas

O coração da solução é o `OcrEngine`. Ao habilitar `EnableTableRecognition` informamos ao Aspose OCR para procurar estruturas semelhantes a grades em vez de tratar tudo como texto simples.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Por que essa etapa é crucial? Sem o reconhecimento de tabelas, o engine achatará a imagem em uma única string, tornando impossível reconstruir linhas e colunas depois. Habilitá‑lo adiciona uma fase leve de análise de layout que quase não impacta o desempenho, mas traz enormes benefícios downstream.

## Etapa 3: Carregar Sua Imagem e Executar o Reconhecimento

Agora apontamos o engine para o arquivo que contém a tabela. `ImageStream.FromFile` aceita os formatos mais comuns (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Se a imagem for grande, considere redimensioná‑la primeiro para acelerar o processamento. Aspose OCR detecta DPI automaticamente, mas uma varredura de 300 DPI costuma ser o ponto ideal para a maioria das tabelas.

## Etapa 4: Extrair o Texto Puro – “extract text from image”

Mesmo que nosso objetivo principal seja a tabela, você frequentemente ainda precisará do texto bruto para logs ou processamento de fallback.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

A propriedade `Text` concatena tudo que o engine vê, preservando quebras de linha. Isso é útil quando você precisa verificar se o OCR leu corretamente cabeçalhos ou rodapés fora da área da tabela.

## Etapa 5: Obter a Tabela Detectada como JSON – “convert table to json” & “get table json”

Aqui é onde a mágica acontece. `GetTableAsJson()` serializa as linhas, colunas e conteúdos das células detectadas em uma string JSON limpa.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

O JSON resultante tem a seguinte aparência (formatado para legibilidade):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Por que JSON é o formato preferido? É independente de linguagem, fácil de desserializar em objetos e funciona muito bem com APIs web modernas. Se precisar de CSV, basta iterar sobre as linhas e juntar os textos das células com vírgulas.

## Etapa 6: (Opcional) Converter o JSON para um Objeto .NET – “convert image to json”

Se você prefere trabalhar com tipos fortes, desserialize o JSON usando `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Você definiria `TableModel`, `RowModel` e `CellModel` para corresponder ao esquema JSON. Esta etapa mostra como ir de **convert image to json** até um objeto tipado, facilitando a validação downstream.

## Exemplo Completo Funcional

Juntando tudo, aqui está o programa completo, pronto‑para‑executar. Salve como `Program.cs` dentro da pasta do projeto criada anteriormente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Saída Esperada

Ao executar `dotnet run`, você deverá ver algo semelhante a:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Se a saída aparecer vazia, verifique se `EnableTableRecognition` está definido como `true` e se a imagem realmente contém linhas de grade claras.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Nenhum JSON retornado** | Detecção de tabela desativada ou imagem com baixo contraste. | Garanta `ocrEngine.Settings.EnableTableRecognition = true` e melhore a qualidade da imagem (aumente contraste, binarize). |
| **Linhas parciais** | OCR confuso por células mescladas ou texto rotacionado. | Pré‑processar a imagem: corrigir inclinação (`ImageProcessor.Rotate`) ou dividir manualmente células mescladas. |
| **Texto Unicode ilegível** | Fonte não reconhecida (ex.: escrita à mão). | Troque pacotes de idioma via `ocrEngine.Language = Language.English;` ou use outro engine OCR para manuscritos. |
| **Desempenho lento** | Imagem muito grande (>5 MP). | Reduza para ~1500 px de largura mantendo o DPI. |

## Próximos Passos: Indo Além do Básico

Agora que você pode **extrair tabela de imagem** e **converter tabela para JSON**, considere estas extensões:

- **Persistir o JSON** em um banco de dados com Entity Framework.  
- **Pós‑processar** o JSON para normalizar formatos de moeda (ex.: remover `$`).  
- **Processar em lote** uma pasta de faturas usando `Directory.GetFiles` e paralelizar com `Parallel.ForEach`.  
- **Integrar** com Azure Functions ou AWS Lambda para pipelines OCR serverless.

Cada um desses tópicos naturalmente traz os outros termos secundários como **convert image to json** (quando você envia todo o resultado OCR para um endpoint na nuvem) e **get table json** para análises downstream.

---

### Conclusão

Acabamos de mostrar como **extrair tabela de imagem** usando Aspose OCR, transformar essa tabela em JSON limpo e até desserializá‑la em objetos C#. O mesmo padrão

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}