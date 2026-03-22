---
category: general
date: 2026-03-21
description: Aprenda a corrigir a inclinação de arquivos de imagem e reconhecer texto
  em imagens com o Aspose OCR. Converta JPG em texto e corrija a rotação da imagem
  em poucas linhas de código C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: pt
og_description: Como corrigir a inclinação de imagens e extrair texto de JPEGs usando
  o Aspose OCR. Siga este guia passo a passo para converter JPG em texto e corrigir
  a rotação da imagem.
og_title: Como Desinclinar Imagem em C# – Tutorial Rápido de OCR da Aspose
tags:
- OCR
- C#
- Aspose
title: Como Desinclinar Imagem em C# – Guia Completo Usando Aspose OCR
url: /pt/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Desinclinar Imagem em C# – Guia Completo Usando Aspose OCR

Já se perguntou **como desinclinar imagem** arquivos que saíram de um scanner inclinado em um ângulo estranho? Você não está sozinho—muitos desenvolvedores enfrentam esse problema ao tentar extrair texto de recibos, faturas ou notas manuscritas. A boa notícia é que com Aspose OCR você pode corrigir a rotação da imagem e obter texto limpo e pesquisável em apenas algumas linhas.

Neste tutorial vamos percorrer todo o processo: desde a instalação da biblioteca, habilitação da desinclinação automática, até o reconhecimento de texto na imagem e, finalmente, a conversão de um JPG para texto. Ao final, você terá um aplicativo de console pronto‑para‑executar que **reconhece arquivos jpg de texto** sem precisar rotacioná‑los manualmente primeiro.

## O que Você Precisa

- **.NET 6.0** ou superior (o código funciona tanto no .NET Core quanto no .NET Framework)  
- Pacote NuGet **Aspose.OCR for .NET** – recomenda‑se a versão 23.12 ou mais recente  
- Um **JPEG inclinado** de exemplo (por exemplo, `skewed_receipt.jpg`) colocado em algum lugar que seu aplicativo possa ler  
- Visual Studio, VS Code ou qualquer editor C# de sua preferência  

Nenhuma outra ferramenta de terceiros é necessária. A biblioteca lida com a desinclinação, OCR e até detecção de idioma internamente.

![exemplo de como desinclinar imagem](/images/deskew-example.png "como desinclinar imagem usando Aspose OCR")

## Etapa 1: Configurar o Projeto e Instalar Aspose.OCR

Para manter as coisas organizadas, inicie um novo projeto de console:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

A linha `dotnet add package` traz os binários **Aspose.OCR** junto com todas as dependências nativas. Se você estiver no Windows, receberá as DLLs nativas automaticamente; no Linux/macOS pode ser necessário o pacote `libgdiplus`, mas isso é uma instalação única.

## Etapa 2: Habilitar a Desinclinação Automática (Corrigir Rotação da Imagem)

Agora abra `Program.cs` e substitua seu conteúdo pelo código abaixo. A linha chave aqui é `ocrEngine.Settings.Deskew = true;` – esse é o sinalizador que indica ao motor **como desinclinar imagem** automaticamente.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Por que Habilitar a Desinclinação?

Quando um scanner alimenta uma página em um ângulo, a linha de base do texto fica inclinada. Motores de OCR tradicionais leriam cada caractere como uma versão inclinada, reduzindo drasticamente a precisão. Ao definir `Deskew = true`, o Aspose OCR executa uma rápida transformada de Hough nos bastidores, rotaciona o bitmap de volta à horizontal e então realiza o reconhecimento. O resultado é o mesmo que se você tivesse rotacionado a imagem manualmente no Photoshop—apenas mais rápido e totalmente automatizado.

## Etapa 3: Reconhecer Texto na Imagem e Converter JPG para Texto

A chamada `Recognize` faz duas coisas ao mesmo tempo:

1. **Desinclina** a imagem (porque ativamos o sinalizador).  
2. **Extrai** o conteúdo textual, retornando‑o em um objeto `OcrResult`.

Você pode tratar `ocrResult.Text` como uma string simples, gravá‑la em um arquivo ou enviá‑la para pipelines de processamento posteriores. Se precisar das pontuações de confiança brutas por palavra, `ocrResult.Words` fornece uma coleção com valores `Confidence`.

### Exemplo de Saída

Assumindo que `skewed_receipt.jpg` contenha um recibo simples, você pode ver algo como:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Observe como os números se alinham perfeitamente apesar da imagem original estar rotacionada em cerca de 7°. Essa é a magia da **correção de rotação da imagem** incorporada na biblioteca.

## Etapa 4: Executando o Exemplo e Verificando os Resultados

Compile e execute:

```bash
dotnet run
```

Se tudo estiver configurado corretamente, você verá o texto extraído impresso no console. Se receber uma exceção como `FileNotFoundException`, verifique novamente o caminho para o seu JPEG e assegure que o arquivo seja legível.

### Armadilhas Comuns & Dicas Profissionais

- **Imagens Grandes** – O uso de memória do OCR cresce com as dimensões da imagem. Redimensione arquivos excessivamente grandes (por exemplo, > 3000 px de largura) antes de enviá‑los ao motor.  
- **Scripts Não‑Latinos** – Por padrão o motor assume inglês. Defina `ocrEngine.Settings.Language = OcrLanguage.French;` (ou qualquer idioma suportado) se precisar **reconhecer texto na imagem** em outros alfabetos.  
- **Processamento em Lote** – Para muitos arquivos, reutilize a mesma instância `OcrEngine`; criar um novo motor por arquivo gera sobrecarga desnecessária.  
- **Verificação de Qualidade** – Após a desinclinação, você pode exportar o bitmap corrigido via `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` para verificar visualmente a correção da rotação.

## Exemplo Completo Funcional (Tudo Junto)

Abaixo está o programa completo e autocontido que você pode copiar‑colar em `Program.cs`. Ele inclui comentários, tratamento de erros e uma etapa opcional para salvar a imagem desinclinado.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Executar o programa **reconhecerá arquivos jpg de texto**, corrigirá automaticamente qualquer inclinação e imprimirá texto limpo e pesquisável no console.

## Conclusão

Agora você tem um trecho de código sólido e pronto para produção que demonstra **como desinclinar imagem** arquivos e extrair seu conteúdo usando Aspose OCR. A abordagem funciona para recibos, faturas, contratos escaneados ou qualquer JPEG onde o texto não está perfeitamente horizontal.

Próximos passos que você pode explorar:

- **Processamento em lote** de uma pasta de JPEGs e gravação de cada resultado em um arquivo `.txt` (relacionado a *converter jpg para texto*).  
- Integrar a etapa de OCR em uma API ASP.NET Core para que clientes possam enviar imagens e receber texto formatado em JSON.  
- Experimentar diferentes configurações de OCR como `ocrEngine.Settings.Language` ou `ocrEngine.Settings.RecognitionMode` para melhorar a precisão em documentos não‑ingleses.

Experimente, ajuste as configurações e deixe o motor fazer o trabalho pesado. Como sempre, se encontrar algum problema ou tiver uma otimização inteligente para compartilhar, deixe um comentário abaixo. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}