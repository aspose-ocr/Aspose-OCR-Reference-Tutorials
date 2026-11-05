---
category: general
date: 2026-04-04
description: Como habilitar GPU no Aspose OCR rapidamente. Aprenda a extrair texto
  de imagem, carregar a imagem para OCR e reconhecer texto usando C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: pt
og_description: Como habilitar a GPU no Aspose OCR rapidamente. Siga este tutorial
  para extrair texto de uma imagem, carregar a imagem para OCR e reconhecer texto
  com C#.
og_title: Como habilitar GPU para OCR em C# – Guia Completo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Como habilitar GPU para OCR em C# – Guia passo a passo
url: /pt/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como habilitar GPU para OCR em C# – Guia Completo

Já se perguntou **como habilitar GPU** ao usar Aspose OCR? Talvez você tenha encontrado um gargalo de desempenho ao processar centenas de recibos, e a CPU simplesmente não aguenta. A boa notícia é que ativar a aceleração por GPU é muito fácil, e, uma vez ativada, você verá o motor de OCR disparar através das imagens.

Neste tutorial, não apenas ligaremos a GPU, mas também mostraremos como **carregar imagem para OCR**, **reconhecer texto** e, finalmente, **extrair texto da imagem** usando um exemplo limpo em C#. Ao final, você terá um programa pronto‑para‑executar que extrai texto puro de qualquer imagem suportada — sem serviços externos.

## O que você precisará

- .NET 6+ (ou .NET Framework 4.7.2 ou superior).  
- Aspose.OCR para .NET, versão 24.2.0 ou mais recente (o sinalizador de GPU foi adicionado nesta versão).  
- Uma máquina com GPU habilitada e os drivers apropriados (NVIDIA CUDA 11+ funciona muito bem).  
- Um arquivo de imagem que você deseja processar — pense em um recibo escaneado, uma fatura fotografada ou uma nota manuscrita.

Se já tem tudo isso, ótimo — vamos começar.

## Etapa 1: Como habilitar GPU – Configurar o Motor OCR

A primeira coisa a fazer é dizer ao Aspose OCR para usar a GPU. Isso é feito definindo a propriedade `UseGpu` na instância `OcrEngine`. A propriedade tem o valor padrão `false`, então a ativamos explicitamente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Por que isso importa:** Quando `UseGpu` está `true`, a biblioteca delega os cálculos de matriz pesados ao processador gráfico. Em uma RTX 3060 modesta, você notará a latência cair de vários segundos por imagem para uma fração de segundo.

> **Dica profissional:** Se você estiver executando em um ambiente CI sem interface gráfica, certifique‑se de que o driver da GPU está instalado e que a conta de serviço tem permissão para acessar o dispositivo. Caso contrário, o motor reverterá silenciosamente para o modo CPU.

## Etapa 2: Carregar imagem para OCR – Apontar o Motor para o Seu Arquivo

Em seguida, precisamos **carregar imagem para OCR**. O Aspose OCR aceita qualquer formato de imagem suportado por System.Drawing (PNG, JPEG, BMP, TIFF, etc.). O helper `ImageStream.FromFile` envolve o arquivo no objeto de stream necessário.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Se preferir carregar a partir de um `byte[]` (por exemplo, quando a imagem vem de um banco de dados), você pode usar `ImageStream.FromBytes(byteArray)` — mesmo resultado, apenas uma fonte diferente.

## Etapa 3: Como reconhecer texto – Executar o Processo OCR

Agora que o motor está configurado e a imagem carregada, é hora de **reconhecer texto**. O método `Recognize` faz todo o trabalho pesado e devolve um objeto `OcrResult` que contém o texto puro, pontuações de confiança e até as caixas delimitadoras, caso você precise delas depois.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Você também pode mudar o idioma definindo `ocrEngine.Language = OcrLanguage.French;` antes de chamar `Recognize()`. A aceleração por GPU funciona independentemente do pacote de idioma que você carregar.

## Etapa 4: Como extrair texto da imagem – Exibir o Resultado

Por fim, **extraímos texto da imagem** lendo a propriedade `Text` do objeto de resultado. Para fins de demonstração, vamos apenas exibi‑lo no console, mas você poderia gravá‑lo em um arquivo, em um banco de dados ou enviá‑lo para outro serviço.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Saída esperada** (o texto real será diferente conforme a imagem):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Se precisar dos valores brutos de confiança, pode iterar `ocrResult.Regions` e inspecionar cada `Region.Confidence`.

## Exemplo Completo – Um Arquivo, Pronto para Executar

Abaixo está o programa completo. Copie‑e cole em um novo projeto de console, restaure o pacote NuGet Aspose.OCR e pressione **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Observação:** Substitua `YOUR_DIRECTORY/receipt.jpg` pelo caminho real da sua imagem. Se o programa lançar uma `FileNotFoundException`, verifique novamente o caminho e as permissões do arquivo.

## Perguntas Frequentes & Casos Especiais

### E se a GPU não for detectada?

O Aspose OCR reverterá automaticamente para o modo CPU e registrará um aviso. Para verificar qual modo está ativo, inspecione `ocrEngine.IsGpuEnabled` após a construção — ele retorna `true` somente quando o driver da GPU foi carregado com sucesso.

### Posso processar várias imagens em um loop?

Com certeza. Basta mover a linha `ocrEngine.Image = …` para dentro de um loop `foreach (var file in files)`. Mantenha a mesma instância de `OcrEngine`; reutilizá‑la evita a sobrecarga de alocar recursos de GPU repetidamente.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Como lidar com idiomas que não são inglês?

Defina o idioma antes de chamar `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

A aceleração por GPU funciona da mesma forma; apenas o modelo de idioma muda.

### E quanto a fotos grandes e de alta resolução?

Se você encontrar erros de falta de memória, reduza a escala da imagem primeiro. O Aspose OCR oferece `ImageHelper.Resize` — uma maneira rápida de diminuir o tamanho sem perder muitos detalhes.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Conclusão

Cobremos **como habilitar GPU** para o Aspose OCR, mostramos como **carregar imagem para OCR**, passamos por **como reconhecer texto** e demonstramos **como extrair texto da imagem** com um programa C# conciso e pronto para produção. Ao alternar o sinalizador `UseGpu`, você obtém um aumento de velocidade perceptível, especialmente ao processar lotes de recibos, faturas ou qualquer fluxo de documentos de alto volume.

Pronto para o próximo passo? Experimente combinar este pipeline de OCR com um banco de dados para armazenar os recibos extraídos, ou alimente o texto puro em um modelo de processamento de linguagem natural para categorizar despesas. Você também pode explorar a coleção `OcrResult.Regions` para obter coordenadas de caixas delimitadoras e criar uma UI que destaque cada palavra na imagem original.

Boa codificação e aproveite a potência extra que a aceleração por GPU traz para suas cargas de trabalho de OCR! 

---

![ilustração de como habilitar gpu](gpu-ocr-diagram.png "ilustração de como habilitar gpu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}