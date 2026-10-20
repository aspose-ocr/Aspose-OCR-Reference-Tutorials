---
category: general
date: 2026-04-01
description: Aprenda a reconhecer texto de arquivos PNG rapidamente definindo o ID
  do dispositivo GPU e habilitando a aceleração GPU no Aspose OCR. Guia passo a passo
  em C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: pt
og_description: Reconheça texto de arquivos PNG rapidamente definindo o ID do dispositivo
  GPU. Siga este guia completo em C# para habilitar a aceleração GPU com o Aspose
  OCR.
og_title: reconhecer texto de png – Tutorial de OCR Aspose acelerado por GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: Reconhecer texto de PNG com Aspose OCR – Demonstração em lote acelerada por
  GPU
url: /pt/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconhecer texto de png – Tutorial completo em lote com aceleração GPU em C#

Já precisou **reconhecer texto de png** imagens mas achou o processo dolorosamente lento? Você não está sozinho. A maioria dos desenvolvedores começa com uma chamada simples de OCR, então fica olhando para um console que anda como uma lesma quando uma pasta contém dezenas de capturas de tela.  

A boa notícia? Aspose OCR pode descarregar o trabalho pesado para sua placa de vídeo, e com apenas algumas linhas você pode **set gpu device id** para escolher a GPU exata que deseja. Neste guia vamos percorrer um exemplo completo e executável que coleta todos os PNGs de uma pasta, ativa a aceleração GPU, seleciona a primeira GPU e imprime a contagem de caracteres para cada arquivo.

Ao final você terá um programa autônomo que pode inserir em qualquer projeto .NET, e entenderá por que habilitar a GPU é importante, como lidar com casos extremos e o que ajustar para obter ainda melhor desempenho.

## O que você vai precisar

- **.NET 6.0** ou superior (o código também compila com .NET Core).  
- O pacote **Aspose.OCR** do NuGet – instale-o com `dotnet add package Aspose.OCR`.  
- Uma máquina com GPU compatível com CUDA (NVIDIA é o mais comum) e o driver apropriado.  
- Uma pasta cheia de imagens **PNG** que você deseja processar.  

Se algum desses itens lhe for desconhecido, não entre em pânico. Os passos abaixo incluem os comandos exatos que você precisa, e também discutiremos o que fazer quando uma GPU não estiver presente.

## Etapa 1: Inicializar o motor OCR e habilitar a aceleração GPU  

A primeira coisa que você precisa fazer é criar uma instância de `OcrEngine` e ativar o suporte à GPU. Essa flag indica ao Aspose que ele deve usar as bibliotecas nativas CUDA nos bastidores.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Por que isso importa:** Sem `UseGpuAcceleration`, cada imagem é processada na CPU, o que pode ser várias ordens de magnitude mais lento, especialmente para PNGs de alta resolução. Habilitar a flag também prepara o motor para aceitar um dispositivo GPU específico mais adiante.

## Etapa 2: Definir o ID da GPU (Opcional, mas recomendado)  

Se sua estação de trabalho possui mais de uma GPU, você pode decidir qual usar. Os IDs de dispositivo começam em **0**, então `0` escolhe a primeira GPU, `1` a segunda e assim por diante.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Dica de especialista:** Ao rodar em um servidor compartilhado, definir explicitamente o ID da GPU pode impedir que seu job roube recursos de outros processos. Se você omitir esta linha, o Aspose escolherá o dispositivo padrão, o que geralmente funciona bem em configurações com uma única GPU.

## Etapa 3: Coletar todos os arquivos PNG da sua pasta de lote  

Em seguida precisamos localizar cada PNG que você deseja processar com OCR. O método `Directory.GetFiles` faz o trabalho pesado.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Caso extremo:** Se a pasta estiver vazia, `imageFiles` será um array vazio. Lidaremos com isso mais adiante com uma mensagem amigável.

