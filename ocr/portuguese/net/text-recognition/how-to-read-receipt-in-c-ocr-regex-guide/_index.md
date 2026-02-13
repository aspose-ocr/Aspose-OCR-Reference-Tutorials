---
category: general
date: 2026-02-13
description: Como ler recibos rapidamente usando Aspose OCR e extrair o valor usando
  regex. Aprenda o processamento passo a passo de recibos com OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: pt
og_description: Como ler recibos em C# usando Aspose OCR e regex. Este guia mostra
  como processar recibos com OCR e extrair o valor total.
og_title: Como Ler Recibos em C# – Tutorial Completo de OCR e Regex
tags:
- OCR
- C#
- Regex
- Aspose
title: Como Ler Recibo em C# – Guia de OCR + Regex
url: /pt/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Ler Recibos em C# – Guia OCR + Regex

Já se perguntou **como ler recibos** sem precisar digitar cada linha manualmente? Em muitos aplicativos de pequenas empresas você precisa extrair o valor total de uma foto de um recibo, e fazer isso à mão anula o objetivo da automação. A boa notícia? Com o Aspose OCR você pode deixar o motor fazer o trabalho pesado, e então uma simples expressão regular localizará o total. Neste tutorial vamos percorrer **process receipt with OCR**, extrair o valor usando regex e obter um valor total pronto para uso.

Você verá um exemplo completo e executável, descobrirá por que o modelo de linguagem de recibos importa e receberá dicas para lidar com casos extremos, como diferentes símbolos de moeda ou a ausência do rótulo “Total”. Nenhuma documentação externa é necessária—tudo que você precisa está aqui.

## O Que Você Vai Aprender

- Como configurar o Aspose OCR para reconhecimento específico de recibos (o modelo de linguagem `Receipt` corrige automaticamente a inclinação e o ruído da imagem).  
- Como aplicar uma expressão regular que **extract amount using regex** funciona para a maioria dos recibos no estilo dos EUA.  
- Como lidar com variações comuns como “TOTAL”, “Total:”, ou “Grand Total – $12.34”.  
- Como exibir o resultado de forma segura e o que fazer quando o padrão não for encontrado.  

**Pré‑requisitos**: .NET 6+ (ou .NET Framework 4.7+), uma licença válida do Aspose OCR ou versão de avaliação, e uma imagem de recibo salva localmente. Só isso—nenhum pacote NuGet extra além do Aspose.OCR.

---

## Etapa 1 – Instalar Aspose OCR e Preparar o Projeto

### Por que isso importa

O Aspose OCR fornece um modelo **process receipt with OCR** criado especificamente para saber como endireitar um papel amassado e ignorar ruídos de fundo. Usar o modelo genérico de texto resultaria em mais erros, especialmente em digitalizações de baixa resolução.

### Código

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Dica profissional:** Mantenha o arquivo de licença fora da pasta de controle de versão para evitar commits acidentais.

---

## Etapa 2 – Configurar o Motor OCR para Reconhecimento de Recibos

### Por que isso importa

O modelo de linguagem `Receipt` inclui correção de inclinação e redução de ruído integradas, o que melhora drasticamente a precisão em recibos reais que costumam estar dobrados ou amassados.

### Código

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Etapa 3 – Reconhecer Texto da Imagem do Recibo

### Por que isso importa

Você precisa do texto bruto antes de aplicar qualquer regex. O método `RecognizeImage` devolve um `OcrResult` contendo a string completa, pontuações de confiança e mais, caso precise deles depois.

### Código

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Saída esperada do OCR (exemplo)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Etapa 4 – Construir uma Regex para **Extract Amount Using Regex**

### Por que isso importa

Recibos vêm em muitos formatos, mas a palavra “Total” (ou variante próxima) seguida de um valor em dólares é um ponto de ancoragem confiável. O padrão abaixo tolera espaços opcionais, dois pontos, hífens e um sinal `$` opcional.

