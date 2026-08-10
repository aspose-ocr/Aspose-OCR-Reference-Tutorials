---
category: general
date: 2026-06-25
description: Carregue a imagem para OCR e realize OCR em PNG com um tutorial passo
  a passo em Python usando aocr. Aprenda depuração, registro de logs e melhores práticas.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: pt
og_description: Carregue a imagem para OCR e execute OCR em PNG usando aocr. Este
  guia orienta você através do registro, carregamento de imagem e reconhecimento com
  código completo.
og_title: Carregar Imagem para OCR – Tutorial Python Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Carregar Imagem para OCR – Guia Completo para Realizar OCR em Arquivos PNG
url: /pt/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carregar Imagem para OCR – Guia Completo para Executar OCR em Arquivos PNG

Já precisou **carregar imagem para OCR** mas não tinha certeza de como configurar a depuração adequada? Você não está sozinho. Em muitos projetos, o primeiro obstáculo é colocar esse PNG no motor enquanto ainda é possível ver o que está acontecendo nos bastidores.  

Neste tutorial vamos guiá‑lo por tudo que você precisa para **executar OCR em PNG** usando a biblioteca `aocr` – desde a configuração de um logger para saída detalhada até o reconhecimento real do texto. Ao final, você terá um script reutilizável que pode ser inserido em qualquer projeto Python e entenderá por que cada parte é importante.

## O que Você Vai Aprender

- Como inicializar o logger do `aocr` para rastrear cada passo.  
- O código exato para **carregar imagem para OCR** com `aocr.OcrEngine`.  
- Como configurar o nível de logging para obter informações de depuração granulares.  
- Executar o motor para **executar OCR em PNG** e recuperar os resultados.  
- Dicas para lidar com armadilhas comuns, como arquivos ausentes ou formatos não suportados.  

Nenhuma experiência prévia com `aocr` é necessária; basta uma instalação funcional do Python 3 e uma imagem que você queira ler. Vamos começar.

![load image for OCR example](assets/load-image-ocr.png "Illustration of loading an image for OCR in Python")

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| Python 3.8+ | `aocr` tem como alvo interpretadores modernos e usa type hints. |
| Biblioteca `aocr` instalada (`pip install aocr`) | Sem o pacote, as classes que usamos não existirão. |
| Uma imagem PNG que você deseja ler | O tutorial foca em **executar OCR em PNG**, portanto um PNG é essencial. |
| Permissão de gravação em um diretório de logs | O logger precisa criar `ocr_debug.log`. |

Se estiver faltando algum desses itens, instale agora – leva apenas um minuto.

```bash
pip install aocr
```

## Etapa 1: Carregar Imagem para OCR – Inicializar Log

Antes de tocar na imagem, configure um logger. Depurar OCR pode ser um pesadelo se você não souber o que o motor está fazendo. A classe `aocr.Logging` grava tudo em um arquivo e, ao definir o nível para `DEBUG`, você verá cada chamada interna.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Por que isso importa:**  
Se o motor OCR não encontrar o arquivo ou o formato da imagem não for suportado, o logger capturará o rastreamento da exceção. Isso salva você de adivinhações intermináveis mais tarde.

## Etapa 2: Executar OCR em PNG – Configurar o Motor

Agora que o logger está pronto, anexe‑o ao motor OCR. Esta etapa conecta os dois para que cada ação do motor seja registrada.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Dica profissional:**  
Você pode reutilizar a mesma instância `ocr_engine` para várias imagens. Apenas lembre‑se de limpar qualquer estado anterior se processar um lote.

## Etapa 3: Carregar Imagem para OCR – Alimentar o Arquivo PNG

Aqui está o núcleo do tutorial: realmente **carregar imagem para OCR**. O método `load_image` aceita um caminho de arquivo; ele decodifica internamente o PNG em um bitmap que o motor pode entender.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Casos Limítrofes a Observar

1. **Arquivo Não Encontrado** – Se o caminho estiver errado, `aocr` gera um `FileNotFoundError`. O logger anotará isso, mas você também pode capturá‑lo:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Formato Não Suportado** – Embora PNG seja amplamente suportado, um arquivo corrompido pode disparar `UnsupportedFormatError`. Nesse caso, considere converter a imagem para um PNG limpo com Pillow antes de carregá‑la.

## Etapa 4: Executar OCR em PNG – Executar o Reconhecimento

Agora que a imagem está na memória, você pode finalmente **executar OCR em PNG**. O método `recognize` inicia os pipelines do motor (pré‑processamento, segmentação, classificação) e preenche o objeto de resultado.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Após esta chamada, o motor contém o texto reconhecido. Você pode acessá‑lo através do atributo `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Por que você deve verificar o resultado:**  
Alguns motores OCR retornam strings vazias para imagens de baixo contraste. Ver o resultado imediatamente permite decidir se é necessário pré‑processar (por exemplo, aumentar o contraste) antes de executar novamente.

## Etapa 5: Consolidar Tudo – Uma Função Reutilizável

Agrupar as peças em uma única função facilita a chamada a partir de outros scripts ou de um serviço web. Isso também demonstra como **carregar imagem para OCR** e **executar OCR em PNG** em um pacote organizado.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Executar o script gerará um `ocr_debug.log` detalhado na pasta `logs` e, em seguida, imprimirá o texto reconhecido no console. Agora você tem uma utilidade de **executar OCR em PNG** que pode ser importada em outros lugares.

## Perguntas Frequentes & Armadilhas

- **Preciso converter o PNG para outro formato?**  
  Normalmente não. `aocr` lida com PNG nativamente, mas se a imagem for muito grande (>10 MP) pode ser interessante reduzi‑la primeiro para acelerar o processamento.

- **E se o arquivo de log crescer demais?**  
  Gire o log após cada execução ou limite o nível para `INFO` quando estiver confiante de que o pipeline funciona.

- **Posso processar várias imagens em um loop?**  
  Absolutamente. Basta chamar `ocr_png` para cada arquivo; a função cria um logger novo a cada vez, mantendo os logs isolados.

- **Existe uma forma de obter caixas delimitadoras ao invés de texto puro?**  
  Sim – `engine.result` também contém `boxes` e `confidences`. Explore a documentação do `aocr` para `result.boxes` se precisar de informações de layout.

## Conclusão

Agora você sabe como **carregar imagem para OCR** e **executar OCR em PNG** usando a biblioteca `aocr`, com uma configuração robusta de logging que torna a depuração indolor. A função de exemplo encapsula todo o fluxo de trabalho, permitindo que você a insira em qualquer projeto e comece a extrair texto imediatamente.

Próximos passos? Experimente alimentar o motor com diferentes tipos de imagem (JPEG, TIFF) para observar como a precisão varia, ou teste técnicas de pré‑processamento como limiarização para melhorar resultados em digitalizações ruidosas. E se estiver curioso sobre a extração de dados estruturados (tabelas, formulários), consulte as seções do `aocr` sobre análise de layout – elas complementam bem o que você acabou de construir.

Feliz codificação, e que seus pipelines de OCR sejam sempre livres de erros!

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como Fazer OCR em Imagem – Executar OCR em Imagem no Reconhecimento de Imagem OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Extrair Texto de Imagem – Otimização de OCR com Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}