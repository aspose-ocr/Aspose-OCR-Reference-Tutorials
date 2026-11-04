---
category: general
date: 2026-06-22
description: Aprenda como listar modelos de IA em cache usando o AI SDK em Python.
  Inclui etapas para recuperar o diretório de cache de modelos e gerenciar modelos
  de IA locais de forma eficiente.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: pt
og_description: Liste os modelos de IA em cache com Python usando o AI SDK. Siga este
  tutorial passo a passo para recuperar o diretório de cache de modelos e lidar com
  modelos de IA locais.
og_title: Listar Modelos de IA em Cache no Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Listar Modelos de IA em Cache no Python – Guia Completo
url: /pt/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Listar Modelos de IA em Cache no Python – Guia Completo

Já se perguntou como **listar modelos de IA em cache** na sua estação de trabalho sem vasculhar pastas obscuras? Você não está sozinho. Muitos desenvolvedores esbarram em um obstáculo quando precisam verificar quais modelos já estão armazenados localmente, especialmente ao trabalhar com largura de banda limitada ou implantações offline. Neste tutorial você verá uma maneira rápida e direta de consultar o AI SDK, imprimir o conteúdo do cache e descobrir exatamente onde esses arquivos estão armazenados.

Também abordaremos tópicos relacionados, como **recuperar o diretório de cache do modelo**, lidar com caches vazios e boas práticas para **gerenciar o cache de modelos de IA** em scripts de produção. Ao final, você terá um trecho autônomo que pode ser inserido em qualquer projeto Python.

## Pré‑requisitos

Antes de mergulharmos, certifique‑se de que você tem:

- Python 3.8 ou mais recente instalado.
- O AI SDK (o pacote `ai`) instalado via `pip install ai-sdk` ou pelo repositório interno da sua organização.
- Familiaridade básica com a execução de scripts a partir da linha de comando.

Nenhuma biblioteca adicional é necessária, portanto o exemplo permanece leve e portátil.

---

## Listar Modelos de IA em Cache – Visão Geral Rápida

A primeira coisa que você precisa fazer é importar o SDK e chamar suas funções auxiliares. O SDK expõe dois métodos úteis:

1. `ai.list_local()` – retorna uma lista Python de identificadores de modelo que já estão em cache.
2. `ai.get_local_path()` – retorna o diretório absoluto onde esses arquivos de modelo residem.

Ambas as chamadas são síncronas e levantam um claro `AIError` se algo der errado, o que simplifica o tratamento de erros.

> **Por que usar essas funções?**  
> Conhecer o conjunto exato de modelos em cache permite evitar downloads desnecessários, depurar incompatibilidades de versão e limpar artefatos antigos automaticamente. É uma pequena parte do fluxo de trabalho maior do **AI SDK Python**, mas pode economizar horas de busca manual no sistema de arquivos.

### Etapa 1: Importar o AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Por que isso importa:* Importar o pacote registra as extensões C subjacentes e carrega arquivos de configuração (como caminhos de cache) do seu ambiente. Pular essa etapa resultará em um `ModuleNotFoundError` no momento em que você chamar qualquer função do SDK.

### Etapa 2: Listar Todos os Modelos em Cache

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**O que você verá:** Se você tem três modelos armazenados, a saída pode ser semelhante a:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Se o cache estiver vazio, você receberá uma lista vazia:

```
Cached models: []
```

> **Dica profissional:** Envolva a chamada em um bloco try/except se suspeitar que o SDK pode não estar inicializado corretamente.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Etapa 3: Recuperar o Diretório de Cache do Modelo

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Saída típica em um sistema Unix‑like:

```
Model cache directory: /home/you/.cache/ai/models
```

No Windows você pode ver algo como `C:\Users\you\AppData\Local\ai\models`. Conhecer esse caminho é essencial quando você precisa **gerenciar o cache de modelos de IA** manualmente — talvez para remover versões antigas ou copiar arquivos para uma unidade compartilhada.

---

## Resumo Visual

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Texto alternativo:* Diagrama ilustrando o processo de **listar modelos de IA em cache** usando o AI SDK em Python.

---

## Tratamento de Casos Limite e Armadilhas Comuns

### Cache Vazio

Se `ai.list_local()` retornar uma lista vazia, você pode se perguntar se o SDK está mal configurado. Verifique a variável de ambiente `AI_CACHE_DIR` (ou o arquivo de configuração do SDK) para garantir que aponta para um local gravável.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Problemas de Permissão

Ao acessar `ai.get_local_path()`, um `PermissionError` pode surgir em sistemas restritivos. A solução geralmente é executar o script com os direitos de usuário adequados ou ajustar as ACLs do diretório.

### Incompatibilidades de Versão

Às vezes o cache contém uma versão mais antiga de um modelo enquanto seu código solicita uma mais nova. O SDK baixará automaticamente a versão mais recente, mas você pode prevenir isso inspecionando a tag de versão na lista:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Limpeza de Modelos Antigos

Se precisar liberar espaço, pode excluir diretamente a pasta de um modelo específico:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Executar `purge_model('bert-base-uncased')` removerá esse modelo e liberará espaço em disco.

---

## Script Completo para Copiar‑e‑Colar

Abaixo está um script pronto para execução que combina todas as etapas, adiciona tratamento básico de erros e imprime um resumo amigável.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Saída esperada (quando o cache está populado):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Execute o script com `python list_models.py` e você saberá instantaneamente o que está armazenado no disco.

---

## Perguntas Frequentes

**P: Isso funciona em todos os sistemas operacionais?**  
R: Sim. O SDK abstrai caminhos específicos de SO, de modo que `ai.get_local_path()` retorna uma string válida no Linux, macOS e Windows.

**P: Posso listar modelos de um cache remoto?**  
R: O `list_local()` interno relata apenas artefatos armazenados localmente. Para registros remotos você usaria `ai.list_remote()` (se sua versão do SDK o disponibilizar).

**P: E se o nome do SDK não for `ai`?**  
R: Substitua a linha de importação pelo nome real do pacote, por exemplo, `import myai as ai`. Todas as chamadas subsequentes permanecem as mesmas porque o contrato da API é consistente entre implementações.

---

## Conclusão

Agora você tem um método sólido e pronto para produção de **listar modelos de IA em cache** usando a biblioteca **AI SDK Python**, recuperar o **diretório de cache do modelo** e até limpar arquivos antigos. Esse conhecimento ajuda a manter seu ambiente organizado, evitar downloads redundantes e depurar questões de versão com facilidade.

Pronto para o próximo passo? Experimente estender o script para baixar automaticamente modelos ausentes ou integrá‑lo a um pipeline de CI que valide a saúde do cache antes de cada build. Explorar estratégias de **gerenciar o cache de modelos de IA** tornará suas aplicações alimentadas por IA mais rápidas e confiáveis.

Boa codificação, e que seus caches permaneçam enxutos!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}