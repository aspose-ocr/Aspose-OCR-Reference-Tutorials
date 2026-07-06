---
category: general
date: 2026-03-28
description: Aprenda como extrair tabelas de imagens com Aspose OCR em C#. Este guia
  aborda como detectar tabelas em imagens, carregar a imagem para OCR e extrair tabelas
  de arquivos PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: pt
og_description: Tutorial passo a passo sobre como extrair tabelas de imagens com Aspose
  OCR em C#. Inclui código, explicações e dicas para detectar tabelas em arquivos
  de imagem.
og_title: Como extrair tabelas de imagens usando Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Como extrair tabelas de imagens usando Aspose OCR (C#)
url: /pt/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Extrair Tabelas de Imagens usando Aspose OCR (C#)

Já se perguntou **como extrair tabelas** de uma fatura escaneada ou de uma captura de tela de uma planilha? Você não está sozinho. Em muitos projetos reais precisamos transformar a foto de uma tabela em algo que possamos consultar — geralmente um CSV ou um DataTable. A boa notícia? O Aspose OCR torna isso muito simples, e você pode fazer isso em apenas algumas linhas de C#.

Neste tutorial vamos percorrer todo o processo: desde **carregar a imagem para OCR**, até **detectar tabelas na imagem**, e finalmente **extrair a tabela da imagem** e salvá‑la como um arquivo CSV. Ao final, você terá um aplicativo console pronto‑para‑executar que pode **extrair tabelas de arquivos PNG** (ou qualquer bitmap suportado) sem complicações.

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem:

- .NET 6.0 SDK ou superior (o código também funciona com .NET Framework)
- Visual Studio 2022 (ou qualquer IDE de sua preferência)
- Um arquivo de licença do Aspose.OCR for .NET (você pode começar com uma avaliação gratuita)
- Uma imagem de exemplo contendo uma tabela (por exemplo, `invoice_table.png`)

Se algum desses itens lhe for desconhecido, não se preocupe — basta instalar o .NET SDK e obter o pacote NuGet, e você estará pronto para prosseguir.

## Visão Geral da Solução

Em alto nível, o fluxo de trabalho se parece com isto:

1. **Carregar a imagem** que você deseja processar.  
2. **Executar o reconhecimento OCR** para que o motor saiba onde o texto está localizado.  
3. **Criar um TableExtractor** que analisa os resultados do OCR em busca de estruturas semelhantes a grades.  
4. **Extrair todas as tabelas detectadas** e escolher a que você precisa.  
5. **Salvar a tabela** como CSV (ou qualquer outro formato que preferir).

Cada passo é explicado em detalhes abaixo, com trechos de código completos que você pode copiar‑colar.

<img src="table_extraction_example.png" alt="exemplo de como extrair tabelas de imagem" width="600">

*(A imagem acima mostra uma tabela de fatura de exemplo que iremos extrair.)*

## Etapa 1 – Carregar a Imagem para OCR

A primeira coisa que você precisa fazer é informar ao Aspose OCR qual arquivo deve ser lido. A biblioteca suporta PNG, JPEG, BMP, TIFF e alguns outros formatos. Aqui está o código mínimo:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Por que isso importa:**  
`Image.FromFile` realiza o trabalho pesado de decodificar o PNG (ou qualquer outro bitmap) para um formato que o motor OCR consegue entender. Se você pular essa etapa ou passar um arquivo corrompido, a chamada subsequente a `Recognize()` lançará uma exceção.

> **Dica:** Se você estiver lidando com PDFs grandes, extraia cada página como imagem primeiro — caso contrário, o motor OCR pode ficar sem memória.

## Etapa 2 – Reconhecer a Página (Obrigatório Antes da Detecção de Tabelas)

O reconhecimento converte os dados brutos de pixels em um layout de texto pesquisável. Sem essa etapa, o `TableExtractor` não tem nada para trabalhar.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**O que está acontecendo nos bastidores?**  
O Aspose OCR executa um detector de texto baseado em rede neural e, em seguida, cria uma hierarquia de objetos `Page`, `Paragraph` e `Word`. O detector de tabelas examina posteriormente as relações espaciais entre essas palavras.

Se você estiver processando muitas imagens em um loop, considere reutilizar a mesma instância de `OcrEngine` e apenas trocar a propriedade `Image` — isso reduz a sobrecarga de alocação.

## Etapa 3 – Criar um TableExtractor e Detectar Tabelas na Imagem

Agora que os dados OCR existem, podemos pedir ao Aspose para encontrar tabelas. A classe `TableExtractor` faz exatamente isso.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Por que usar `ExtractAll()`?**  
Uma única imagem pode conter várias tabelas (pense em um relatório com múltiplas seções). `ExtractAll()` devolve uma `List<Table>` para que você possa iterar, escolher a correta ou até mesclá‑las depois.

Se você precisar apenas da primeira tabela, pode usar com segurança `extractedTables[0]`, mas sempre verifique se a lista não está vazia para evitar `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Etapa 4 – Salvar a Tabela Extraída como CSV (ou Qualquer Outro Formato)

O Aspose torna a exportação trivial. A classe `Table` possui métodos integrados `SaveCsv`, `SaveXls` e `SaveJson`. Veja como gravar um arquivo CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Como fica o CSV?**  
Assumindo que a imagem de origem continha uma grade 4 × 3, o CSV pode aparecer assim:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Você pode abrir esse arquivo no Excel, Power BI ou alimentá‑lo diretamente em seu pipeline de dados.

## Exemplo Completo de Ponta a Ponta

Abaixo está o programa completo e autocontido. Copie‑o para um novo projeto console (`dotnet new console`) e execute. Certifique‑se de que o pacote NuGet `Aspose.OCR` está instalado (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Saída Esperada

Ao executar o programa, você deverá ver algo semelhante a:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Abra `invoice_table.csv` e você encontrará as linhas e colunas espelhando a imagem original.

## Perguntas Frequentes & Casos de Borda

### E se a imagem for JPEG em vez de PNG?

O mesmo código funciona — basta mudar a extensão do arquivo em `Image.FromFile`. O Aspose OCR detecta o formato automaticamente, portanto **extrair tabelas de png** não é um requisito rígido; ele funciona com qualquer bitmap suportado.

### Minha tabela tem células mescladas. Elas serão preservadas?

Células mescladas são tratadas como colunas separadas na saída CSV porque o CSV não suporta mesclagem. Se você precisar de formatação mais rica (por exemplo, Excel com células mescladas), use `SaveXls`:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### A detecção perdeu uma coluna. Como melhorar a precisão?

- Aumente a resolução da imagem (≥300 dpi é ideal).  
- Pré‑procese a imagem: converta para escala de cinza, aumente o contraste ou aplique um filtro de correção de inclinação.  
- Ajuste as configurações do Aspose OCR, como `PageSegMode` ou `Language`, se a tabela contiver caracteres não latinos.

### Posso extrair tabelas de um PDF diretamente?

Sim. Converta cada página do PDF em imagem primeiro (usando `Aspose.PDF` ou qualquer biblioteca de PDF‑para‑imagem) e, em seguida, alimente essas imagens ao mesmo fluxo de trabalho.

## Dicas para Implementações Prontas para Produção

1. **Envolva o OCR em try/catch** – ambientes com licença de rede podem lançar exceções de licenciamento.  
2. **Dispose dos objetos `Image`** – envolva‑os em blocos `using` para liberar recursos nativos.  
3. **Registre os scores de confiança** – `TableExtractor` expõe `Table.Confidence` que você pode armazenar para monitoramento de qualidade.  
4. **Processamento em lote** – ao lidar com centenas de faturas, paralelize as chamadas ao OCR, mas respeite as diretrizes de segurança de threads da licença.

## Próximos Passos

Agora que você sabe **como extrair tabelas** de imagens, pode explorar:

- **Detectar tabelas em vídeos** (usando o `TableExtractor` do Aspose em cada frame).  
- **Carregar imagem para OCR** a partir de uma API web, habilitando serviços de extração de tabelas baseados em nuvem.  
- **Extrair tabelas de arquivos PNG** armazenados no Azure Blob Storage, integrando com Azure Functions para processamento serverless.

Sinta‑se à vontade para experimentar diferentes formatos de arquivo, ajustar as configurações do OCR ou encaminhar a saída CSV diretamente para um banco de dados. O céu é o limite.

---

*Feliz codificação! Se você encontrou algum obstáculo ou tem ideias de melhoria, deixe um comentário abaixo. Vamos descobrir juntos.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}