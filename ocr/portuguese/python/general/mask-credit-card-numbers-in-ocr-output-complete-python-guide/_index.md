---
category: general
date: 2026-04-26
description: Mascarar números de cartão de crédito rapidamente usando o pós‑processamento
  OCR do AsposeAI. Aprenda conformidade PCI, mascaramento com expressões regulares
  e sanitização de dados em um tutorial passo a passo.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: pt
og_description: Mascarar números de cartão de crédito nos resultados de OCR com AsposeAI.
  Este tutorial aborda conformidade PCI, mascaramento com expressões regulares e sanitização
  de dados.
og_title: Mascarar Números de Cartão de Crédito – Guia Completo de Pós‑Processamento
  OCR em Python
tags:
- OCR
- Python
- security
title: Mascarar números de cartão de crédito na saída de OCR – Guia completo de Python
url: /pt/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mascarar Números de Cartão de Crédito – Guia Completo em Python

Já precisou **mascarar números de cartão de crédito** em texto que vem direto de um motor OCR? Você não está sozinho. Em indústrias regulamentadas, expor um PAN completo (Primary Account Number) pode causar problemas com auditores de conformidade PCI. A boa notícia? Com algumas linhas de Python e o hook de pós‑processamento da AsposeAI, você pode ocultar automaticamente os oito dígitos centrais e ficar seguro.

Neste tutorial vamos percorrer um cenário real: executar OCR em uma imagem de recibo e, em seguida, aplicar uma função personalizada de **pós‑processamento OCR** que sanitiza quaisquer dados PCI. Ao final, você terá um trecho reutilizável que pode inserir em qualquer fluxo de trabalho AsposeAI, além de algumas dicas práticas para lidar com casos extremos e escalar a solução.

## O que você aprenderá

- Como registrar um pós‑processador personalizado com **AsposeAI**.  
- Por que uma abordagem de **mascaramento com expressão regular** é rápida e confiável.  
- O básico da **conformidade PCI** relacionado à sanitização de dados.  
- Como estender o padrão para múltiplos formatos de cartão ou números internacionais.  
- Saída esperada e como verificar se o mascaramento funcionou.

> **Pré‑requisitos** – Você deve ter um ambiente Python 3 funcionando, o pacote Aspose.AI for OCR instalado (`pip install aspose-ocr`), e uma imagem de exemplo (por exemplo, `receipt.png`) que contenha um número de cartão de crédito. Nenhum outro serviço externo é necessário.

---

## Etapa 1: Definir um Pós‑Processador que Mascarar Números de Cartão de Crédito

O coração da solução está em uma pequena função que recebe o resultado do OCR, executa uma rotina de **mascaramento com expressão regular** e devolve o texto sanitizado.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Por que isso funciona:**  
- A regex `(\d{4})\d{8}(\d{4})` corresponde exatamente a 16 dígitos consecutivos, o formato comum para Visa, MasterCard e muitos outros.  
- Ao capturar os quatro primeiros e os quatro últimos dígitos (`\1` e `\2`) preservamos informação suficiente para depuração, ao mesmo tempo que cumprimos as regras de **conformidade PCI** que proíbem armazenar o PAN completo.  
- A substituição `\1****\2` oculta os oito dígitos centrais sensíveis, transformando `1234567812345678` em `1234****5678`.

> **Dica profissional:** Se precisar dar suporte a números American Express de 15 dígitos, adicione um segundo padrão como `r'(\d{4})\d{6}(\d{5})'` e execute ambas as substituições sequencialmente.

---

## Etapa 2: Inicializar o Motor AsposeAI

Antes de podermos anexar nosso pós‑processador, precisamos de uma instância do motor OCR. A AsposeAI inclui o modelo OCR e uma API simples para processamento customizado.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Por que inicializar aqui?**  
Criar o objeto `AsposeAI` uma única vez e reutilizá‑lo em várias imagens reduz a sobrecarga. O motor também faz cache dos modelos de idioma, o que acelera chamadas subsequentes — útil quando você está escaneando lotes de recibos.

## Etapa 3: Registrar a Função de Mascaramento Personalizada

