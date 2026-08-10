---
category: general
date: 2026-05-25
description: Aprenda como extrair texto de uma imagem com uma API mínima ASP.NET Core.
  Envie a imagem via POST, leia os dados de formulário multipart e execute OCR na
  imagem.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: pt
og_description: Extrair texto de imagem usando uma API minimal do ASP.NET Core. Este
  guia mostra como fazer upload de imagem via POST, ler dados de formulário multipart
  e realizar OCR na imagem.
og_title: Extrair Texto de Imagem no ASP.NET Core – Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Extrair Texto de Imagem em ASP.NET Core Minimal API – Guia Completo
url: /pt/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em ASP.NET Core Minimal API – Guia Completo

Já se perguntou como **extrair texto de imagem** sem lidar com frameworks pesados? Você não está sozinho. Muitos desenvolvedores precisam de uma maneira rápida de permitir que os usuários enviem uma foto e recebam de volta os caracteres brutos, seja escaneando recibos, digitalizando notas manuscritas ou alimentando um índice de busca.

Neste tutorial vamos criar uma pequena ASP.NET Core Minimal API que **faz upload de imagem via POST**, analisa o payload *multipart/form‑data* e então **executa OCR na imagem** usando um singleton `OcrEngine`. Ao final, você terá um aplicativo totalmente executável que pode ser inserido em qualquer projeto .NET 8 e começar a extrair texto de imagem imediatamente.

## O que você vai construir

- Um aplicativo web minimal que escuta em `/ocr`.
- Um endpoint que aceita um arquivo de imagem enviado com uma requisição POST `multipart/form-data`.
- Lógica que lê o arquivo enviado, o encaminha para o motor OCR e retorna resultados em texto simples.
- Trecho opcional de aceleração por GPU (comentado) para quem tem uma placa compatível.

**Pré-requisitos**  
- .NET 8 SDK (ou superior).  
- Familiaridade básica com C# e a linha de comando.  
- Uma biblioteca OCR que exponha a classe `OcrEngine` (o exemplo assume um pacote NuGet hipotético).

Se você tem isso, vamos mergulhar.

## Etapa 1: Configurar o Projeto e Adicionar o Pacote OCR

Primeiro, crie um novo projeto web e inclua a biblioteca OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Dica profissional:** Mantenha suas dependências atualizadas. Versões mais recentes costumam trazer ganhos de desempenho, especialmente para inferência acelerada por GPU.

## Etapa 2: Registrar um Engine OCR Singleton (Serviço Principal)

Queremos uma única instância de `OcrEngine` para todo o aplicativo — não há necessidade de criar um novo engine por requisição. Registre-a no contêiner de serviços do builder.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**Por que um singleton?**  
Criar um engine OCR pode ser caro — pense em carregar pesos de redes neurais na memória. Reutilizando a mesma instância, economizamos ciclos de CPU e RAM, o que se traduz em tempos de resposta mais rápidos para cada chamada `/ocr`.

## Etapa 3: Construir a Aplicação

Agora materializamos o objeto `WebApplication`.

```csharp
var app = builder.Build();
```

Essa linha parece quase mágica, mas nos bastidores ela configura o roteamento, middleware e o contêiner DI que acabamos de configurar.

## Etapa 4: Definir o Endpoint POST – “Upload Image via POST”

Aqui está o coração do tutorial: um endpoint que **faz upload de imagem via POST**, lê o payload multipart e entrega os dados ao engine OCR.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Detalhando a Lógica

| Etapa | O que acontece | Por que importa |
|------|----------------|-----------------|
| **ReadFormAsync** | Analisa a requisição *multipart/form-data* entrante. | Sem isso, você não pode acessar os arquivos enviados. |
| **form.Files["image"]** | Recupera o arquivo cujo nome de campo no formulário é `image`. | Garante um contrato previsível para os chamadores. |
| **Content‑type check** | Verifica se o arquivo é uma imagem (ex., `image/png`). | Impede que o engine OCR falhe ao receber dados que não são imagens. |
| **Image.FromStream** | Converte o fluxo bruto em um `System.Drawing.Image`. | A biblioteca OCR espera um objeto `Image`, não um array de bytes bruto. |
| **ocr.Recognize(img)** | Chama o engine OCR para **como reconhecer texto a partir da imagem**. | Este é o passo central de **executar OCR na imagem**. |
| **Results.Text** | Retorna a resposta em texto simples. | Um formato simples e consumível para serviços downstream. |

## Etapa 5: Executar a API

Finalmente, inicie o servidor web.

```csharp
app.Run();
```

Ao executar `dotnet run`, a API ouvirá em `http://localhost:5000` (ou em uma porta de sua escolha). Você pode testá-la com `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Saída esperada:** O console imprimirá os caracteres reconhecidos, por exemplo:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Se a imagem estiver borrada ou o idioma não for suportado, o engine OCR retornará uma string vazia ou uma mensagem de erro — trate esses casos no código de produção.

## Casos de Borda & Boas Práticas

### 1. Arquivos Grandes

O limite padrão do corpo da requisição é 30 MB. Para digitalizações maiores, talvez seja necessário ajustar:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR Assíncrono

Algumas bibliotecas OCR expõem métodos assíncronos (`RecognizeAsync`). Se a sua fizer isso, substitua `ocr.Recognize(img)` por `await ocr.RecognizeAsync(img)` e marque a lambda como `async`.

### 3. Considerações de Segurança

- **Validar o tamanho do arquivo** antes de carregá-lo na memória.
- **Sanitizar o nome do arquivo** se você alguma vez o gravar em disco.
- **Aplicar rate‑limit** ao endpoint para evitar ataques de negação de serviço.

### 4. Aceleração por GPU

Se você descomentar a linha `engine.GpuDevice = new GpuDevice(0);` e seu hardware suportar CUDA ou DirectML, verá um aumento de velocidade perceptível, especialmente em imagens de alta resolução.

## Exemplo Completo Funcional

Abaixo está o `Program.cs` completo que você pode copiar‑colar em um novo projeto Minimal API.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Salve, execute `dotnet run`, e você estará pronto para **extrair texto de imagem** sob demanda.

## Conclusão

Percorremos uma **solução completa, de ponta a ponta** para extrair texto de imagem usando ASP.NET Core Minimal API. Começando da estruturação do projeto, **registramos um engine OCR singleton**, construímos um endpoint que **faz upload de imagem via POST**, **lê dados multipart de formulário**, e finalmente **executa OCR na imagem** para retornar texto simples limpo.

A partir daqui você pode:

- Adicionar wrappers JSON para respostas mais ricas.  
- Conectar um banco de dados para armazenar o texto extraído.  
- Expandir o suporte para múltiplos idiomas (`OcrLanguage.Spanish`, etc.).  

O padrão escala bem — basta inserir o mesmo endpoint em um microserviço maior ou expô-lo por trás de um gateway de API.

Tem perguntas sobre manipulação de PDFs, processamento em lote ou ajuste de GPU? Deixe um comentário, e feliz codificação!

## Tutoriais Relacionados

- [Extrair Texto de Imagem Usando Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrair Texto de Imagem – Otimização OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}