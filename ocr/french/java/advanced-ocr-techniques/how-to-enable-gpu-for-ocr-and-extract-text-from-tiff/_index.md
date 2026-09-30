---
category: general
date: 2026-02-14
description: Comment activer le GPU dans Aspose OCR Java pour extraire rapidement
  du texte d’une image. Apprenez à convertir un TIFF en texte, à définir l’ID du dispositif
  GPU et à lire le texte des fichiers TIFF.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: fr
og_description: Comment activer le GPU dans Aspose OCR Java pour extraire rapidement
  du texte d’une image. Suivez ce guide pour convertir un TIFF en texte, définir l’ID
  du dispositif GPU et lire le texte d’un TIFF.
og_title: Comment activer le GPU pour l’OCR – Extraire le texte d’un TIFF
tags:
- OCR
- Java
- GPU acceleration
title: Comment activer le GPU pour l'OCR et extraire le texte d'un fichier TIFF
url: /fr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU pour l'OCR et extraire du texte d'un TIFF

Vous vous êtes déjà demandé **comment activer le GPU** lors de l'exécution de l'OCR sur de gros fichiers TIFF ? Vous n'êtes pas le seul—les développeurs recherchent constamment ce gain de vitesse supplémentaire, surtout lorsque l'image source est un TIFF de plusieurs mégaoctets. Bonne nouvelle ? Avec Aspose OCR for Java, vous pouvez basculer un commutateur, pointer vers le bon GPU, et voir le moteur parcourir l'image à toute vitesse.

Dans ce tutoriel, nous parcourrons l'ensemble du flux de travail : charger un TIFF, activer l'accélération GPU, choisir éventuellement un dispositif GPU spécifique, exécuter l'OCR, et enfin **extraire le texte de l'image**. À la fin, vous pourrez **convertir un TIFF en texte** en quelques lignes de code, et vous verrez également comment **lire le texte d'un TIFF** sur n'importe quelle plateforme prise en charge.

## Ce dont vous avez besoin

- Java 17 ou plus récent (le code fonctionne également avec Java 8+)
- Aspose OCR for Java 23.10 (ou la dernière version au moment de la rédaction)
- Un GPU compatible CUDA avec le dernier pilote installé
- Un exemple de TIFF multi‑pages (nous l'appellerons `sample_large.tif`)

Pas de magie Maven ? Pas de problème—déposez simplement le JAR dans votre classpath et vous êtes prêt à l'emploi.

![Comment activer le GPU pour l'OCR en Java](gpu-ocr.png)

*Texte alternatif de l'image : Comment activer le GPU pour l'OCR en Java*

## Étape 1 : Charger une image TIFF pour l'OCR

Tout d'abord : vous avez besoin d'une instance `OcrEngine` et d'une image source. Aspose OCR peut lire pratiquement n'importe quel format raster, mais le TIFF est courant pour les documents numérisés.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Pourquoi c'est important :** L'appel `setImage` enveloppe le fichier dans un `ImageStream`, ce qui permet au moteur de gérer les TIFF multi‑pages sans que vous ayez à les découper manuellement. Si le fichier est introuvable, vous recevrez une `FileNotFoundException` claire—vérifiez donc le chemin.

## Étape 2 : Activer l'accélération GPU

Maintenant, la magie opère. Activer le GPU n'est qu'un drapeau booléen, mais cela peut économiser des secondes—voire des minutes—sur le temps de traitement.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Astuce pro :** Si votre machine possède plusieurs GPU, le défaut est généralement le premier (device 0). Vous pouvez laisser Aspose choisir automatiquement le meilleur dispositif, mais le spécifier peut éviter des surprises sur les stations de travail multi‑GPU.

## Étape 3 : Définir l'ID du dispositif GPU (optionnel)

Parfois, vous savez exactement quel GPU vous voulez utiliser—peut-être que la deuxième carte est dédiée aux charges de travail IA. C'est là que `setGpuDeviceId` brille.

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Cas limite :** Si vous transmettez un ID invalide, le moteur lève une `IllegalArgumentException`. Un rapide `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` peut lister les IDs pour vous.

## Étape 4 : Traiter l'image et **extraire le texte de l'image**

Avec le moteur configuré, il est temps d'exécuter l'OCR. L'objet résultat vous fournit la chaîne brute, ainsi que les scores de confiance si vous en avez besoin.

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Sortie attendue

Si le TIFF contient la phrase « Hello, World! », vous devriez voir quelque chose comme :

```
Recognized text:
Hello, World!
```

Le moteur gère les sauts de ligne, la ponctuation, et même la détection de mise en page basique. Pour un contrôle plus granulaire (par ex., extraire le texte par page), explorez `ocrResult.getPages()`.

## Étape 5 : Vérifier la sortie et gérer les problèmes courants

### Pourquoi le GPU pourrait-il ne pas être utilisé ?

- **Incompatibilité du pilote :** Le pilote GPU doit être au moins la version recommandée par Aspose (vérifiez les notes de version).
- **Mémoire insuffisante :** Les images très volumineuses peuvent dépasser la VRAM du GPU. Dans ce cas, le moteur revient gracieusement au CPU—recherchez un avertissement dans la console.
- **Matériel non supporté :** Les graphiques intégrés manquent souvent de la capacité de calcul requise.

### Comment revenir au CPU de manière programmatique

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Lire le texte d'un TIFF dans une boucle

Si vous avez un dossier rempli de TIFF, vous pouvez itérer :

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Cet extrait montre comment **lire le texte d'un TIFF** en masse, tout en bénéficiant toujours de l'accélération GPU.

## Questions fréquemment posées (FAQ)

**Q : Cela fonctionne-t-il sous Linux ?**  
R : Absolument—Aspose OCR est multiplateforme. Assurez‑vous simplement que le toolkit CUDA et les pilotes sont installés.

**Q : Et si je n’ai pas de GPU ?**  
R : Réglez `setUseGpu(false)` ou omettez simplement l’appel. Le moteur utilise le CPU par défaut.

**Q : Puis‑je extraire du texte d’autres formats ?**  
R : Oui, la même méthode `setImage` accepte les flux JPEG, PNG, BMP, et même PDF.

**Q : Quelle est la précision de l'OCR sur des TIFF à basse résolution ?**  
R : La précision chute en dessous de 300 dpi. Envisagez de pré‑traiter l'image (binarisation, redressement) avant de la transmettre au moteur.

## Conclusion

Vous savez maintenant **comment activer le GPU** pour Aspose OCR Java, comment **définir l'ID du dispositif GPU**, et—plus important—comment **extraire le texte d'une image** efficacement, notamment **convertir un TIFF en texte** et **lire le texte d'un TIFF**. En basculant un seul drapeau et éventuellement en choisissant un dispositif, vous débloquez d'énormes gains de performance sans réécrire aucune logique OCR.

Prêt pour l'étape suivante ? Essayez d'expérimenter avec :

- **Traitement par lots** de centaines de TIFF en threads parallèles.
- **Packs de langues personnalisés** pour améliorer la reconnaissance sur des documents spécialisés.
- **Post‑traitement** de la chaîne extraite avec des expressions régulières pour nettoyer le formatage.

N'hésitez pas à laisser un commentaire si vous rencontrez des problèmes, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}