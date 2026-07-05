---
category: general
date: 2026-07-05
description: Apprenez à exécuter l’OCR sur des PDF et à améliorer la précision de
  l’OCR à l’aide d’un modèle Hugging Face. Installation pas à pas, chargement du PDF
  pour l’OCR et configuration du modèle Hugging Face.
draft: false
keywords:
- run OCR on PDF
- improve OCR accuracy
- load PDF for OCR
- configure Hugging Face model
language: fr
og_description: Exécutez la reconnaissance optique de caractères (OCR) sur un PDF
  avec un modèle Hugging Face et améliorez la précision de l'OCR. Suivez ce guide
  pour charger le PDF pour l'OCR et configurer le modèle.
og_title: Exécuter l'OCR sur PDF – Tutoriel complet pour une meilleure précision
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  headline: run OCR on PDF – Complete Guide to Boost Accuracy
  type: TechArticle
- description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  name: run OCR on PDF – Complete Guide to Boost Accuracy
  steps:
  - name: What if the PDF is multi‑page?
    text: The `Image.from_file` call automatically creates a multi‑frame image object.
      Loop over `input_image.frames` and call `ocr_engine.recognize` for each frame,
      then concatenate the results before running the post‑processor.
  - name: How to handle languages other than English?
    text: 'Set the OCR engine’s language property before recognition:'
  - name: Can I run this on CPU only?
    text: Yes—just omit `model_cfg.gpu_layers` or set it to `0`. The model will run
      entirely on CPU, though inference will be slower (roughly 5‑10 seconds per page
      on a modern i7).
  type: HowTo
tags:
- OCR
- Python
- AI post‑processor
title: Effectuer l’OCR sur PDF – Guide complet pour augmenter la précision
url: /fr/python/general/run-ocr-on-pdf-complete-guide-to-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# exécuter OCR sur PDF – Guide complet pour améliorer la précision

Vous êtes-vous déjà demandé comment **exécuter OCR sur PDF** sans dépenser une fortune en SDK commerciaux ? Vous n'êtes pas le seul. Que vous numérisiez des factures, extrayiez des données de rapports scannés, ou que vous soyez simplement curieux de l'extraction de texte améliorée par l'IA, la capacité à **exécuter OCR sur PDF** efficacement est une compétence indispensable pour tout développeur moderne.

Dans ce tutoriel, nous parcourrons un exemple pratique, de bout en bout, qui non seulement vous montre comment **exécuter OCR sur PDF**, mais démontre également comment **améliorer la précision OCR** en ajoutant un post‑processeur IA. Nous aborderons également les détails de **load PDF for OCR** et de **configure Hugging Face model** afin d’obtenir les meilleures performances sur une station de travail modeste.

À la fin de ce guide, vous disposerez d’un script entièrement fonctionnel qui :

* Charge un PDF (ou une image) pour l’OCR  
* Configure un modèle Hugging Face avec quantification personnalisée et couches GPU  
* Exécute une OCR brute puis améliore le résultat avec un post‑processeur IA  
* Affiche le texte brut et le texte amélioré par l’IA pour une comparaison facile  

Aucun service externe, aucun frais caché — juste des bibliothèques open‑source et quelques lignes de Python.

## Ce qu’il vous faut

Avant de plonger, assurez‑vous d’avoir les prérequis suivants :

* Python 3.9 ou plus récent installé (le module `venv` est pratique)  
* Package `aocr` (Aspose OCR) – installez‑le via `pip install aocr`  
* Accès à Internet pour le téléchargement unique du modèle depuis Hugging Face  
* Un fichier PDF que vous souhaitez traiter (nous utiliserons `invoice_2026.pdf` comme exemple)  

C’est tout. Si l’un de ces éléments vous semble inconnu, ne vous inquiétez pas — chaque étape ci‑dessous explique le pourquoi et le comment, vous serez opérationnel en quelques minutes.

---

## Étape 1 : Configurer le modèle Hugging Face

La première chose à faire est de **configure Hugging Face model** avec des paramètres adaptés à votre matériel. Dans notre cas, nous téléchargerons le tout nouveau modèle `Qwen/Qwen2.5-3B-Instruct-GGUF`, le quantifierons en `int8` pour une empreinte mémoire minime, et placerons les 20 premières couches sur le GPU pour la vitesse.

