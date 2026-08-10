---
category: general
date: 2026-04-04
description: Crie PDF pesquisável a partir de uma imagem TIF em C# – aprenda como
  converter a imagem em PDF, adicionar metadados ao PDF e gerar um documento pesquisável
  usando Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: pt
og_description: Crie PDF pesquisável a partir de um arquivo TIF com C#. Converta a
  imagem para PDF, adicione metadados ao PDF e produza um documento pesquisável usando
  Aspose.OCR.
og_title: Criar PDF pesquisável a partir de TIF – Guia passo a passo
tags:
- Aspose.OCR
- C#
- PDF generation
title: Criar PDF pesquisável a partir de TIF – Converter imagem em PDF, adicionar
  metadados ao PDF
url: /pt/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de TIF – Guia completo em C#

Já precisou **criar um PDF pesquisável** a partir de uma fatura escaneada, mas não sabia como manter o texto pesquisável e os metadados do arquivo organizados? Você não está sozinho. Em muitos projetos de automação o PDF precisa ser tanto legível por máquina quanto devidamente marcado com informações como título, autor e limites de confiança.

Neste guia vamos percorrer uma solução completa que **converte uma imagem em PDF**, insere **metadados no PDF** e filtra resultados de OCR de baixa confiança — tudo com a biblioteca Aspose.OCR. Ao final, você terá um trecho de código pronto para usar em qualquer projeto .NET, além de algumas dicas para lidar com casos especiais.

## Pré‑requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.6+)  
- Pacote NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Uma imagem TIF que você deseja transformar em PDF pesquisável (por exemplo, `input.tif`)  
- Familiaridade básica com C# e Visual Studio (ou sua IDE favorita)

Nenhum serviço externo adicional é necessário — todo o processo roda localmente.

## Etapa 1 – Configurar o mecanismo de OCR (Criar o núcleo do PDF pesquisável)

A primeira coisa que precisamos é de uma instância `OcrEngine` que saiba qual idioma reconhecer. Na maioria dos cenários empresariais o inglês basta, mas você pode trocar `Language.English` por qualquer idioma suportado.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Por que isso importa:** O mecanismo de OCR faz o trabalho pesado de transformar pixels raster em texto Unicode. Definir o idioma corretamente melhora a precisão e reduz a quantidade de palavras de baixa confiança que serão filtradas depois.

> **Dica profissional:** Se você processa documentos multilíngues, instancie vários mecanismos ou use `Language.Multilingual` para que o Aspose detecte o idioma automaticamente.

## Etapa 2 – Carregar a imagem TIF (Criar PDF a partir de TIF)

Agora apontamos o mecanismo para o arquivo de origem. O auxiliar `ImageStream.FromFile` lê a imagem para um stream que o mecanismo de OCR pode consumir.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Você pode estar se perguntando: *“Posso usar um JPEG ou PNG em vez disso?”* Absolutamente — o Aspose.OCR suporta a maioria dos formatos raster. Basta mudar a extensão do arquivo e está tudo pronto.

## Etapa 3 – Configurar opções de PDF (Adicionar metadados ao PDF)

Antes da conversão, definimos um objeto `PdfOptions`. É aqui que **adicionamos metadados ao PDF** como título e autor, e também instruímos o mecanismo a descartar palavras cuja confiança esteja abaixo de um limite.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**O que está acontecendo aqui?**  
- `Title` e `Author` passam a fazer parte do dicionário de informações do documento PDF, facilitando a indexação em sistemas de gerenciamento de documentos.  
- `MinConfidence` funciona como uma barreira de segurança: o OCR costuma errar caracteres apagados; filtrá‑los mantém a camada pesquisável limpa e melhora a extração de texto posterior.

Se precisar de metadados personalizados (por exemplo, `Subject`, `Keywords`), pode defini‑los via `PdfOptions.CustomProperties`.

