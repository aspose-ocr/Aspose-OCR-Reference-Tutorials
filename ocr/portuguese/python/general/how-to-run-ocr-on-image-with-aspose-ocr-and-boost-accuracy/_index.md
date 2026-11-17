---
category: general
date: 2026-09-22
description: Aprenda como executar OCR em imagens usando o Aspose OCR, configurar
  o modelo OCR, extrair texto de faturas e melhorar a precisão do OCR em Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: pt
lastmod: 2026-09-22
og_description: Execute OCR em imagem com Aspose OCR, configure o modelo OCR, extraia
  texto de fatura e melhore a precisão do OCR em um tutorial completo, passo a passo.
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: Execute OCR em imagem com Aspose OCR – guia completo em Python
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: Como executar OCR em imagem com Aspose OCR e melhorar a precisão
url: /pt/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como executar OCR em imagem com Aspose OCR e melhorar a precisão

Se você precisa **executar OCR em imagem** arquivos em Python, este guia mostra um fluxo de trabalho completo, pronto para produção. Você verá como configurar o modelo OCR, extrair texto de fotos de faturas e melhorar a precisão do OCR com o pós‑processador de IA da Aspose.

Processar faturas escaneadas é um ponto crítico—o OCR bruto costuma retornar palavras com erros de ortografia ou números quebrados. Ao final deste tutorial você terá um script pronto‑para‑executar que fornece extração de texto mais limpa e confiável, e entenderá por que cada etapa de configuração é importante.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8 ou mais recente instalado.
* Uma licença ativa do Aspose OCR (o teste gratuito funciona para avaliação).
* Uma imagem de fatura de exemplo (por exemplo, `sample_invoice.png`) colocada em um diretório conhecido.
* Familiaridade básica com a instalação de pacotes Python.

Nenhuma dependência adicional ao nível do sistema é necessária; o SDK lida com o download dos modelos automaticamente.

## Etapa 1: Instalar o pacote Aspose OCR

A primeira coisa que você deve fazer é adicionar a biblioteca Aspose OCR ao seu ambiente. O pacote inclui o modelo de IA e o pós‑processador que você usará mais adiante.

```bash
pip install aspose-ocr
```

Executar este comando instala `asposeocr`, que fornece a classe `AsposeAI` usada para **configurar as definições do modelo OCR** como downloads automáticos e execução apenas em CPU.

## Etapa 2: Configurar o modelo OCR (opcional, mas recomendado)

Ajustar o modelo melhora velocidade e precisão, especialmente quando você executa OCR em imagens de faturas que contêm muitos números e caracteres especiais. O código a seguir demonstra as configurações mais úteis:

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*Por que essas flags?*  
* `allow_auto_download` garante que o modelo OCR esteja presente mesmo em uma máquina nova.  
* `gpu_layers = 0` elimina a necessidade de uma GPU compatível com CUDA, que muitos desenvolvedores não possuem.  
* `context_size` controla quantos tokens ao redor o IA considera ao corrigir erros; uma janela maior costuma **melhorar a precisão do OCR** em textos densos como faturas.

## Etapa 3: Inicializar o motor de IA

A inicialização valida que os arquivos do modelo estão prontos e os carrega na memória. Pular esta etapa pode gerar um erro em tempo de execução quando você chamar o pós‑processador posteriormente.

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

Se o motor falhar, a exceção informa exatamente onde o problema ocorreu, economizando tempo de depuração.

## Etapa 4: Executar o motor OCR padrão em uma imagem

