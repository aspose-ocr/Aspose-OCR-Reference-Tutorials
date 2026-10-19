---
category: general
date: 2026-04-26
description: Como executar OCR em um formulário escaneado, aprender a pré‑processar
  a imagem para reduzir ruído e extrair texto da imagem rapidamente.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: pt
og_description: Como executar OCR em documentos escaneados, pré-processar imagens,
  reduzir ruído e extrair texto de forma eficiente.
og_title: Como Executar OCR e Pré‑processar Imagens – Guia Rápido
tags:
- OCR
- image processing
- Python
title: Como Executar OCR e Pré‑processar Imagens – Extrair Texto de Formulários Digitalizados
url: /pt/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR – Um Guia Completo para Extrair Texto de Imagens

Já se perguntou **como executar OCR** em um formulário escaneado bagunçado e obter texto limpo e pesquisável? Você não está sozinho. Em muitos projetos do mundo real a imagem bruta está cheia de manchas, iluminação desigual e outras imperfeições que fazem o OCR padrão falhar.  

A boa notícia? Com apenas algumas linhas de Python e um pipeline inteligente de pré‑processamento, você pode aumentar drasticamente a precisão do reconhecimento, **reduzir o ruído** e extrair exatamente as palavras que precisa. Neste tutorial vamos percorrer cada passo — desde carregar a imagem até imprimir a string final — para que você saia com um trecho pronto para uso que pode ser adaptado a faturas, recibos ou qualquer documento escaneado.

## O Que Você Vai Construir

- Uma instância `OcrEngine` que se comunica com a biblioteca OCR subjacente.  
- Uma cadeia de pré‑processamento que **binariza** a imagem e aplica um **desfoque mediano** para suavizar as manchas.  
- Uma chamada simples a `process()` que devolve um objeto expondo `text`, a string extraída.  

Ao final, você terá um script autônomo que pode ser executado em qualquer arquivo de imagem e verá imediatamente o texto extraído no console.

## Pré‑requisitos

- Python 3.9+ (a sintaxe usada aqui corresponde à última versão estável).  
- O pacote fictício `aocr` – pense nele como um wrapper leve em torno do Tesseract ou de qualquer motor OCR moderno. Instale com `pip install aocr`.  
- Uma imagem escaneada (`scanned_form.jpg`) colocada em uma pasta que você possa referenciar.  

Se você estiver usando uma biblioteca OCR real como `pytesseract`, pode substituir `OcrEngine` pela classe apropriada — tudo o mais permanece igual.

![](how-to-run-ocr-example.png "exemplo de como executar OCR mostrando um formulário escaneado e o texto extraído")

*Texto alternativo: como executar OCR em um documento escaneado e visualizar o texto extraído.*

---

## Etapa 1: Como Executar OCR – Inicializar o Motor

Antes que o motor possa ler qualquer coisa, precisamos criar uma instância. Pense no `OcrEngine` como o cérebro que mais tarde interpretará os dados visuais.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Por que isso importa:** Instanciar o motor configura modelos internos, carrega pacotes de idioma e prepara o ambiente de execução. Pular esta etapa geralmente resulta em um erro `NoneType` quando você chama `process()` mais tarde.

---

## Etapa 2: Como Pré‑processar a Imagem – Carregar Seu Formulário Escaneado

Agora que o cérebro está pronto, alimentamos ele com uma foto. A imagem pode estar em qualquer formato suportado por `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Dica profissional:** Use caminhos absolutos durante o desenvolvimento para evitar surpresas de “arquivo não encontrado” quando o script for executado a partir de um diretório de trabalho diferente.

---

## Etapa 3: Como Reduzir Ruído – Aplicar Binarização & Desfoque Mediano

Escaneamentos brutos costumam conter pontos soltos, fundo desigual ou sombras tênues. Dois truques clássicos — **binarização** e **desfoque mediano** — limpam a imagem sem sacrificar as bordas que definem os caracteres.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Aprofun­dando

- **Binarização**: O valor `threshold=180` indica ao algoritmo: “Tudo que for mais claro que 180 vira branco; o resto vira preto.” Ajuste esse número se seu escaneamento estiver muito escuro ou muito claro.  
- **Desfoque Mediano**: Um raio de `2` significa que o filtro observa uma janela de 5×5 pixels e substitui o pixel central pelo valor mediano. Isso suaviza manchas isoladas enquanto mantém os traços das letras intactos.

> **Caso limite:** Se seu documento tem realces coloridos, um limiar binário simples pode apagá‑los. Nesse cenário, considere usar `aocr.ImageFilters.adaptive_threshold()` — ele adapta o corte localmente em toda a imagem.

---

## Etapa 4: Como Extrair Texto – Executar o Processo OCR

Com uma imagem limpa em mãos, finalmente deixamos o motor fazer sua mágica.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **O que acontece nos bastidores?** O motor executa uma rede neural (ou um matcher de padrões legado) sobre a matriz de pixels, traduz cada glifo reconhecido em caracteres Unicode e os reúne em linhas e parágrafos.

---

## Etapa 5: Como Extrair Texto – Imprimir o Resultado

O objeto `ocr_result` expõe um atributo conveniente `text`. Vamos ver o que obtivemos.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Saída Esperada

Se o formulário escaneado contiver:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Você deverá ver algo como:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Observe como a etapa de pré‑processamento eliminou pontos soltos que antes transformavam “Amount” em “Am0unt”. Esse é o poder de **como reduzir ruído** antes do OCR.

---

## Armadilhas Comuns & Como Corrigi‑las

| Sintoma | Causa Provável | Correção Rápida |
|---------|----------------|-----------------|
| Caracteres embaralhados (ex.: “@#%”) | Imagem muito escura ou muito clara | Ajuste o `threshold` em `binarize()`; experimente `adaptive_threshold`. |
| Palavras ausentes | Ruído ainda presente | Aumente o `radius` em `median_blur` ou adicione um filtro `gaussian_blur`. |
| Idioma errado (ex.: letras em inglês viram chinês) | Pacote de idioma incorreto carregado | Passe `language="eng"` ao criar `OcrEngine()` se a biblioteca suportar. |
| Processamento lento em arquivos grandes | Alta resolução | Reduza a imagem primeiro: `aocr.ImageFilters.resize(width=1200)` antes da binarização. |

---

## Avançando – Próximos Passos e Tópicos Relacionados

- **Processamento em lote**: Envolva a lógica acima em um loop para lidar com dezenas de arquivos automaticamente.  
- **Saída estruturada**: Use expressões regulares em `ocr_result.text` para extrair campos como datas ou valores.  
- **Bibliotecas alternativas**: Troque `aocr` por `pytesseract` — o código muda apenas na etapa de inicialização do motor.  
- **Como pré‑processar imagens para PDFs**: Converta cada página do PDF em imagem e aplique o mesmo pipeline.  

Essas extensões permitem escalar a solução de um único formulário para um pipeline de ingestão de documentos de nível empresarial.

---

## Conclusão

Cobremos **como executar OCR** do início ao fim, mostramos **como pré‑processar a imagem** para **reduzir ruído**, e demonstramos **como extrair texto de imagem** com um script limpo e reproduzível. O ponto principal? Alguns filtros simples — binarização e desfoque mediano — podem transformar um escaneamento ruidoso em uma fonte confiável de dados, economizando horas de limpeza manual.

Teste o script com seus próprios documentos, ajuste os limiares e veja a precisão subir. Quando estiver pronto, explore o processamento em lote ou integre a saída a um banco de dados para arquivos pesquisáveis. Boa codificação, e que seu OCR esteja sempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}