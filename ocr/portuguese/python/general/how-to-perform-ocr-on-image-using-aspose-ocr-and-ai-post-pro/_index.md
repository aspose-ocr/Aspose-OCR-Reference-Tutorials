---
category: general
date: 2026-09-25
description: Aprenda como realizar OCR em uma imagem com Aspose OCR, carregar a imagem
  para OCR e reconhecer texto de um recibo em um exemplo completo em Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: pt
lastmod: 2026-09-25
og_description: Execute OCR em imagem usando Aspose OCR em Python. Este guia mostra
  como carregar a imagem para OCR e reconhecer texto de um recibo com aprimoramento
  de IA.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: Realize OCR em imagem com Aspose OCR e pós-processador de IA – Guia Python
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: Como realizar OCR em imagem usando Aspose OCR e pós-processador de IA em Python
url: /pt/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como executar OCR em imagem usando Aspose OCR e pós‑processador de IA em Python

Se você precisa **executar OCR em arquivos de imagem** em Python, este tutorial mostra uma solução completa, pronta‑para‑executar. Você aprenderá como **carregar imagem para OCR**, executar o motor Aspose OCR e **reconhecer texto de documentos de recibo** com pós‑processamento opcional impulsionado por IA.

Percorreremos cada passo, desde a instalação do SDK até a liberação de recursos, para que você possa integrar extração de texto confiável em suas próprias aplicações sem perder nenhum detalhe.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- Python 3.8+ instalado  
- Aspose OCR para Python via pip (`pip install aspose-ocr`)  
- Acesso à internet para o download opcional do modelo de IA  
- Uma imagem de recibo de exemplo (`receipt.png`) colocada em um diretório conhecido  

Nenhum serviço externo adicional é necessário; o código roda localmente e usa o modelo gratuito Qwen2‑3B‑Instruct quando camadas de GPU estão disponíveis.

## Etapa 1: Instalar os pacotes necessários

```bash
pip install aspose-ocr
```

O pacote `aspose-ocr` contém tanto a classe `OcrEngine` quanto o pós‑processador `AsposeAI` que usaremos para **executar OCR em arquivos de imagem**.

## Etapa 2: Criar e configurar o motor OCR – carregar imagem para OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

Chamar `load_image` informa ao motor qual arquivo analisar. Você pode substituir o caminho por qualquer arquivo PNG, JPG ou TIFF que precise **executar OCR em imagem**.

## Etapa 3: Configurar o pós‑processador opcional AsposeAI

O pós‑processador de IA pode corrigir ortografia, melhorar formatação ou aplicar lógica personalizada após o resultado bruto do OCR ser retornado.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

A configuração instrui o processador a baixar o modelo Qwen2 padrão, permitindo que você **execute OCR em imagem** com compreensão de linguagem de nível superior.

## Etapa 4: Anexar uma função simples de pós‑processamento

Você pode conectar qualquer callable que receba o texto bruto e retorne uma versão corrigida. Aqui está um exemplo mínimo que corrige um erro de digitação comum:

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

Como a função está registrada, toda vez que você chamar `run_postprocessor`, a saída do OCR passará por esta etapa.

## Etapa 5: Executar OCR e aprimorar o resultado – reconhecer texto de recibo

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

A chamada `recognize` devolve um objeto cujo atributo `text` contém os caracteres brutos extraídos da imagem do recibo. A chamada subsequente `run_postprocessor` devolve um novo resultado onde nossa verificação ortográfica (e quaisquer melhorias baseadas em modelo) foram aplicadas.

### Saída esperada

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

Observe como o texto aprimorado por IA corrige o erro de digitação e insere quebras de linha para melhorar a legibilidade — exatamente o que você deseja ao **reconhecer texto de recibo**.

## Etapa 6: Liberar recursos

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

Liberar recursos é especialmente importante ao processar muitas imagens em um serviço de longa duração.

## Script completo executável

Juntando todas as peças, você obtém um único script que pode copiar, colar e executar:

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

Execute o script com:

```bash
python ocr_receipt.py
```

Você deverá ver as saídas original e aprimorada por IA impressas no console.

## Dicas avançadas e armadilhas comuns

- **A qualidade da imagem importa** – garanta que a imagem do recibo esteja bem iluminada e não excessivamente comprimida; caso contrário, o motor OCR pode perder caracteres, reduzindo o benefício do pós‑processamento.  
- **Disponibilidade de GPU** – se sua máquina não possuir uma GPU compatível, defina `gpu_layers=0` para forçar inferência em CPU; o modelo ainda será executado, embora mais lentamente.  
- **Pós‑processadores personalizados** – você pode encadear várias funções ou usar um modelo de linguagem mais sofisticado para reformatar datas, valores ou nomes de fornecedores.  
- **Processamento em lote** – instancie um único objeto `AsposeAI` e reutilize‑o em várias instâncias de `OcrEngine` para evitar downloads repetidos do modelo.  

## Conclusão

Agora você sabe como **executar OCR em arquivos de imagem** usando Aspose OCR, como **carregar imagem para OCR** e como **reconhecer texto de recibo** com aprimoramentos impulsionados por IA. Seguindo os passos acima, você pode integrar processamento de recibos preciso e de alta taxa de transferência em qualquer aplicação Python.

**Próximos passos**: explore técnicas adicionais de pós‑processamento, como normalização de moedas, integre o resultado em um banco de dados ou troque para um modelo maior para recibos multilíngues. Para personalizações mais avançadas, consulte a documentação do Aspose OCR sobre pacotes de idioma personalizados e pré‑processamento avançado de imagens.

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Perform OCR in C# – Extract Text from Image Using Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}