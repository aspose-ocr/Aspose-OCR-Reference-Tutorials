---
category: general
date: 2026-02-16
description: Crie PDF pesquisável a partir de uma imagem TIFF usando Aspose OCR. Aprenda
  como converter TIFF para PDF, fazer OCR de imagem para PDF e reconhecer texto de
  imagem em C#.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- ocr image to pdf
- recognize text from image
- convert scanned image pdf
language: pt
og_description: Crie PDF pesquisável rapidamente. Este tutorial mostra como converter
  TIFF para PDF, fazer OCR de imagem para PDF e reconhecer texto de imagem com Aspose
  OCR.
og_title: Criar PDF pesquisável a partir de TIFF – Guia OCR da Aspose
tags:
- Aspose OCR
- C#
- PDF/A
- Document Processing
title: Criar PDF pesquisável a partir de TIFF – Guia passo a passo do Aspose OCR
url: /pt/net/text-recognition/create-searchable-pdf-from-tiff-aspose-ocr-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de TIFF – Guia passo a passo do Aspose OCR

Já precisou **criar PDF pesquisável** a partir de um TIFF digitalizado, mas não tinha certeza de qual biblioteca faria o trabalho pesado? Você não está sozinho. Em muitos projetos de automação de escritório acabamos com uma pilha de arquivos TIFF que parecem imagens, não texto. A boa notícia? Com o Aspose OCR você pode **converter tiff para pdf**, executar OCR na imagem e obter um PDF/A‑2b totalmente pesquisável.

Neste tutorial, percorreremos um exemplo completo e executável em C# que mostra exatamente como **criar PDF pesquisável**, por que cada etapa é importante e quais armadilhas observar. Ao final, você será capaz de **reconhecer texto de imagens**, **OCR de imagem para pdf**, e até **converter pdf de imagem escaneada** que atendam aos padrões de arquivamento.

## O que você aprenderá

- Como instalar e referenciar o pacote NuGet Aspose OCR.  
- O código exato necessário para **criar PDF pesquisável** a partir de um arquivo TIFF.  
- Por que carregar o modelo de idioma correto é crucial para um OCR preciso.  
- Dicas para lidar com digitalizações grandes, TIFFs de várias páginas e conformidade PDF/A.  
- Onde encontrar o arquivo resultante e como verificar se o texto é pesquisável.

### Pré-requisitos

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later (any recent .NET runtime) | Aspose OCR fornece binários para .NET Standard 2.0+, que rodam em qualquer lugar, desde .NET Core até .NET Framework. |
| Visual Studio 2022 (or VS Code with C# extension) | Fornece IntelliSense e gerenciamento fácil de pacotes NuGet. |
| An active Aspose OCR license (or a free evaluation key) | A avaliação gratuita limita o número de páginas; uma licença remove a marca d'água e habilita a saída PDF/A‑2b. |
| A TIFF file you want to process (e.g., `input.tif`) | Esta é a imagem de origem que transformaremos em um **PDF pesquisável**. |

> **Dica profissional:** Se você estiver trabalhando com TIFFs de várias páginas, o Aspose OCR tratará cada página como uma imagem separada automaticamente — sem necessidade de código extra.

---

## Etapa 1: Instalar o pacote NuGet Aspose OCR

Primeiro, adicione a biblioteca ao seu projeto. Abra o Console do Gerenciador de Pacotes e execute:

```powershell
Install-Package Aspose.OCR
```

Ou, se preferir a interface gráfica, procure por “Aspose.OCR” no **NuGet Package Manager** e clique em **Install**. Isso traz todas as DLLs necessárias, incluindo os modelos de idioma que precisaremos mais tarde.

> **Por que esta etapa?** Sem o pacote, a classe `OcrEngine` não existe, e você receberá erros de compilação. A abordagem NuGet garante que você tenha a versão correta (atualmente 23.12) e traz automaticamente quaisquer dependências transitivas.

## Etapa 2: Inicializar o motor OCR

Criar uma instância do motor é a primeira linha de código real que você escreverá. Pense no `OcrEngine` como o cérebro que faz todo o trabalho pesado.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine – this object will manage the entire pipeline
OcrEngine ocrEngine = new OcrEngine();
```

> **O que está acontecendo?** O construtor configura buffers internos e prepara o motor para o carregamento do modelo de idioma. Se você pular isso, chamadas posteriores como `LoadLanguage` lançarão uma `NullReferenceException`.

## Etapa 3: Carregar o modelo de idioma Inglês (ou outro)

A precisão do OCR depende do modelo de idioma que você carrega. Para a maioria dos documentos ocidentais, o Inglês é suficiente, mas o Aspose suporta dezenas de idiomas.

```csharp
// Load English language data – essential for recognizing Latin characters
ocrEngine.LoadLanguage(LanguageModel.English);
```

> **Por que carregar um modelo?** O motor precisa de uma representação estatística das formas dos caracteres. Sem ele, você obterá texto sem sentido ou um resultado vazio. Se precisar **reconhecer texto de imagem** em francês, substitua `LanguageModel.English` por `LanguageModel.French`.

## Etapa 4: Fornecer a imagem TIFF e gerar um PDF/A‑2b

Agora apontamos o motor para o nosso arquivo de origem. O helper `ImageStream.FromFile` lê o TIFF (de página única ou múltipla) para a memória.

```csharp
// Step 4: Assign the TIFF image to the engine
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

// Run OCR and produce a PDF/A‑2b document – this is the searchable PDF we want
PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);
```

> **O que isso faz?** `RecognizePdfA` realiza três ações internamente:  
> 1️⃣ Executa OCR em cada página do TIFF.  
> 2️⃣ Incorpora o texto reconhecido como uma camada invisível.  
> 3️⃣ Envolve tudo em um contêiner PDF/A‑2b, que é o padrão ISO para preservação a longo prazo.  

Se você precisar apenas de um PDF simples (sem conformidade de arquivamento), pode chamar `ocrEngine.RecognizePdf()` em vez disso. Mas para a maioria dos cenários corporativos, PDF/A‑2b é a opção mais segura.

## Etapa 5: Salvar o PDF pesquisável no disco

Finalmente, grave o resultado em um arquivo. O método `Save` recebe um caminho e lida com todo o I/O.

```csharp
// Save the generated searchable PDF to your output folder
searchablePdf.Save("YOUR_DIRECTORY/output.pdf");
```

Ao abrir `output.pdf` no Adobe Reader, você deve ser capaz de digitar uma palavra na caixa de pesquisa e encontrá‑la instantaneamente — mesmo que o arquivo original fosse apenas uma imagem. Essa é a magia dos fluxos de trabalho de **criar PDF pesquisável**.

## Converter TIFF para PDF – Resumo rápido

Abaixo está o programa completo, pronto‑para‑executar, que une tudo. Sinta‑se à vontade para copiar‑colar em um aplicativo de console e pressionar **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the desired language model (English in this case)
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 3️⃣ Point the engine at the TIFF you want to convert
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.tif");

        // 4️⃣ Recognize the image and produce a PDF/A‑2b (searchable PDF)
        PdfAResult searchablePdf = ocrEngine.RecognizePdfA(PdfAStandard.PdfA2b);

        // 5️⃣ Persist the result to disk
        searchablePdf.Save("YOUR_DIRECTORY/output.pdf");

        Console.WriteLine("✅ Searchable PDF created successfully!");
    }
}
```

