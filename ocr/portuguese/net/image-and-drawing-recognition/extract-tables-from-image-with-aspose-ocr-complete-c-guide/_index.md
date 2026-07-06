---
category: general
date: 2026-05-31
description: Extraia tabelas de imagens usando Aspose OCR em C#. Aprenda como converter
  a imagem em tabela, habilitar a detecção de tabelas e gerar resultados de forma
  eficiente.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: pt
og_description: Extraia tabelas de imagens com Aspose OCR. Este guia mostra como converter
  imagem em tabela, habilitar a detecção de tabelas e tratar os resultados em C#.
og_title: Extrair Tabelas de Imagem – Tutorial C# Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Extrair tabelas de imagem com Aspose OCR – Guia completo em C#
url: /pt/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Tabelas de Imagem – Guia Completo em C#

Já precisou **extrair tabelas de imagem** mas não sabia por onde começar? Você não está sozinho; muitos desenvolvedores encontram esse obstáculo ao tentar transformar notas fiscais ou recibos escaneados em dados utilizáveis. A boa notícia? Com o Aspose OCR você pode **converter imagem em tabela** em apenas algumas linhas de código C#.

Neste tutorial vamos percorrer um exemplo do mundo real: carregar um PNG que contém uma tabela, transformar esse layout visual em uma grade estruturada e imprimir o conteúdo de cada célula com pontuações de confiança. Ao final você terá um trecho totalmente funcional que pode ser inserido em qualquer projeto .NET, além de dicas para lidar com casos de borda e escalar a solução.

## O que você precisará

- **.NET 6.0** ou superior (o código também funciona com .NET Framework 4.6+)
- Pacote NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- Um arquivo de imagem que realmente contenha uma tabela (por exemplo, `invoice_with_table.png`)
- Um IDE básico para C# (Visual Studio, Rider ou VS Code com a extensão C#)

É só isso — sem motores OCR adicionais, sem dependências pesadas. Pronto? Vamos começar.

## Etapa 1: Inicializar o Engine OCR para **Extrair Tabelas de Imagem**

Primeiro, criamos uma instância `OcrEngine` e apontamos para a imagem de origem. Pense no engine como o cérebro que lerá cada pixel e tentará entender o layout.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Por que isso importa:** Sem inicializar o engine corretamente, o OCR não tem nada para analisar e você nunca obterá tabelas da imagem. A chamada `ImageStream.FromFile` também cuida de problemas comuns de formato (PNG, JPEG, BMP) para que você não precise de etapas de conversão extras.

## Etapa 2: Habilitar a Detecção de Tabelas – A Chave para **Converter Imagem em Tabela**

Aspose OCR pode ler texto simples de uma imagem, mas não entenderá magicamente linhas e colunas a menos que você indique que procure por tabelas. É aqui que a flag `DetectTables` entra em ação.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Dica profissional:** Se você precisar apenas do texto bruto, deixe `DetectTables` como `false`. Habilitá‑la adiciona um pequeno overhead, mas o retorno é um resultado limpo e estruturado que pode ser enviado diretamente para uma planilha ou banco de dados.

## Etapa 3: Executar o Reconhecimento OCR – O Momento da Verdade

Agora pedimos ao engine que realmente leia a imagem. O método `Recognize` devolve um objeto `OcrResult` que contém tanto o texto simples quanto quaisquer tabelas detectadas.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **O que acontece nos bastidores?** Aspose executa uma série de etapas de pré‑processamento de imagem (deskewing, binarização) antes de aplicar seu reconhecedor de texto baseado em redes neurais. Quando `DetectTables` está true, ele também realiza uma passagem de análise de layout que agrupa caracteres em linhas e colunas.

## Etapa 4: Iterar Sobre as Tabelas Detectadas – **Extrair Tabelas de Imagem** em Ação

Se o engine encontrou tabelas, elas aparecerão em `result.Tables`. Vamos percorrer cada tabela, depois cada linha e coluna, imprimindo o texto da célula e a porcentagem de confiança.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Por que verificar a confiança?** OCR não é perfeito, especialmente com digitalizações de baixa resolução. O valor `Confidence` (0‑100) permite decidir se aceita a célula como está ou se a sinaliza para revisão manual. Um limiar típico é 80 % para dados críticos.

### Saída Esperada

Assumindo que a imagem de origem contém uma tabela 3 × 4 de itens de fatura, você pode ver algo como:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Se nenhuma tabela for detectada, `result.Tables` ficará vazio — nada a imprimir, mas o programa ainda encerrará graciosamente.

## Etapa 5: Lidando com Casos de Borda e Armadilhas Comuns

### Imagens de Baixa Resolução

Quando sua imagem de origem está abaixo de 150 dpi, o algoritmo de detecção de tabelas pode perder os limites das células. Uma solução rápida é ampliar a imagem usando `System.Drawing` antes de enviá‑la ao Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Tabelas Inclinadas

Se a tabela estiver rotacionada alguns graus, habilite o auto‑deskew:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Múltiplas Tabelas em Uma Página

Aspose OCR devolve cada tabela como um objeto separado em `result.Tables`. Você pode tratá‑las individualmente ou mesclá‑las em um único `DataTable` se precisar de uma visão unificada.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Exportando para Excel

Depois de ter um `DataTable`, exportar para um arquivo `.xlsx` é muito fácil com `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Agora você realmente **converteu imagem em tabela** e pode entregar a planilha para processos subsequentes.

## Exemplo Completo – Do Início ao Fim

Abaixo está o programa completo, pronto para ser executado, que reúne tudo. Cole-o em um novo projeto de console, substitua o caminho do arquivo e pressione **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Explicação do fluxo**

1. **Engine setup** – Carrega a imagem e indica ao Aspose que procure por tabelas.  
2. **Options tuning** – `DetectTables` faz o trabalho pesado; `Deskew` melhora a precisão em digitalizações inclinadas.  
3. **Recognition** – Retorna tanto texto simples quanto uma coleção de objetos `Table`.  
4. **Iteration** – Imprime cada célula com confiança, ao mesmo tempo que constrói um `DataTable` para exportação posterior.  
5. **Export** – Usa `ClosedXML` (uma biblioteca leve, sem interop) para gravar um arquivo `.xlsx` — perfeito para análises ou relatórios downstream.

## Perguntas Frequentes

- **Isso funciona com PDFs?**  
  Sim. Converta cada página PDF em uma imagem primeiro (`PdfRenderer` ou `Ghostscript`), depois alimente o bitmap ao Aspose OCR.

- **Posso extrair tabelas de um JPG?**  
  Absolutamente. O método `ImageStream.FromFile` aceita JPEG, PNG, BMP e TIFF nativamente.

- **E se minha tabela tiver células mescladas?**  
  Aspose OCR trata células mescladas como células lógicas separadas; pode ser necessário pós‑processar a saída para combiná‑las com base na confiança ou em padrões de conteúdo.

- **Existe um limite de tamanho para a tabela?**  
  Na prática, o engine lida com tabelas de até várias centenas de linhas. O desempenho degrada linearmente, portanto considere dividir digitalizações muito grandes.

## Conclusão

Acabamos de mostrar como

## O que Você Deve Aprender a Seguir?

- [Como extrair tabela de imagem usando Aspose.OCR para .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extrair Texto de Imagem – Otimização OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Como Extrair Texto de Imagem Preparando Retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}