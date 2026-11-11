---
category: general
date: 2026-05-28
description: Crie PDF pesquisável usando Aspose OCR em C#. Aprenda como executar OCR
  em PDF, reconhecer texto em PDF e transformar um PDF escaneado com OCR em um PDF
  pesquisável.
draft: false
keywords:
- create searchable pdf
- run ocr on pdf
- recognize text pdf
- ocr scanned pdf
- aspose ocr pdf
language: pt
og_description: Crie PDF pesquisável usando Aspose OCR em C#. Siga este guia passo
  a passo para executar OCR em PDF, reconhecer texto em PDF e lidar com arquivos PDF
  escaneados com OCR.
og_title: Criar PDF pesquisável com Aspose OCR – Executar OCR em PDF
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  headline: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  type: TechArticle
- description: Create searchable PDF using Aspose OCR in C#. Learn how to run OCR
    on PDF, recognize text PDF, and turn an OCR scanned PDF into a searchable PDF.
  name: Create Searchable PDF with Aspose OCR – Run OCR on PDF
  steps:
  - name: Multiple Languages (OCR Scanned PDF)
    text: 'If your source PDF contains both English and Spanish text, combine languages:'
  - name: Password‑Protected PDFs
    text: 'When dealing with secured PDFs, supply the password before calling `Recognize`:'
  - name: Controlling Image Quality
    text: 'Higher DPI yields better OCR results but consumes more memory. Adjust the
      DPI if you notice garbled characters:'
  - name: License vs. Evaluation Mode
    text: 'In evaluation mode a watermark appears on each page. To remove it, apply
      your license before any OCR call:'
  - name: What’s Next?
    text: '- Explore the **aspose ocr pdf** API further: extract plain text, export
      to DOCX, or generate searchable PDFs in bulk. - Combine the searchable PDF output
      with Aspose.PDF to add bookmarks or watermarks. - Experiment with different
      DPI settings or custom OCR dictionaries for niche fonts.'
  type: HowTo
tags:
- Aspose
- OCR
- PDF
- C#
title: Criar PDF pesquisável com Aspose OCR – Executar OCR em PDF
url: /pt/net/text-recognition/create-searchable-pdf-with-aspose-ocr-run-ocr-on-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável com Aspose OCR – Executar OCR em PDF

Já precisou **criar PDFs pesquisáveis** a partir de um conjunto de documentos escaneados? Você não está sozinho. Em muitos fluxos de trabalho de escritório, a única coisa que impede você de ter um arquivo totalmente pesquisável são algumas linhas de código que executam OCR nas páginas de PDF.  

Neste tutorial, percorreremos um exemplo completo, pronto‑para‑executar, que mostra exatamente como **criar PDFs pesquisáveis** usando a biblioteca Aspose OCR para .NET. Ao final, você saberá como *executar OCR em PDF*, *reconhecer PDFs de texto* e transformar um *PDF escaneado com OCR* em uma versão pesquisável sem nenhum serviço de terceiros.

> **Pré‑requisitos** – Um SDK .NET recente (recomendado 6.0+), uma licença válida do Aspose.OCR para .NET (ou uma chave de avaliação temporária) e um PDF que você deseja processar.

![Create searchable PDF diagram](alt="Diagram illustrating the create searchable pdf workflow using Aspose OCR")  

---

## O que este guia cobre

- Configurar a biblioteca Aspose OCR em um projeto C#.
- Carregar um PDF de origem (qualquer número de páginas).
- Configurar o motor para gerar um **PDF pesquisável**.
- Executar o processo de OCR e salvar o resultado.
- Dicas para lidar com documentos multipágina, seleção de idioma e armadilhas comuns.  

Se você seguir cada passo, terminará com um arquivo que pode abrir no Adobe Reader, pressionar **Ctrl + F** e pesquisar instantaneamente qualquer palavra que apareça na digitalização original.

---

## Etapa 1: Instalar Aspose OCR para .NET

