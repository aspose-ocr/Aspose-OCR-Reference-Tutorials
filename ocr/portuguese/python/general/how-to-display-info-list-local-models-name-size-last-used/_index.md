---
category: general
date: 2026-01-12
description: Aprenda como exibir informações do AsposeAI listando os modelos locais,
  mostrando o nome do modelo, o tamanho e o carimbo de data/hora da última utilização
  em um exemplo claro em Python.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: pt
og_description: 'Como exibir informações do AsposeAI: listar modelos locais, exibir
  nome do modelo, tamanho e timestamp da última utilização com um tutorial completo
  em Python.'
og_title: Como exibir informações – Listar modelos locais, nome, tamanho, último uso
tags:
- AsposeAI
- Python
- Model Management
title: Como exibir informações – listar modelos locais, nome, tamanho, último uso
url: /pt/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Exibir Informações – Listar Modelos Locais, Nome, Tamanho, Último Uso

Já se perguntou **como exibir informações** da sua instalação AsposeAI sem precisar vasculhar logs ou a interface? Você não está sozinho. Em muitos pipelines de ciência de dados, a primeira coisa que se precisa é um olhar rápido para quais modelos estão na sua máquina, como eles se chamam, o tamanho deles e quando foram usados pela última vez.

É exatamente isso que vamos abordar: um trecho conciso, de ponta a ponta, em Python que **lista modelos locais**, depois **exibe o nome do modelo**, **mostra o tamanho do modelo** e **mostra o timestamp do último uso**. Sem bibliotecas externas, sem mágica oculta — apenas o cliente AsposeAI que você já tem.

Ao final deste tutorial você poderá inserir o código em qualquer script, executá‑lo e obter instantaneamente uma tabela organizada dos seus modelos em cache local. É perfeito para validar ambientes, construir dashboards de saúde ou simplesmente saciar a curiosidade sobre o que está armazenado em disco.

## Pré-requisitos

- Python 3.8 ou superior (o exemplo usa f‑strings, portanto 3.6+ é obrigatório)
- Pacote `asposeai` instalado (`pip install asposeai`)
- Uma licença AsposeAI válida ou chave de avaliação (o cliente buscará credenciais em variáveis de ambiente ou em um arquivo de configuração)

Se você já tem tudo isso, ótimo — vamos começar.

## Etapa 1: Como Exibir Informações – Inicializar o Cliente AsposeAI

Antes de podermos **listar modelos locais**, precisamos de um objeto cliente que se comunique com o runtime AsposeAI. Esta etapa é a base; sem ela o restante do código levantaria um `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Por que isso importa*: Inicializar o cliente estabelece uma sessão com o motor de inferência local, carregando quaisquer bibliotecas nativas necessárias. Também valida que sua licença está ativa, evitando erros crípticos mais tarde quando você tentar consultar modelos.

> **Dica profissional**: Se você executar isso em um servidor CI, defina `ASPOSEAI_LICENSE` no ambiente para que o cliente possa iniciar sem prompts interativos.

## Etapa 2: Listar Modelos Locais – Recuperar os Modelos Disponíveis

Agora que o cliente está pronto, podemos **listar modelos locais**. O método `list_local()` devolve uma coleção de objetos, cada um expondo propriedades como `name`, `size_mb` e `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*O que está acontecendo nos bastidores*: `list_local()` varre o diretório onde o AsposeAI guarda os arquivos de modelo (`~/.asposeai/models` por padrão) e cria objetos leves de metadados. Isso é rápido porque não carrega os pesos do modelo — apenas lê um pequeno manifesto JSON.

Se algum dia você se perguntar se um modelo específico já está em cache, esta chamada é a maneira mais rápida de confirmar.

## Etapa 3: Exibir Nome do Modelo, Mostrar Tamanho do Modelo e Mostrar Último Uso

Com os modelos em mãos, finalmente **exibimos informações** iterando sobre a coleção e imprimindo cada atributo. É aqui que **exibimos o nome do modelo**, **mostramos o tamanho do modelo** e **mostramos o último uso** tudo em uma linha organizada.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Saída esperada** (seus timestamps serão diferentes):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Por que formatamos assim*: O traço (`–`) separa os campos para melhorar a legibilidade, e a linha de cabeçalho torna a saída do console amigável à leitura. Se precisar de um formato legível por máquinas mais tarde (CSV, JSON), basta substituir a chamada `print` por um `writer.writerow` ou `json.dump`.

### Tratamento de Casos de Borda

- **Nenhum modelo em cache** – `list_local()` devolve uma lista vazia. O laço simplesmente será ignorado, deixando apenas o cabeçalho. Você pode querer adicionar uma proteção:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Atributos ausentes** – Em casos raros o manifesto pode estar corrompido. Acessar `model_info.last_used` pode gerar `AttributeError`. Envolva o `print` em um `try/except` se antecipar esses problemas.

- **Diretórios de modelos muito grandes** – Se houver centenas de modelos, considere paginar a saída ou gravá‑la em um arquivo ao invés de imprimir no console.

## Resumo Visual (Opcional)

Se você prefere uma pista visual rápida, o diagrama abaixo ilustra o fluxo desde a inicialização do cliente até a exibição final.

![Diagrama mostrando como exibir informações do cliente AsposeAI](/images/how-to-display-info.png "diagrama de como exibir informações")

*Texto alternativo*: **como exibir informações** – esquema da inicialização do cliente AsposeAI, listagem de modelos e exibição de informações.

## Script Completo

Juntando tudo, aqui está o script completo, pronto para ser executado:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Salve este arquivo como `list_models.py`, torne‑o executável (`chmod +x list_models.py`) e execute:

```bash
./list_models.py
```

Você verá a lista organizada demonstrada anteriormente.

## Conclusão

Percorremos **como exibir informações** do AsposeAI ao **listar modelos locais**, depois **exibir o nome do modelo**, **mostrar o tamanho do modelo** e **mostrar os timestamps de último uso**. A abordagem é leve, requer apenas o pacote padrão `asposeai` e pode ser inserida em qualquer pipeline de automação ou sessão de depuração.

A partir daqui você pode:

- Exportar a saída para CSV para análise em planilhas (`módulo csv`).
- Alimentar os timestamps em um dashboard de monitoramento para alertar sobre modelos obsoletos.
- Combinar este script com `aspose_ai.download()` para atualizar automaticamente modelos que não foram usados há algum tempo.

Lembre‑se, visibilidade clara do seu inventário de modelos economiza tempo, reduz o acúmulo de armazenamento e mantém seus serviços de IA funcionando suavemente. Experimente o script, ajuste a formatação ao seu gosto e deixe‑o se tornar um item básico na sua caixa de ferramentas.

Feliz codificação, e que seus modelos estejam sempre atualizados!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}