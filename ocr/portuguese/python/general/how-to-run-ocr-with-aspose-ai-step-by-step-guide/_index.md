---
category: general
date: 2026-02-09
description: como executar OCR usando Aspose AI e um modelo Hugging Face – aprenda
  a baixar o modelo Hugging Face, corrigir erros de OCR e liberar memória da GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: pt
og_description: Como executar OCR com o Aspose AI é explicado no primeiro parágrafo
  – descubra como baixar o modelo Hugging Face, corrigir erros de OCR e liberar memória
  da GPU.
og_title: como executar OCR com Aspose AI – Guia Completo
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Como executar OCR com Aspose AI – Guia passo a passo
url: /pt/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como executar OCR com Aspose AI – Guia Completo

Já se perguntou **como executar OCR** em uma nota fiscal escaneada e obter números perfeitamente limpos sem passar horas corrigindo erros de digitação? Você não está sozinho. Em muitos projetos do mundo real, o texto bruto que sai de um motor OCR clássico ainda contém caracteres estranhos, símbolos de moeda quebrados ou dígitos embaralhados — especialmente quando a imagem de origem está ruidosa.  

A boa notícia é que você pode conectar um LLM ao Aspose OCR, baixar um modelo Hugging Face on‑the‑fly e deixar a IA polir a saída para você. Neste tutorial vamos percorrer todo o pipeline, desde a obtenção do modelo (sim, vamos mostrar como **download hugging face model** automaticamente) até a liberação dos recursos da GPU quando terminar. Ao final, você terá um script reproduzível que **corrects OCR errors**, roda rápido em uma GPU modesta e limpa tudo depois de si, evitando desperdício de memória.

## O que você aprenderá

- Configurar o Aspose AI para buscar um modelo **Qwen2.5‑3B‑Instruct‑GGUF** no Hugging Face.  
- Executar o motor padrão Aspose OCR em um arquivo de imagem.  
- Usar um prompt LLM customizado que mantém números e símbolos de moeda intactos.  
- Liberar memória da GPU com a rotina embutida **free gpu memory**.  
- Ajustar o fluxo de trabalho para casos extremos como PDFs de várias páginas ou GPUs de baixa performance.

> **Pré‑requisitos** – Python 3.9+, pacote `aspose-ocr`, acesso à internet para o primeiro download do modelo e uma GPU com pelo menos 4 GB de VRAM (opcional, mas recomendado). Se você não tem uma GPU, o script automaticamente recairá para CPU nas camadas restantes.

---

## Como Executar OCR e Melhorar os Resultados

Abaixo está o script Python completo, pronto‑para‑executar. Salve‑o como `ocr_with_ai.py` e substitua os caminhos de placeholder pelos seus próprios arquivos.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Dica profissional:** O parâmetro `gpu_layers` permite decidir quantas camadas do transformer permanecem na GPU. Se você estiver encontrando erros de falta de memória, diminua esse número e o restante será executado na CPU – você ainda poderá **free gpu memory** mais tarde com `ai.free_resources()`.

### Saída esperada

Executar o script em uma nota fiscal de exemplo produz algo como:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Observe como a IA corrigiu o “O” em `$1O0.00` para um zero correto, preservando o símbolo do dólar. Essa é a essência de **correct OCR errors** para documentos financeiros.

---

## Download Hugging Face Model – O que acontece nos bastidores?

Quando você define `allow_auto_download="true"` o wrapper Aspose AI verifica o `directory_model_path`. Se os arquivos do modelo não estiverem lá, ele acessa o Hugging Face Hub, puxa a versão **int8‑quantized** de `Qwen2.5‑3B‑Instruct‑GGUF` e a armazena localmente. Esse download único costuma ter menos de 2 GB, tornando‑o viável mesmo em SSDs modestos.

> **Por que int8?** Quantizar para 8‑bits reduz drasticamente o uso de memória — crucial quando você também quer **free gpu memory** após o processamento. O trade‑off é uma pequena perda de precisão, mas para pós‑processamento de texto OCR o impacto é insignificante.

