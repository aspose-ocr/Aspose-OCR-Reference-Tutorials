---
category: general
date: 2026-06-25
description: Obtenha rapidamente os caracteres suportados por OCR usando a biblioteca
  aocr. Aprenda como listar os caracteres OCR, definir idiomas e depurar seu mecanismo
  OCR em Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: pt
og_description: Obtenha os caracteres suportados pelo OCR com aocr. Este guia mostra
  como listar os caracteres OCR, escolher idiomas e lidar com casos de borda em Python.
og_title: Obtenha os caracteres suportados pelo OCR em Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Obtenha os caracteres suportados por OCR em Python – Guia completo
url: /pt/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenha Caracteres Suportados por OCR em Python – Guia Completo

Já se perguntou como **obter caracteres suportados por OCR** para um idioma específico enquanto mexe em um motor OCR? Você não está sozinho. Seja construindo um scanner de recibos ou um analisador de documentos multilíngues, saber exatamente quais glifos seu motor pode reconhecer é uma mão na roda. Neste tutorial vamos percorrer todo o processo — instalar a biblioteca, configurar o idioma e, finalmente, listar esses caracteres — para que você possa depurar e ajustar finamente seu pipeline OCR em minutos.

Usaremos a biblioteca **aocr**, um motor OCR leve em Python que facilita a consulta das capacidades de idioma. Ao final deste guia você será capaz de **listar caracteres OCR**, alternar entre **idiomas OCR suportados** e até identificar lacunas na cobertura antes que elas prejudiquem a produção.

---

## Pré-requisitos

* Python 3.8 ou mais recente (o pacote aocr deixou de suportar 3.7)
* Um terminal ou prompt de comando com acesso à internet
* Familiaridade básica com scripts Python (se você já escreveu um `print()`, está pronto)

Sem dependências externas pesadas — apenas o pacote pip `aocr`.

## Instale a Biblioteca aocr (Motor OCR Python)

A primeira coisa que você precisa é uma instalação funcional do **OCR engine Python**. O pacote aocr está disponível no PyPI, então um único comando pip resolve:

```bash
pip install aocr
```

Se você estiver usando um ambiente virtual (altamente recomendado), ative-o primeiro:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Dica profissional:** Fixe a versão (`pip install aocr==1.2.4`) para evitar mudanças inesperadas na API mais tarde.

## Escolha um Idioma (Idiomas OCR Suportados)

aocr vem com um conjunto de pacotes de idioma integrados. Cada pacote define o conjunto de pontos de código Unicode que o motor pode reconhecer. Para consultar esses pacotes, você precisará definir o atributo `language` na instância do motor.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Você pode substituir `aocr.Language.ENGLISH` por qualquer outro valor enum (`FRENCH`, `GERMAN`, etc.). Se você tentar atribuir um idioma que não está incluído, aocr gera um `ValueError`. Por isso é uma boa ideia verificar a lista de **idiomas OCR suportados** primeiro:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

## Recupere o Conjunto de Caracteres (Obtenha Caracteres Suportados por OCR)

Agora vem o coração do tutorial: realmente **obter caracteres suportados por OCR**. O motor expõe um método útil chamado `get_supported_characters()` que retorna uma lista de strings de um único caractere.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Nos bastidores, aocr lê um arquivo JSON incluído no pacote de idioma e converte cada ponto de código Unicode em uma string Python. O resultado é determinístico, ou seja, você obterá a mesma lista toda vez que executar o script na mesma versão de idioma.

## Mostre Quantos Caracteres São Suportados

Saber a quantidade ajuda a avaliar rapidamente a amplitude da cobertura. Para o inglês, você normalmente verá alguns milhares de caracteres (incluindo pontuação e dígitos).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

A chamada `len()` é O(1) porque o Python armazena o tamanho da lista internamente, portanto não há penalidade de desempenho mesmo para alfabetos grandes.

## Visualize os Primeiros 100 Caracteres Suportados