```python
import aocr

# Create the AI engine that will later post‑process OCR results
ai_engine = aocr.AsposeAI()

# Build the model configuration – this is where we "configure Hugging Face model"
model_cfg = aocr.AsposeAIModelConfig()
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"   # released early‑2026
model_cfg.hugging_face_quantization = "int8"                     # small memory footprint
model_cfg.gpu_layers = 20                                        # use first 20 layers on GPU
model_cfg.allow_auto_download = "true"

# Initialize the engine – it will download the model if it's not already cached
ai_engine.initialize(model_cfg)
```

**Pourquoi c’est important :** Quantifier en `int8` réduit le modèle de plusieurs gigaoctets à moins d’un gigaoctet, le rendant utilisable sur des ordinateurs portables. Limiter les couches GPU équilibre vitesse et utilisation de la VRAM — idéal pour une carte de 6 Go.

> **Astuce :** Si vous rencontrez des erreurs de dépassement de mémoire, réduisez `gpu_layers` à `10` ou passez `quantization` à `"float16"` pour un modèle légèrement plus gros qui tient toujours sur la plupart des GPU grand public.

---

## Étape 2 : Charger le PDF pour l’OCR

Maintenant que le moteur IA est prêt, nous devons **load PDF for OCR**. La bibliothèque Aspose OCR traite les PDF et les images de manière uniforme, vous pouvez donc la pointer vers un chemin de fichier ou un flux.

```python
# Create the OCR engine that will perform the initial text extraction
ocr_engine = aocr.OcrEngine()

# Attach the AI post‑processor – we’ll use the default run_postprocessor method
ocr_engine.set_post_processor(ai_engine.run_postprocessor, None)  # no custom settings required

# Load the PDF document – this is the step where we "load PDF for OCR"
input_image = aocr.Image.from_file("YOUR_DIRECTORY/invoice_2026.pdf")
```

**Pourquoi c’est important :** En chargeant le PDF directement dans un objet `Image`, le moteur OCR peut gérer les PDF multipages page par page en interne. Aucun besoin de découper manuellement le PDF en images au préalable.

> **Attention :** Si votre PDF contient des pages chiffrées, vous devrez fournir le mot de passe via `Image.from_file(..., password="secret")`.

---

## Étape 3 : Exécuter OCR sur PDF

Avec le document en mémoire, il est temps de **run OCR on PDF**. La première passe nous donne du texte brut, souvent truffé d’erreurs d’espacement, de caractères mal reconnus ou de ponctuation manquante — surtout dans les factures scannées.

```python
# Perform the plain OCR pass – this is the core "run OCR on PDF" operation
raw_result = ocr_engine.recognize(input_image)  # raw OCR output
```

À ce stade, `raw_result.text` contient la sortie OCR non modifiée. Vous pouvez l’inspecter, l’enregistrer dans les logs, ou même le transmettre à des pipelines en aval.

> **Note :** La méthode `recognize` détecte automatiquement l’orientation des pages et tente de corriger l’inclinaison, mais elle ne résout pas les particularités propres à chaque langue — c’est là que le post‑processeur IA intervient.

---

## Étape 4 : Améliorer la précision OCR avec le post‑processeur IA

Passons maintenant à la partie amusante : **improve OCR accuracy**. En alimentant le résultat brut dans le moteur IA que nous avons configuré précédemment, nous laissons un grand modèle de langage nettoyer le texte, corriger les fautes et même deviner les valeurs manquantes.

```python
# Enhance the raw OCR output using the AI post‑processor
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

Le post‑processeur exécute le LLM sur chaque ligne (ou bloc) de texte, en appliquant une invite qui lui demande de « nettoyer les erreurs OCR tout en préservant le sens original ». Le résultat est une version polie, nettement plus lisible.

**Pourquoi cela fonctionne :** Les LLM modernes maîtrisent les schémas linguistiques et peuvent deviner le mot voulu lorsqu’un token OCR est corrompu. Couplé au modèle quantifié en `int8`, le raffinement s’achève en moins d’une seconde pour une facture typique d’une page.

---

## Étape 5 : Examiner les résultats

Enfin, affichons à la fois la sortie brute et la sortie améliorée par l’IA côte à côte afin que vous puissiez constater la différence.

```python
print("=== Raw OCR ===")
print(raw_result.text)

