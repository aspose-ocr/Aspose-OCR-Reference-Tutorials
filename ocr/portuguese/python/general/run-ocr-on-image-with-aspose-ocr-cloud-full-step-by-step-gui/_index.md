---
category: general
date: 2026-03-28
description: Aprenda a executar OCR em imagens, baixar o modelo Hugging Face automaticamente,
  limpar o texto OCR e configurar o modelo LLM em Python usando o Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: pt
og_description: Execute OCR em imagem e limpe a saída usando um modelo Hugging Face
  baixado automaticamente. Este guia mostra como configurar o modelo LLM em Python.
og_title: Executar OCR em Imagem – Tutorial Completo do Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Execute OCR em imagem com Aspose OCR Cloud – Guia completo passo a passo
url: /pt/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Executar OCR em Imagem – Tutorial Completo do Aspose OCR Cloud

Já precisou executar OCR em arquivos de imagem, mas a saída bruta parecia uma bagunça? Na minha experiência, o maior ponto crítico não é o reconhecimento em si — é a limpeza. Felizmente, o Aspose OCR Cloud permite anexar um pós‑processador LLM que pode *limpar o texto OCR* automaticamente. Neste tutorial, vamos percorrer tudo o que você precisa: desde **baixar um modelo do Hugging Face** até configurar o LLM, executar o motor OCR e, finalmente, polir o resultado.

Ao final deste guia você terá um script pronto‑para‑executar que:

1. Baixa um modelo compacto Qwen 2.5 do Hugging Face (baixado automaticamente para você).  
2. Configura o modelo para executar parte da rede na GPU e o resto na CPU.  
3. Executa o motor OCR em uma imagem de nota manuscrita.  
4. Usa o LLM para limpar o texto reconhecido, fornecendo uma saída legível por humanos.

> **Pré‑requisitos** – Python 3.8+, pacote `asposeocrcloud`, uma GPU com pelo menos 4 GB de VRAM (opcional, mas recomendado) e conexão à internet para o primeiro download do modelo.

---

## O Que Você Precisa

- **Aspose OCR Cloud SDK** – instale via `pip install asposeocrcloud`.  
- **Uma imagem de exemplo** – por exemplo, `handwritten_note.jpg` colocada em uma pasta local.  
- **Suporte a GPU** – se você possui uma GPU com CUDA, o script descarregará 30 camadas; caso contrário, ele retornará automaticamente para a CPU.  
- **Permissão de escrita** – o script armazena em cache o modelo em `YOUR_DIRECTORY`; certifique‑se de que a pasta exista.

---

## Etapa 1 – Configurar o Modelo LLM (baixar modelo Hugging Face)

A primeira coisa que fazemos é informar ao Aspose AI onde buscar o modelo. A classe `AsposeAIModelConfig` cuida do download automático, quantização e alocação de camadas na GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Por que isso importa** – Quantizar para `int8` reduz drasticamente o uso de memória (≈ 4 GB vs 12 GB). Dividir o modelo entre GPU e CPU permite rodar um LLM de 3 bilhões de parâmetros mesmo em uma RTX 3060 modesta. Se você não tem GPU, defina `gpu_layers=0` e o SDK manterá tudo na CPU.

> **Dica:** A primeira execução baixará ~ 1,5 GB, então reserve alguns minutos e uma conexão estável.

---

## Etapa 2 – Inicializar o Motor de IA com a Configuração do Modelo

Agora iniciamos o motor Aspose AI e fornecemos a configuração que acabamos de criar.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**O que está acontecendo nos bastidores?** O SDK verifica `directory_model_path` em busca de um modelo existente. Se encontrar uma versão compatível, carrega-a instantaneamente; caso contrário, baixa o arquivo GGUF do Hugging Face, descompacta‑o e prepara o pipeline de inferência.

---

## Etapa 3 – Criar o Motor OCR e Anexar o Pós‑Processador de IA

O motor OCR realiza o trabalho pesado de reconhecer caracteres. Ao anexar `ocr_ai.run_postprocessor` habilitamos **limpeza automática do texto OCR** após o reconhecimento.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Por que usar um pós‑processador?** OCR bruto costuma incluir quebras de linha nos lugares errados, pontuação detectada incorretamente ou símbolos estranhos. O LLM pode reescrever a saída em frases corretas, corrigir ortografia e até inferir palavras ausentes — essencialmente transformando um dump bruto em prosa polida.

---

## Etapa 4 – Executar OCR em um Arquivo de Imagem

Com tudo conectado, é hora de alimentar uma imagem ao motor.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Caso extremo:** Se a imagem for grande (> 5 MP), pode ser interessante redimensioná‑la primeiro para acelerar o processamento. O SDK aceita um objeto Pillow `Image`, então você pode pré‑processar com `PIL.Image.thumbnail()` se necessário.

---

## Etapa 5 – Deixar a IA Limpar o Texto Reconhecido e Mostrar Ambas as Versões

Por fim, invocamos o pós‑processador que anexamos anteriormente. Esta etapa demonstra o contraste entre *antes* e *depois* da limpeza.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Saída Esperada

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Observe como o LLM:

- Corrigiu erros comuns de OCR (`Th1s` → `This`).  
- Removeu símbolos estranhos (`&` → `and`).  
- Normalizou quebras de linha em frases adequadas.

---

## 🎨 Visão Geral Visual (Fluxo de Execução de OCR em Imagem)

![Run OCR on image workflow](run_ocr_on_image_workflow.png "Diagram showing the run OCR on image pipeline from model download to cleaned output")

O diagrama acima resume o pipeline completo: **download do modelo Hugging Face → configurar LLM → inicializar IA → motor OCR → pós‑processador de IA → texto OCR limpo**.

---

## Perguntas Frequentes & Dicas Profissionais

### E se eu não tiver GPU?

Defina `gpu_layers=0` em `AsposeAIModelConfig`. O modelo será executado totalmente na CPU, o que é mais lento, mas ainda funcional. Você também pode mudar para um modelo menor (por exemplo, `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) para manter o tempo de inferência razoável.

### Como mudar o modelo depois?

Basta atualizar `hugging_face_repo_id` e reexecutar `ocr_ai.initialize(model_config)`. O SDK detectará a mudança de versão, baixará o novo modelo e substituirá os arquivos em cache.

### Posso personalizar o prompt do pós‑processador?

Sim. Passe um dicionário para `custom_settings` com a chave `prompt_template`. Por exemplo:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Devo armazenar o texto limpo em um arquivo?

Com certeza. Após a limpeza você pode gravar o resultado em um arquivo `.txt` ou `.json` para processamento posterior:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Conclusão

Acabamos de mostrar como **executar OCR em arquivos de imagem** com Aspose OCR Cloud, **baixar automaticamente um modelo Hugging Face**, configurar habilmente as **configurações do modelo LLM** e, finalmente, **limpar o texto OCR** usando um poderoso pós‑processador LLM. Todo o processo cabe em um único script Python fácil de executar e funciona tanto em máquinas com GPU quanto apenas com CPU.

Se você está confortável com este pipeline, experimente:

- **Modelos diferentes** – teste `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` para uma janela de contexto maior.  
- **Processamento em lote** – percorra uma pasta de imagens e agregue os resultados limpos em um CSV.  
- **Prompts personalizados** – ajuste a IA ao seu domínio (documentos legais, notas médicas, etc.).

Sinta‑se à vontade para ajustar o valor de `gpu_layers`, trocar o modelo ou inserir seu próprio prompt. O céu é o limite, e o código que você tem agora é a plataforma de lançamento.

Bom código, e que suas saídas OCR estejam sempre limpas! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}