A AsposeAI expõe o método `set_post_processor` que permite conectar qualquer callable. Passamos nossa função `mask_pci` junto com um dicionário de configurações opcional (vazio por enquanto).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**O que está acontecendo nos bastidores?**  
Quando você invocar `run_postprocessor` mais tarde, a AsposeAI entregará o resultado bruto do OCR à `mask_pci`. A função recebe um objeto leve (`data`) que contém o texto reconhecido, e você devolve uma nova string. Esse design mantém o OCR central intacto enquanto permite impor políticas de **sanitização de dados** em um único ponto.

## Etapa 4: Executar OCR na Imagem do Recibo

Agora que o motor sabe como limpar a saída, alimentamos uma imagem. Para fins deste tutorial, assumimos que você já possui um objeto `engine` configurado com o idioma e as definições de resolução corretas.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Dica:** Se você ainda não tem um objeto pré‑configurado, pode criá‑lo com:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

A chamada `recognize_image` devolve um objeto cujo atributo `text` contém a string bruta, sem mascaramento.

## Etapa 5: Aplicar o Pós‑Processador Registrado

Com os dados OCR brutos em mãos, os entregamos à instância de IA. O motor executa automaticamente a função `mask_pci` que registramos anteriormente.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Por que usar `run_postprocessor` em vez de chamar a função manualmente?**  
Isso mantém o fluxo de trabalho consistente, especialmente quando há múltiplos pós‑processadores (por exemplo, correção ortográfica, detecção de idioma). A AsposeAI os enfileira na ordem em que são registrados, garantindo saída determinística.

## Etapa 6: Verificar a Saída Sanitizada

Por fim, vamos imprimir o texto sanitizado e confirmar que quaisquer números de cartão de crédito foram corretamente mascarados.

```python
print(final_result.text)
```

**Saída esperada** (trecho):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Se o recibo não continha número de cartão, o texto permanece inalterado — nada a mascarar, nada a se preocupar.

## Lidando com Casos Extremos e Variações Comuns

### Vários Números de Cartão em um Mesmo Documento
Se um recibo inclui mais de um PAN (por exemplo, um cartão de fidelidade mais um cartão de pagamento), a regex roda globalmente, mascarando todas as ocorrências automaticamente. Não é necessário código extra.

### Formatação Não‑Padrão
Às vezes o OCR insere espaços ou hífens (`1234 5678 1234 5678` ou `1234-5678-1234-5678`). Amplie o padrão para ignorar esses caracteres:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

O `[ -]?` adicionado tolera espaços ou hífens opcionais entre blocos de dígitos.

### Cartões Internacionais
Para PANs de 19 dígitos usados em algumas regiões, você pode ampliar o padrão:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Lembre‑se apenas de que **conformidade PCI** ainda exige mascarar os dígitos centrais, independentemente do comprimento.

### Registro de Valores Mascarados (Opcional)
Se precisar de trilhas de auditoria, passe uma bandeira via `custom_settings` e ajuste a função:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Em seguida registre com:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Executar este script em um recibo que contenha `4111111111111111` produzirá:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Esse é todo o pipeline — do OCR bruto à **sanitização de dados** — encapsulado em algumas linhas limpas de Python.

## Conclusão

Acabamos de mostrar como **mascarar números de cartão de crédito** em resultados de OCR usando o hook de pós‑processamento da AsposeAI, uma rotina concisa de expressão regular e algumas dicas de boas práticas para **conformidade PCI**. A solução é totalmente autônoma, funciona com qualquer imagem que o motor OCR consiga ler e pode ser estendida para cobrir formatos de cartão mais complexos ou requisitos de registro.

Pronto para o próximo passo? Experimente combinar esse mascaramento com uma rotina de **inserção em banco de dados** que armazene apenas os quatro últimos dígitos para referência, ou integre um **processador em lote** que escaneie uma pasta inteira de recibos durante a noite. Você também pode explorar outras tarefas de **pós‑processamento OCR**, como padronização de endereços ou detecção de idioma — todas seguem o mesmo padrão que usamos aqui.

Tem dúvidas sobre casos extremos, desempenho ou como adaptar o código para outra biblioteca OCR? Deixe um comentário abaixo e vamos continuar a conversa. Feliz codificação e mantenha‑se seguro!  

![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}