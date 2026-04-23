---
date: 2026-04-23
description: Melhore a precisão do OCR com Aspose OCR para .NET, aproveitando a verificação
  ortográfica, o suporte a pacotes de idioma OCR e dicionários personalizados para
  aumentar a qualidade do OCR em documentos digitalizados.
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: Melhore a precisão do OCR com verificação ortográfica em imagens
second_title: Aspose.OCR .NET API
title: Melhore a precisão do OCR com verificação ortográfica em imagens
url: /pt/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Melhorar a Precisão do OCR com Verificação Ortográfica em Imagens

Quando você trabalha com Reconhecimento Óptico de Caracteres (OCR), o objetivo final é **melhorar a precisão do OCR** para que o texto extraído corresponda perfeitamente à imagem original. Palavras com erros ortográficos, fundos ruidosos e fontes incomuns são culpados comuns que degradam o resultado. Ao combinar o mecanismo de verificação ortográfica embutido do Aspose.OCR com seu extenso pacote de idiomas OCR, você pode aumentar drasticamente **a qualidade do OCR** para qualquer documento escaneado.

## Como melhorar a precisão do OCR com verificação ortográfica

Nesta seção, percorreremos o fluxo de trabalho completo — desde o carregamento de uma imagem até a aplicação da verificação ortográfica e, finalmente, o polimento da saída com um dicionário de usuário personalizado. Você verá exemplos reais de antes e depois, aprenderá por que isso é importante ao processar documentos escaneados e descobrirá dicas para aproveitar ao máximo o recurso de verificação ortográfica do OCR.

## Respostas Rápidas
- **O que a verificação ortográfica faz para o OCR?** Ela detecta automaticamente palavras com erros ortográficos na saída do OCR e as substitui pelas alternativas corretas mais prováveis.  
- **Qual biblioteca fornece esse recurso?** Aspose.OCR para .NET inclui uma API de verificação ortográfica pronta para uso.  
- **Preciso de conexão com a internet?** Não, o mecanismo de verificação ortográfica funciona totalmente offline.  
- **Posso adicionar minha própria terminologia?** Sim, você pode fornecer um dicionário de usuário personalizado para lidar com palavras específicas de domínio.  
- **Quais idiomas são suportados?** Veja a seção “aspose ocr language support” para detalhes.

## O que é Verificação Ortográfica no OCR?

A verificação ortográfica examina o texto bruto retornado pelo motor OCR, identifica tokens que não correspondem a palavras conhecidas no dicionário do idioma selecionado e sugere ou aplica correções. Esta etapa é essencial para **melhorar a precisão do OCR**, especialmente ao processar documentos escaneados, recibos ou formulários onde o OCR pode interpretar erroneamente caracteres.

## Por que usar o Pacote de Idioma Aspose OCR?

Aspose.OCR vem com pacotes de idiomas extensos e permite que você conecte dicionários adicionais. Aproveitar **aspose ocr language support** significa que você pode lidar com documentos multilíngues sem escrever analisadores personalizados, e ganha acesso a regras específicas de idioma que melhoram ainda mais a qualidade do reconhecimento.

## Pré-requisitos

Antes de mergulharmos na magia da verificação ortográfica, certifique-se de que os seguintes pré-requisitos estejam atendidos:

- Aspose.OCR para .NET Library: Baixe e instale a biblioteca Aspose.OCR a partir da [release page](https://releases.aspose.com/ocr/net/).

- Diretório de Documentos: Certifique-se de ter um diretório designado para seus documentos. Substitua `"Your Document Directory"` nos trechos de código pelo caminho real.

## Importar Namespaces

Vamos começar importando os namespaces necessários em seu projeto .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Etapa 1: Inicializar Aspose.OCR

Inicialize uma instância do Aspose.OCR para iniciar o processo de OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Etapa 2: Reconhecer Imagem

Em seguida, reconheça o texto em uma imagem usando Aspose.OCR. Aqui está um trecho que demonstra esse processo:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Etapa 3: Antes da Correção

Recupere o resultado do OCR antes da correção para comparar com a versão corrigida.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Etapa 4: Depois da Correção

Aplique a verificação ortográfica para obter o resultado corrigido. O trecho de código a seguir ilustra esta etapa:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Etapa 5: Palavras com Erro Ortográfico e Sugestões

Obtenha uma lista de palavras com erro ortográfico juntamente com as correções sugeridas usando o código a seguir:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Etapa 6: Corrigir Texto do Usuário

Corrija texto específico fornecido pelo usuário usando a biblioteca Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Etapa 7: Correção com Dicionário de Usuário

Aprimore ainda mais a correção incorporando um dicionário de usuário personalizado:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Dicas para Melhorar a Qualidade do OCR

- **Selecione o pacote de idioma OCR correto** que corresponde ao documento de origem. Usar `Language.Eng` em um documento em francês reduzirá drasticamente a precisão.  
- **Pré‑processar imagens** (corrigir inclinação, remover ruído, aumentar contraste) antes de enviá‑las ao motor OCR; imagens mais limpas produzem menos erros ortográficos.  
- **Mantenha um dicionário de usuário conciso**—uma palavra por linha—para que o verificador ortográfico possa localizar rapidamente termos personalizados sem desacelerar lotes grandes.  
- **Processar páginas em lote** ao lidar com PDFs de várias páginas; isso reduz o consumo de memória e acelera a fase de verificação ortográfica.

## Problemas Comuns e Soluções

| Problema | Por que acontece | Como corrigir |
|----------|------------------|---------------|
| Nenhuma sugestão retornada | O pacote de idioma não está carregado ou o texto é muito curto. | Certifique-se de que `RecognitionSettings(Language.Eng)` corresponde ao idioma da imagem de origem e que o resultado do OCR contenha caracteres suficientes. |
| Dicionário personalizado não aplicado | Caminho ou formato de arquivo incorreto. | Verifique se `dictionary.txt` existe no local especificado e usa uma palavra por linha. |
| Verificador ortográfico desacelera documentos grandes | Processar cada palavra individualmente adiciona sobrecarga. | Processar páginas em lotes ou aumentar a alocação de memória se estiver executando no .NET Core. |

## Perguntas Frequentes

### Q1: Posso usar Aspose.OCR para idiomas diferentes do inglês?

A1: Sim, Aspose.OCR suporta vários idiomas. Ajuste as configurações de idioma conforme necessário.

### Q2: Como integrar Aspose.OCR ao meu projeto .NET?

A2: Consulte a [documentation](https://reference.aspose.com/ocr/net/) para etapas detalhadas de integração.

### Q3: Existe uma versão de avaliação disponível para Aspose.OCR?

A3: Sim, você pode explorar os recursos com a [free trial version](https://releases.aspose.com/).

### Q4: Posso enviar um dicionário personalizado para verificação ortográfica?

A4: Absolutamente! O tutorial demonstra como melhorar a correção usando um dicionário fornecido pelo usuário.

### Q5: Onde posso buscar suporte para Aspose.OCR?

A5: Visite o [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) para suporte da comunidade e orientações.

---

**Última atualização:** 2026-04-23  
**Testado com:** Aspose.OCR para .NET versão mais recente  
**Autor:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}