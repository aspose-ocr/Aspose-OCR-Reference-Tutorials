---
category: general
date: 2026-03-28
description: Como fazer OCR de ROI em Python – Aprenda a definir opções de pré‑processamento
  para extração precisa de texto de regiões específicas da imagem.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: pt
og_description: Como fazer OCR de ROI em Python – Este guia mostra como definir o
  pré-processamento para extração confiável de texto de regiões de imagem definidas.
og_title: Como fazer OCR de ROI em Python – Como definir o pré-processamento
tags:
- OCR
- Python
- Aspose
title: Como fazer OCR de ROI em Python – Como definir o pré-processamento
url: /pt/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR de ROI em Python – Como definir pré-processamento

Já se perguntou **como fazer OCR de ROI** em uma imagem de nota fiscal ruidosa sem carregar a página inteira na memória? Você não está sozinho. Em muitos projetos do mundo real, precisamos apenas de alguns campos — nome do cliente, endereço, totais — então escanear o documento inteiro é excessivo.  

A boa notícia? Com Aspose OCR você pode dizer ao motor exatamente **onde procurar** e ainda instruí‑lo a limpar a imagem primeiro. Neste tutorial, vamos percorrer as opções de **como definir pré-processamento**, definir Regions of Interest (ROIs) e extrair texto limpo em apenas algumas linhas de Python.

Ao final deste guia, você terá um script pronto‑para‑executar que extrai blocos específicos de qualquer nota fiscal, recibo ou formulário. Nenhuma ferramenta extra necessária, apenas Aspose OCR e um pouco de lógica em Python.

---

## O que você precisará

- **Python 3.8+** (o código funciona em qualquer versão recente)  
- **Aspose OCR for Python via .NET** – instale com `pip install aspose-ocr`  
- Uma imagem de exemplo (ex., `invoice.png`) colocada em uma pasta que você pode referenciar  
- Familiaridade básica com funções Python e sintaxe orientada a objetos  

Se você já tem isso, ótimo — vamos direto ao código.

---

![Diagrama de como fazer OCR de ROI](ocr-roi.png "Exemplo de como fazer OCR de ROI")

*Alt text: diagrama de como fazer OCR de ROI mostrando caixas de ROI em uma imagem de nota fiscal*

---

## Etapa 1 – Inicializar o Motor OCR (Como fazer OCR de ROI)

Antes de podermos dizer ao motor *onde* procurar, precisamos de uma instância do processador OCR. Este objeto contém toda a configuração e executa a passagem de reconhecimento.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Por que isso importa*: A classe `OcrEngine` abstrai o trabalho pesado (detecção de fontes, análise de layout, etc.). Ao criar um único motor, você evita re‑inicializar recursos pesados para cada imagem, o que mantém o desempenho ágil.

---

## Etapa 2 – Carregar sua Imagem Fonte (Como fazer OCR de ROI)

Aspose Storage facilita o carregamento de imagens. Aponte para o caminho do arquivo e você obtém um objeto `Image` pronto para processamento.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Dica*: Se você estiver trabalhando com streams (ex., imagens enviadas via uma API web), pode passar um objeto `BytesIO` para `Image.load` em vez de um caminho de arquivo.

---

## Etapa 3 – Definir as Regiões de Interesse (ROIs)