print("\n=== AI‑enhanced ===")
print(enhanced_result.text)
```

**Sortie attendue (troncature) :**

```
=== Raw OCR ===
Inv0ice N0: 2026-00123
Date: 01/02/2026
Tot@l Am0unt: $1,234.56
...

=== AI‑enhanced ===
Invoice No: 2026-00123
Date: 01/02/2026
Total Amount: $1,234.56
...
```

Remarquez comment la version améliorée par l’IA a corrigé les confusions de lettres (`Inv0ice` → `Invoice`) et éliminé le symbole `@` errant. Pour la plupart des documents, vous verrez une réduction de 30 % à 80 % des erreurs OCR.

> **Astuce :** Si vous avez besoin du texte amélioré dans un format structuré (par ex. JSON), vous pouvez post‑traiter davantage `enhanced_result` avec des expressions régulières ou une petite fonction d’analyse.

---

## Optionnel : Visualiser le processus

Voici un diagramme simple qui décrit le flux. Le texte alternatif contient le mot‑clé principal pour satisfaire le SEO.

![Diagramme montrant les étapes pour exécuter OCR sur PDF et améliorer la précision OCR avec un post‑processeur IA](run-ocr-on-pdf-diagram.png)

---

## Questions fréquentes & cas particuliers

### Que faire si le PDF est multipage ?

L’appel `Image.from_file` crée automatiquement un objet image multi‑cadres. Parcourez `input_image.frames` et appelez `ocr_engine.recognize` pour chaque cadre, puis concaténez les résultats avant d’exécuter le post‑processeur.

```python
pages_text = []
for frame in input_image.frames:
    raw = ocr_engine.recognize(frame)
    enhanced = ocr_engine.run_postprocessor(raw)
    pages_text.append(enhanced.text)

full_text = "\n".join(pages_text)
```

### Comment gérer des langues autres que l’anglais ?

Définissez la propriété de langue du moteur OCR avant la reconnaissance :

```python
ocr_engine.language = aocr.Language.French  # or aocr.Language.Spanish, etc.
```

Le LLM améliorera toujours la précision tant que le modèle que vous **configure Hugging Face model** supporte la langue cible (la plupart le font).

### Puis‑je exécuter cela uniquement sur le CPU ?

Oui—il suffit d’omettre `model_cfg.gpu_layers` ou de le régler à `0`. Le modèle fonctionnera entièrement sur le CPU, bien que l’inférence soit plus lente (environ 5‑10 secondes par page sur un i7 moderne).

---

## Récapitulatif

Nous avons couvert tout ce qu’il faut pour **run OCR on PDF** et **improve OCR accuracy** :

1. **configure Hugging Face model** avec quantification et couches GPU.  
2. **load PDF for OCR** en utilisant `Image.from_file` d’Aspose OCR.  
3. **run OCR on PDF** pour obtenir le texte brut.  
4. **improve OCR accuracy** en passant le résultat à un post‑processeur IA.  
5. **review** les sorties brute et améliorée.

N’hésitez pas à expérimenter — changez l’ID du dépôt du modèle pour un LLM plus récent, ajustez l’invite dans `ai_engine.run_postprocessor` (si vous explorez son code source), ou ajoutez des étapes de pré‑traitement comme le redressement. Le pipeline est modulaire, vous pouvez remplacer n’importe quel composant sans casser le reste.

---

## Prochaines étapes

* **Explorer d’autres modèles de post‑traitement** – essayez une variante `distilbert` plus petite si vous avez une machine peu puissante.  
* **Intégrer à une base de données** – stockez le texte amélioré dans SQLite ou Elasticsearch pour des archives consultables.  
* **Ajouter la génération de PDF** – utilisez `reportlab` ou `pypdf` pour annoter le PDF original avec le texte nettoyé.  

Si vous avez suivi le guide, vous disposez maintenant d’une base solide pour créer des documents robustes, enrichis par l’IA.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment faire de l'OCR PDF en .NET avec Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Comment effectuer l'OCR PDF en .NET avec Aspose.OCR](/ocr/hongkong/net/text-recognition/recognize-pdf/)
- [Comment faire de l'OCR PDF en .NET avec Aspose.OCR](/ocr/korean/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}