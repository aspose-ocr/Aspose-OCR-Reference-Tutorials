---
category: general
date: 2026-06-03
description: Exemplo Aspose OCR C# que mostra como definir o limite de memória da
  GPU, carregar imagem para OCR e reconhecer texto de arquivos TIF com código completo
  e dicas.
draft: false
keywords:
- aspose ocr c# example
- set gpu memory limit
- load image for ocr
- recognize text from tif
- gpu acceleration asp ocr
- high‑resolution OCR c#
- asp ocr cuda setup
language: pt
og_description: 'Aprenda um exemplo completo de Aspose OCR em C#: habilite a GPU,
  defina o limite de memória da GPU, carregue uma imagem para OCR e reconheça texto
  de arquivos TIF. Código completo incluído.'
og_title: Exemplo Aspose OCR C# – Aceleração por GPU, Limite de Memória e Processamento
  de TIF
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  headline: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  type: TechArticle
- description: Aspose OCR C# example showing how to set GPU memory limit, load image
    for OCR and recognize text from TIF files with full code and tips.
  name: Aspose OCR C# Example – Enable GPU, Set Memory Limit & Process TIF Images
  steps:
  - name: Why set a memory limit?
    text: '- **Stability:** Prevents out‑of‑memory crashes when processing gigantic
      images. - **Co‑existence:** Allows other GPU‑heavy apps (e.g., TensorFlow models)
      to run side‑by‑side. - **Predictability:** Makes performance testing repeatable
      because the GPU won’t start swapping.'
  - name: Handling multi‑page TIFFs
    text: If your TIFF contains several pages, Aspose OCR will only read the first
      one by default. To process all pages, you can loop over `image.Pages` (available
      in newer SDK versions) and feed each page to the engine separately.
  - name: Why this works well with TIF
    text: '- **Lossless compression:** TIFF often stores raw pixel data, giving the
      OCR engine the highest fidelity. - **Multiple color spaces:** Aspose can handle
      grayscale, RGB, or even CMYK TIFFs without extra conversion code.'
  - name: Expected output
    text: 'Running the program on a clear, 300 dpi scan of a printed page typically
      yields something like:'
  - name: Quick checklist
    text: '- ✅ **Aspose OCR C# example** compiled without errors. - ✅ **GPU enabled**
      (`Enable = true`). - ✅ **GPU memory limit** set to 2048 MB. - ✅ **Image loaded**
      from a TIF file. - ✅ **Text recognized** and printed.'
  type: HowTo
tags:
- Aspose
- OCR
- C#
- GPU
title: Exemplo Aspose OCR C# – Ativar GPU, Definir Limite de Memória e Processar Imagens
  TIF
url: /pt/net/ocr-optimization/aspose-ocr-c-example-enable-gpu-set-memory-limit-process-tif/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exemplo Aspose OCR C# – Ativar GPU, Definir Limite de Memória e Processar Imagens TIF

Já se perguntou como extrair o máximo de desempenho do **Aspose OCR C# example** ao lidar com escaneamentos TIFF massivos? Você não está sozinho. Em muitos projetos reais — pense em digitalizar arquivos ou extrair dados de recibos de alta resolução — o gargalo não é o algoritmo de OCR em si, mas a utilização do hardware.

A verdade é que o Aspose OCR suporta aceleração por GPU, mas você precisa informar exatamente quanta memória ele pode usar, carregar o tipo correto de imagem e, por fim, extrair o texto reconhecido de um arquivo .tif. Este tutorial guia você por cada passo, desde a instalação do SDK até o ajuste das configurações da GPU, para que você possa executar OCR em velocidade impressionante sem estourar a RAM da sua GPU.

Também incluiremos alguns cenários “e se” — como lidar com TIFFs multipáginas ou reverter para CPU quando não houver GPU — para que você termine com uma solução robusta, não apenas um trecho de código pontual.

## O que você vai precisar

Antes de mergulharmos, certifique‑se de que você tem o seguinte na sua máquina:

| Pré‑requisito | Por que é importante |
|--------------|----------------------|
| **.NET 6 SDK** (ou superior) | O Aspose OCR tem como alvo .NET Standard 2.0+, então qualquer versão recente do .NET funciona. |
| **Pacote NuGet Aspose.OCR** (`Install-Package Aspose.OCR`) | A biblioteca principal que fornece `OcrEngine`, `GpuSettings`, etc. |
| **CUDA 11+** (NVIDIA) **ou ROCm 5+** (AMD) | Necessário para aceleração por GPU; o SDK verificará a presença de um driver compatível em tempo de execução. |
| Uma **GPU com pelo menos 2 GB de VRAM** (vamos limitar a 2048 MB) | Sem memória suficiente, o motor pode reverter silenciosamente para CPU. |
| Uma imagem **TIFF de alta resolução** que você deseja processar | O Aspose OCR consegue ler praticamente qualquer formato raster, mas TIF é comum para escaneamentos. |
| Visual Studio 2022 (ou qualquer editor de sua preferência) | Para compilar e depurar o projeto C#. |

Se algum desses itens estiver ausente, o código ainda compilará, mas você não verá os ganhos de desempenho que buscamos.

## Etapa 1: Criar o Motor do Exemplo Aspose OCR C#

A primeira coisa em todo **Aspose OCR C# example** é instanciar o motor de OCR. Pense no `OcrEngine` como o diretor de um filme — ele coordena tudo, desde o carregamento da imagem até a extração do texto.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Dica de especialista:** Se você pretende processar muitas imagens em sequência, mantenha um único `OcrEngine` ativo. Recriar o motor a cada imagem adiciona overhead que pode superar o tempo de OCR.

## Etapa 2: Definir Limite de Memória da GPU (e Habilitar Aceleração)

Agora vem a parte que costuma confundir as pessoas: **definir limite de memória da GPU**. Por padrão, o Aspose OCR tenta usar toda a VRAM disponível, o que em uma estação de trabalho compartilhada pode privar outros aplicativos. O objeto `GpuSettings` permite limitar essa alocação.

```csharp
        // Step 2: Enable GPU acceleration (requires CUDA 11+ or ROCm 5+)
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,          // Turn on the GPU path
            DeviceId = 0,           // First GPU in the system (change if you have multiple)
            MemoryLimitMb = 2048    // Optional cap – 2 GB in this example
        };
```

### Por que definir um limite de memória?

- **Estabilidade:** Impede travamentos por falta de memória ao processar imagens gigantescas.  
- **Co‑existência:** Permite que outros aplicativos pesados em GPU (por exemplo, modelos TensorFlow) rodem lado a lado.  
- **Previsibilidade:** Torna os testes de desempenho repetíveis, pois a GPU não começará a fazer swap.

Se você omitir `MemoryLimitMb`, o Aspose alocará o que considerar necessário, o que pode ser aceitável em um servidor dedicado de inferência, mas arriscado em um laptop de desenvolvedor.

## Etapa 3: Carregar a Imagem para OCR

Carregar o formato de arquivo correto é o próximo passo crucial. O método `OcrImage.FromFile` detecta automaticamente o tipo da imagem, mas ainda assim você deve verificar se o arquivo existe e se ele é uma variante TIFF suportada (por exemplo, compressão LZW ou CCITT‑G4).

```csharp
        // Step 3: Load the high‑resolution image to be processed
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);
```

### Manipulando TIFFs multipáginas

Se o seu TIFF contiver várias páginas, o Aspose OCR lerá apenas a primeira por padrão. Para processar todas as páginas, você pode iterar sobre `image.Pages` (disponível em versões mais recentes do SDK) e alimentar cada página ao motor separadamente.

```csharp
        foreach (var page in image.Pages)
        {
            var result = ocrEngine.Recognize(page);
            System.Console.WriteLine($"--- Page {page.Index + 1} ---");
            System.Console.WriteLine(result.Text);
        }
        return; // Skip the single‑image path below
```

O trecho acima demonstra um padrão **carregar imagem para OCR** que funciona tanto para arquivos de página única quanto para multipáginas.

## Etapa 4: Reconhecer Texto do TIF (ou qualquer raster)

Agora que a imagem está na memória, pedimos ao Aspose que faça a mágica. O método `Recognize` devolve um `OcrResult` que contém o texto puro, pontuações de confiança e até informações de caixa delimitadora, caso você precise delas.

```csharp
        // Step 4: Perform OCR recognition on the image
        var ocrResult = ocrEngine.Recognize(image);
```