Agora respondemos à questão central **como fazer OCR de ROI**: dizemos ao motor os retângulos exatos que contêm os dados que nos interessam. Cada ROI é definido por seu canto superior esquerdo (`x`, `y`) e seu tamanho (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Por que usar ROIs?*  
- **Velocidade** – O motor ignora partes irrelevantes da imagem.  
- **Precisão** – Ao focar em uma área pequena, ruídos em outras partes não confundem o reconhecedor.  
- **Flexibilidade** – Você pode adicionar quantas ROIs precisar; o motor devolve uma lista de resultados na mesma ordem.

---

## Etapa 4 – Como Definir Pré‑processamento para Melhor Precisão de OCR

Imagens diretamente de scanners ou telefones costumam sofrer de inclinação, baixo contraste ou iluminação irregular. Aspose OCR oferece um objeto `PreprocessingOptions` que permite habilitar correções comuns antes da execução do reconhecimento.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Como isso ajuda*:  
- **Deskew** remove a inclinação que torna as formas dos caracteres ambíguas.  
- **Binarize** reduz o ruído de cor, fornecendo ao motor OCR uma imagem binária limpa.  
- **Contrast** amplifica traços fracos, o que é especialmente útil para recibos desbotados.

Você pode experimentar esses parâmetros — desative um e veja se a saída muda. Esse é o espírito de **como definir pré‑processamento** de forma eficaz.

---

## Etapa 5 – Executar OCR Apenas Dentro das ROIs Definidas

Com o motor, a imagem, as ROIs e o pré‑processamento prontos, é hora de chamar `recognize`. O método devolve um objeto `OcrResult` que contém uma coleção `regions` — cada entrada corresponde à ordem das ROIs que fornecemos.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Nos bastidores*: O motor recorta cada ROI, aplica o pipeline de pré‑processamento e executa o modelo de reconhecimento no trecho limpo. Como passamos uma lista, o resultado mantém a mesma ordem, tornando o pós‑processamento simples.

---

## Etapa 6 – Ler e Usar o Texto Extraído (Como fazer OCR de ROI)

Finalmente, itere sobre a lista `regions` e imprima — ou armazene — as strings reconhecidas. O objeto `Region` expõe uma propriedade `text` que contém o resultado Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Saída esperada (exemplo)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Se o texto parecer confuso, revise **como definir pré‑processamento**: talvez aumente `contrast` ou desative `binarize` para logos coloridos.

---

## Armadilhas Comuns e Dicas Profissionais

| Problema | Por que acontece | Correção (Como definir pré‑processamento) |
|----------|------------------|------------------------------------------|
| Texto inclinado aparece como lixo | `deskew` desativado ou imagem muito rotacionada | Ative `preprocessing_options.deskew = True` |
| Números viram pontos ou marcas soltas | Baixo contraste ou binarização agressiva | Reduza `contrast` (ex., `1.2`) ou defina `binarize = False` |
| Coordenadas da ROI deslocadas alguns pixels | DPI diferente ou escala do scanner | Use uma ferramenta (ex., Paint.NET) para medir posições exatas em pixels, ou adicione uma pequena margem (`+5` pixels) a cada ROI |
| Resultado vazio para uma região | ROI fora dos limites da imagem | Verifique as dimensões da imagem: `source_image.width`, `source_image.height` |

---

## Expandindo a Solução (Como fazer OCR de ROI em Diferentes Cenários)

- **ROIs Dinâmicas**: Se suas notas fiscais têm layouts variáveis, você pode primeiro executar um OCR rápido de página inteira para localizar palavras‑chave (“Customer:”, “Address:”) e então calcular as ROIs dinamicamente.  
- **Processamento em Lote**: Envolva as etapas acima em uma função e itere sobre uma pasta de imagens. Lembre‑se de reutilizar a mesma instância `ocr_engine` para manter o uso de memória baixo.  
- **Exportação para JSON**: Em vez de imprimir, construa um dicionário e despeje‑o com `json.dumps`; isso torna a integração downstream (ex., alimentar um sistema ERP) trivial.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Conclusão

Agora você tem um exemplo completo e executável que mostra **como fazer OCR de ROI** em Python enquanto domina **como definir pré‑processamento** para precisão ideal. Ao limitar o motor aos retângulos exatos que lhe interessam e limpar a imagem antes, você obtém resultados mais rápidos e limpos — perfeito para automação de notas fiscais, digitalização de formulários ou qualquer cenário onde apenas uma parte da página importa.

Pronto para o próximo passo? Tente ajustar as coordenadas das ROIs para um tipo de documento diferente, ou experimente flags adicionais de pré‑processamento como `sharpen` ou `noise_reduction`. A flexibilidade do Aspose OCR permite que você ajuste o pipeline para praticamente qualquer qualidade de imagem.

Se encontrar algum problema, verifique a saída do console para regiões vazias e revise as configurações de pré‑processamento. Boa codificação, e que seu OCR seja sempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}