Uma verificação visual rápida pode revelar se o motor inclui os símbolos que você precisa (pense no símbolo do Euro ou aspas tipográficas). Vamos imprimir os primeiros cem caracteres:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

A operação `join` concatena a fatia em uma única string, que é mais legível do que imprimir uma lista Python.

## Script Completo – Todas as Etapas em Um Só Lugar

Abaixo está o exemplo completo e executável que une tudo. Salve como `list_supported_chars.py` e execute `python list_supported_chars.py` a partir do seu terminal.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Saída esperada (truncada para brevidade):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

A contagem exata pode variar ligeiramente dependendo da versão do aocr, mas você sempre verá um alfabeto extenso mais pontuação comum.

## Lidando com Casos de Borda

### E se o pacote de idioma estiver ausente?

Se você solicitar um idioma que não está incluído, `aocr.Language` não conterá o enum, e você encontrará um `AttributeError`. Proteja-se contra isso com uma verificação simples:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Lista de caracteres vazia

Alguns idiomas de nicho podem retornar uma lista vazia se os dados de treinamento subjacentes estiverem incompletos. Nesse cenário, você pode recorrer a um padrão (por exemplo, Inglês) ou gerar um aviso:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalização Unicode

A lista pode conter caracteres combinados (por exemplo, “é” como `e` + acento agudo). Se o seu processamento subsequente espera glifos pré‑compostos, execute uma etapa de normalização:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

## Dicas Profissionais para Projetos Reais

* **Cache a lista de caracteres** – Se você estiver processando milhares de imagens, chamar `get_supported_characters()` a cada iteração adiciona sobrecarga desnecessária. Armazene a lista em uma variável de nível de módulo ou serialize-a para JSON para reutilização posterior.
* **Validação cruzada de idiomas** – Quando você suporta múltiplos idiomas em um único aplicativo, interseccione os conjuntos de caracteres para encontrar um subconjunto comum. Isso ajuda a projetar elementos de UI que permanecem consistentes entre localidades.
* **Depuração de falhas de OCR** – Se o motor classificar erroneamente um glifo, compare o caractere problemático com a saída de `list_supported_chars`. Se estiver ausente, você identificou uma lacuna de cobertura que pode exigir um passo de treinamento customizado.
* **Combine com fontes personalizadas** – aocr respeita o intervalo Unicode, mas a qualidade de renderização pode variar conforme a fonte. Teste seus caracteres suportados com a fonte exata que será usada em produção para evitar surpresas.

## Perguntas Frequentes

**Q: Isso funciona com aocr versão 2.x?**  
A: Sim, o método `get_supported_characters()` é estável nas versões 1.x e 2.x. A única mudança é que os enums de idioma foram movidos para `aocr.languages`.

**Q: Posso obter o ponto de código Unicode para cada caractere?**  
A: Absolutamente. Use `ord(ch)` dentro de uma list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: E quanto a scripts da direita para a esquerda, como o Árabe?**  
A: aocr inclui um enum `ARABIC`. A lista de caracteres conterá glifos árabes, mas pode ser necessário habilitar a renderização RTL na sua UI subsequente.

## Conclusão

Agora você sabe **como obter caracteres suportados por OCR** usando a biblioteca aocr em Python, como alternar entre **idiomas OCR suportados**, e por que **listar caracteres OCR** é essencial para pipelines de reconhecimento de texto robustos. Munido do script completo e das dicas acima, você pode verificar rapidamente a cobertura de idiomas, depurar glifos ausentes e construir aplicações OCR mais inteligentes.

Pronto para o próximo passo? Experimente combinar esta lista de caracteres com um filtro de lista de palavras personalizado, ou experimente um motor OCR diferente (Tesseract, EasyOCR) e compare os resultados. Quanto mais você explorar, melhores serão suas soluções OCR.

Feliz codificação, e que seus conjuntos de caracteres estejam sempre completos!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Especificar Caracteres Permitidos OCR – Usando Aspose.OCR para .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Como OCR Texto de Imagem com Idioma Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Pós‑Processamento OCR – Obter Opções de Caracteres](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}