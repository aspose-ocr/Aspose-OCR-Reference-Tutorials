---
category: general
date: 2026-02-22
description: Aprenda a listar modelos em cache e a exibir rapidamente o diretório
  de cache na sua máquina. Inclui etapas para visualizar a pasta de cache e gerenciar
  o armazenamento local de modelos de IA.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: pt
og_description: Descubra como listar modelos em cache, mostrar o diretório de cache
  e visualizar a pasta de cache em alguns passos simples. Exemplo completo em Python
  incluído.
og_title: Listar modelos em cache – guia rápido para visualizar o diretório de cache
tags:
- AI
- caching
- Python
- development
title: listar modelos em cache – como visualizar a pasta de cache e mostrar o diretório
  de cache
url: /pt/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

output showing models and cache path". Translate to Portuguese: "list cached models – saída de console mostrando modelos e o caminho do cache". Keep "list cached models" unchanged.

Now translate all paragraphs.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# list cached models – guia rápido para visualizar o diretório de cache

Já se perguntou como **listar modelos em cache** na sua estação de trabalho sem precisar vasculhar pastas obscuras? Você não está sozinho. Muitos desenvolvedores esbarram em um obstáculo quando precisam verificar quais modelos de IA já estão armazenados localmente, especialmente quando o espaço em disco é limitado. A boa notícia? Em apenas algumas linhas você pode **listar modelos em cache** e **mostrar o diretório de cache**, obtendo total visibilidade da sua pasta de cache.

Neste tutorial vamos percorrer um script Python autônomo que faz exatamente isso. Ao final, você saberá como visualizar a pasta de cache, entender onde o cache reside em diferentes sistemas operacionais e até ver uma lista impressa organizada de cada modelo que foi baixado. Sem documentação externa, sem adivinhações — apenas código claro e explicações que você pode copiar‑colar agora mesmo.

## O que você vai aprender

- Como inicializar um cliente de IA (ou um stub) que oferece utilitários de cache.  
- Os comandos exatos para **listar modelos em cache** e **mostrar o diretório de cache**.  
- Onde o cache fica no Windows, macOS e Linux, para que você possa navegar até ele manualmente, se desejar.  
- Dicas para lidar com casos de borda, como cache vazio ou caminho de cache personalizado.  

**Pré‑requisitos** – você precisa de Python 3.8+ e de um cliente de IA instalável via pip que implemente `list_local()`, `get_local_path()` e, opcionalmente, `clear_local()`. Se ainda não tem um, o exemplo usa uma classe mock `YourAIClient` que pode ser substituída pelo SDK real (por exemplo, `openai`, `huggingface_hub`, etc.).  

Pronto? Vamos começar.

## Etapa 1: Configurar o cliente de IA (ou um mock)

Se você já tem um objeto cliente, pule este bloco. Caso contrário, crie um pequeno substituto que imite a interface de cache. Isso permite que o script seja executado mesmo sem um SDK real.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Dica profissional:** Se você já tem um cliente real (por exemplo, `from huggingface_hub import HfApi`), basta substituir a chamada `YourAIClient()` por `HfApi()` e garantir que os métodos `list_local` e `get_local_path` existam ou estejam adequadamente encapsulados.

## Etapa 2: **list cached models** – recuperar e exibir

Agora que o cliente está pronto, podemos pedir que ele enumere tudo o que conhece localmente. Este é o núcleo da nossa operação de **list cached models**.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Saída esperada** (com os dados fictícios da Etapa 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Se o cache estiver vazio, você verá simplesmente:

```
Cached models:
```

Aquela linha em branco indica que ainda não há nada armazenado — útil quando você está escrevendo rotinas de limpeza.

## Etapa 3: **show cache directory** – onde o cache reside?

Conhecer o caminho costuma ser metade da batalha. Sistemas operacionais diferentes colocam caches em locais padrão diferentes, e alguns SDKs permitem sobrescrevê‑los via variáveis de ambiente. O trecho a seguir imprime o caminho absoluto para que você possa `cd` nele ou abri‑lo no explorador de arquivos.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Saída típica** em um sistema Unix‑like:

```
Cache directory: /home/youruser/.ai_cache
```

No Windows você pode ver algo como:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Agora você sabe exatamente **como visualizar a pasta de cache** em qualquer plataforma.

## Etapa 4: Junte tudo – um script único executável

Abaixo está o programa completo, pronto para ser executado, que combina as três etapas. Salve como `view_ai_cache.py` e execute `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Execute e você verá instantaneamente tanto a lista de modelos em cache **quanto** a localização do diretório de cache.

## Casos de borda & variações

| Situação | O que fazer |
|----------|-------------|
| **Cache vazio** | O script imprimirá “Cached models:” sem entradas. Você pode adicionar um aviso condicional: `if not models: print("⚠️ No models cached yet.")` |
| **Caminho de cache personalizado** | Passe um caminho ao construir o cliente: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. A chamada `get_local_path()` refletirá essa localização customizada. |
| **Erros de permissão** | Em máquinas restritas, o cliente pode levantar `PermissionError`. Envolva a inicialização em um bloco `try/except` e faça fallback para um diretório gravável pelo usuário. |
| **Uso de SDK real** | Substitua `YourAIClient` pela classe cliente real e garanta que os nomes dos métodos coincidam. Muitos SDKs expõem um atributo `cache_dir` que pode ser lido diretamente. |

## Dicas avançadas para gerenciar seu cache

- **Limpeza periódica:** Se você baixa modelos grandes com frequência, agende um cron job que chame `shutil.rmtree(ai.get_local_path())` após confirmar que não os precisa mais.  
- **Monitoramento de uso de disco:** Use `du -sh $(ai.get_local_path())` no Linux/macOS ou `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` no PowerShell para acompanhar o tamanho.  
- **Pastas versionadas:** Alguns clientes criam subpastas por versão de modelo. Quando você **list cached models**, verá cada versão como uma entrada separada — use isso para remover revisões antigas.  

## Visão geral visual

![captura de tela de list cached models](https://example.com/images/list-cached-models.png "list cached models – saída de console mostrando modelos e o caminho do cache")

*Texto alternativo:* *list cached models – saída de console exibindo nomes de modelos em cache e o caminho do diretório de cache.*

## Conclusão

Cobrimos tudo o que você precisa para **list cached models**, **show cache directory** e, de modo geral, **como visualizar a pasta de cache** em qualquer sistema. O script curto demonstra uma solução completa e executável, explica **por que** cada passo importa e oferece dicas práticas para uso no mundo real.  

A seguir, você pode explorar **como limpar o cache** programaticamente ou integrar essas chamadas a um pipeline de implantação maior que valide a disponibilidade dos modelos antes de iniciar jobs de inferência. Seja como for, agora você tem a base para gerenciar o armazenamento local de modelos de IA com confiança.

Tem dúvidas sobre um SDK de IA específico? Deixe um comentário abaixo e feliz cache!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}