---
category: general
date: 2026-07-05
description: Como listar modelos com Aspose AI, habilitar download automático e baixar
  modelo Hugging Face em Python. Siga este tutorial passo a passo para configurar
  o cache e começar a usar o Aspose AI hoje.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: pt
og_description: Como listar modelos com Aspose AI, habilitar o download automático
  e baixar um modelo do Hugging Face. Aprenda a configurar o cache e usar o Aspose
  AI em minutos.
og_title: Como listar modelos com Aspose AI – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Como listar modelos com Aspose AI – Guia Completo
url: /pt/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como listar modelos com Aspose AI – Guia Completo

Como listar modelos com Aspose AI é uma pergunta que surge no momento em que você começa a experimentar com grandes modelos de linguagem em Python. Neste tutorial, vamos percorrer a habilitação do **auto download**, a configuração de um cache local e a obtenção de um modelo diretamente do Hugging Face — para que você possa começar a usar sem precisar procurar arquivos manualmente.

Se você já se perguntou *“como uso Aspose para IA baseada em OCR?”* ou *“qual a maneira mais fácil de definir cache para arquivos de modelo?”* você está no lugar certo. Ao final, você terá um script totalmente funcional que lista todos os modelos armazenados localmente, baixa automaticamente os que faltam e mostra exatamente onde os arquivos estão no disco.

---

## O Que Você Precisa

Antes de mergulharmos, certifique‑se de que você tem:

- Python 3.9 ou mais recente (a biblioteca usa type hints que exigem um interpretador recente)
- Acesso ao `pip` para instalar o pacote **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Uma conexão à internet para o primeiro download do Hugging Face.
- Uma pasta onde você deseja manter o cache de modelos (por exemplo, `./model_cache`).

É só isso — sem contêineres Docker extras, sem ambientes virtuais pesados além de uma instalação limpa do Python.

---

## ## Como listar modelos com Aspose AI

O coração deste guia é a capacidade de **listar modelos** que o Aspose AI armazenou em cache localmente. Uma vez que o cache esteja configurado, a biblioteca pode enumerar tudo o que conhece, facilitando depuração e controle de versão.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Por que isso funciona:**  
- `AsposeAI()` cria o ponto de entrada de alto nível que se comunica com o mecanismo de inferência subjacente.  
- `AsposeAIModelConfig()` contém todas as opções que você pode ajustar; definir `allow_auto_download` como `"true"` indica à biblioteca que deve buscar arquivos ausentes automaticamente do repositório que você especificar.  
- `directory_model_path` é o *diretório de cache* — o local onde todos os binários baixados vivem.  
- `initialize()` aplica a configuração, realizando o primeiro download se o cache estiver vazio.  
- Por fim, `list_local()` varre a pasta de cache e devolve uma lista Python de identificadores de modelo, que imprimimos.

### Saída esperada (primeira execução)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Se você executar o script novamente, a biblioteca pulará o download e simplesmente listará o modelo já presente, provando que **como definir cache** realmente compensa em execuções subsequentes.

---

## ## Habilitar auto download para modelos ausentes

Frequentemente você trabalhará com vários modelos em diferentes projetos. Baixar cada um manualmente do Hugging Face pode ser tedioso. Ao habilitar o auto download, o Aspose AI cuida do trabalho pesado.

```python
cfg.allow_auto_download = "true"
```

> **Dica profissional:** Mantenha `allow_auto_download` definido como `"true"` **apenas** em ambientes de desenvolvimento ou CI. Em produção, pode ser interessante travar o cache para evitar tráfego de rede inesperado.

Se mais tarde decidir desativá‑lo, basta definir a flag como `"false"` antes de chamar `initialize()` novamente.

---

## ## Baixar modelo do Hugging Face sob demanda

A linha

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

indica ao Aspose AI de qual repositório remoto ele deve puxar. A biblioteca suporta qualquer modelo público no Hugging Face que forneça um arquivo GGUF. Quer outro modelo? Troque o ID do repositório:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Ao executar o script, o Aspose AI verifica o cache:

- **Se o modelo existir**, ele o carrega instantaneamente.  
- **Se não existir**, a flag de auto‑download dispara o download, armazena o arquivo em `directory_model_path` e então o registra para uso imediato.

Essa abordagem elimina o processo de “download‑então‑execução” em duas etapas que muitos tutoriais forçam você a seguir.

---

## ## Como usar Aspose AI depois que o modelo for listado

Listar modelos é apenas metade da história. Uma vez que você saiba que um modelo está presente, pode iniciar a inferência:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Por que isso importa:**  
- `run_inference()` abstrai tokenização, batching e gerenciamento de GPU.  
- Ao passar o *nome do modelo* obtido de `list_local()`, você garante que a chamada de inferência corresponde exatamente ao arquivo no disco.

---

## ## Como definir localização de cache para múltiplos projetos

Se você lida com vários projetos, pode querer que cada um tenha sua própria pasta de cache. O campo `directory_model_path` é apenas uma string simples, então você pode construí‑la dinamicamente:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Agora cada projeto obtém uma sub‑pasta isolada (`./model_cache/sentiment_analysis`), evitando conflitos de versão e facilitando a limpeza.

---

## ## Armadilhas comuns e como evitá‑las

| Sintoma | Causa provável | Solução |
|---------|----------------|---------|
| **`PermissionError` ao acessar o cache** | Pasta de cache pertence a outro usuário (comum em servidores compartilhados) | Crie a pasta manualmente com permissões adequadas: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Modelo nunca aparece em `list_local()`** | `allow_auto_download` definido como `"false"` e o modelo ainda não está em cache | Ative a flag temporariamente, execute uma vez, depois desative se desejar |
| **Versão de modelo inesperada** | Dois repositórios diferentes compartilham o mesmo nome, mas arquivos diferentes | Fixe o ID exato do repositório (incluindo tag/commit) ou bloqueie o cache desativando o auto‑download após o primeiro pull bem‑sucedido |
| **Erros de falta de memória** | Arquivos GGUF grandes em máquina sem RAM/VRAM suficiente | Use um modelo menor (ex.: `Qwen2.5-1.5B`) ou defina `cfg.device = "cpu"` para forçar inferência em CPU |

---

## ## Script completo que você pode copiar‑colar

Abaixo está o exemplo completo, pronto para execução, que incorpora todos os conceitos acima. Salve como `list_models_demo.py` e execute com `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Executá‑lo** produzirá uma saída semelhante ao exemplo anterior, seguida de uma resposta concisa do modelo. Sinta‑se à vontade para substituir o prompt por qualquer coisa que desejar — esta é a maneira mais rápida de testar se o modelo está realmente utilizável depois que você **sabe como listar modelos**.

---

## ## Resumo

Cobremos tudo o que você precisa para **listar modelos** usando Aspose AI, desde habilitar **auto download** até configurar um **cache** persistente e puxar um **modelo Hugging Face** sob demanda. Os principais pontos:

1. Crie um objeto `AsposeAI` e um `AsposeAIModelConfig`.  
2. Defina `allow_auto_download = "true"` e aponte `directory_model_path` para uma pasta que você controla.  
3. Inicialize a IA, então chame `list_local()` para ver exatamente o que está em cache.  
4. Use o nome do modelo listado para inferência, e você está pronto para construir aplicações reais.

---

## O Que Vem a Seguir?

- **Experimente diferentes modelos** – troque `cfg.hugging_face_repo_id` por outro repositório e veja como a lista muda.  
- **Ajuste o cache**

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}