### Por que isso funciona bem com TIF

- **Compressão sem perdas:** TIFF costuma armazenar dados de pixel brutos, oferecendo ao motor de OCR a mais alta fidelidade.  
- **Múltiplos espaços de cor:** O Aspose pode lidar com TIFF em escala de cinza, RGB ou até CMYK sem código de conversão extra.

Se precisar ajustar pacotes de idioma (por exemplo, francês ou japonês), defina `ocrEngine.Settings.Language = "fr"` antes de chamar `Recognize`.

## Etapa 5: Exibir o Texto Reconhecido

Por fim, exibimos o texto no console. Em uma aplicação real você poderia gravar em um banco de dados, em um arquivo JSON ou alimentar a string em um pipeline de NLP subsequente.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Saída esperada

Executar o programa em um escaneamento claro, 300 dpi, de uma página impressa normalmente produz algo como:

```
=== OCR Output ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
...
```

Se a imagem estiver borrada ou o limite de memória da GPU for muito baixo, você pode ver caracteres corrompidos ou um resultado truncado. Reduzir `MemoryLimitMb` abaixo da pegada da imagem (geralmente ~1 GB para um TIFF de 6000×8000 pixels) pode fazer o motor reverter automaticamente para CPU.

## Exemplo Completo Funcional

Abaixo está o programa completo, pronto para ser executado. Copie‑e‑cole em um novo projeto Console App, substitua `YOUR_DIRECTORY/large_photo.tif` pelo caminho da sua própria TIFF e pressione **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration and set a memory cap
        ocrEngine.Settings.Gpu = new GpuSettings
        {
            Enable = true,
            DeviceId = 0,
            MemoryLimitMb = 2048 // 2 GB limit – adjust to your GPU size
        };

        // Step 3: Load the image (ensure the file exists)
        var imagePath = "YOUR_DIRECTORY/large_photo.tif";

        if (!System.IO.File.Exists(imagePath))
        {
            System.Console.WriteLine($"Error: File not found -> {imagePath}");
            return;
        }

        var image = OcrImage.FromFile(imagePath);

        // Step 4: Perform OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 5: Output the recognized text
        System.Console.WriteLine("=== OCR Output ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Checklist rápido

- ✅ **Aspose OCR C# example** compilado sem erros.  
- ✅ **GPU habilitada** (`Enable = true`).  
- ✅ **Limite de memória da GPU** definido para 2048 MB.  
- ✅ **Imagem carregada** a partir de um arquivo TIF.  
- ✅ **Texto reconhecido** e impresso.

## Armadilhas Comuns & Como Evitá‑las

| Sintoma | Causa provável | Solução |
|---------|----------------|---------|
| `System.DllNotFoundException: cudart64_110.dll` | Runtime CUDA não instalado ou versão incompatível. | Instale o CUDA 11.x (ou 12.x) compatível com seu driver. |
| OCR devolve string vazia | Imagem muito escura ou DPI < 150. | Pré‑processar com `image.AdjustContrast()` ou reamostrar para 300 dpi. |
| Travamento por falta de memória na GPU | `MemoryLimitMb` muito baixo para a imagem. | Aumente o limite ou divida a imagem em blocos usando `image.Crop`. |
| Erro `Unsupported image format` | TIFF usa compressão exótica (por exemplo, JPEG‑2000). | Converta o TIFF para um formato suportado com ImageMagick antes do OCR. |

## Expandindo a Demonstração

Agora que você tem um **aspose ocr c# example** sólido, pode explorar:

- **Processamento em lote:** Percorrer uma pasta de TIFs, gravando cada resultado em um arquivo `.txt`.  
- **Pacotes de idioma:** `ocrEngine.Settings.Language = "es"` para espanhol, ou carregar dicionários personalizados.  
- **Caixas delimitadoras:** Use `ocrResult.Regions` para obter coordenadas de cada palavra — útil para ferramentas de redação.  
- **Fallback para CPU:** Envolva o bloco de GPU em um try/catch; em caso de falha, defina `ocrEngine.Settings.Gpu.Enable = false` e tente novamente.

Essas extensões mantêm o padrão central intacto enquanto adicionam valor para casos de uso específicos.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}