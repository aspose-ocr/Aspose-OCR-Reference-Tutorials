---
title: Performing OCR on BufferedImage in Aspose.OCR for Java
linktitle: Performing OCR on BufferedImage in Aspose.OCR for Java
second_title: Aspose.OCR Java API
description: 
type: docs
weight: 10
url: /java/advanced-ocr-techniques/perform-ocr-buffered-image/
---

## Complete Source Code
```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class PerformOCROnBufferedImage {

	public static void main(String[] args) {
		// ExStart:1
		// The path to the documents directory.
		String dataDir = "Your Document Directory";

		// The image path
		String imagePath = dataDir + "p3.png";

		//Create api instance
		AsposeOCR api = new AsposeOCR();

		// Recognize page from BufferedImage
		try {
			BufferedImage loaded = ImageIO.read(new File(imagePath));
			String result = api.RecognizePage(loaded);
			System.out.println("Result BufferedImage: " + result);
		} catch (IOException e) {
			e.printStackTrace();
		}
		// ExEnd:1
	}
}

```