## Etapa 4: Processar cada imagem e exibir a contagem de caracteres reconhecidos  

Agora o loop principal. Para cada PNG chamamos `Recognize`, então imprimimos o nome do arquivo e o tamanho do texto extraído.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**O que você verá:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Se uma imagem não contiver texto, a contagem será `0`. Isso é perfeitamente normal para capturas de tela que são puramente gráficas.

## Etapa 5: Executar o programa e verificar o uso da GPU  

Compile o arquivo (`dotnet build`) e execute-o (`dotnet run`). Enquanto o console rola, você pode abrir sua ferramenta de monitoramento da GPU (como NVIDIA Smi) para ver o pico de utilização da GPU brevemente para cada imagem. Se não observar nenhuma atividade, verifique novamente:

1. O driver CUDA está instalado.  
2. `UseGpuAcceleration` está definido como `true`.  
3. O `GpuDeviceId` correto corresponde a uma GPU física.

Se a GPU não estiver disponível, o Aspose recairá automaticamente para a CPU, mas você perderá a vantagem de velocidade.

## Variações comuns & dicas  

| Situação | O que mudar |
|-----------|----------------|
| **Formato de imagem diferente** (ex., JPEG) | Alterar o padrão de busca para `*.jpg` ou `*.*` e o Aspose ainda reconhecerá o texto. |
| **Tamanho do lote muito grande** (milhares de arquivos) | Processar em blocos para evitar pressão de memória: dividir `imageFiles` em arrays menores. |
| **Precisa do texto real, não apenas do comprimento** | Substituir `ocrResult.Text.Length` por `ocrResult.Text` no `WriteLine`. |
| **Executando em um servidor sem interface gráfica** | Garantir que o servidor tenha driver de GPU; caso contrário, definir `UseGpuAcceleration = false` para evitar erros desnecessários. |
| **Múltiplas GPUs, deseja balancear a carga** | Percorrer `ocrEngine.GpuDeviceId = i % gpuCount` dentro do `foreach` para rotacionar os dispositivos. |

## Saída esperada & verificação  

Quando tudo funciona, o console imprime cada nome de arquivo seguido da contagem de caracteres, como mostrado anteriormente. Para confirmar a saída real do OCR, você pode temporariamente despejar o texto:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Apenas lembre‑se de remover ou comentar essa linha para lotes grandes; imprimir milhares de linhas pode sobrecarregar seu terminal.

## Exemplo completo funcional (pronto para copiar e colar)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Salve isso como `GpuBatchDemo.cs`, execute `dotnet add package Aspose.OCR` e depois `dotnet run`. Você deverá ver as contagens de caracteres aparecerem quase instantaneamente para cada PNG, graças à aceleração GPU.

## Conclusão  

Agora você sabe como **recognize text from png** arquivos de forma eficiente habilitando a aceleração GPU e definindo explicitamente **set gpu device id** no Aspose OCR. O programa completo, pronto para copiar e colar, trata da descoberta de pastas, verificações de casos extremos e fornece feedback imediato sobre o desempenho do OCR.  

Próximos passos? Experimente trocar a chamada `Recognize` por `ocrEngine.RecognizeAsync` se precisar de processamento não bloqueante, ou experimente diferentes opções de pré‑processamento de imagem (ex., binarização) que o Aspose oferece. Você também pode canalizar os resultados do OCR para um banco de dados ou um índice de busca para uma solução de pesquisa full‑text.

Tem dúvidas sobre como lidar com PDFs de múltiplas páginas, ou quer comparar o Aspose OCR com o Tesseract? Deixe um comentário ou explore nossos outros tutoriais sobre **batch OCR C#**, **OCR performance tips**, e **GPU‑driven image processing**. Feliz codificação!  

![Saída do console mostrando contagens de caracteres reconhecidos para arquivos PNG – reconhecer texto de png usando aceleração GPU](image-placeholder.png "recognize text from png output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}