Se preferir hospedar o modelo você mesmo, basta colocar os arquivos `.gguf` em `YOUR_DIRECTORY/Models` e o Aspose os carregará sem precisar acessar a internet novamente.

---

## Como liberar a GPU – Melhores práticas

Recursos de GPU são um bem compartilhado em muitas estações de trabalho. Deixar tensores vivos após o término do script pode causar erros “CUDA out of memory” em jobs subsequentes. A chamada `ai.free_resources()` faz três coisas:

1. **Disposes the underlying transformer** – todos os pesos residentes na GPU são liberados.  
2. **Clears the PyTorch cache** – `torch.cuda.empty_cache()` é invocado internamente.  
3. **Deletes temporary files** – quaisquer caches em disco criados durante o download são removidos.

Você também pode invocar manualmente `torch.cuda.empty_cache()` se estiver combinando Aspose AI com outras cargas de trabalho PyTorch, mas o método embutido geralmente é suficiente.

---

## Passo a passo (H2s com palavras‑chave secundárias)

### Download Hugging Face Model Automatically

O construtor `AsposeAIModelConfig` esconde a complexidade de lidar com a API Hugging Face. Apenas certifique‑se de ter acesso à internet na primeira execução do script. Depois disso, o modelo fica em `YOUR_DIRECTORY/Models`, e execuções subsequentes iniciam instantaneamente.

### Free GPU Memory After Inference

Se você estiver rodando isso dentro de um serviço de longa duração (por exemplo, uma API Flask), chame `ai.free_resources()` após cada requisição. Isso previne vazamentos de memória e garante que a próxima requisição possa reutilizar a mesma GPU sem interrupções.

### Correct OCR Errors with a Custom Prompt

Nossa função `financial_prompt` retorna um dicionário com uma única chave `prompt`. Você pode adaptá‑la a qualquer domínio:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Troque o nome da função em `ai.set_post_processor(...)` e você terá um pipeline de **correct OCR errors** para registros médicos.

### How to Run OCR on Multi‑Page PDFs

Aspose OCR pode lidar com PDFs nativamente:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Depois de obter a string bruta, o mesmo pós‑processador LLM limpará o texto de cada página. Nenhum código extra necessário.

### When You Don’t Have a GPU – How to Free GPU (Even Without One)

Mesmo em máquinas apenas com CPU, chamar `ai.free_resources()` não causa problemas. Ele simplesmente limpa caches internos, o que ainda pode liberar RAM. Portanto, o conselho **how to free gpu** se aplica universalmente: sempre limpe depois de usar.

---

## Armadilhas comuns & como as resolvemos

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Out‑of‑Memory on GPU** | `gpu_layers` definido alto demais para sua placa | Reduza `gpu_layers` para 10 ou 5, deixe o restante rodar na CPU |
| **Model never downloads** | Firewall corporativo bloqueia HTTPS para huggingface.co | Baixe o modelo manualmente em outra rede e aponte `directory_model_path` para a pasta local |
| **Numbers get corrupted** | Prompt não explícito o suficiente sobre preservação de dígitos | Adicione “preserve all numeric values and currency symbols exactly as they appear” ao prompt |
| **`free_resources` raises an exception** | Uso de versão antiga do Aspose OCR | Atualize para o último pacote `aspose-ocr` (pip install --upgrade aspose-ocr) |

---

## Recapitulação do Exemplo Completo

Aqui está o script novamente, agora com comentários inline que explicam cada linha para referência futura:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Conclusão

Cobrimos **how to run OCR** com Aspose, baixamos um modelo Hugging Face sob demanda, criamos um prompt que **corrects OCR errors** e, finalmente, **free gpu memory** para que sua estação de trabalho permaneça responsiva. Todo o fluxo de trabalho cabe em um único arquivo Python autônomo — sem scripts externos, sem manipulação manual de modelo e sem alocações de GPU persistentes.

Próximos passos? Experimente trocar o `financial_prompt` por um

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}