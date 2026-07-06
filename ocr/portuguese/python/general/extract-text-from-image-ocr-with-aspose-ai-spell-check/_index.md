---
category: general
date: 2026-05-03
description: extrair texto de imagem usando Aspose OCR e correção ortográfica com
  IA. Aprenda como fazer OCR em imagem, carregar imagem para OCR, reconhecer texto
  de fatura e liberar recursos da GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: pt
og_description: extraia texto de imagem com Aspose OCR e correção ortográfica por
  IA. Guia passo a passo cobrindo como fazer OCR em imagem, carregar a imagem para
  OCR e liberar recursos da GPU.
og_title: extrair texto de imagem – Guia completo de OCR e verificação ortográfica
tags:
- OCR
- Aspose
- AI
- Python
title: Extrair texto de imagem – OCR com Aspose AI Spell‑Check
url: /pt/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extrair texto de imagem – Guia Completo de OCR & Spell‑Check

Já precisou **extrair texto de imagem** mas não sabia qual biblioteca ofereceria velocidade e precisão? Você não está sozinho. Em muitos projetos reais — pense em processamento de faturas, digitalização de recibos ou escaneamento de contratos — obter texto limpo e pesquisável a partir de uma foto é o primeiro obstáculo.

A boa notícia é que o Aspose OCR combinado com um modelo leve Aspose AI pode fazer esse trabalho em poucas linhas de Python. Neste tutorial vamos percorrer **como fazer OCR em imagem**, carregar a foto corretamente, executar um pós‑processador de correção ortográfica embutido e, por fim, **liberar recursos da GPU** para que seu aplicativo continue econômico em memória.

Ao final deste guia você será capaz de **reconhecer texto de faturas** em imagens, corrigir automaticamente erros comuns de OCR e manter sua GPU limpa para o próximo lote.

---

## O que você precisará

- Python 3.9 ou superior (o código usa type hints, mas funciona em versões 3.x anteriores)
- Pacotes `aspose-ocr` e `aspose-ai` (instale via `pip install aspose-ocr aspose-ai`)
- Uma GPU com suporte a CUDA é opcional; o script recairá para CPU se nenhuma for encontrada.
- Uma imagem de exemplo, por exemplo `sample_invoice.png`, colocada em uma pasta que você possa referenciar.

Sem frameworks pesados de ML, sem downloads massivos de modelos — apenas um pequeno modelo quantizado Q4‑K‑M que cabe confortavelmente na maioria das GPUs.

---

## Etapa 1: Inicializar o OCR Engine – extrair texto de imagem

A primeira coisa que você faz é criar uma instância de `OcrEngine` e informar qual idioma você espera. Aqui escolhemos inglês e solicitamos saída em texto simples, ideal para processamento posterior.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Por que isso importa:** Definir o idioma restringe o conjunto de caracteres, melhorando a precisão. O modo de texto simples remove informações de layout que você normalmente não precisa quando só quer extrair texto de imagem.

---

## Etapa 2: Carregar imagem para OCR – como fazer OCR em imagem

Agora alimentamos o engine com uma foto real. O helper `Image.load` entende formatos comuns (PNG, JPEG, TIFF) e abstrai as peculiaridades de I/O de arquivos.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Dica:** Se suas imagens de origem são grandes, considere redimensioná‑las antes de enviá‑las ao engine; dimensões menores podem reduzir o uso de memória da GPU sem prejudicar a qualidade do reconhecimento.

---

## Etapa 3: Configurar o Modelo Aspose AI – reconhecer texto de fatura

Aspose AI vem com um modelo GGUF pequeno que pode ser baixado automaticamente. O exemplo usa o repositório `Qwen2.5‑3B‑Instruct‑GGUF`, quantizado para `q4_k_m`. Também instruímos o runtime a alocar 20 camadas na GPU, equilibrando velocidade e uso de VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Nos bastidores:** O modelo quantizado tem cerca de 1,5 GB no disco, uma fração de um modelo de precisão total, mas ainda captura nuance linguística suficiente para identificar erros típicos de OCR.

---

## Etapa 4: Inicializar AsposeAI e anexar o pós‑processador de correção ortográfica

Aspose AI inclui um pós‑processador de correção ortográfica pronto para uso. Ao anexá‑lo, cada resultado de OCR será limpo automaticamente.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Por que usar o pós‑processador?** Engines de OCR frequentemente leem “Invoice” como “Invo1ce” ou “Total” como “T0tal”. A correção ortográfica executa um modelo de linguagem leve sobre a string bruta e corrige esses erros sem que você precise criar um dicionário personalizado.

---

## Etapa 5: Executar o pós‑processador de correção ortográfica no resultado do OCR

Com tudo conectado, uma única chamada produz o texto corrigido. Também imprimimos as versões original e limpa para que você veja a melhoria.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Saída típica para uma fatura pode ser assim:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Observe como “Invo1ce” se transformou na palavra correta “Invoice”. Esse é o poder da correção ortográfica AI embutida.

---

## Etapa 6: Liberar recursos da GPU – liberar recursos da GPU com segurança

Se você estiver executando isso em um serviço de longa duração (por exemplo, uma API web que processa dezenas de faturas por minuto), deve liberar o contexto da GPU após cada lote. Caso contrário, ocorrerão vazamentos de memória e, eventualmente, erros de “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Dica de especialista:** Chame `free_resources()` dentro de um bloco `finally` ou de um gerenciador de contexto para que ele sempre seja executado, mesmo se ocorrer uma exceção.

---

## Exemplo Completo Funcional

Juntando todas as peças, você obtém um script autocontido que pode ser inserido em qualquer projeto.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Salve o arquivo, ajuste o caminho para sua imagem e execute `python extract_text_from_image.py`. Você deverá ver o texto da fatura limpo impresso no console.

---

## Perguntas Frequentes (FAQ)

**Q: Isso funciona em máquinas apenas com CPU?**  
A: Absolutamente. Se nenhuma GPU for detectada, Aspose AI recai para execução em CPU, embora seja mais lento. Você pode forçar a CPU definindo `model_cfg.gpu_layers = 0`.

**Q: E se minhas faturas estiverem em outro idioma que não o inglês?**  
A: Altere `ocr_engine.language` para o valor enum apropriado (por exemplo, `aocr.Language.Spanish`). O modelo de correção ortográfica é multilíngue, mas você pode obter melhores resultados com um modelo específico para o idioma.

**Q: Posso processar várias imagens em um loop?**  
A: Sim. Basta mover as etapas de carregamento, reconhecimento e pós‑processamento para dentro de um `for` loop. Lembre‑se de chamar `ocr_ai.free_resources()` após o loop ou após cada lote se estiver reutilizando a mesma instância AI.

**Q: Qual o tamanho do download do modelo?**  
A: Aproximadamente 1,5 GB para a versão quantizada `q4_k_m`. Ele é armazenado em cache após a primeira execução, então execuções subsequentes são instantâneas.

---

## Conclusão

Neste tutorial demonstramos como **extrair texto de imagem** usando Aspose OCR, configurar um modelo AI pequeno, aplicar um pós‑processador de correção ortográfica e liberar **recursos da GPU** com segurança. O fluxo cobre tudo, desde o carregamento da foto até a limpeza final, oferecendo um pipeline confiável para cenários de **reconhecimento de texto de fatura**.

Próximos passos? Experimente substituir a correção ortográfica por um modelo personalizado de extração de entidades.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}