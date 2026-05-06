---
category: general
date: 2026-05-06
description: Aprenda a reconhecer texto a partir de imagens usando Aspose OCR em C#.
  Extraia texto de um recibo, carregue a imagem para OCR e veja um exemplo completo
  do Aspose OCR.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: pt
og_description: Aprenda a reconhecer texto em imagens com o Aspose OCR, extrair texto
  de recibos e carregar imagens para OCR em um guia conciso, passo a passo.
og_title: Reconhecer texto de imagem em C# – Tutorial completo de OCR com Aspose
tags:
- C#
- OCR
- Aspose
title: Reconhecer texto de imagem em C# – Tutorial completo de OCR da Aspose
url: /pt/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de imagem em C# – Tutorial Completo de Aspose OCR

Já precisou **reconhecer texto de imagem** mas não tinha certeza de qual biblioteca escolher? Você não é o único—muitos desenvolvedores enfrentam o mesmo problema ao tentar extrair números de um recibo ou escanear um formulário. A boa notícia é que o Aspose OCR torna todo o processo muito fácil, e neste tutorial vamos guiá‑lo através de um **exemplo completo de Aspose OCR** que permite **extrair texto de recibo** em apenas algumas linhas de C#.

Nos próximos minutos você aprenderá como **carregar imagem para OCR**, definir a região exata que contém o valor total, executar o motor e, finalmente, exibir o resultado. Sem referências vagas a documentos externos, sem peças faltando—tudo que você precisa copiar‑colar e executar está aqui. Um pouco de configuração, alguns passos, e você será capaz de reconhecer texto de arquivos de imagem em tempo real.

> **O que você levará consigo**  
> * Um aplicativo console C# executável que reconhece texto de arquivos de imagem.  
> * Entendimento de por que você pode querer limitar o OCR a um retângulo específico (velocidade e precisão).  
> * Dicas para lidar com casos comuns, como recibos borrados ou digitalizações rotacionadas.  

---

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

| Requisito | Por que é importante |
|-----------|----------------------|
| .NET 6.0 SDK (ou posterior) | O Aspose OCR é distribuído como uma biblioteca .NET Standard 2.0 / .NET 5+, portanto qualquer runtime recente funciona. |
| Visual Studio 2022 (ou VS Code) | Um IDE confortável acelera a depuração, mas qualquer editor que compile C# serve. |
| **Aspose.OCR for .NET** pacote NuGet | Esta é a biblioteca central que realmente reconhece texto de imagem. |
| Uma imagem de recibo de exemplo (`receipt.jpg`) | Usaremos este arquivo para demonstrar **extrair texto de recibo**. |

Você pode instalar o pacote NuGet com o seguinte comando:

```bash
dotnet add package Aspose.OCR
```

Depois disso, você está pronto para começar a carregar a imagem para OCR.

---

## Etapa 1: Carregar a imagem para OCR

A primeira coisa que você precisa fazer é apontar o motor para o arquivo que deseja analisar. É aqui que a palavra‑chave secundária **carregar imagem para OCR** aparece naturalmente.

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **Dica profissional:** Se sua imagem estiver na pasta do projeto, você pode usar um caminho relativo como `ocrEngine.SetImage("receipt.jpg");`. Apenas certifique‑se de que o arquivo seja copiado para o diretório de saída (`Copy to Output Directory = PreserveNewest`).

O método `SetImage` aceita qualquer formato que o System.Drawing consiga decodificar (JPEG, PNG, BMP, etc.), portanto você não está limitado a um único tipo de arquivo.

---

## Etapa 2: Definir a região de interesse – **extrair texto de recibo**

Escanear a imagem inteira desperdiça ciclos de CPU e pode introduzir ruído. Ao dizer ao Aspose OCR exatamente onde o valor total está, você aumenta tanto a velocidade quanto a precisão. Esta é a parte onde **extrair texto de recibo**.

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **Por que um retângulo?**  
> O motor OCR trabalha em uma grade de pixels. Quando você o restringe a uma região, ele ignora todo o resto—não há mais caracteres estranhos do logotipo da loja ou da linha de cabeçalho.

Se você não souber as coordenadas exatas, pode usar qualquer visualizador de imagens que mostre a posição dos pixels (por exemplo, Paint.NET) para estimar os números.

