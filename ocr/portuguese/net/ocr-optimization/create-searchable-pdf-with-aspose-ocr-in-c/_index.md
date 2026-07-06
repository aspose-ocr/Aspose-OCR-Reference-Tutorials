---
category: general
date: 2026-04-01
description: Crie PDF pesquisável em C# usando Aspose OCR – aprenda a converter PDF
  escaneado, adicionar OCR ao PDF e habilitar aceleração GPU para resultados rápidos.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: pt
og_description: Crie PDF pesquisável em C# rapidamente — converta PDF escaneado, adicione
  OCR ao PDF e habilite aceleração por GPU para processamento de alto desempenho.
og_title: Criar PDF pesquisável com Aspose OCR em C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Criar PDF pesquisável com Aspose OCR em C#
url: /pt/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável com Aspose OCR em C#

Já precisou **criar PDFs pesquisáveis** a partir de uma pilha de documentos escaneados? Você não está sozinho — muitas equipes lutam para transformar PDFs apenas com imagens em ativos pesquisáveis por texto. A boa notícia? Com o Aspose OCR você pode **converter PDF escaneado** para uma versão totalmente pesquisável em apenas algumas linhas de código C#. Neste guia, percorreremos todo o processo, desde a adição de OCR ao PDF até, opcionalmente, **habilitar aceleração por GPU** para ganhar velocidade.

Também mostraremos como **converter pdf para pesquisável**, discutiremos por que você pode querer **adicionar OCR ao PDF** e daremos dicas práticas para lidar com lotes grandes. Ao final, você terá um aplicativo console pronto‑para‑executar que produz um PDF pesquisável que pode ser inserido em qualquer sistema de gerenciamento de documentos.

---

## O que você precisará

Antes de mergulharmos, certifique‑se de que tem o seguinte:

- **.NET 6.0** ou posterior (a API funciona também com .NET Framework, mas .NET 6+ é o ponto ideal).
- Pacote NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`).
- Um arquivo PDF escaneado (apenas imagem) para usar como entrada.
- Opcional: uma máquina compatível com GPU com CUDA® instalado se quiser **habilitar aceleração por GPU**.

É só isso — sem motores OCR pesados, sem serviços externos. Tudo roda localmente.

---

## Criar PDF pesquisável – Visão geral passo a passo

A seguir está o fluxo de alto nível que seguiremos:

1. **Inicializar o motor OCR** – informe ao Aspose qual idioma procurar e se deve usar a GPU.
2. **Apontar o motor para o seu PDF escaneado** – defina os caminhos de entrada e saída.
3. **Executar a conversão** – o Aspose faz o trabalho pesado e grava um PDF pesquisável.
4. **Verificar o resultado** – abra o arquivo de saída e tente uma busca por texto.

Cada passo está detalhado em sua própria seção, para que você possa escolher apenas as partes que lhe interessam.

---

## Converter PDF escaneado para PDF pesquisável

A primeira coisa a fazer é criar uma instância de `OcrEngine`. Esse objeto é o responsável por ler as imagens raster dentro do seu PDF e extrair o texto.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Por que isso funciona:** `ConvertToSearchablePdf` lê cada página, executa OCR no conteúdo raster e, em seguida, incorpora uma camada de texto invisível atrás da imagem original. O resultado tem a aparência exatamente como o documento escaneado original, mas agora você pode copiar, selecionar e buscar o texto.

---

## Adicionar OCR ao PDF usando Aspose

Se você já tem um PDF e só quer **adicionar OCR ao PDF** sem converter todo o arquivo, pode chamar o mesmo método — o Aspose trata a operação como “adicionar OCR”. O código acima já faz isso, mas aqui está uma variante rápida que mostra como processar vários arquivos em um loop:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Dica:** Mantenha a mesma instância de `OcrEngine` para todo o lote. Recriar a cada vez adiciona sobrecarga desnecessária, especialmente quando você **habilita aceleração por GPU**.

---

## Habilitar aceleração por GPU para OCR mais rápido

A aceleração por GPU pode reduzir minutos em um lote grande. O Aspose OCR utiliza NVIDIA CUDA nos bastidores, então basta mudar um sinalizador booleano:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Quando usar:** Se você estiver processando PDFs maiores que 10 MB ou lidando com mais de algumas dezenas de arquivos, a GPU normalmente oferece um aumento de velocidade de 2‑3×. Em um laptop modesto sem GPU compatível com CUDA, deixe `false` — a biblioteca reverte automaticamente para CPU.

**Erro comum:** Esquecer de instalar a versão correta do driver CUDA pode causar uma exceção em tempo de execução (`CudaException`). Certifique‑se de que seu driver corresponde à versão que o Aspose espera (verifique as notas de versão na página do NuGet).

---

## Exemplo completo (todos os passos combinados)

A seguir está um aplicativo console autocontido que você pode copiar‑colar em um novo projeto .NET. Ele inclui comentários úteis, tratamento de erros e uma etapa final de verificação que imprime o número de páginas processadas.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Saída esperada**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Abra `output.pdf` em qualquer visualizador de PDF e tente digitar uma palavra que apareça nas imagens escaneadas. Se o texto for destacado, você **criou pdf pesquisável** com sucesso.

---

## Armadilhas comuns e dicas avançadas

| Problema | Por que acontece | Como corrigir / evitar |
|----------|------------------|------------------------|
| **GPU não detectada** | Driver CUDA ausente ou incompatível. | Instale a versão do driver listada nas notas de versão da Aspose; defina `UseGpuAcceleration = false` como alternativa. |
| **Idioma errado** | OCR padrão é inglês; outros idiomas precisam ser definidos explicitamente. | Defina `Language = Language.Spanish` (ou qualquer enum suportado) antes da conversão. |
| **PDFs grandes causam OutOfMemory** | O motor carrega páginas inteiras na memória. | Processar o PDF em blocos usando `ocrEngine.PageRange = new PageRange(1, 5)` para cada lote. |
| **Arquivo de saída corrompido** | Pasta de destino sem permissões de gravação. | Execute o app com privilégios elevados ou escolha um caminho gravável. |
| **Camada de texto não pesquisável** | Visualizador mantém versão em cache. | Atualize o visualizador de PDF ou reabra o arquivo. |

**Dica avançada:** Quando estiver lidando com uma mistura de PDFs escaneados e nativos, verifique o sinalizador `HasText` de cada página (`PdfPageInfo.HasText`) antes de executar OCR. Isso economiza ciclos de CPU e evita OCR duplicado em páginas que já são pesquisáveis.

---

## Verificar o resultado programaticamente (opcional)

Se quiser automatizar a verificação, o Aspose.PDF pode extrair o texto oculto:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Este trecho comprova que você realmente **converte pdf para pesquisável**, não apenas sobrepõe uma imagem.

---

## Exemplo de imagem

![Exemplo de saída de PDF pesquisável](https://example.com/images/searchable-pdf.png "Criar PDF pesquisável usando Aspose OCR")

*Texto alternativo:* **exemplo de criar pdf pesquisável** mostrando antes (escaneado) e depois (pesquisável).

---

## Próximos passos e tópicos relacionados

- **Processamento em lote:** Envolva o loop da seção “Adicionar OCR ao PDF” em um Windows Service ou Azure Function para trabalhos noturnos.
- **Suporte avançado a idiomas:** Explore `ocrEngine.Language = Language.Multilingual` para documentos contendo scripts mistos.
- **Limpeza pós‑OCR:** Use `TextFragmentAbsorber` do Aspose.PDF para corrigir erros comuns de OCR (ex.: “0” vs “O”).
- **Segurança

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}