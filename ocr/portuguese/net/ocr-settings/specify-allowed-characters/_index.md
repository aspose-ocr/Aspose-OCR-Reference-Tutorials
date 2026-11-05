---
date: 2026-05-24
description: Aprenda como melhorar OCR definindo caracteres permitidos com Aspose.OCR
  para .NET, permitindo reconhecimento preciso de dígitos e processamento mais rápido.
  Siga um guia passo a passo.
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: Como melhorar OCR – Definir caracteres permitidos com Aspose.OCR para .NET
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Como melhorar OCR – Definir caracteres permitidos com Aspose.OCR para .NET
url: /pt/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como melhorar OCR – Definir caracteres permitidos com Aspose.OCR para .NET

Neste tutorial você descobrirá **como melhorar os resultados de OCR** ao **especificar caracteres permitidos** ao usar Aspose.OCR para .NET. Restringir o motor de OCR a uma lista branca conhecida — como apenas dígitos — aumenta a precisão, reduz o tempo de processamento e elimina símbolos indesejados. Seja extraindo números de série, IDs de faturas ou leituras de medidores, os passos abaixo permitirão aplicar essa técnica em minutos.

## Respostas rápidas
- **O que faz “specify allowed characters OCR”?** Limita o OCR a uma lista branca predefinida, aumentando drasticamente a precisão para conjuntos de dados direcionados.  
- **Quais caracteres posso permitir?** Qualquer combinação que você precisar — dígitos (`0‑9`), letras maiúsculas, símbolos personalizados ou uma mistura como “ABC‑123”.  
- **Por que limitar os caracteres?** A lista branca reduz reconhecimentos falsos em até 70 % e acelera o processamento em cerca de 30 % em média.  
- **Preciso de licença?** Um teste gratuito funciona para desenvolvimento; uma licença comercial é necessária para implantações em produção.  
- **Quais versões do .NET são suportadas?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Posso combinar isso com pacotes de idioma?** Sim — combine uma lista branca com um pacote de idioma para lidar com cadeias de dígitos multilíngues.

## O que é “specify allowed characters OCR”?

**Resposta direta:** Especificar caracteres permitidos indica ao Aspose.OCR para ignorar todo padrão visual que não corresponda aos caracteres listados, de modo que o motor retorne apenas resultados dessa lista branca. Essa abordagem focada elimina ruído, melhora as pontuações de confiança e reduz o esforço de pós‑processamento. Também acelera o processo de reconhecimento.

## Por que usar Aspose.OCR para reconhecer imagens de dígitos?

**Resposta direta:** O recurso interno `AllowedCharacters` do Aspose.OCR permite reconhecer imagens contendo apenas dígitos com uma única linha de código, oferecendo até 95 % de precisão em digitalizações de baixa resolução sem lógica de filtragem adicional. A biblioteca suporta mais de 30 idiomas, processa lotes de imagens de 500 páginas em menos de 2 segundos por página e funciona totalmente offline, tornando‑a ideal para cenários de alta taxa de transferência e on‑premises, como leitura de medidores de utilidade ou extração de IDs de faturas.

## Pré-requisitos

