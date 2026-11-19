---
category: general
date: 2026-04-04
description: Aprenda como usar o Aspose para extrair dados de recibos, carregar a
  imagem do recibo e fazer OCR da imagem do recibo com um exemplo completo em C#.
  Guia passo a passo para desenvolvedores.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: pt
og_description: Como usar o Aspose para extrair dados de recibo de uma imagem de recibo
  escaneada. Código C# completo, explicações e dicas para o processamento de imagens
  de recibos com OCR.
og_title: Como usar o Aspose – Extrair dados de recibos de imagens
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Como usar o Aspose – Extrair dados de recibos de imagens em C#
url: /pt/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar Aspose – Extrair Dados de Recibo de Imagens em C#

Já se perguntou **como usar Aspose** para extrair informações estruturadas de uma foto de um recibo? Você não está sozinho. Seja construindo um aplicativo de controle de despesas ou automatizando a entrada de faturas, o ponto problemático é o mesmo: você tem um PNG ou JPEG e precisa do nome do estabelecimento, data e valor total sem digitação manual.

Veja só—Aspose.OCR torna todo esse pipeline muito fácil. Neste tutorial, vamos percorrer o carregamento de uma imagem de recibo, executar OCR e, finalmente, extrair os dados do recibo com algumas linhas de C#. Ao final, você terá um programa de console executável que imprime o estabelecimento, a data e o valor total diretamente no console.

> **Resultado rápido:** Se você só precisa do código, vá direto para a seção “Exemplo Completo em Funcionamento” na parte inferior e copie‑cole.

## O que você precisará

- **.NET 6.0 ou posterior** (a API funciona com .NET Core e .NET Framework)
- **Aspose.OCR for .NET** pacote NuGet (`Install-Package Aspose.OCR`)
- Uma imagem de recibo de exemplo (PNG, JPG ou BMP) salva localmente
- Visual Studio 2022 ou qualquer editor que suporte projetos C#

Nenhuma outra biblioteca de terceiros é necessária. O único pré-requisito é um entendimento básico de aplicativos de console C#—se você já escreveu “Hello World”, está pronto para prosseguir.

## Etapa 1 – Instalar e Referenciar Aspose.OCR

Para **como usar Aspose**, você primeiro precisa da biblioteca no seu projeto. Abra o Console do Gerenciador de Pacotes e execute:

```powershell
Install-Package Aspose.OCR
```

Alternativamente, use a UI do NuGet e procure por “Aspose.OCR”. Uma vez instalado, adicione os namespaces necessários no topo do seu arquivo:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Dica profissional:** Mantenha seus pacotes NuGet atualizados. A partir de hoje (abril 2026) a versão estável mais recente é 23.11.0, que inclui melhorias de desempenho para OCR em recibos de alta resolução.

## Etapa 2 – Carregar a Imagem do Recibo

Ao **carregar imagem de recibo**, você tem duas fontes comuns: um caminho local ou um stream de uma requisição web. Para este tutorial, vamos manter simples e ler do disco:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Substitua `YOUR_DIRECTORY/receipt.png` pelo caminho real do seu arquivo de recibo. Se você estiver lidando com uploads de usuários, pode fornecer um `MemoryStream` para `ImageStream.FromStream`.

> **Por que isso importa:** Especificar o idioma (English) informa ao motor OCR qual conjunto de caracteres esperar, reduzindo reconhecimentos falsos—especialmente importante quando você **ocr receipt image** que contém números e símbolos.

## Etapa 3 – Executar OCR e Capturar Informações de Layout

A etapa de OCR faz mais do que simplesmente gerar texto bruto; ela também captura o layout, que é crucial para a extração estruturada posteriormente.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Depois que `Recognize()` termina, o `ocrEngine` contém tanto o texto simples quanto os dados posicionais de cada palavra. Esta é a base para a próxima etapa, onde pediremos ao Aspose para “**how to extract receipt**” campos automaticamente.

## Etapa 4 – Inicializar o Reconhecedor de Layout

Aspose fornece a classe `LayoutRecognizer` que sabe como os recibos são tipicamente organizados (estabelecimento no topo, linha de data, total próximo ao final). Você simplesmente passa o motor OCR configurado:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

Nos bastidores, o reconhecedor aplica um conjunto de heurísticas—como procurar símbolos de moeda ou padrões de data—para mapear texto bruto para campos semânticos.