Antes de escrever qualquer código, adicione o pacote NuGet ao seu projeto:

```bash
dotnet add package Aspose.OCR
```

> **Dica profissional:** Use a flag `--version` para fixar na versão estável mais recente (por exemplo, `Aspose.OCR 23.10`). Isso garante compatibilidade com .NET 6 e versões mais recentes.

---

## Etapa 2: Criar uma Instância do Motor OCR

O coração do processo é o `OcrEngine`. Pense nele como o cérebro que lê imagens e gera texto. Inicializá‑lo é simples:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Instantiate the OCR engine
            var ocrEngine = new OcrEngine();
```

O objeto `OcrEngine` armazenará tanto o fluxo de imagem de entrada quanto a configuração que indica ao Aspose como você deseja a saída.

---

## Etapa 3: Carregar o PDF de Origem (Executar OCR em PDF)

O Aspose OCR pode ingerir um PDF diretamente; ele extrai cada página como uma imagem internamente. Substitua o caminho placeholder pela localização do seu documento escaneado:

```csharp
            // Step 3: Load the source PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);
```

> **Por que isso funciona:** O método `ImageStream.FromFile` detecta automaticamente o formato PDF e prepara uma representação raster para OCR. Nenhuma etapa de conversão extra é necessária.

---

## Etapa 4: Configurar Formato de Saída e Idioma

Aqui informamos ao Aspose o que queremos de volta. Definir `OutputFormat` como `SearchablePdf` instrui o motor a incorporar o texto reconhecido atrás das imagens das páginas originais, produzindo um **PDF pesquisável**. Você também pode escolher o idioma para melhorar a precisão — o inglês é o padrão, mas pode mudar para francês, alemão, etc.

```csharp
            // Step 4: Choose output format and language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf; // creates searchable PDF
            ocrEngine.Configuration.Language = Language.English;               // *recognize text PDF* in English
```

Se precisar processar um documento bilíngue, pode combinar idiomas usando as flags do enum `Language`.

---

## Etapa 5: Executar o Processo OCR – Reconhecer PDF de Texto

Agora o trabalho pesado acontece. O método `Recognize` escaneia cada página, extrai glifos e constrói um fluxo interno de PDF que contém tanto a imagem original quanto uma camada de texto invisível. Esta é a etapa onde *reconhecemos PDF de texto*.

```csharp
            // Step 5: Execute OCR – this *recognizes text PDF* and builds the searchable stream
            ocrEngine.Recognize();
```

> **Pergunta comum:** *E se o PDF tiver 200 páginas?*  
> O motor processa as páginas sequencialmente e transmite os resultados, portanto o consumo de memória permanece modesto. Contudo, para arquivos extremamente grandes, pode ser necessário aumentar a configuração `MemoryLimit` em `ocrEngine.Configuration`.

---

## Etapa 6: Salvar o PDF Pesquisável

Finalmente, grave a saída no disco. O método `Save` grava o fluxo interno em um novo arquivo que pode ser aberto com qualquer visualizador de PDF.

```csharp
            // Step 6: Save the searchable PDF to disk
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

Execute o programa (`dotnet run`) e observe o console confirmar a criação do arquivo. Abra `handbook_searchable.pdf` e tente pesquisar uma palavra que você sabe que aparece na digitalização original – você deverá ver correspondências instantaneamente.

---

## Lidando com Casos de Borda e Cenários Avançados

### Múltiplos Idiomas (PDF Escaneado com OCR)

Se o seu PDF de origem contém texto em inglês e espanhol, combine os idiomas:

```csharp
ocrEngine.Configuration.Language = Language.English | Language.Spanish;
```

O Aspose OCR trocará dicionários em tempo real, aumentando a precisão para documentos com múltiplos idiomas.

### PDFs Protegidos por Senha

Ao lidar com PDFs protegidos, forneça a senha antes de chamar `Recognize`:

