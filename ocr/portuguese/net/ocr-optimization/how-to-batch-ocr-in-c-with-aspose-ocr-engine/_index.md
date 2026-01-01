---
category: general
date: 2026-01-01
description: Como fazer OCR em lote usando o Aspose OCR Engine em C#. Aprenda a reconhecer
  texto a partir de imagens e extrair texto de arquivos TIFF com aceleração por GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: pt
og_description: Como fazer OCR em lote em C# com o Aspose OCR Engine. Este guia mostra
  como reconhecer texto em imagens e extrair texto de arquivos TIFF de forma eficiente.
og_title: Como fazer OCR em lote em C# – Guia completo da Aspose
tags:
- OCR
- C#
- Aspose
- GPU
title: Como fazer OCR em lote em C# com o motor OCR da Aspose
url: /pt/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em lote em C# com o mecanismo Aspose OCR

Já se perguntou **como fazer OCR em lote** quando você tem dezenas de documentos escaneados em uma pasta? Você não está sozinho — muitos desenvolvedores enfrentam esse desafio ao passar do reconhecimento de uma única imagem para o processamento de uma coleção inteira. A boa notícia é que o Aspose OCR torna isso muito simples, seja rodando em CPU ou aproveitando a aceleração por GPU.

Neste tutorial vamos percorrer um exemplo completo e executável que **reconhece texto de imagens** e ainda **extrai texto de arquivos TIFF** em massa. Sem atalhos vagos como “veja a documentação” — apenas uma solução autocontida que você pode copiar‑colar e executar hoje.

## Pré‑requisitos

Antes de começarmos, certifique‑se de que você tem:

* .NET 6.0 ou superior instalado (o código tem como alvo o .NET 6, mas o .NET 5 também funciona).
* Pacote NuGet Aspose.OCR para .NET (as versões CPU e GPU estão disponíveis; instale a que corresponde ao seu hardware).
* Uma pasta com alguns arquivos TIFF ou PNG de exemplo que você deseja processar.
* Visual Studio 2022 ou qualquer IDE de sua preferência.

> **Dica profissional:** Se você pretende usar a versão GPU, verifique se o driver da sua placa gráfica está atualizado e se o CUDA 11+ está instalado. O mecanismo reverterá automaticamente para CPU caso não encontre uma GPU compatível.

## Etapa 1 – Configurar o projeto e instalar o Aspose.OCR

### H2: Crie um novo aplicativo de console e adicione o Aspose.OCR

Abra um terminal (ou o Package Manager Console no Visual Studio) e execute:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Se você possui uma licença habilitada para GPU, adicione o pacote GPU em vez disso:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

É isso — seu projeto agora referencia a biblioteca OCR que usaremos para **OCR em lote**.

## Etapa 2 – Inicializar o mecanismo OCR (CPU ou GPU)

### H2: Como fazer OCR em lote – Inicialização do mecanismo

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Por que isso importa:** Ao alternar `UseGpu`, você permite que o Aspose escolha o caminho mais rápido. Se a GPU não estiver disponível, o mecanismo muda silenciosamente para CPU, de modo que seu trabalho em lote nunca falha por falta de hardware.

## Etapa 3 – Coletar os arquivos que você deseja processar

### H2: Reconhecer texto de imagens – Construindo a lista de arquivos

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Observação de caso extremo:** Se você tem uma mistura de formatos, altere o padrão de busca para `"*.*"` e filtre por extensão dentro do laço. Isso mantém o lote flexível.

## Etapa 4 – Processar cada imagem e exibir uma pré‑visualização

### H2: Extrair texto de TIFF – Percorrendo os arquivos

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**O que você verá:** Para cada TIFF, o console imprime algo como:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Essa pré‑visualização confirma que o lote foi concluído sem precisar abrir cada arquivo manualmente.

## Etapa 5 – Salvar os resultados (Opcional, mas útil)

### H3: Persistir a saída OCR em arquivos de texto

Se você precisar do texto completo para processamento posterior, adicione isso dentro do laço `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Agora cada TIFF recebe um arquivo `.txt` acompanhante contendo a saída completa do OCR — perfeito para indexação, busca ou alimentação a um modelo de linguagem.

## Etapa 6 – Executar a demonstração e verificar

1. Compile o projeto: `dotnet build`.
2. Execute: `dotnet run --project GpuBatchDemo.csproj`.

Você deverá ver as linhas de pré‑visualização impressas no console e (se adicionou a etapa opcional) uma série de arquivos `.txt` ao lado das imagens de origem.

### H3: Problemas comuns e como corrigi-los

| Sintoma | Causa provável | Solução |
|---------|----------------|--------|
| **`ocrResult.Text` vazio** | Imagem muito escura ou DPI baixo | Pré‑processar imagens (aumentar contraste, upscale) ou definir `ocrEngine.Settings.PreprocessImage = true`. |
| **Erro GPU “CUDA driver version is insufficient”** | Driver desatualizado | Atualize o driver da GPU ou defina `UseGpu = false` para forçar CPU. |
| **Exceção “File not found”** | Separador de caminho errado em Linux/macOS | Use `Path.Combine` ou barras (`/`). |

## Etapa 7 – Escalando (Além de alguns arquivos)

Quando você passa de algumas dezenas de TIFFs para milhares, considere:

* **Processamento paralelo:** Envolva o `foreach` em `Parallel.ForEach` (garanta que a instância do mecanismo seja thread‑safe; caso contrário, crie uma por thread).
* **I/O em blocos:** Leia imagens em lotes para evitar esgotar a RAM.
* **Log:** Grave o progresso em um arquivo de log; isso ajuda a retomar após uma falha.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Lembre‑se:** A memória da GPU é compartilhada, portanto criar muitas tarefas paralelas de GPU pode, na verdade, diminuir a performance. Teste com poucos threads primeiro.

## Exemplo completo funcional (pronto para copiar e colar)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Executar este programa **reconhecerá texto de imagens**, **extrairá texto de TIFF** e demonstrará **como fazer OCR em lote** de forma eficiente.

---

## Conclusão

Agora você tem um exemplo sólido, de ponta a ponta, de **como fazer OCR em lote** em C# usando o mecanismo OCR da Aspose. O tutorial abordou tudo, desde a configuração do projeto, alternância de aceleração GPU, construção da lista de arquivos, processamento de cada imagem e persistência dos resultados. Seja extraindo texto de arquivos TIFF ou de qualquer outro formato de imagem, o mesmo padrão se aplica — basta trocar as extensões dos arquivos.

Pronto para o próximo passo? Experimente integrar a saída OCR a um índice de busca, alimentar o texto a um modelo de linguagem grande ou testar o processamento paralelo para reduzir minutos em lotes massivos. O céu é o limite, e você já tem a base para construir.

Tem perguntas ou quer compartilhar suas próprias dicas de OCR em lote? Deixe um comentário abaixo — boa codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}