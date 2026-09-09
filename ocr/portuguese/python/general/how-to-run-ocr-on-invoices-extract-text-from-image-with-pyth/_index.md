---
category: general
date: 2026-01-07
description: Como executar OCR e extrair texto de imagem para processamento de faturas.
  Aprenda a melhorar a precisão do OCR, carregar a imagem para OCR e processar OCR
  de faturas de forma eficiente.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: pt
og_description: Como executar OCR em faturas passo a passo. Extraia texto da imagem,
  melhore a precisão do OCR e carregue a imagem para OCR usando o Aspose AI.
og_title: Como Executar OCR em Faturas – Guia Completo de Python
tags:
- OCR
- Python
- Image Processing
title: Como executar OCR em faturas – Extrair texto de imagem com Python
url: /pt/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR em Notas Fiscais – Extrair Texto de Imagem com Python

Já se perguntou **como executar OCR** em uma nota fiscal escaneada e obter texto limpo e pesquisável? Você não está sozinho. Muitos desenvolvedores esbarram em um muro quando a saída bruta do OCR está repleta de erros ortográficos, quebras de linha quebradas e pontuação ausente. Neste tutorial vamos percorrer uma solução full‑stack que não só **extrai texto da imagem**, mas também **melhora a precisão do OCR** ao pós‑processar com um modelo Aspose AI.

Você verá como **carregar a imagem para OCR**, executar o mecanismo embutido e, em seguida, aplicar uma verificação ortográfica leve que deixa o resultado pronto para análises posteriores. Ao final, você terá um script reutilizável que pode ser inserido em qualquer pipeline de processamento de notas fiscais.

> **O que você precisará**  
> * Python 3.9 ou superior  
> * Pacotes `aspose-ocr` e `aspose-ai` (instalados via `pip`)  
> * Uma imagem de nota fiscal (PNG, JPEG ou TIFF) – usaremos `sample_invoice.png` como exemplo  
> * Opcional: uma GPU com pelo menos 4 GB de VRAM para inferência mais rápida (o script funciona em CPU também)

---

## Etapa 1: Instalar Pacotes Necessários e Preparar o Ambiente

Antes de podermos **carregar a imagem para OCR**, precisamos garantir que as bibliotecas necessárias estejam disponíveis. O motor Aspose OCR vem com um wrapper Python simples, enquanto o pós‑processador AI depende de um modelo quantizado da Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Dica profissional:** Se você pretende usar aceleração por GPU, instale `torch` com suporte CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Etapa 2: Carregar a Imagem da Nota Fiscal

Carregar a imagem é direto, mas vale mencionar por que definimos explicitamente o caminho como uma string bruta (`r"..."`). Isso evita problemas acidentais de caracteres de escape em caminhos do Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Por que isso importa:* Usar `ocr.Image.load` garante que a imagem seja pré‑processada (binarização, correção de inclinação) de acordo com os padrões ótimos da Aspose, o que já **melhora a precisão do OCR** antes de qualquer mágica de IA acontecer.

---

## Etapa 3: Executar o Motor OCR Incorporado

Agora realmente **executamos o OCR** e capturamos o texto bruto. Esta etapa mostra a saída típica que você obteria de uma execução OCR padrão — frequentemente uma bagunça de quebras de linha e erros ortográficos ocasionais.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Saída bruta típica** (truncada para brevidade):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Você pode notar que “Invoice” aparece como “Invo1ce” ou que a pontuação está ausente. É aí que o pós‑processador AI entra em ação.

---

## Etapa 4: Configurar o Modelo Aspose AI

O modelo AI que usaremos é **Qwen2.5‑3B‑Instruct‑GGUF**, um LLM leve ajustado por instrução que roda confortavelmente em uma GPU de médio porte. A configuração abaixo indica à Aspose onde buscar o modelo, quantas camadas manter na GPU e o tamanho de contexto para lidar com parágrafos longos.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Por que essa configuração?**  
> * `gpu_layers=30` equilibra velocidade e memória — a maior parte da inferência ocorre na GPU, enquanto as camadas restantes permanecem na CPU para evitar erros de OOM.  
> * `context_size=4096` garante que o modelo possa ver a nota fiscal inteira de uma vez, impedindo o truncamento de campos importantes.

---