- Experiência básica em desenvolvimento .NET.  
- Biblioteca **Aspose.OCR for .NET** – faça o download no site oficial **[aqui](https://releases.aspose.com/ocr/net/)**.  
- Visual Studio 2019+ (ou qualquer IDE .NET compatível).  

## Importar Namespaces

Os namespaces a seguir dão acesso ao motor OCR e suas configurações:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Como melhorar OCR especificando caracteres permitidos?

`AsposeOcr` é a classe principal do motor OCR fornecida pela biblioteca Aspose.OCR.  
`RecognizeLine` processa uma única linha de texto de uma imagem e retorna a string reconhecida.

**Resposta direta:** Carregue sua imagem, crie uma instância `AsposeOcr` com uma lista branca apenas de dígitos (`"0123456789"`), chame `RecognizeLine` (ou `Recognize` para múltiplas linhas) e leia a propriedade `Text` do resultado. Esse fluxo de três etapas entrega cadeias numéricas limpas em menos de um segundo para imagens típicas de 300 dpi.

### Etapa 1: Definir o caminho para a pasta de imagens

Defina a pasta que contém as imagens de exemplo que você deseja processar.

```csharp
string dataDir = "Your Document Directory";
```

### Etapa 2: Inicializar Aspose.OCR com uma lista de permissões apenas de dígitos

`AllowedCharacters` é uma propriedade que define a lista branca de caracteres que o motor OCR pode reconhecer.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Etapa 3: Reconhecer uma única linha contendo dígitos

O método `RecognizeLine` escaneia a imagem e retorna a linha que melhor corresponde à lista branca.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Etapa 4: Exibir os dígitos reconhecidos

Grave o resultado no console (ou no log) para que você possa verificar a saída instantaneamente.

```csharp
Console.WriteLine(result);
```

### Etapa 5: Usar `RecognitionSettings` para mais controle

`RecognitionSettings` permite personalizar parâmetros de OCR como DPI, pacotes de idioma e modo de processamento.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Etapa 6: Exibir o resultado do segundo caso

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Etapa 7: Confirmar execução bem-sucedida

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Seguindo esses passos, você aprendeu **como melhorar a precisão do OCR** limitando o conjunto de caracteres e agora pode extrair de forma confiável cadeias de dígitos de imagens usando Aspose.OCR para .NET.

## Armadilhas comuns e solução de problemas

- **Resultado vazio:** Verifique se a imagem tem contraste claro e ruído de fundo mínimo; recomenda‑se no mínimo 300 dpi.  
- **Caracteres inesperados:** Verifique a string da lista branca; espaços extras ou caracteres invisíveis quebrarão o filtro.  
- **Arquivo não encontrado:** Garanta que `dataDir` aponte para a pasta correta e que o nome do arquivo corresponda ao sistema de arquivos sensível a maiúsculas/minúsculas.  
- **Atraso de desempenho:** Para lotes grandes, reutilize uma única instância `AsposeOcr` em vez de criar uma nova para cada imagem.

## Perguntas Frequentes

### Q1: O Aspose.OCR para .NET é adequado tanto para iniciantes quanto para desenvolvedores experientes?
**A:** Absolutamente. A API oferece uma configuração de linha única para tarefas rápidas e `RecognitionSettings` avançados para usuários avançados, atendendo a todos os níveis de habilidade.

### Q2: Posso reconhecer caracteres em vários idiomas enquanto uso uma lista branca de caracteres permitidos?
**A:** Sim. Carregue o pacote de idioma apropriado (por exemplo, `ocrEngine.LoadLanguage("en")`) e combine‑o com uma lista branca como `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` para lidar com cadeias de dígitos multilíngues.

### Q3: Com que frequência o Aspose.OCR para .NET é atualizado?
**A:** Novas versões são publicadas aproximadamente a cada 6‑8 semanas, adicionando suporte a idiomas, melhorias de desempenho e correções de bugs. Veja os detalhes mais recentes na [documentação](https://reference.aspose.com/ocr/net/).

### Q4: Existe um teste gratuito disponível?
**A:** Sim — faça o download do **[free trial](https://releases.aspose.com/)** para avaliar todos os recursos sem licença. O uso em produção requer uma licença comercial.

### Q5: Onde posso obter ajuda da comunidade ou suporte oficial?
**A:** Junte‑se à comunidade ativa no **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** onde você pode fazer perguntas, compartilhar trechos de código e receber orientações dos engenheiros da Aspose.

---

**Last Updated:** 2026-05-24  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose

## Tutoriais Relacionados

- [Configurações de Reconhecimento de Imagem OCR - Especificar Caracteres Ignorados](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Pré‑processar Imagem OCR com Filtros Aspose.OCR para .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [Como Definir Valor de Limiar no Reconhecimento de Imagem OCR](/ocr/net/ocr-settings/set-threshold-value/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}