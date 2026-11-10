---
category: general
date: 2026-09-22
description: Apprenez à exécuter la reconnaissance optique de caractères (OCR) sur
  une image avec Aspose OCR, à configurer le modèle OCR, à extraire le texte d’une
  facture et à améliorer la précision de l’OCR en Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from invoice
- improve OCR accuracy
- configure OCR model
language: fr
lastmod: 2026-09-22
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  avec Aspose OCR, configurez le modèle OCR, extrayez le texte d’une facture et améliorez
  la précision de l’OCR dans un tutoriel complet, étape par étape.
og_image_alt: Screenshot showing raw OCR and AI‑enhanced text extracted from an invoice
  image
og_title: Effectuer l’OCR sur une image avec Aspose OCR – guide complet Python
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to run OCR on image using Aspose OCR, configure the OCR model,
    extract text from invoice and improve OCR accuracy in Python.
  headline: How to run OCR on image with Aspose OCR and boost accuracy
  type: TechArticle
tags:
- Aspose OCR
- Python
- AI post‑processing
title: Comment exécuter l’OCR sur une image avec Aspose OCR et améliorer la précision
url: /fr/python/general/how-to-run-ocr-on-image-with-aspose-ocr-and-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR sur une image avec Aspose OCR et améliorer la précision

Si vous devez **exécuter l'OCR sur des fichiers image** en Python, ce guide vous montre un flux de travail complet, prêt pour la production. Vous verrez comment configurer le modèle OCR, extraire du texte à partir de photos de factures, et améliorer la précision de l'OCR avec le post‑processeur IA d’Aspose.

Le traitement des factures numérisées est un point de douleur fréquent — l'OCR brut renvoie souvent des mots mal orthographiés ou des nombres tronqués. À la fin de ce tutoriel, vous disposerez d’un script prêt à l’emploi qui fournit une extraction de texte plus propre et plus fiable, et vous comprendrez pourquoi chaque étape de configuration est importante.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Python 3.8 ou une version plus récente installé.
* Une licence active Aspose OCR (l’essai gratuit suffit pour l’évaluation).
* Une image de facture d’exemple (par ex. `sample_invoice.png`) placée dans un répertoire connu.
* Une connaissance de base de l’installation de paquets Python.

Aucune dépendance système supplémentaire n’est requise ; le SDK gère automatiquement le téléchargement du modèle.

## Étape 1 : Installer le package Aspose OCR

La première chose à faire est d’ajouter la bibliothèque Aspose OCR à votre environnement. Le package inclut le modèle IA et le post‑processeur dont vous aurez besoin plus tard.

```bash
pip install aspose-ocr
```

L’exécution de cette commande installe `asposeocr`, qui fournit la classe `AsposeAI` utilisée pour **configurer les paramètres du modèle OCR** tels que les téléchargements automatiques et l’exécution uniquement CPU.

## Étape 2 : Configurer le modèle OCR (optionnel mais recommandé)

Affiner le modèle améliore la vitesse et la précision, surtout lorsque vous exécutez l'OCR sur des images de factures contenant de nombreux chiffres et caractères spéciaux. Le code suivant montre les paramètres les plus utiles :

```python
import asposeocr as ocr   # import the Aspose OCR package

# Create an AsposeAI instance with default logging
ai = ocr.AsposeAI()

# Enable automatic model download, force CPU execution, and enlarge the context window
ai.allow_auto_download = "true"   # download missing model files automatically
ai.gpu_layers = 0                 # use CPU only – avoids GPU‑related errors on most machines
ai.context_size = 2048           # larger context improves correction quality
```

*Pourquoi ces indicateurs ?*  
* `allow_auto_download` garantit que le modèle OCR est présent même sur une machine fraîche.  
* `gpu_layers = 0` supprime le besoin d’un GPU compatible CUDA, que beaucoup de développeurs n’ont pas.  
* `context_size` contrôle le nombre de tokens environnants que l’IA considère lors de la correction des erreurs ; une fenêtre plus grande **améliore la précision de l'OCR** sur du texte dense comme les factures.

## Étape 3 : Initialiser le moteur IA

L’initialisation vérifie que les fichiers du modèle sont prêts et les charge en mémoire. Ignorer cette étape peut entraîner une erreur d’exécution lorsque vous appelez plus tard le post‑processeur.

```python
# Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")
```

Si le moteur échoue, l’exception indique exactement où le problème s’est produit, vous faisant gagner du temps de débogage.

## Étape 4 : Exécuter le moteur OCR standard sur une image

Vous pouvez maintenant **exécuter l'OCR sur une image**. La classe `OcrEngine` effectue l’extraction brute du texte sans aucune correction basée sur l’IA.

```python
# Path to the invoice image you want to process
image_path = "YOUR_DIRECTORY/sample_invoice.png"

# Perform raw OCR
ocr_result = ocr.OcrEngine().recognize_image(image_path)
```

`ocr_result.text` contient la chaîne brute reconnue par le moteur OCR. Pour une facture typique, vous pourriez voir des chiffres manquants, une ponctuation mal placée ou des mots tronqués.

## Étape 5 : Appliquer le post‑processeur IA pour améliorer la précision de l'OCR

Le post‑processeur IA d’Aspose analyse la sortie brute et corrige les erreurs d’OCR courantes (par ex. « 5um » → « Sum »). Cette étape est la clé pour **améliorer la précision de l'OCR** des documents financiers.

```python
# Apply the AI post‑processor
cleaned_result = ai.run_postprocessor(ocr_result)
```

Le post‑processeur utilise la configuration définie à l’Étape 2, de sorte que le `context_size` plus grand contribue à des corrections plus fiables.