## Etapa 4 – Converter a imagem em um PDF pesquisável (Converter imagem para PDF)

Com o mecanismo preparado e as opções definidas, a chamada final realiza a conversão. Ela grava um PDF pesquisável no disco, incorporando a camada de texto OCR sob a imagem original.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Depois que esta linha for executada, `output.pdf` conterá:
- A imagem TIF original como plano de fundo visual  
- Uma camada de texto invisível que mecanismos de busca e operações de copiar‑colar podem ler  
- Os metadados que definimos anteriormente (título, autor, etc.)

### Resultado esperado

Abra o PDF gerado no Adobe Reader ou em qualquer visualizador de PDF e tente selecionar texto. Você deverá conseguir copiar frases que correspondam à digitalização original. A caixa de diálogo **Propriedades** do documento mostrará o título “Invoice #12345” e o autor “MyCompany”.

## Etapa 5 – Verificar o filtro de confiança (Por que MinConfidence ajuda)

É útil confirmar que as palavras de baixa confiança foram realmente removidas. Você pode inspecionar o texto oculto do PDF usando uma ferramenta como `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Se a palavra nunca aparecer, o filtro `MinConfidence` funcionou como esperado. Ajuste o limite (por exemplo, `0.7f`) se precisar de um filtro mais agressivo ou mais permissivo.

## Etapa 6 – Manipular várias páginas (Criar PDF pesquisável a partir de TIF multipágina)

Muitas faturas chegam como TIFFs de várias páginas. O Aspose.OCR trata cada quadro como uma página separada automaticamente. Basta apontar o mecanismo para o arquivo multipágina; a mesma chamada `ConvertToSearchablePdf` gerará um PDF pesquisável de várias páginas.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Caso especial:** Se uma página estiver em branco, o OCR pode ainda gerar uma camada de texto vazia, o que não causa problemas. Contudo, você pode pular páginas em branco verificando `ocrEngine.HasText` antes da conversão.

## Etapa 7 – Empacotar o exemplo completo (Todas as etapas juntas)

Abaixo está um programa único, pronto para execução, que une tudo. Substitua `YOUR_DIRECTORY` pelo caminho real da pasta em sua máquina.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Execute o programa (`dotnet run` ou pressione **F5** no Visual Studio) e você verá a mensagem de confirmação. O PDF gerado ficará ao lado da sua imagem de origem, pronto para indexação ou arquivamento.

## Perguntas frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| **Posso adicionar uma fonte personalizada à camada pesquisável?** | A camada OCR usa Unicode; a aparência visual é fornecida pela imagem subjacente, portanto não é necessário incorporar fontes extras. |
| **E se meu TIF for colorido?** | O Aspose.OCR converte automaticamente imagens coloridas para tons de cinza para OCR, mas você pode manter as cores originais no PDF definindo `PdfOptions.PreserveColor = true`. |
| **A biblioteca é thread‑safe?** | Cada instância `OcrEngine` deve ser usada por uma única thread. Para processamento paralelo, crie um mecanismo separado por thread. |
| **Como criptografar o PDF?** | Use `PdfOptions.Security` para definir senha e permissões após a conversão OCR. |

## Próximos passos (Expanda seu kit de ferramentas PDF)

- **Processamento em lote:** Percorra uma pasta de TIFFs e gere um PDF pesquisável para cada um.  
- **Pós‑processamento:** Use Aspose.PDF para mesclar os PDFs gerados em um único documento mestre.  
- **Metadados avançados:** Preencha campos XMP personalizados para melhor integração com SharePoint ou sistemas ECM.  

Todas essas extensões se baseiam no padrão central que acabamos de cobrir: **criar PDF pesquisável**, **converter imagem para PDF** e **adicionar metadados ao PDF**.

---

*Bom código! Se encontrar algum obstáculo, deixe um comentário abaixo ou consulte a documentação do Aspose.OCR para as atualizações mais recentes da API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}