## Etapa 5 – Extrair Dados Estruturados do Recibo

Agora vem a parte boa: **extract receipt data**. Uma chamada de método faz o trabalho pesado:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` é um objeto do tipo `ReceiptData` (definido em `Aspose.OCR.Structured`). Ele contém três propriedades principais:

- `Merchant` – o nome da loja
- `Date` – a data da compra como um `DateTime` (se detectada)
- `TotalAmount` – o valor total como um `decimal`

Se o motor não conseguir encontrar um campo específico, a propriedade será `null` ou `0`. Você pode adicionar lógica de fallback se necessário (por exemplo, solicitar ao usuário que confirme).

## Etapa 6 – Exibir as Informações Extraídas

Finalmente, exiba os resultados no console. É aqui que você vê os frutos do seu trabalho:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

As strings de formato (`:d` e `:C`) produzem, respectivamente, uma data curta e uma string de moeda, tornando a saída legível para humanos.

### Saída Esperada

Assumindo que o recibo pertence a “Coffee Corner”, datado de 2025‑12‑01, com um total de $4.75, o console exibirá:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Se algum campo estiver ausente, você verá uma linha vazia ou um valor padrão—perfeito para depuração.

## Casos de Borda & Armadilhas Comuns

### 1. Imagens de Baixa Resolução

Se a imagem do recibo estiver borrada ou com menos de 150 dpi, a precisão do OCR cai drasticamente. Redimensionar a imagem com um filtro bilinear simples antes de enviá-la ao Aspose pode melhorar os resultados.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Recibos Não‑Inglês

O exemplo principal usa `Language.English`. Para recibos multilíngues, defina `Language` para o enum apropriado (por exemplo, `Language.French`) ou use `Language.AutoDetect` se não tiver certeza.

### 3. Vários Recibos em Uma Imagem

O reconhecedor de layout da Aspose espera um único recibo por imagem. Se você tem uma foto de vários recibos lado a lado, precisará pré‑processar a imagem—cortar cada recibo em seu próprio arquivo antes de executar OCR.

### 4. Símbolo de Moeda Ausente

Às vezes o valor total aparece sem o sinal `$`. O reconhecedor ainda captura os números, mas pode ser necessário pós‑processar a string para garantir a colocação decimal correta.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Dicas Profissionais para Produção

- **Cache the OCR engine** se você processar muitos recibos em lote; reutilizar a mesma instância reduz a sobrecarga de alocação.
- **Log the raw OCR text** (`ocrEngine.Text`) para trilhas de auditoria. É útil quando um campo falha ao ser extraído.
- **Wrap the entire flow in a try/catch** e exiba uma mensagem de erro amigável (por exemplo, “Unable to read receipt, please upload a clearer image”).

## Exemplo Completo em Funcionamento

Abaixo está um aplicativo de console autônomo que você pode compilar e executar como está. Basta substituir o caminho da imagem e você está pronto para usar.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Executando o código**

1. Crie um novo projeto de console .NET (`dotnet new console -n ReceiptExtractor`).
2. Adicione o pacote Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Substitua o `Program.cs` gerado pelo trecho acima.
4. Coloque uma imagem de recibo no caminho que você especificou.
5. Compile e execute (`dotnet run`).

Você deverá ver o estabelecimento, a data e o total impressos exatamente como mostrado anteriormente.

## Conclusão

Neste guia, abordamos **how to use Aspose** para **load receipt image**, executar **ocr receipt image**, e finalmente **extract receipt data** com apenas algumas linhas. O principal aprendizado é que o Aspose.OCR faz o trabalho pesado—uma vez que o motor OCR está configurado, o `LayoutRecognizer` transforma texto bruto em um objeto estruturado em que você pode confiar.

Próximos passos? Tente inserir os valores extraídos em um banco de dados, gerar um resumo de recibo em PDF, ou até mesmo alimentá‑los a um modelo de machine‑learning para classificação de despesas. Você também pode experimentar outros tipos de documentos estruturados, como faturas ou etiquetas de envio—`ExtractInvoiceData` da Aspose funciona de forma muito semelhante.

Tem perguntas sobre casos de borda ou quer ver como lidar com PDFs de várias páginas? Deixe um comentário ou consulte a documentação oficial do Aspose.OCR para cenários avançados. Boa codificação, e aproveite a simplicidade de **how to use Aspose** para automação de recibos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}