---
category: general
date: 2026-06-06
description: 'Guia de conjunto de caracteres OCR: aprenda como usar o motor OCR para
  listar os caracteres suportados para scripts latinos e cirílicos com exemplos completos
  em Python.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: pt
og_description: 'Guia de conjunto de caracteres OCR: descubra como usar o motor OCR
  em Python para listar os caracteres suportados para vários scripts, completo com
  código e dicas.'
og_title: Conjunto de Caracteres OCR – Recuperar e Utilizar o Motor OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: Conjunto de Caracteres OCR – Recuperar e Usar o Motor OCR em Python
url: /pt/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conjunto de Caracteres OCR – Recuperar e Usar o Motor OCR em Python

Quer saber o **conjunto de caracteres OCR** que sua biblioteca suporta? Neste tutorial vamos mostrar como **usar o motor OCR** para consultar os caracteres suportados para diferentes scripts e por que isso importa em projetos reais.

Se você já ficou encarando uma tela em branco se perguntando por que algumas letras nunca aparecem após o processamento OCR, não está sozinho. A resposta costuma estar escondida no conjunto de caracteres que o motor conhece. Ao final deste guia você será capaz de:

* Listar cada caractere que um motor OCR pode reconhecer para um script específico.  
* Tratar casos em que um script não é suportado.  
* Inserir as informações do conjunto de caracteres em validações posteriores ou lógica de UI.

Sem truques mágicos de caixa‑preta — apenas Python puro, algumas linhas de código e um pouco de explicação.

---

## Pré‑requisitos

Antes de começarmos, verifique se você tem:

* Python 3.8+ instalado (o código usa f‑strings).  
* A biblioteca OCR que fornece `ocr.OcrEngine` — para este exemplo vamos assumir que um pacote chamado `ocr` já está instalado via `pip install ocr-lib`.  
* Familiaridade básica com o sistema de importação do Python e impressão.

Se estiver faltando a biblioteca, execute:

```bash
pip install ocr-lib
```

É só isso — nenhum binário extra ou dependência nativa é necessário para as consultas básicas ao conjunto de caracteres que faremos.

---

## Etapa 1: Inicializar a Instância do Motor OCR

Criar um objeto de motor é a primeira coisa que você faz ao **usar o motor OCR**. Pense nisso como ligar um scanner; sem ele, você não pode fazer perguntas.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

A classe `OcrEngine` é um wrapper leve ao redor do motor de reconhecimento subjacente. Ela não inicia processamento pesado até que você solicite algo, portanto o custo de inicialização é insignificante.

> **Dica profissional:** Se sua aplicação cria muitas instâncias do motor, reutilize uma única. Isso economiza memória e reduz a latência de inicialização.

---

## Etapa 2: Consultar o Conjunto de Caracteres OCR para um Script Específico

Agora que temos um motor, podemos perguntar a ele quais caracteres conhece para um determinado sistema de escrita. O método `get_supported_characters(script_name)` devolve uma `list` Python de caracteres Unicode.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Executar o trecho acima imprime algo como:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

A saída exata depende da versão da biblioteca OCR, mas você sempre receberá uma lista plana de caracteres. Se precisar tanto de maiúsculas quanto de minúsculas, basta solicitar o script `"Latin"` e então aplicar `.lower()` a cada elemento, ou consultar um script separado `"Latin‑lower"` se a biblioteca os distinguir.

### Por que isso importa?

Quando você fornece uma imagem contendo diacríticos incomuns (por exemplo, “ñ” ou “ø”), o motor OCR pode substituir silenciosamente esses caracteres por um placeholder ou descartá‑los totalmente. Conhecer o **conjunto de caracteres OCR** com antecedência permite pré‑validar a entrada, avisar os usuários ou recorrer a outro motor.

---

## Etapa 3: Recuperar Caracteres para Outro Script – Exemplo Cirílico

O mesmo método funciona para qualquer script que o motor afirma suportar. Vamos ver o que acontece com o cirílico.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Saída típica:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Se o motor **não** suportar o script solicitado, normalmente ele lança um `ValueError` (ou devolve uma lista vazia, dependendo da implementação). Vamos proteger contra isso.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

---

## Etapa 4: Visualizar o Conjunto de Caracteres OCR (Opcional)

Às vezes uma visualização rápida ajuda, especialmente quando você precisa mostrar aos interessados quais caracteres estão cobertos. Abaixo está um exemplo mínimo usando `matplotlib` para renderizar uma grade de caracteres.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Texto alternativo da imagem:** ![OCR character set diagram](ocr_character_set.png){alt="OCR character set overview"}

O diagrama não é obrigatório para a solução principal, mas demonstra como você pode **usar o motor OCR** para obter metadados além da simples impressão.

---

## Etapa 5: Integrar o Conjunto de Caracteres em Fluxos de Trabalho Reais

Agora que podemos recuperar o **conjunto de caracteres OCR**, vejamos um cenário prático: validar a saída OCR antes de armazená‑la em um banco de dados.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Esse padrão impede que dados lixo escapem para pipelines posteriores, um ponto de dor comum ao lidar com documentos multilíngues.

---

## Armadilhas Comuns e Casos de Borda

| Armadilha | Por que acontece | Como evitar |
|-----------|------------------|--------------|
| **Erro de digitação no nome do script** (ex.: `"Cyrillic "` com espaço ao final) | O motor trata a string literalmente e não encontra o script. | Remova espaços em branco: `script.strip()` antes de chamar `get_supported_characters`. |
| **Lista de caracteres vazia** | Alguns motores expõem um script, mas ainda não carregaram o modelo de idioma. | Chame `engine.load_language_model(script)` se a biblioteca oferecer esse método, ou garanta que os arquivos de modelo estejam presentes. |
| **Problemas de normalização Unicode** | Caracteres como “é” podem aparecer como compostos (`\u00E9`) ou decompostos (`e\u0301`). | Normalize strings com `unicodedata.normalize('NFC', text)` antes da validação. |
| **Desempenho em scripts extensos** (ex.: Chinês) | Recuperar milhares de caracteres pode ser lento. | Cache o resultado após a primeira chamada; a maioria das aplicações só precisa da lista uma vez. |

---

## Exemplo Completo Funcional

Juntando tudo, aqui está um script único que você pode copiar‑colar e executar:



## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Tutorial Aspose OCR – Reconhecimento Óptico de Caracteres](/ocr/english/)
- [Pós‑processamento OCR – Obter Opções de Caracteres](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Como Definir Valor de Limiar no Reconhecimento de Imagem OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}