---

## Etapa 3: Executar o motor – **reconhecer texto de imagem** (palavra‑chave principal)

Agora a mágica acontece. Você instrui o Aspose a realmente ler os pixels dentro do retângulo que acabou de definir.

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` contém o texto bruto, pontuações de confiança e até as caixas delimitadoras de cada palavra. Para uma demonstração rápida, vamos apenas imprimir o texto simples.

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

Ao executar o programa, você deverá ver algo como:

```
Total amount detected: $23.45
```

Se a saída aparecer confusa, verifique novamente as coordenadas da ROI ou tente aumentar a resolução da imagem.

---

## Etapa 4: Manipular o resultado – aprimorando o **exemplo de Aspose OCR**

Uma solução robusta faz mais do que simplesmente despejar a string no console. Abaixo está um pequeno helper que remove espaços em branco, elimina quebras de linha indesejadas e valida se o valor extraído parece um montante monetário.

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

O helper demonstra um **exemplo realista de Aspose OCR** que você pode inserir em qualquer sistema maior de faturamento.

---

## Etapa 5: Programa completo executável – a demonstração definitiva de **extrair texto de recibo**

Juntando tudo, você obtém um único arquivo pronto para copiar‑colar. Salve como `Program.cs` e execute `dotnet run`.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**Saída esperada**

```
Total amount detected: $23.45
```

Se a imagem do recibo estiver mais escura ou o texto inclinado, você pode ver algo como `Total amount detected: 23,45`. O método `CleanAmount` normaliza isso para um formato decimal padrão.

---

## Armadilhas comuns ao **reconhecer texto de imagem**

### 1. Coordenadas de ROI incorretas
Se o retângulo for muito pequeno, o motor cortará caracteres; se for muito grande, você reintroduz ruído. Use uma ferramenta visual para ajustar os números, ou detecte programaticamente os limites do recibo com uma biblioteca simples de processamento de imagem (por exemplo, OpenCV).

### 2. Digitalizações de baixa resolução
A precisão do OCR cai drasticamente abaixo de 150 dpi. Se você controla o processo de digitalização, mire ao menos 300 dpi. Se estiver preso a um arquivo de baixa resolução, tente `ocrEngine.SetResolution(300);` antes de chamar `Recognize()`.

### 3. Recibos inclinados ou rotacionados
O Aspose OCR pode auto‑rotacionar, mas você precisa habilitá‑lo:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. Configurações de idioma
O idioma padrão é Inglês. Se seu recibo contiver outros alfabetos, defina o idioma explicitamente:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## Casos de borda & variações – expandindo o **exemplo de Aspose OCR**

* **Múltiplos campos:** Quer extrair também a data e o valor do imposto? Basta repetir a etapa de ROI com um novo retângulo e chamar `Recognize()` novamente (ou reutilizar o mesmo motor após redefinir a ROI).  
* **Processamento em lote:** Envolva a lógica em um loop `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` para tratar dezenas de arquivos automaticamente.  
* **Execução assíncrona:** O método `Recognize` é síncrono, mas você pode delegá‑lo a uma thread em segundo plano com `Task.Run` se estiver construindo um aplicativo UI.

---

## Referência visual

![exemplo de reconhecer texto de imagem](/images/ocr-demo.png "Captura de tela mostrando o resultado do Aspose OCR – reconhecer texto de imagem")

*A captura de tela demonstra a saída do console após a execução do programa completo.*

---

## Conclusão

Acabamos de **reconhecer texto de imagem** usando Aspose OCR, percorremos como **carregar imagem para OCR** e construímos um fluxo prático de **extrair texto de recibo** que você pode inserir em qualquer projeto .NET. O **exemplo completo de Aspose OCR** tem apenas algumas linhas, mas cobre os cenários mais comuns: seleção de ROI, limpeza do resultado e tratamento de armadilhas típicas.

Próximos passos? Experimente substituir o retângulo por uma rotina de detecção dinâmica, teste diferentes idiomas ou integre a saída a um banco de dados para rastreamento automático de despesas. O céu é o limite, e com a base que você tem agora, será fácil expandir.

Tem perguntas ou um recibo complicado que se recusa a cooperar?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}