**Resultado esperado:** `output.pdf` aparece em `YOUR_DIRECTORY`. Abra‑o, selecione a ferramenta de texto e você verá texto selecionável e pesquisável sobreposto à imagem raster original.

## OCR de imagem para PDF – Lidando com casos extremos

### TIFFs de várias páginas

Se o seu arquivo de origem contiver mais de uma página, o Aspose OCR processa automaticamente cada página e adiciona uma página correspondente no PDF. Não é necessário loop extra.

### Arquivos grandes e gerenciamento de memória

Para digitalizações em escala de gigabytes, considere habilitar o **modo de streaming**:

```csharp
ocrEngine.Image = ImageStream.FromFile("large.tif", useMemoryCache: false);
```

Isso instrui o motor a ler blocos do disco em vez de carregar a imagem inteira na RAM — ótimo para trabalhos em lote no servidor.

### Diferentes formatos de saída

Às vezes você não precisa de PDF/A‑2b, mas de um PDF simples. Altere a chamada:

```csharp
PdfResult plainPdf = ocrEngine.RecognizePdf();
plainPdf.Save("plain.pdf");
```

Ou, se você quiser apenas o texto bruto (sem PDF), use:

```csharp
string extractedText = ocrEngine.RecognizeText();
System.IO.File.WriteAllText("text.txt", extractedText);
```

Essas variações atendem ao cenário de **converter pdf de imagem escaneada** onde sistemas downstream aceitam apenas PDFs simples.

## Dicas profissionais para OCR confiável

- **DPI importa:** Digitalizações a 300 DPI ou mais oferecem as melhores taxas de reconhecimento. Abaixo de 200 DPI você verá queda na precisão.  
- **Pré‑processamento:** Se o TIFF estiver ruidoso, execute `ocrEngine.Image = ImageProcessor.Deskew(...).Apply(ocrEngine.Image);` antes do reconhecimento.  
- **Licenciamento:** Lembre‑se de definir sua licença cedo no aplicativo (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`). Sem ela, a saída conterá uma marca d'água “Evaluation”.  
- **Processamento em lote:** Envolva a lógica principal em um loop `foreach` sobre um diretório de TIFFs para **converter tiff para pdf** em massa.

## Perguntas Frequentes

**Q: Isso funciona no Linux?**  
A: Absolutamente. O Aspose OCR tem como alvo .NET Standard, então você pode executar o mesmo binário no Windows, Linux ou macOS com o runtime .NET 6.

**Q: E se eu precisar reconhecer um idioma diferente do Inglês?**  
A: Basta substituir `LanguageModel.English` pelo enum apropriado, por exemplo, `LanguageModel.Spanish`. Você também pode carregar vários idiomas simultaneamente para documentos com idiomas mistos.

**Q: Posso incorporar uma fonte personalizada no PDF/A?**  
A: Sim. Use `ocrEngine.Options.PdfOptions.Font = PdfFont.CreateFont("path/to/font.ttf");` antes de chamar `RecognizePdfA`.

## Conclusão

Cobremos tudo o que você precisa para **criar PDF pesquisável** a partir de imagens TIFF usando o Aspose OCR. Desde a instalação do pacote NuGet, o carregamento do modelo de idioma correto, até a geração de um PDF/A‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}