## Étape 6 : Extraire le texte de la facture et afficher les résultats

À ce stade vous avez deux versions du texte extrait : la sortie brute de l’OCR et la version améliorée par l’IA. Les afficher toutes les deux vous permet de vérifier l’amélioration et vous donne également la possibilité d’enregistrer les données originales à des fins d’audit.

```python
# Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)

print("\n=== AI‑enhanced ===")
print(cleaned_result.text)
```

**Sortie typique**

```
=== Raw OCR ===
Inv0ice No: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00

=== AI‑enhanced ===
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Remarquez comment l’étape IA a corrigé les confusions zéro‑un et a reformatté les montants — exactement le type d’amélioration dont vous avez besoin lorsque vous **extrayez du texte d’une facture**.

## Étape 7 : Libérer les ressources

Enfin, libérez les ressources natives utilisées par le moteur IA. Cela est particulièrement important dans les services de longue durée ou les traitements par lots.

```python
# Release resources when finished
ai.free_resources()
```

Négliger cet appel peut entraîner des fuites de mémoire, car le modèle sous‑jacent s’exécute en code natif.

## Script complet à copier‑coller

Voici le programme complet, exécutable, qui intègre chaque étape décrite ci‑dessus. Remplacez `YOUR_DIRECTORY` par le chemin réel vers votre fichier image.

```python
import asposeocr as ocr   # import the Aspose OCR package

# Step 1: Create an AsposeAI instance (default logging)
ai = ocr.AsposeAI()

# Step 2: (Optional) Tune the model configuration for this demo
#   • Enable automatic download of the model if missing
#   • Use CPU only (no GPU layers)
#   • Increase context size for better correction quality
ai.allow_auto_download = "true"
ai.gpu_layers = 0
ai.context_size = 2048

# Step 3: Initialise the AI engine – ensures the model is ready to use
if not ai.is_initialized():
    raise RuntimeError("AI engine failed to initialise")

# Step 4: Run the standard OCR engine on an image
image_path = "YOUR_DIRECTORY/sample_invoice.png"
ocr_result = ocr.OcrEngine().recognize_image(image_path)

# Step 5: Apply the AI post‑processor to improve the raw OCR output
cleaned_result = ai.run_postprocessor(ocr_result)

# Step 6: Display both the raw and the AI‑enhanced text
print("=== Raw OCR ===")
print(ocr_result.text)
print("\n=== AI‑enhanced ===")
print(cleaned_result.text)

# Step 7: Release resources when finished
ai.free_resources()
```

Enregistrez-le sous le nom `process_invoice.py` et exécutez :

```bash
python process_invoice.py
```

Vous devriez voir le texte brut et le texte corrigé affichés dans la console, confirmant que vous avez **exécuté l'OCR sur une image**, **configuré le modèle OCR**, et **amélioré la précision de l'OCR** pour votre tâche d’extraction de factures.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|--------|
| *Que faire si le modèle ne parvient pas à se télécharger ?* | Assurez‑vous que votre machine a accès à Internet et que le drapeau `allow_auto_download` est réglé sur `"true"`. Vous pouvez également télécharger le modèle manuellement depuis le portail Aspose et indiquer le chemin local à `AsposeAI` via `ai.model_path = "path/to/model"` |
| *Puis‑je exécuter cela sur un GPU ?* | Oui. Réglez `ai.gpu_layers` à un entier positif (par ex. `2`) et installez les bibliothèques CUDA appropriées. L’exécution sur GPU accélère les gros lots mais nécessite un GPU compatible. |
| *Comment traiter de nombreuses factures dans un dossier ?* | Enveloppez la logique principale dans une boucle qui itère sur `os.listdir(folder)`. N’oubliez pas d’appeler `ai.free_resources()` uniquement après la fin de la boucle, pas après chaque fichier, afin de garder le modèle chargé. |
| *Le post‑processeur est‑il sûr pour des factures non‑anglais ?* | Le modèle par défaut est entraîné sur du texte anglais. Pour d’autres langues, téléchargez le pack linguistique correspondant et définissez `ai.language = "fr"` (ou le code ISO approprié). |
| *Que faire si le résultat OCR est vide ?* | Vérifiez que `image_path` pointe vers une image lisible et que le fichier n’est pas corrompu. Vous pouvez également augmenter `ai.context_size` pour offrir plus de contexte au modèle lors de scans de mauvaise qualité. |

## Prochaines étapes

Maintenant que vous pouvez **exécuter l'OCR sur une image** et extraire de façon fiable du texte de factures, envisagez les extensions suivantes :

* **Traitement par lots** – combinez le script avec `multiprocessing` pour gérer des milliers de factures en parallèle.  
* **Validation des données** – utilisez des expressions régulières pour vérifier les numéros de facture, les dates et les montants après extraction.  
* **Intégration avec des bases de données** – stockez le texte nettoyé directement dans PostgreSQL ou MongoDB pour des analyses en aval.  
* **Affinage de modèle personnalisé** – si vous disposez d’un grand jeu de données propriétaire, entraînez un modèle spécifique au domaine et pointez `ai.model_path` vers celui‑ci pour une précision encore plus élevée.  

En expérimentant ces idées, vous transformerez une simple démonstration d’OCR en un pipeline de traitement de documents robuste, répondant aux exigences de production.

---

*Vous savez maintenant comment exécuter l'OCR sur des fichiers image avec Aspose OCR, configurer le modèle OCR pour des performances optimales, et améliorer la précision de l'OCR à l’aide du post‑processeur IA. Appliquez ces étapes à vos propres flux de traitement de factures et profitez d’une extraction de texte plus propre et plus fiable.*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Run OCR on Invoices – Extract Text from Image with Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}