```csharp
ocrEngine.Image = ImageStream.FromFile(inputPath, "MySecretPassword");
```

Se a senha estiver errada, `Recognize` lança uma `InvalidPasswordException`; capturá‑la permite solicitar ao usuário a senha correta.

### Controlando a Qualidade da Imagem

Um DPI mais alto gera melhores resultados de OCR, mas consome mais memória. Ajuste o DPI se notar caracteres distorcidos:

```csharp
ocrEngine.Configuration.Dpi = 300; // default is 200
```

### Licença vs. Modo de Avaliação

No modo de avaliação, uma marca d'água aparece em cada página. Para removê‑la, aplique sua licença antes de qualquer chamada de OCR:

```csharp
var license = new License();
license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");
```

---

## Dicas Profissionais para Uso em Produção

- **Processamento em lote:** Envolva a lógica principal em um loop `foreach` que itere sobre uma lista de PDFs. Libere o `OcrEngine` após cada arquivo para liberar recursos nativos.
- **Log:** Use `ocrEngine.Configuration.Logger` para capturar estatísticas detalhadas de OCR (por exemplo, caracteres reconhecidos por segundo). Isso é inestimável ao solucionar baixa precisão.
- **Ajuste de desempenho:** Em servidores multi‑core, instancie objetos `OcrEngine` separados por thread; a biblioteca é segura para threads quando cada instância está isolada.
- **Tratamento de erros:** Sempre envolva `Recognize` e `Save` com blocos `try/catch`. Exceções típicas incluem `FileNotFoundException`, `OutOfMemoryException` e `UnsupportedFormatException`.

---

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace PdfSearchableDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Apply license (optional – removes evaluation watermark)
            // var license = new License();
            // license.SetLicense(@"C:\Aspose\Aspose.OCR.lic");

            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Load PDF – this is where we *run OCR on PDF*
            string inputPath = @"C:\Docs\handbook.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Configure output as searchable PDF and set language
            ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
            ocrEngine.Configuration.Language = Language.English;

            // 4️⃣ Run OCR – *recognize text PDF*
            ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\handbook_searchable.pdf";
            ocrEngine.Save(outputPath);

            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Saída esperada** (console):

```
Searchable PDF created at: C:\Docs\handbook_searchable.pdf
```

Abra o arquivo resultante, pressione **Ctrl + F** e você poderá localizar qualquer palavra que apareça nas páginas escaneadas originais. Essa é a mágica de transformar um *PDF escaneado com OCR* em um **PDF pesquisável**.

---

## Conclusão

Acabamos de demonstrar como **criar PDFs pesquisáveis** com Aspose OCR para .NET, cobrindo tudo, desde a instalação do pacote até o tratamento de PDFs multilíngues e protegidos por senha. Seguindo estes passos, você pode executar OCR em documentos PDF de forma confiável, *reconhecer conteúdo de PDF de texto* e converter qualquer *PDF escaneado com OCR* em um recurso totalmente pesquisável.

### O que vem a seguir?

- Explore mais a API **aspose ocr pdf**: extraia texto simples, exporte para DOCX ou gere PDFs pesquisáveis em massa.  
- Combine a saída de PDF pesquisável com Aspose.PDF para adicionar marcadores ou marcas d'água.  
- Experimente diferentes configurações de DPI ou dicionários OCR personalizados para fontes específicas.

Sinta‑se à vontade para ajustar o exemplo, integrá‑lo ao seu pipeline de gerenciamento de documentos ou fazer perguntas nos comentários. Feliz codificação e aproveite transformar essas digitalizações ilegíveis em ouro pesquisável!

## Tutoriais Relacionados

- [Como fazer OCR de PDF em .NET com Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Como fazer OCR de PDF em .NET com Aspose.OCR](/ocr/spanish/net/text-recognition/recognize-pdf/)
- [Como fazer OCR de PDF em .NET usando Aspose.OCR](/ocr/arabic/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}