Agora você pode **executar OCR em imagem** arquivos. A classe `OcrEngine` realiza a extração de texto bruta sem correções baseadas em IA.

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` contém a string simples que o motor OCR reconheceu. Em uma fatura típica, você pode observar dígitos ausentes, pontuação fora de lugar ou palavras quebradas.

## Etapa 5: Aplicar o pós‑processador de IA para melhorar a precisão do OCR

O pós‑processador de IA da Aspose analisa a saída bruta e corrige erros comuns de OCR (por exemplo, “5um” → “Sum”). Executar esta etapa é a chave para **melhorar a precisão do OCR** em documentos financeiros.

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

O pós‑processador usa a configuração definida na Etapa 2, portanto o `context_size` maior contribui para correções mais confiáveis.

## Etapa 6: Extrair texto da fatura e exibir resultados

Neste ponto você tem duas versões do texto extraído: a saída OCR bruta e a versão aprimorada por IA. Imprimir ambas permite verificar a melhoria e também oferece a oportunidade de registrar os dados originais para fins de auditoria.

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**Saída típica**

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Observe como a etapa de IA corrigiu as trocas zero‑um e ajustou a formatação dos valores—exatamente o tipo de melhoria que você precisa ao **extrair texto de fatura** arquivos.

## Etapa 7: Liberar recursos

Por fim, libere os recursos nativos usados pelo motor de IA. Isso é especialmente importante em serviços de longa duração ou trabalhos em lote.

```python
# Release resources when finished
ai.free_resources()
```

Negligenciar esta chamada pode causar vazamentos de memória porque o modelo subjacente roda em código nativo.

## Script completo que você pode copiar‑colar

Abaixo está o programa completo e executável que incorpora todas as etapas descritas acima. Substitua `YOUR_DIRECTORY` pelo caminho real do seu arquivo de imagem.

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

Salve como `process_invoice.py` e execute:

```bash
python process_invoice.py
```

Você deverá ver o texto bruto e o texto corrigido impressos no console, confirmando que você **executou OCR em imagem**, **configurou o modelo OCR** e **melhorou a precisão do OCR** para sua tarefa de extração de faturas.

## Perguntas frequentes e casos de borda

| Pergunta | Resposta |
|----------|----------|
| *E se o modelo falhar ao baixar?* | Verifique se sua máquina tem acesso à internet e se a flag `allow_auto_download` está definida como `"true"`. Você também pode baixar o modelo manualmente do portal Aspose e apontar `AsposeAI` para a pasta local via `ai.model_path = "path/to/model"` |
| *Posso executar isso em uma GPU?* | Sim. Defina `ai.gpu_layers` para um inteiro positivo (por exemplo, `2`) e instale as bibliotecas CUDA apropriadas. A execução em GPU acelera lotes grandes, mas requer uma GPU compatível. |
| *Como processar muitas faturas em uma pasta?* | Envolva a lógica principal em um loop que itere sobre `os.listdir(folder)`. Lembre‑se de chamar `ai.free_resources()` somente após o término do loop, não após cada arquivo, para manter o modelo carregado. |
| *O pós‑processador é seguro para faturas não‑inglês?* | O modelo padrão foi treinado com texto em inglês. Para outros idiomas, baixe o pacote de idioma correspondente e defina `ai.language = "fr"` (ou o código ISO adequado). |
| *E se o resultado do OCR estiver vazio?* | Verifique se `image_path` aponta para uma imagem legível e se o arquivo não está corrompido. Você também pode aumentar `ai.context_size` para dar ao modelo mais contexto em digitalizações de baixa qualidade. |

## Próximos passos

Agora que você pode **executar OCR em imagem** e extrair texto de fatura de forma confiável, considere estas extensões:

* **Processamento em lote** – combine o script com `multiprocessing` para lidar com milhares de faturas em paralelo.  
* **Validação de dados** – use expressões regulares para verificar números de fatura, datas e valores monetários após a extração.  
* **Integração com bancos de dados** – armazene o texto limpo diretamente no PostgreSQL ou MongoDB para análises posteriores.  
* **Ajuste fino de modelo personalizado** – se você possui um grande conjunto de dados proprietário, treine um modelo específico para o domínio e aponte `ai.model_path` para ele, obtendo ainda mais precisão.

Experimentando essas ideias, você transformará uma demonstração simples de OCR em um pipeline robusto de processamento de documentos que atende aos requisitos de produção.

---

*Agora você sabe como **executar OCR em imagem** com Aspose OCR, configurar o modelo OCR para desempenho ideal e melhorar a precisão do OCR usando o pós‑processador de IA. Aplique estas etapas aos seus próprios fluxos de processamento de faturas e desfrute de extração de texto mais limpa e confiável.*

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Run OCR on Invoices – Extract Text from Image with Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}