### Código

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Explicação do padrão**

| Parte | Significado |
|------|-------------|
| `Total` | Procura a palavra “Total” (ignora maiúsculas/minúsculas). |
| `\s*[:\-]?` | Permite qualquer espaço em branco, seguido de dois pontos ou hífen opcionais. |
| `\s*\$?` | Espaço em branco opcional e sinal de dólar opcional. |
| `(\d+(\.\d{2})?)` | Captura um ou mais dígitos, opcionalmente seguidos de ponto decimal e dois centavos. |

---

## Etapa 5 – Exibir o Total Extraído ou Tratar Dados Ausentes

### Por que isso importa

Mesmo o melhor OCR pode perder uma palavra, especialmente em recibos borrados. Fornecer um fallback elegante evita falhas e oferece um ponto de extensão para lógica personalizada (ex.: solicitar confirmação ao usuário).

### Código

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Exemplo de saída no console**

```
Total: $12.25
```

---

## Exemplo Completo – Todas as Etapas em Um Arquivo

Abaixo está um programa único e autocontido que você pode copiar‑colar em um projeto de console. Inclui comentários, tratamento de erros e o carregamento opcional da licença.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Executando o programa**

1. Crie um novo projeto de console (`dotnet new console -n ReceiptReader`).  
2. Adicione o pacote NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Substitua `YOUR_DIRECTORY/receipt.jpg` pelo caminho real da imagem do recibo.  
4. Compile e execute (`dotnet run`).  

Você deverá ver o dump do OCR seguido de `Total: $xx.xx` se tudo estiver correto.

---

## Tratando Casos Extremos & Variações Comuns

### 1. Diferentes Símbolos de Moeda

Se você trabalha com euros (€) ou libras (£), amplie o padrão:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Rótulo “Total” Ausente

Alguns recibos mostram apenas “Grand Total”. Adicione uma alternância:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Múltiplos Totais (ex.: “Subtotal” e “Total”)

Se a regex encontrar a primeira ocorrência, talvez você queira a **última** correspondência:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Imagens de Baixa Resolução

- Aumente o DPI ao digitalizar (`300 DPI` é um ponto ideal).  
- Pré‑procese a imagem com um filtro simples de redução de desfoque antes de enviá‑la ao Aspose (fora do escopo deste guia, mas vale a pena explorar).

---

## Dicas Profissionais para Projetos Reais

- **Cache o resultado do OCR** se precisar extrair vários campos (imposto, itens, etc.) – você paga o custo do OCR apenas uma vez.  
- **Registre o texto bruto do OCR** em um banco de dados; ele se torna um valioso registro de auditoria para despesas contestadas.  
- Ao construir uma API web, **execute o OCR em um worker em segundo plano**; ele pode levar algumas centenas de milissegundos, o que é aceitável de forma assíncrona, mas não ideal para uma requisição síncrona.  
- **Valide o valor extraído** contra regras de negócio (ex.: valor deve ser > 0) antes de persistir.

---

## Conclusão

Cobrimos **como ler recibos** em C# usando Aspose OCR e **extrair o valor usando regex** para encontrar de forma confiável a linha do total. Ao aproveitar o modelo de linguagem `Receipt` você obtém texto corrigido de inclinação e ruído, e uma expressão regular concisa lida com a maioria das peculiaridades de formatação. O trecho de código completo acima está pronto para ser inserido em qualquer projeto .NET console ou de serviço, e as sugestões de casos extremos fornecem uma base sólida para uso em produção.

Pronto para o próximo passo? Experimente estender a solução para extrair itens individuais, calcular impostos automaticamente ou integrar com uma API de controle de despesas. E se encontrar um recibo que quebre o padrão, lembre‑se de que a abordagem **regex find total** é apenas um ponto de partida—você pode sempre ajustar o padrão para atender ao seu locale específico.

Bom código, e que seu processamento de recibos seja rápido, preciso e totalmente automatizado!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}