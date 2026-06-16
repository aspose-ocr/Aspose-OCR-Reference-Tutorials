---
category: general
date: 2026-02-24
description: วิธีเปิดใช้งาน GPU ในตัวอย่าง Aspose OCR C# – แปลงภาพเป็นข้อความธรรมดาอย่างรวดเร็ว
  รวมการตั้งค่า GPU device ID และคำแนะนำการอ่านข้อความจากภาพด้วย C#
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: th
og_description: วิธีเปิดใช้งาน GPU ในตัวอย่าง Aspose OCR ด้วย C# เรียนรู้การตั้งค่า
  GPU device ID และอ่านข้อความจากภาพด้วย C# อย่างมีประสิทธิภาพ.
og_title: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR ใน C# – แปลงภาพเป็นข้อความอย่างรวดเร็ว
tags:
- Aspose OCR
- C#
- GPU acceleration
title: วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR ใน C# – แปลงภาพเป็นข้อความอย่างรวดเร็ว
url: /th/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ Aspose OCR ใน C# – แปลงรูปภาพเป็นข้อความธรรมดาอย่างรวดเร็ว

เคยสงสัย **วิธีเปิดใช้งาน GPU** เมื่อใช้ Aspose OCR เพื่อแปลงรูปภาพเป็นข้อความที่แก้ไขได้หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอข้อจำกัดด้านประสิทธิภาพเมื่อต้องประมวลผลใบแจ้งหนี้ขนาดใหญ่หรือสัญญาที่สแกนแล้ว ข่าวดีคือ การแปลงรูปภาพเป็นข้อความธรรมดาสามารถทำได้เร็วแสงเมื่อใช้การ์ดกราฟิกของคุณ

ในบทความนี้เราจะพาคุณผ่าน **ตัวอย่าง Aspose OCR** อย่างครบถ้วน ที่แสดงให้เห็นวิธีเปิดใช้งาน GPU ตั้งค่า GPU Device ID และ **อ่านข้อความจากรูปภาพด้วย C#** สไตล์เดียวกัน เมื่อเสร็จคุณจะได้โปรแกรมที่สามารถดึงข้อความจากรูปภาพที่รองรับใด ๆ ได้ในระยะเวลาน้อยกว่าการใช้ CPU เพียงอย่างเดียวอย่างมาก

## สิ่งที่คุณต้องมี

ก่อนที่เราจะเริ่ม ให้แน่ใจว่าคุณมี:

- .NET 6.0 หรือใหม่กว่า (API ทำงานกับ .NET Core และ .NET Framework)
- GPU ที่รองรับ CUDA พร้อมติดตั้งไดรเวอร์ล่าสุด
- ไลเซนส์ Aspose.OCR for .NET (หรือทดลองฟรีซึ่งใช้ได้สำหรับการพัฒนา)
- Visual Studio 2022 (หรือเครื่องมือแก้ไข C# ใด ๆ ที่คุณชอบ)

ไม่ต้องการแพคเกจ NuGet เพิ่มเติมนอกจาก `Aspose.OCR`—แค่ไลบรารีเดียวนี้ก็พอ

---

## Step 1 – Install the Aspose OCR NuGet Package

เริ่มต้นด้วยการเพิ่มไลบรารี Aspose OCR อย่างเป็นทางการเข้าไปในโปรเจกต์ของคุณ เปิด **Package Manager Console** แล้วรัน:

```powershell
Install-Package Aspose.OCR
```

คำสั่งนี้จะดึง `Aspose.OCR.dll` พร้อมกับ dependencies ทั้งหมด หากคุณชอบใช้ GUI ให้คลิกขวาที่โปรเจกต์ → **Manage NuGet Packages** → ค้นหา *Aspose.OCR* แล้วคลิก **Install**  
*Pro tip:* หลังการติดตั้ง ตรวจสอบว่าโฟลเดอร์ `Aspose.OCR` ปรากฏใต้ **Dependencies** ใน **Solution Explorer**

---

## Step 2 – Create a Simple Console App Skeleton

เราจะสร้างแอปคอนโซลขนาดเล็กเพื่อสาธิตขั้นตอนทั้งหมด สร้างโปรเจกต์ใหม่:

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

แทนที่ไฟล์ `Program.cs` ที่สร้างขึ้นโดยอัตโนมัติด้วยโค้ดเต็มที่จะแสดงต่อไปนี้ โครงสร้างนี้ให้จุดเริ่มต้นที่สะอาดและทำให้เรามุ่งเน้นที่ตรรกะ OCR ได้ง่ายขึ้น

---

## Step 3 – How to Enable GPU and Set GPU Device ID

ตอนนี้มาถึงส่วนสำคัญ: **วิธีเปิดใช้งาน GPU** ใน Aspose OCR ไลบรารีมีอ็อบเจ็กต์ `OcrSettings` ที่คุณสามารถสลับ `UseGpu` และเลือกอุปกรณ์ CUDA เฉพาะผ่าน `GpuDeviceId` ตัวอย่างโค้ดที่ต้องใส่ในโปรแกรมของคุณคือ:

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### ทำไมต้องเปิดใช้งาน GPU?

การเปิดใช้งาน GPU จะย้ายงานหนัก—การเตรียมพิกเซล, การแยกอักขระ, และการทำ inference ของเครือข่ายประสาทเทียม—ไปยังการ์ดกราฟิก บน GTX 1650 แบบปานกลาง คุณอาจเห็น **การเพิ่มความเร็ว 2‑3×** เมื่อเทียบกับโหมดใช้ CPU อย่างเดียว โดยเฉพาะกับเอกสารความละเอียดสูง

### การเลือก Device ID

หากเครื่องของคุณมี GPU หลายตัว `GpuDeviceId` จะช่วยให้คุณกำหนดเป้าหมายได้ `0` เลือกอุปกรณ์ตัวแรก; `1` จะเลือกอุปกรณ์ตัวที่สอง เป็นต้น คุณสามารถตรวจสอบ ID ที่มีได้ด้วยเครื่องมือ `nvidia-smi` ของ NVIDIA หรือโดยการ query คลาส `GpuInfo` ของ Aspose (ไม่ได้แสดงในที่นี้เพื่อความกระชับ)

---

## Step 4 – Full Working Example (Copy‑Paste Ready)

ต่อไปนี้เป็นโปรแกรมที่พร้อมรัน เพียงคัดลอกวางลงใน `Program.cs` แทนที่พาธรูปภาพด้วยไฟล์จริงบนดิสก์ของคุณ แล้วกด **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หากรูปภาพที่ให้มีข้อความ *“Invoice #12345 – Total $1,250.00”* คอนโซลจะพิมพ์:

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

ผลลัพธ์เป็นข้อความธรรมดา พร้อมสำหรับการประมวลผลต่อ (เช่น นำเข้าไปยังฐานข้อมูลหรือ parser ภาษาแบบธรรมชาติ)

---

## Step 5 – Verify GPU Utilisation (Optional)

เพื่อยืนยันว่า GPU ถูกใช้จริง ให้เปิดเครื่องมือมอนิเตอร์ GPU (เช่น **NVIDIA‑Smi** หรือ **GPU‑Z**) ขณะโปรแกรมทำงาน คุณควรเห็นการใช้ compute ที่พุ่งขึ้นบนอุปกรณ์ที่เลือก หากเห็นแค่กิจกรรมของ CPU ให้ตรวจสอบว่า:

- ไดรเวอร์ GPU เป็นเวอร์ชันล่าสุด
- ค่าฟล็ัก `UseGpu` ตั้งเป็น `true`
- รูปภาพของคุณอยู่ในฟอร์แมตที่รองรับ (PNG, JPEG, TIFF ฯลฯ)

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **GPU not detected** | ไดรเวอร์เก่าหรือไม่มี CUDA runtime | ติดตั้งไดรเวอร์ NVIDIA ล่าสุดและ CUDA toolkit |
| **`Aspose.OCR` throws “GPU not supported”** | ใช้ GPU ที่ไม่รองรับ CUDA (เช่น AMD รุ่นเก่า) | ตั้ง `UseGpu = false` หรือเปลี่ยนไปใช้ GPU ที่รองรับ |
| **Incorrect image path** | พาธ relative ชี้ไปยังโฟลเดอร์ผิด | ใช้พาธ absolute หรือรับพาธเป็นอาร์กิวเมนต์บรรทัดคำสั่ง |
| **License not applied** | โหมดทดลองอาจจำกัดการใช้ GPU | ลงทะเบียนไลเซนส์ด้วย `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Extending the Example: Batch Processing with GPU

หากต้องประมวลผลใบแจ้งหนี้หลายสิบใบ ให้ห่อการเรียก OCR ไว้ในลูป เนื่องจาก GPU ยังคงอุ่นอยู่ ภาพต่อ ๆ ไปจะได้ประโยชน์จาก **warm‑up caching** ทำให้ลดมิลลิวินาทีต่อไฟล์ได้อีก

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

อย่าลืมใช้ instance ของ `OcrEngine` เดียวกัน—การสร้าง engine ใหม่สำหรับแต่ละไฟล์จะทำให้ GPU context ถูกรีอินิชิอัลไลซ์ใหม่และทำให้ประสิทธิภาพลดลง

---

## Conclusion

ตอนนี้คุณมีตัวอย่าง **Aspose OCR** ครบวงจรที่แสดง **วิธีเปิดใช้งาน GPU**, **วิธีตั้งค่า GPU device ID**, และ **วิธีอ่านข้อความจากรูปภาพด้วย C#** การสลับ `UseGpu` และชี้ไปยังอุปกรณ์ที่ถูกต้อง จะทำให้งาน OCR ที่ช้าแบบใช้ CPU กลายเป็นไพป์ไลน์ความเร็วสูงที่รับมือกับใบแจ้งหนี้, ใบเสร็จ, หรือเอกสารสแกนใด ๆ ได้อย่างมีประสิทธิภาพ

ลองทดลองต่อไป: ใช้ฟอร์แมตรูปภาพต่าง ๆ, ปรับ `GpuDeviceId` บนเครื่องหลาย GPU, หรือผสานกับไลบรารี Aspose อื่น ๆ เพื่อสร้าง PDF เป็นต้น เมื่อ GPU ทำงานแล้วไม่มีขีดจำกัดใด ๆ

---

<img src="gpu-ocr.png" alt="วิธีเปิดใช้งาน GPU กับ Aspose OCR ใน C# – แปลงรูปภาพเป็นข้อความธรรมดาอย่างรวดเร็ว">

*Happy coding! หากเจอปัญหาใด ๆ คอมเมนต์ด้านล่างหรือเยี่ยมชมฟอรั่มอย่างเป็นทางการของ Aspose เพื่อเรียนรู้เพิ่มเติม*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}