## Etapa 5: Criar um Pós‑Processador de Verificação Ortográfica Simples

Envolvemos a chamada AI em uma função pequena chamada `simple_spell_check`. O prompt é deliberadamente conciso: “Correct spelling and punctuation:” seguido do texto OCR bruto. O modelo devolve uma versão limpa.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Como funciona:** `ai.run_prompt` envia o prompt para o LLM carregado localmente, que então retorna uma única string com ortografia corrigida, pontuação adequada e um layout de quebras de linha mais natural.

---

## Etapa 6: Aplicar o Pós‑Processador ao Texto OCR Bruto

Agora a mágica acontece. Alimentamos a saída OCR bruta ao nosso pós‑processador e imprimimos o resultado aprimorado.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Exemplo de saída aprimorada**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Observe a correção da ortografia de “Invoice”, o uso correto de dois‑pontos e quebras de linha consistentes — exatamente o que você precisa para um parsing confiável nas etapas posteriores.

---

## Etapa 7: Liberar Recursos

Tanto o motor OCR quanto o modelo AI alocam recursos nativos. É uma boa prática liberá‑los quando terminar, especialmente em serviços de longa duração.

```python
ai.free_resources()
engine.dispose()
```

---

## Script Completo – Pronto para Colar

Abaixo está o script completo e executável que une todas as etapas. Salve como `invoice_ocr.py`, substitua `YOUR_DIRECTORY` pela pasta que contém sua imagem de nota fiscal e execute com `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Execute o script e você verá tanto o dump ruidoso do OCR bruto quanto a versão polida, **com precisão de OCR aprimorada**, lado a lado.

---

## Perguntas Frequentes & Casos de Borda

### 1. E se minha imagem de nota fiscal for um PDF de várias páginas?

Aspose OCR pode carregar páginas de PDF diretamente. Substitua a linha de carregamento da imagem por:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Itere `page_index` para processar cada página sequencialmente.

### 2. Minha GPU fica sem memória — posso usar apenas CPU?

Absolutamente. Defina `gpu_layers=0` na `AsposeAIModelConfig`. O modelo rodará totalmente na CPU, o que é mais lento, mas seguro para hardware de baixa capacidade.

### 3. Como lidar com notas fiscais que não são em inglês?

Troque o ID do repositório do modelo por um modelo específico de idioma, por exemplo, `"mistralai/Mistral-7B-Instruct-v0.2"` para suporte multilíngue. O restante do pipeline permanece inalterado.

### 4. Posso encadear múltiplos pós‑processadores (ex.: formatar datas, extrair totais)?

Sim. `ai.set_post_processor` aceita uma lista de callables. Por exemplo:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

A saída será primeiro verificada ortograficamente e depois terão os totais extraídos.

---

## Dicas de Performance & Boas Práticas

| Dica | Por que ajuda |
|------|----------------|
| **Processar várias notas em lote** – carregue-as em uma lista e processe em um loop. | Reduz a sobrecarga do interpretador Python e mantém o modelo AI aquecido na memória. |
| **Cachear o modelo** – evite chamar `initialize` repetidamente em um serviço web. | O carregamento do modelo pode levar ~30 segundos; o cache fornece respostas instantâneas. |
| **Redimensionar imagens grandes** para 1500 px de largura antes do OCR. | Imagens menores aceleram tanto o OCR quanto a inferência AI sem sacrificar a precisão. |
| **Definir `allow_auto_download="false"` em produção** – inclua o modelo na sua implantação. | Garante tempos de inicialização determinísticos e evita falhas de rede. |

---

## Conclusão

Cobrimos **como executar OCR** em notas fiscais, desde o carregamento da imagem até o polimento do resultado com uma verificação ortográfica impulsionada por IA. Seguindo estas etapas, você pode **extrair texto de imagem**, **melhorar a precisão do OCR** e processar notas fiscais de forma fluida em qualquer fluxo de trabalho baseado em Python.

Teste com diferentes layouts de notas — talvez um recibo manuscrito ou um contrato escaneado. O mesmo pipeline se adapta com ajustes mínimos, provando que uma combinação bem estruturada de OCR + IA é uma ferramenta versátil para qualquer projeto de automação de documentos.

Se este guia foi útil, considere compartilhá‑lo com colegas ou dar uma estrela ao repositório que hospeda os pacotes Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}