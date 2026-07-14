# Lecture Knowledge Base

> Course: **310-3311 Image Processing** (CDTI, CPE)
> Built from the four PDF lecture decks in `Lecture/`.

---

## 1. Knowledge Base Information

- **Date created:** 13 July 2026
- **Location of the source folder:** `/Users/winter/Desktop/Web_App/Lecture/`
- **Number of files analyzed:** 4 files (4 PDFs, 282 slides total). Exactly 4 files were present — no nested folders, no extra supporting files.
- **Purpose of this knowledge base:**
  - Serve as the primary AI reference for this course: assignments, exercises, exam preparation, concept explanations, problem analysis, report writing, and code generation (especially the **LUMA Web App project**, which is the 40 % project component of this subject and the reason this `Web_App` folder exists).
- **Important limitations:**
  - This document is a *reorganized and explained* version of the lectures, **not** a verbatim copy. Where wording matters (definitions, formulas, project requirements), the original phrasing is preserved and the slide number is cited.
  - The lectures are bilingual (English + Thai). Thai text is preserved in parentheses where it carries meaning that the English does not.
  - The decks are slide-based: some slides are images/screenshots only. Two slides rendered as solid black (probably embedded videos) — see §17.
  - A few slides contain apparent errors (e.g. an OpenCV call, a library name). These are recorded **as they appear**, with the concern noted separately, never silently "fixed".
  - Anything not in the lectures but added for clarity is explicitly marked as **[AI-added]**.
- **How this knowledge base should be used:**
  1. Find the relevant topic in §3 (overview), §9 (formulas), §10 (terms), or §13 (decision guide).
  2. Read the deep section for that file (§4–§7).
  3. Follow the problem-solving framework in §11.
  4. If the knowledge base is ambiguous, **re-open the original PDF** — the source file is always the final authority.

---

## 2. Source File Overview

| No. | File Name | File Type | Main Topic | Status |
|---|---|---|---|---|
| 1 | `Lecture 1 - Introduction to Image Processing.pdf` | PDF, 58 slides | What digital image processing is; course structure & grading; how to find an image-processing problem; a real case study (moulting detection in farmed crustaceans); current research (XAI/Grad-CAM); **AI image generation with Stable Diffusion** (diffusion models, U-Net noise predictor, VAE/latent space, conditioning, cross-attention, LoRA); 4 hands-on workshops | Fully analyzed |
| 2 | `Lecture 2 - Control and Fine-tune.pdf` | PDF, 62 slides | **Controlling Stable Diffusion**: CFG, seed, sampling steps, samplers, attention/emphasis syntax, X/Y/Z plot, Prompt S/R, **ControlNet** (OpenPose / Canny / Depth), **Regional Prompter**, and **img2img** (text, sketch, inpaint, inpaint-sketch) | Fully analyzed |
| 3 | `Lecture 3 - Human Visual Perception.pdf` | PDF, 59 slides | Two decks in one file: **(a) Human Visual Perception** (eye anatomy, eye vs camera lens, optical illusions) and **(b) Fundamental Operation** (digital image as an array, Python/OpenCV/NumPy setup and basics, image acquisition: pinhole → lens → aberrations, camera selection, **FOV/angle-of-view calculation**, CCD vs CMOS) | Fully analyzed (2 slides are un-renderable black frames — see §17) |
| 4 | `Lecture 4 - Point Operation.pdf` | PDF, 103 slides | Three decks in one file: **(a) Point Operation / Intensity Transformation** (T[f(x,y)], power-law/gamma, log, piecewise-linear contrast stretching, histogram, dynamic range, auto-contrast, histogram equalization, histogram specification); **(b) Class Project "LUMA"** (features, target users, distributed architecture, team roles); **(c) Web Application & Flask** (stacks, routing, debug mode, HTTP status codes, Jinja templates, project milestones) | Fully analyzed |

**Status legend:** *Fully analyzed* = every slide was opened and read as an image (not just text-extracted), and the embedded text layer was cross-checked with `pdftotext -layout`.

---

## 3. Overall Subject Overview

### 3.1 What the four files are about, together

The course has **two intertwined tracks** that meet in the class project:

1. **Classical image processing** (the "engineering" track)
   *Lecture 3 (part b)* → images are numbers in an array; how light becomes those numbers (optics, sensors).
   *Lecture 4 (part a)* → the first real processing operation: **point operations**, i.e. changing a pixel's value using only that pixel's value.
   *Lecture 1 (slides 1–13)* → why we do it at all: the problem-finding method and the standard pipeline.

2. **Generative / AI image processing** (the "modern tool" track)
   *Lecture 1 (slides 19–58)* → how Stable Diffusion actually works, and workshops to use it.
   *Lecture 2 (all)* → how to **control** it precisely (parameters, ControlNet, regional prompts, img2img).

3. **The bridge — the deliverable**
   *Lecture 4 (parts b & c)* → the **LUMA web application**: an AI image generation/editing web app built with **Flask**, deployed as a **distributed system** over several PCs. This is where both tracks are used at once, and it is worth **40 %** of the grade (Lecture 1, slide 6).

*Human Visual Perception* (Lecture 3, part a) is the philosophical anchor for the whole subject: **our eyes are unreliable measuring instruments** (illusions, simultaneous contrast), which is exactly why we quantify images with numbers, histograms and algorithms instead of trusting a glance.

### 3.2 Main learning objectives

By the end of the four lectures a student should be able to:

- Define digital image processing and distinguish its three output types (image → image / image → descriptor / image → class label). *(L1 s.1–2)*
- Turn a vague real-world need into a scoped image-processing problem and decompose it into sub-processes. *(L1 s.5–7)*
- Explain how a diffusion model generates an image, and name every block in the Stable Diffusion pipeline. *(L1 s.22–43)*
- Steer a generative model deliberately (CFG, seed, steps, sampler, emphasis, LoRA, ControlNet, regional prompts, img2img). *(L2)*
- Explain why human vision cannot be trusted for measurement, and describe eye anatomy in the terms the lecture uses. *(L3 s.2–12)*
- Read/write/modify images as NumPy arrays with OpenCV; set up an isolated Python environment. *(L3 s.14–30)*
- Choose a camera for a project and compute **Angle of View** and **Field of View**. *(L3 s.50–57)*
- Apply and justify a point operation: power-law/gamma, log, contrast stretching, auto-contrast, histogram equalization, histogram specification. *(L4 s.7–50)*
- Build a Flask web app with routing, templates (Jinja), debug mode, and a distributed multi-PC architecture. *(L4 s.51–103)*

### 3.3 How the files are related

```
                    L3(a) Human Visual Perception
                    "eyes lie → we need numbers"
                                 │
                                 ▼
L1 (s.1–13)  ──►  L3(b) Fundamental Operation  ──►  L4(a) Point Operation
Problem finding    image = array; optics; camera        g(x,y) = T[f(x,y)]
& the pipeline     acquisition; FOV; CCD/CMOS           histogram-driven decisions
      │                                                        │
      │                                                        │
      ▼                                                        ▼
L1 (s.19–58)  ──►  L2  Control and Fine-tune  ─────────►  L4(b,c) LUMA + Flask
How Stable          CFG/seed/steps/sampler,               The Web App project
Diffusion works     ControlNet, Regional Prompt,          (40 % of the grade)
                    img2img
```

### 3.4 Recommended study order

| Order | Read | Why |
|---|---|---|
| 1 | **L1, slides 1–13** | Framing: what the subject is, how the project is graded, how to pick a problem. |
| 2 | **L3, slides 2–12** (Human Visual Perception) | Motivates everything: perception ≠ measurement. |
| 3 | **L3, slides 14–30** (Digital image, Python, OpenCV, NumPy) | You cannot run any later example without this. |
| 4 | **L3, slides 31–59** (Acquisition, lens, camera, FOV, sensors) | How the numbers get created; needed for the project's image-acquisition stage. |
| 5 | **L4, slides 1–50** (Point Operation) | The first processing algorithms; the histogram is the diagnostic tool. |
| 6 | **L1, slides 19–58** (Stable Diffusion theory + workshops) | The generative engine of the project. |
| 7 | **L2, all** (Control and Fine-tune) | Making that engine obey you. |
| 8 | **L4, slides 51–103** (LUMA + Flask) | Assemble everything into the graded Web App. |

> ⚠️ **Note on file numbering vs. content order.** The *file names* suggest L1→L2→L3→L4, but the *technical* dependency is different: L3's "Fundamental Operation" and L4's "Point Operation" form a classical-IP chain that does not depend on L1/L2's generative content, while L4's last two decks depend on L1 + L2. Study in the order in the table, cite by file name.

### 3.5 Prerequisite knowledge

Explicitly stated in the lectures:

- **Python** (L3 s.18; L4 s.70 "What you need to know before: HTML5, CSS, Python").
- **HTML5 + CSS** (L4 s.70) and JavaScript/Bootstrap for the frontend role (L4 s.54).
- **Networking** — L4 s.54 (Thai): *"ให้ใช้ความรู้จากรายวิชา Network เพื่อทำให้ PCs เชื่อมโยงกัน แต่ละเครื่องทำหน้าที่แตกต่างกัน"* ("use knowledge from the Network course to link the PCs together, each machine with a different role").
- Basic trigonometry (for FOV: `tan`, `tan⁻¹`) and basic statistics (mean, variance, skewness, kurtosis — L4 s.27).
- **[AI-added]** Basic linear algebra / array indexing helps for the NumPy sections, though the lecture never says so.

---

## 4. File 1: `Lecture 1 - Introduction to Image Processing.pdf`

### 4.1 File Overview

58 slides. It answers three questions: **(1)** What is digital image processing and what is this course? **(2)** What does research in the field look like today? **(3)** How does modern AI image generation (Stable Diffusion) actually work — and how do I use it? It ends with four practical workshops that produce the character assets students reuse.

| Slides | Block |
|---|---|
| 1–13 | Introduction, applications, grading, problem-finding, case study (crustacean moulting detection) |
| 14–18 | Research in Image Processing (two 2026 papers, Grad-CAM) |
| 19–45 | Image Generation with A.I. — diffusion theory → Stable Diffusion pipeline |
| 46–49 | Model types (checkpoint, textual inversion, LoRA, LyCORIS, hypernetwork) + where files go |
| 50–58 | Workshops #1–#4 |

### 4.2 Main Topics

1. **Definition of Digital Image Processing** (s.1, Thai):
   *"การใช้การประมวลผลทางคอมพิวเตอร์ (Computer Algorithm) ในการจัดการรูปภาพ มีจุดประสงค์การทำงานที่หลากหลาย เช่น การปรับปรุงรูปภาพ (Enhancement) การตรวจจับวัตถุ (Detection) การแบ่งแยกบริเวณในภาพ (Segmentation) เป็นต้น"*
   → Using **computer algorithms** to manipulate images, for many different purposes, e.g. **Enhancement**, **Detection**, **Segmentation**.

2. **The three output types of an image-processing system** (s.2) — the most useful classification in the deck:
   - `IMAGE → IMAGE` (e.g. a silhouette/edge image)
   - `IMAGE → DESCRIPTOR` (e.g. "5 OBJECTS", "HEIGHT 1.5 M") — numbers/measurements
   - `IMAGE → RECOGNITION / CLASSIFICATION` (e.g. "A cat that is lying down and looking at the camera")

3. **Applications shown** (s.3–4): style transfer / stylisation of faces, **license plate recognition**, **quality control** (optical recognition on a production line), **image restoration** (repairing a damaged photo), fingertip/gesture tracking.

4. **Class projects & the "hard problem" rule** (s.5) — in red on the slide:
   *"*** ถ้าโจทย์ปัญหายาก ให้ใช้วิธีกำหนดเงื่อนไข, ขอบเขตของงาน, แบ่งเป็นงานย่อย"*
   → **If the problem is hard: impose conditions, bound the scope of the work, and split it into sub-tasks.** Illustrated as `Process A → Process B → Process C` (take image from camera → edge & corner detection → image transformation).

5. **Grading** (s.6):

   | การวัดผลสัมฤทธิ์ในการเรียน (Assessment) | ร้อยละ (%) |
   |---|---|
   | 1. การบ้านและโจทย์ปัญหาในชั้นเรียน (Homework & in-class problems) | 30 |
   | 2. โครงงานด้านการประมวลภาพ **(Web App)** (Image-processing project) | **40** |
   | 3. สอบปลายภาค (Final exam) | 30 |

6. **Project decomposition** (s.6) — the five sub-systems every project must contain:
   1. การเก็บข้อมูลภาพ — **Image Acquisition**
   2. การตรวจสอบคุณภาพและปรับปรุงคุณภาพของภาพ — **Quality Assessment & Enhancement**
   3. การตรวจจับบริเวณของวัตถุที่ต้องการ — **Segmentation**
   4. การสกัดคุณลักษณะสำคัญ — **Feature Extraction** → **Classification** / **Analysis**
   5. การวัดประสิทธิภาพการทำงานของโครงงาน — **Evaluation**

7. **The canonical pipeline** (s.7):
   `Visual Problem Domain → Image Acquisition → Image Enhancement → Feature Extraction → Object Recognition → Image Understanding`

8. **How to find a problem** (s.7, Thai) — *แนวทางการหาโจทย์ปัญหา (อย่างง่าย)*:
   1. งานที่ใช้ตา (มอง) และทำการตัดสินใจ — tasks where a human **looks and then decides**
   2. งานที่มีการทำงานอย่างต่อเนื่อง ⇒ ต้องการระบบอัตโนมัติ — **continuous/repetitive** work ⇒ needs automation
   3. งานที่จำเป็นต้องมีการแก้ไข ปรับปรุงภาพ — work that **needs image correction/enhancement**

   Task verbs listed: การคัดแยกวัตถุ (**classify** objects), การนับชิ้นวัตถุ (**count** objects), การตรวจสอบความสมบูรณ์ (**inspect completeness/defects**), การวัดปริมาณจากสิ่งที่เห็น (**measure quantity** from what is seen), การหาวัตถุที่กำหนดในภาพ (**locate** a specified object).

### 4.3 Important Concepts and Theories

#### A. Diffusion models (s.22–26)

- Stable Diffusion belongs to a class of deep-learning models called **diffusion models**. They are **generative models**: *"designed to generate new data like what they have seen in training"*. For SD, the data are images. (s.22)
- The name comes from physics: *"its math looks very much like diffusion in physics"* (s.22).
- **Forward diffusion** (s.23–24): progressively **adds noise** to a training image until it becomes pure noise. In the distribution figure, the two peaks (cats / dogs) smear into a single broad Gaussian.
- **Reverse diffusion** (s.25): running it backwards — *"like playing a video backward… we will see where the ink drop was initially added"*.
- Every diffusion process has **two parts** (s.26):
  1. **Drift** (แนวโน้มทิศทางเฉพาะ) — a specific directional tendency
  2. **Random motion** (การเคลื่อนแบบสุ่ม)

  The reverse diffusion *"drifts towards either cat OR dog images but nothing in between. That's why the result can either be a cat or a dog."*

#### B. The noise predictor (U-Net) and training (s.27–28)

To reverse the diffusion you must know **how much noise was added**. The solution: train a neural network to **predict the noise added** — the **noise predictor**, which in Stable Diffusion is a **U-Net model**.

Training loop (verbatim, s.27):
1. Pick a training image, like a photo of a cat.
2. Generate a random noise image.
3. Corrupt the training image by adding this noisy image up to a certain number of steps.
4. Teach the noise predictor to tell us how much noise was added. This is done by **tuning its weights and showing it the correct answer**.

#### C. Reverse diffusion at generation time (s.29–30)

1. Generate a **completely random image**.
2. Ask the noise predictor to **tell us the noise**.
3. **Subtract** the estimated noise from the image.
4. Repeat → you get an image of either a cat or a dog.

At this stage there is **no control** over which: *"For now, image generation is **unconditioned**."* (s.30)

#### D. Latent space and the VAE (s.31–34)

- Doing this in pixel space needs **a lot of GPU memory**: *"It is computationally very, very slow. You won't be able to run on any single GPU."* (s.31)
- **Stable Diffusion is a latent diffusion model**: *"Instead of operating in the high-dimensional image space, it first compresses the image into the latent space. The latent space is **48 times smaller**, so it reaps the benefit of crunching a lot fewer numbers."* (s.31)
- Compression uses a **Variational Autoencoder (VAE)** with two parts (s.33):
  - **Encoder** — compresses an image to a lower-dimensional representation in the latent space.
  - **Decoder** — restores the image from the latent space.
- **Reverse diffusion in latent space** (s.34, verbatim):
  1. A **random latent space matrix** is generated.
  2. The **noise predictor estimates the noise** of the latent matrix.
  3. The estimated noise is **subtracted** from the latent matrix.
  4. Steps 2 and 3 are **repeated** up to specific **sampling steps**.
  5. The **decoder of VAE** converts the latent matrix to the final image.

#### E. Conditioning and text conditioning (s.35–39)

- **Conditioning** (s.35): *"The purpose of conditioning is to **steer the noise predictor so that the predicted noise will give us what we want** after subtracting from the image."*
- **Text conditioning (text-to-image)** (s.36–37):
  `Text Prompt → Tokenizer → Embedding → Text transformer → Noise predictor`
  - The **tokenizer** converts each word in the prompt to a number called a **token** (slide example: Photo → 50, of → 24, a → 59, cat → 239).
  - Each token is converted to a **768-value vector** called an **embedding**.
  - The embeddings are processed by the **text transformer** and are then ready to be consumed by the noise predictor.
- **Cross-attention** (s.38–39): *"The output of the text transformer is used **multiple times** by the noise predictor throughout the U-Net. The U-Net consumes it by a **cross-attention mechanism**. That's where the prompt meets the image."* Illustrated with an English↔Hindi attention matrix ("We are friends" ↔ "हम / दोस्त / हैं"), bubble size = attention strength.

#### F. The four steps of text-to-image (s.40–43) — **exam-critical**

| Step | What happens | Detail from slide |
|---|---|---|
| **1** | SD generates a **random tensor in the latent space** | You control this tensor by setting the **seed** of the random number generator. Tensor **4×64×64**. |
| **2** | The **noise predictor U-Net** takes the *latent noisy image* **and** the *text prompt* as input and **predicts the noise**, also in latent space | Predicted noise is a **4×64×64** tensor. |
| **3** | **Subtract** the latent noise from the latent image → **new latent image** | *"Steps 2 and 3 are repeated for a certain number of sampling steps, for example, 20 times."* |
| **4** | The **decoder of the VAE** converts the latent image back to **pixel space** | *"This is the image you get after running Stable Diffusion."* |

#### G. Model types (s.46–47)

- **Checkpoint / base models**: *"Base models are AI image models trained with billions of images of diverse subjects and styles. They cost a lot of money and expertise to create, and only a few of them exist."* Most popular: **Stable Diffusion v1.5**, **Stable Diffusion XL**, **Flux.1 dev**.
- Other model types: **textual inversion** (also called *embedding*), **LoRA**, **LyCORIS**, **hypernetwork**.
- **LoRA** (s.47) — the focus of the course:
  - *"LoRA is a great way to customize AI art models **without filling up local storage**."*
  - *"LoRA applies small changes to the most critical part of Stable Diffusion models: **The cross-attention layers**. It is the part of the model where **the image and the prompt meet**. Researchers found it sufficient to fine-tune this part of the model to achieve good training."*
- **Where the files go** (s.49): checkpoint model → **`[StableDiffusion]`**; LoRA model → **`[Lora]`**. (The model-folder screenshot also lists ControlNet, VAE, Embeddings, Hypernetwork, LyCORIS, ESRGAN, GFPGAN, IpAdapter, T2IAdapter, TextEncoders, Ultralytics, …)

### 4.4 Terminology and Definitions

| Term | Definition (as used in the lecture) | Simple Explanation | Source Section |
|---|---|---|---|
| Digital Image Processing | Using computer algorithms to manipulate images for purposes such as enhancement, detection, segmentation | Making a computer do something useful with a picture | L1 s.1 |
| Enhancement (การปรับปรุงรูปภาพ) | Improving the image | Make it look/measure better | L1 s.1 |
| Detection (การตรวจจับวัตถุ) | Finding objects | "Where is the thing?" | L1 s.1 |
| Segmentation (การแบ่งแยกบริเวณในภาพ) | Splitting the image into regions | "Which pixels belong to the object?" | L1 s.1 |
| Descriptor | A numeric/textual output extracted from an image ("5 objects", "height 1.5 m") | The measurement, not a picture | L1 s.2 |
| Recognition / Classification | Assigning a label/description to the image | "This is a cat lying down" | L1 s.2 |
| Diffusion model | A class of deep-learning **generative** models whose math resembles physical diffusion | Learns to turn noise into a picture | L1 s.22 |
| Forward diffusion | Process that **adds** noise to a training image | Destroy the picture, step by step | L1 s.23–24 |
| Reverse diffusion | Process that **removes** noise, generating an image | Rebuild a picture from noise | L1 s.25, 29 |
| Drift | Directional component of a diffusion process (แนวโน้มทิศทางเฉพาะ) | The "pull" toward cat or dog | L1 s.26 |
| Random motion | Stochastic component (การเคลื่อนแบบสุ่ม) | The random jiggle | L1 s.26 |
| Noise predictor | Neural network trained to predict how much noise was added; in SD it is a **U-Net** | "How much of this is noise?" | L1 s.27 |
| U-Net | The architecture used as the noise predictor | The denoising engine | L1 s.27, 41 |
| Unconditioned | Generation with no prompt steering | You get a random member of the training distribution | L1 s.30 |
| Latent space | Compressed representation, **48× smaller** than image space | A small "sketch space", cheap to compute in | L1 s.31 |
| Latent diffusion model | Diffusion model that runs in latent space (= Stable Diffusion) | Diffusion done in the small space | L1 s.31 |
| VAE (Variational Autoencoder) | Network with an **encoder** (image→latent) and a **decoder** (latent→image) | The zipper / unzipper for images | L1 s.32–33 |
| Sampling steps | Number of repetitions of (predict noise → subtract) | How many denoising passes | L1 s.34, 42 |
| Conditioning | Steering the noise predictor so the predicted noise yields what we want | Telling the model what to draw | L1 s.35 |
| Token | The number a word is converted to by the tokenizer | Word → number | L1 s.36 |
| Embedding | A **768-value vector** representing a token | Number → meaning-vector | L1 s.36 |
| Text transformer | Processes embeddings into what the noise predictor consumes | Prepares the prompt for the U-Net | L1 s.36 |
| Cross-attention | Mechanism by which the U-Net consumes the text output, used **multiple times** throughout the U-Net | "Where the prompt meets the image" | L1 s.38 |
| Seed | Value that sets the random-number-generator state → controls the initial latent tensor | The dice-roll ID; same seed ⇒ same start | L1 s.40 |
| Checkpoint / base model | Full SD model trained on billions of images (SD v1.5, SDXL, Flux.1 dev) | The big brain | L1 s.46 |
| LoRA | Small add-on model that modifies the **cross-attention layers** | A lightweight style/character patch | L1 s.47 |
| Grad-CAM | "Visual Explanations from Deep Networks via Gradient-based Localization" | Heat-map of what the network looked at | L1 s.18 |

### 4.5 Formulas and Calculations

Lecture 1 contains **no closed-form mathematical formulas** — it is conceptual. The quantitative facts to remember:

| Quantity | Value | Condition / Note | Source |
|---|---|---|---|
| Embedding vector length | **768 values** per token | Stable Diffusion text encoder | s.36–37 |
| Latent tensor size | **4 × 64 × 64** | For the SD version discussed | s.40–41 |
| Latent-space compression | **48× smaller** than image space | The reason SD runs on one GPU | s.31 |
| Typical sampling steps | **e.g. 20** | "…repeated for a certain number of sampling steps, for example, 20 times" | s.42 |
| Grade weights | **30 / 40 / 30** | Homework / Web-App project / Final exam | s.6 |
| Research data split (egg/YOLO example) | **70 % train / 30 % test** | From the Explainable-YOLO paper diagram | s.16 |

> **[AI-added] consistency check:** 4×64×64 = 16,384 latent values vs 3×512×512 = 786,432 pixel values → exactly **48×**. So s.31 ("48 times smaller") and s.40–41 ("4×64×64") agree.

### 4.6 Processes and Procedures

**Procedure 1 — Framing an image-processing project (s.5–7)**
1. Find candidate problems with the three finders (eye-and-decide / continuous / needs-enhancement).
2. If hard → **impose conditions, bound the scope, split into sub-tasks** (s.5).
3. Map onto the pipeline: Acquisition → Enhancement → Feature Extraction → Recognition → Understanding.
4. Deliver the 5 sub-systems (acquisition; quality assessment & enhancement; segmentation; feature extraction → classification/analysis; evaluation).

**Procedure 2 — Training the noise predictor (s.27):** see §4.3 B.
**Procedure 3 — Reverse diffusion in latent space (s.34):** see §4.3 D.
**Procedure 4 — Text-to-image, Steps 1–4 (s.40–43):** see §4.3 F.

### 4.7 Code Examples

**Lecture 1 contains no source code.** It is theory + workshops. (All Python code in this course appears in Lecture 3 and Lecture 4.) The only "syntax" introduced is conceptual: prompts, seeds, and LoRA usage — the concrete `<lora:name:weight>` syntax appears in **Lecture 2** (s.17–19).

### 4.8 Examples from the Lecture

**Example A — The crustacean moulting case study (s.8–13).** The flagship worked example. *(Note: the slides never name the species in text — s.8–13 are image-only. The photographs show a moulting crustacean held in a basket grid, and the Thai label is **ลอกคราบ** = "moulting". Any species name is an AI inference — see §17.)*

- **Problem / Goal** (s.8–9): a farm task that is a **24 × 7 Workload** and needs a **skilled worker (need to train)**. Photos show hundreds of floating crates and a worker manually inspecting them.
- **Setup** (s.10): a controlled rig — a darkened enclosure with controlled lighting above the tanks. *This is the "impose conditions" rule of s.5 in action.*
- **Algorithm** (s.11): each specimen produces a chain of derived images (`A8_[0].png … A8_[5].png`): grayscale → enhanced → **binary/segmented mask** → cleaned mask → **contour/outline** → filled silhouette, plus a `.txt` of measurements.
- **Experiment** (s.12): table of *ภาพกล้อง* (camera image) vs *ภาพตรวจจับ* (detected image) against *เวลา (นาที)* (time, minutes) and *พื้นที่ (ร้อยละ)* (**area, percent**):

  | เวลา (นาที) / Time (min) | 1 | 2 | 3 | … | 6 | 7 | 8 | 9 | 10 |
  |---|---|---|---|---|---|---|---|---|---|
  | พื้นที่ (ร้อยละ) / Area (%) | 15.02 | 15.14 | 15.51 | … | 25.57 | 27.34 | 29.60 | 29.28 | 29.09 |

  (Minutes 4–5 are hidden behind an overlapping table on the slide — see §17.)
- **Conclusion** (s.13): line chart, x = *เวลา (นาที)*, y = *ร้อยละของพื้นที่ที่เพิ่มขึ้นเทียบกับเวลาแรก* (**% area increase vs the first time point**), two series: **มีการลอกคราบ** (*moulting*) and **ไม่มีการลอกคราบ** (*not moulting*). Moulting rises steeply from ≈ minute 4–5 and saturates near **95–97 %**; non-moulting oscillates around 0 (≈ −8 … +16 %).
- **Why it matters:** the measured feature (growth of segmented area over time) **separates the two classes** — the whole purpose of feature extraction. A simple threshold on that curve is already a classifier.

**Example B — Research: 3D structural MRI schizophrenia classification, "evaluated with saliency maps" [2026] (s.15).**
Pipeline: **Classification** (7 candidate nets: Seq1, OhNet, Med3D, BrainID, RiekeNet, MixedConv, ResNet) → **Local Explanation** (Plausibility Check = network metrics *Accuracy / ROC* **+ Grad-CAM metrics**: Visual Examination, CoM, MassAccuracy) → choose **Best Network Type** → **Global Explanation** (Saliency Maps Consistency → Region Intersection) → *Biomarker?*
Cohort table: Schizophrenia **101** subjects / Control **91**; age 34.2 ± 11.2 vs 32.3 ± 11.8; gender (m/f) 78/23 vs 61/30.
*Relevance:* shows the **Evaluation** stage done rigorously, and that **explainability is part of the method**.

**Example C — Research: Explainable YOLO for egg size measurement and classification [2026] (s.16–18).**
Pipeline: Egg Dataset → **Pre-processing** (Data Cleaning, Labeling) → **Exploratory Data Analysis** → **Data Augmentation** → **Random split (Training 70 % / Testing 30 %)** → **YOLO Model Training** ⇄ **Parameters Optimization** → **Performance Evaluation**; **XAI / GradCAM** explains the **Egg Size?** decision (**Small / Medium / Large / XLarge**).
Physical rig (s.17): **conveyor belt** → **illumination cabinet** with an **industrial camera** → data-processing system.
*Relevance:* the closest template to a real student project — controlled lighting box + camera + model + evaluation + explanation.

**Example D — Workshops (s.50–58).** Sequential; each builds on the previous:

| Workshop | Requirements (verbatim) |
|---|---|
| **#1 Character creation** (s.50) | 1. Create specific character with **clear background**. 2. Can be **well-known character** or **specific body characteristic and specific cloth**. 3. Character must be in **Full-Body view**. 4. Character must be in **standing pose**. 5. **Create 3 images** in this condition. |
| **#2 Make a random or specific pose** (s.52) | 1. Character must be the **same character from previous workshop**. 2. **Edit the prompt and parameter** to make a various pose. 3. Create **3 images** (3 difference poses). |
| **#3 Control a camera view** (s.54) | 1. Same character. 2. Use **either prompt editing or LoRA** to control camera view. 3. Create **3 difference camera views** (**difference perspective vanishing point**). |
| **#4 Put everything together** (s.56) | 1. Same character. 2. Give a **background prompt** to your image. 3. You can make your character do some **facial expression**. 4. Create **a perfect 1 image** with your idea. |

Example outputs (s.51, 53, 55, 57–58) show the **same** anime schoolgirl character: standing full-body on white → dynamic/kneeling poses → low-angle & bird's-eye views → full scenes (rooftop city sunrise; sunset roadside crouch). **Pedagogical point: character consistency + increasing control.**

### 4.9 Important Tables, Figures, and Diagrams

| Slide | Visual | What it shows | Why it matters |
|---|---|---|---|
| s.2 | Output-type diagram | IMAGE→IMAGE, IMAGE→DESCRIPTOR, IMAGE→RECOGNITION | Tells you what *kind* of system you must build |
| s.6 | Grading table + 5 sub-systems | 30/40/30 | The Web App is the largest component |
| s.7 | Pipeline strip | Visual Problem Domain → … → Image Understanding | The mental template for any project |
| s.12–13 | Experiment table + conclusion chart | Segmented area (%) vs time, moulting vs not | A feature that *separates classes* is the goal |
| s.15 | XAI/Grad-CAM decision-process diagram | Classification → Local → Global explanation → Biomarker? | Modern evaluation methodology |
| s.16–17 | YOLO pipeline + conveyor rig | 70/30 split, augmentation, illumination cabinet | Template for a deployable project |
| s.23, 25 | SDE / Probability-Flow-ODE figure | Cat & dog peaks diffusing into one Gaussian, and back | Intuition for drift + random motion |
| s.28 | "Step 1–4 / Noise 1–4" strip | Progressive corruption of a cat photo | What the noise predictor is trained on |
| s.30 | Denoising strip with "−" circles | image − predicted noise, repeated | The generation loop in one picture |
| s.32 | Encoder → Latent-space cube → Decoder | The VAE | Where the 48× saving comes from |
| s.37 | Text Prompt → Tokenizer → Embedding → Text transformer → Noise predictor | With "768-value vector for each token" | Exam-favourite diagram |
| s.39 | Cross-attention bubble matrix | Bubble size = attention weight | What "attention" concretely means |
| s.41–43 | Latent cube → U-Net → predicted noise; subtraction; VAE decode | The 4-step text-to-image | The most examinable diagram in the deck |
| s.49 | Model-folder screenshot | `[StableDiffusion]` vs `[Lora]` | Needed to actually run the workshops |

### 4.10 Common Mistakes and Important Warnings

- **Confusing forward and reverse diffusion.** Forward = *adds* noise (training-time corruption); reverse = *removes* noise (generation). The model is **only ever trained to predict noise** — it never "draws" directly (s.23–29).
- **Thinking the U-Net outputs an image.** It outputs the **predicted noise** (4×64×64 latent tensor), which is then **subtracted** (s.41–42).
- **Forgetting the VAE decode.** Without Step 4 you have a latent matrix, not a picture (s.43).
- **Assuming the prompt is "read" as text.** It is tokenized → embedded (768-d) → transformed → injected via **cross-attention**. No prompt ⇒ **unconditioned** ⇒ uncontrolled output (s.30, 36–38).
- **Thinking LoRA retrains the whole model.** It only patches the **cross-attention layers** (s.47) — which is also why LoRA files are small.
- **Putting model files in the wrong folder.** Checkpoints → `[StableDiffusion]`, LoRAs → `[Lora]` (s.49). Wrong folder ⇒ the model silently never appears in the UI.
- **Attacking a huge problem head-on.** The explicit rule (s.5): impose conditions, bound scope, decompose. The moulting study only worked because a **controlled lighting enclosure** was built first (s.10).
- **Skipping Evaluation.** It is sub-system #5 (s.6), and both research examples spend most of their effort there (s.15–16).

### 4.11 Easy-to-Understand Summary

Image processing = making a computer do something useful with a picture, and the "something useful" is always one of three things: **a better picture**, **a number**, or **a label**. To build such a system you follow a pipeline (acquire → enhance → extract features → recognise → understand); if the problem looks too big, you **shrink it**: fix the lighting, fix the camera, fix the rules, cut it into small processes. The moulting case study shows the payoff — once the scene is controlled, one simple measurement (how fast the animal's silhouette grows) cleanly separates moulting from non-moulting.

The second half explains **Stable Diffusion**. Imagine dripping noise onto a photo until it is TV static — that's *forward diffusion*. Now train a network (a **U-Net**) whose only job is to look at a noisy picture and say "this much of it is noise". If it can do that, you can start from pure static and repeatedly subtract the predicted noise until a real image appears — *reverse diffusion*. Doing this on full-size pixels is far too slow, so SD first squeezes the image into a **latent space 48× smaller** using a **VAE**, denoises there, and only at the end **decodes** back to pixels. To make the output obey your words, the prompt becomes **tokens → 768-value embeddings → transformer output**, fed into the U-Net at many points via **cross-attention** — literally "where the prompt meets the image", and exactly the part **LoRA** patches when you want a custom character or style.

### 4.12 Source References

- Definition & purposes: **s.1** · Output types: **s.2** · Applications: **s.3–4**
- Hard-problem rule + Process A/B/C: **s.5** · Grading + 5 project sub-systems: **s.6**
- Pipeline + problem-finding guidelines: **s.7**
- Crustacean moulting case study (Problem/Goal → Algorithm → Experiment → Conclusion): **s.8–13**
- Research section (MRI/XAI; Explainable YOLO; Grad-CAM): **s.14–18**
- Why AI generation matters: **s.19–20** · SD prompt→image (teddy bears): **s.21**
- Diffusion model / forward / reverse / drift & random motion: **s.22–26**
- Training the noise predictor: **s.27–28** · Reverse diffusion, unconditioned: **s.29–30**
- GPU cost → latent diffusion → VAE: **s.31–33** · Reverse diffusion in latent space: **s.34**
- Conditioning / text conditioning / cross-attention: **s.35–39**
- Text-to-image Steps 1–4: **s.40–43**
- Checkpoint/base models; LoRA & other model types; model folders: **s.46–49**
- Workshops #1–#4 + example outputs: **s.50–58**

---

## 5. File 2: `Lecture 2 - Control and Fine-tune.pdf`

### 5.1 File Overview

62 slides, subtitled **"Control and Fine-tune (Image Generation)"**. Where Lecture 1 explained *how Stable Diffusion works*, Lecture 2 is entirely about **making it do what you want**. It assumes you are using the **AUTOMATIC1111** web-UI (and, for regional prompting, a Forge-style *Regional Prompter* / *Forge Couple* extension).

| Slides | Block |
|---|---|
| 1–10 | The five tuning levers: checkpoint, prompt, extra models, parameters, manual retouch → **CFG, Seed, Steps, Sampler** |
| 11–12 | **Attention / emphasis** syntax |
| 13–20 | **X/Y/Z Plot**, **Prompt S/R**, LoRA sliders + Workshop |
| 21–43 | **ControlNet** (preprocessors: OpenPose family, Canny, Depth; settings; multi-unit) |
| 44–55 | **Regional Prompt** (Forge Couple / Regional Prompter) |
| 56–62 | **img2img**: with Text, with Sketch, with Inpaint, with Inpaint-Sketch |

### 5.2 Main Topics

**The five ways to tune Stable Diffusion** (s.2, verbatim):
*"When we use stable diffusion from **Automatic1111**, we usually can set certain parameters which define how result turns out in the end."*

- `# Change checkpoint model`
- `# Prompt editing`
- `# Extra model` (LoRA, embeddings, ControlNet …)
- `# Parameter tuning` (CFG, seed, steps, sampler)
- `# Manual re-touch` (img2img / inpaint / sketch)

Everything else in the deck is a deep dive into one of these five.

### 5.3 Important Concepts and Theories

#### A. CFG — Classifier Free Guidance (s.3–4)

- Framed as **"Prompt vs Creativity"**.
- Mechanically it is a comparison of two predictions (s.3):
  **noise prediction _including_ the prompt** **VS** **noise prediction _without_ the prompt**.
- The scale controls how far the result is pushed from the unconditional toward the conditional prediction:
  - **CFG : 0** → *"not follow the prompt"*
  - **CFG : 20** → *"strict to the prompt"*
  - Slide arrow: `not follow the prompt ➔ strict to the prompt`
- **Recommended working range: 8–14** (s.10, *"Drive towards prompt, use 8-14"*).
- Demonstration grid (s.4): prompt = fried rice, rows = **Seed 36 / 360 / 3600**, columns = **CFG Scale 1.0 / 3.0 / 5.0 / 7.0 / 9.0**. At CFG 1.0 the images are *not* fried rice at all (a person lying in snow, a portrait, an unrelated dish); by CFG 5.0–9.0 every cell is clearly the requested fried rice, and gets progressively more saturated/contrasty.
  → **This is the single most instructive figure in the deck**: low CFG = the model ignores you; high CFG = obedient but increasingly over-cooked.

#### B. Seed (s.5–6)

- *"seed parameter makes up the **random number generator state**"* (s.5–6).
- Same prompt (`1girl, kimono, sakura tree,`), three seeds (**360 / 777 / 55**) → three different women/compositions. The prompt fixes the *content*; the seed fixes the *particular sample*.
- **Seed = −1 means random** (s.6). Set a fixed seed when you want reproducibility or when you want to change one variable at a time.
- Links back to L1 s.40: the seed determines the **initial random latent tensor**.

#### C. Sampling steps (s.7)

- **"Stable Diffusion Step" = number of loops for denoising.**
- `more step = more compute = longer time`
- *"usually around **20 – 60 steps** is enough"*.
- The strips on s.7 (cat, singer, schoolgirl at Steps 5/10/15/20/25/30) show the image is already coherent at ~15–20 and changes only marginally afterwards.
- Cheat-sheet line (s.10): *"More steps ~ higher image quality, but 💰"* (i.e. cost).

#### D. Sampler / sampling method (s.8–9)

- **Definition (s.8):** *"A rule that control how we denoising the image in each iteration."*
- The UI field is **Sampling method** (screenshot shows `DPM++ SDE Karras`).
- Comparison (s.9): **Euler a**, **Heun**, **DPM++ SDE Karras** — same prompt/seed, visibly different faces, armour details and lighting.
- Cheat-sheet line (s.10): *"Noise schedule, **DDIM for low step counts**"*.

#### E. The five-lever cheat sheet (s.10) — memorise this

| # | Lever | Guidance (verbatim) |
|---|---|---|
| 1 | **Prompt** | Prompt generators + **Lexica.art** |
| 2 | **Seed** | Generate different images |
| 3 | **CFG** | Drive towards prompt, **use 8–14** |
| 4 | **Sampler** | Noise schedule, **DDIM for low step counts** |
| 5 | **Steps** | More steps ~ higher image quality, but 💰 |

#### F. Attention / emphasis (s.11–12) — **exam-critical, arithmetic required**

Cheat sheet (verbatim, s.12):

| Syntax | Effect |
|---|---|
| `a (word)` | **increase** attention to *word* by a factor of **1.1** |
| `a ((word))` | **increase** attention by a factor of **1.21** ( = 1.1 × 1.1 ) |
| `a [word]` | **decrease** attention to *word* by a factor of **1.1** |
| `a (word:1.5)` | **increase** attention by a factor of **1.5** |
| `a (word:0.25)` | **decrease** attention by a factor of **4** ( = 1 / 0.25 ) |

Rules to extract from it:
- Round brackets **multiply** the weight by 1.1 **per level of nesting** → `(((word)))` = 1.1³ = 1.331.
- Square brackets **divide** by 1.1 per level.
- Explicit `(word:N)` **replaces** the weight with **N** (N > 1 emphasises, N < 1 de-emphasises).
- *"Decrease by a factor of 4"* means the weight is 0.25, i.e. **1/0.25 = 4** is the reduction factor.

#### G. X/Y/Z Plot (s.13–17) — the experimentation tool

- **Purpose (s.15):** *"Select which parameters should be shared by rows, columns and batch by using **X type**, **Y type** and **Z Type** fields, and input those parameters separated by comma into X/Y/Z values fields. For integer, and floating-point numbers, and ranges are supported."*
- **Range syntax (verbatim, s.15):**

  | Form | Example | Expands to |
  |---|---|---|
  | Simple range | `1-5` | 1, 2, 3, 4, 5 |
  | Range with **increment in (brackets)** | `1-5 (+2)` | 1, 3, 5 |
  | | `10-5 (-3)` | 10, 7 |
  | | `1-3 (+0.5)` | 1, 1.5, 2, 2.5, 3 |
  | Range with **count in [square brackets]** | `1-10 [5]` | 1, 3, 5, 7, 10 |
  | | `0.0-1.0 [6]` | 0.0, 0.2, 0.4, 0.6, 0.8, 1.0 |

- Example grid (s.14): X = **CFG Scale 8.0 / 10.0 / 12.0**, Y = background **space / a castle**, Z = colour theme **multicolored / turquoise and gold** → a 2 × 3 × 2 comparison sheet.
- The UI (s.17) also offers: *Draw legend*, *Include Sub Images/Sub Grids*, *Keep -1 for seeds*, *Vary seeds for X/Y/Z*, *Grid margins*, and **Swap X/Y, Y/Z, X/Z axes**.

#### H. Prompt S/R (s.16)

- **Definition (verbatim):** *"S/R stands for **search/replace**… you input a list of words or phrases, it takes **the first from the list and treats it as keyword** and **replaces all instances of that keyword** with other entries from the list."*
- Worked example: prompt = `a man holding an apple, 8k clean,` and Prompt S/R = `an apple, a watermelon, a gun` → three prompts:
  1. `a man holding an apple, 8k clean`
  2. `a man holding a watermelon, 8k clean`
  3. `a man holding a gun, 8k clean`
- **Critical gotcha:** the first entry of the S/R list **must literally exist in the prompt**, otherwise nothing is replaced.

#### I. LoRA weight as an axis (s.17–19)

- LoRA is invoked in the prompt with the syntax `<lora:NAME:WEIGHT>` — slide example:
  `<lora:Long legs slider2_alpha16.0_rank32_full_last:-1.5>`
- Using **Prompt S/R on the weight** with Z values `-1.5, 0.0, 1.5` produces a **slider sweep**: at −1.5 the character has short legs, 0.0 is neutral, +1.5 gives long legs (s.18–19).
- **Key insight:** LoRA weights can be **negative** — a "slider" LoRA works in both directions.

#### J. Workshop (s.20, Thai)

> *ปรับอัตราส่วนของ Prompt ด้วย **Emphasis** และ/หรือ **LoRA** แสดงผลลัพธ์โดยการใช้ **X/Y/Z Plot***
> *เปลี่ยน **Seed** ในแกน **X** ของ X/Y/Z Plot และเปลี่ยน **Prompt 1 ตัว** ในแกน **Y** ด้วย **S/R Prompt***

→ Adjust prompt proportions using **Emphasis** and/or **LoRA**; present the result with an **X/Y/Z Plot**. Put **Seed on the X axis** and change **one prompt term on the Y axis** using **S/R Prompt**.

#### K. ControlNet (s.21–43)

**Motivation (s.22, Thai):**
> *รูปภาพ 1 รูป แทนคำได้หลายคำ / ดังนั้นในทางกลับกัน / เราไม่อาจอธิบายรายละเอียดของภาพได้ด้วยเพียงคำบรรยาย*
> "One image stands for many words; therefore, conversely, **we cannot describe the details of an image with a verbal description alone**."

That is the entire justification for ControlNet: **text is not enough** — you need an image-shaped control signal.

**Definition (s.23, verbatim):**
- *"ControlNet is a Stable Diffusion model that lets you **copy compositions or human poses from a reference image**."*
- *"ControlNet is a **neural network model for controlling Stable Diffusion models**. You can use ControlNet along with **any** Stable Diffusion models."*
- *"ControlNet **adds one more conditioning** in addition to the text prompt. The extra conditioning can take many forms."*

**How it plugs in (s.24–25):**
```
Input image ── annotation (e.g. canny edge detector / openpose keypoint detection) ──► [preprocessed map] ─┐
                                                                                                            ├─► Stable Diffusion + ControlNet ─► Output
Input prompt ("full-body, a young female, highlights in hair, dancing outside a restaurant, brown eyes, wearing jeans") ─┘
```

**Using ControlNet (s.26):**
1. **Download / Install** ControlNet
2. **Upload an image** to the image canvas
3. Check the **Enable** checkbox
4. **Select a preprocessor and a model**

**Preprocessors (s.28, verbatim):** *"The first step of using ControlNet is to choose a preprocessor. It is helpful to turn on the preview so that you know what the preprocessor is doing. **Once the preprocessing is done, the original image is discarded, and only the preprocessed image will be used for ControlNet.**"*
- Select **Allow Preview**.
- Optionally select **Pixel Perfect** — *"ControlNet will use the image height and width you specified in text-to-image to generate the preprocessed image."*
- Click the **explosion icon** next to the Preprocessor dropdown to run it.

**The preprocessor family (s.29–38):**

| Preprocessor | What it detects (verbatim) | Use it when |
|---|---|---|
| **OpenPose** (s.31) | *"eyes, nose, eyes, neck, shoulder, elbow, wrist, knees, and ankles"* (see §17 — "eyes" is listed twice) | You want to copy a **body pose** |
| **OpenPose_face** (s.32) | *"does everything the OpenPose processor does but detects additional facial details."* → *"useful for copying the **facial expression**"* | Pose **+** expression |
| **OpenPose_faceonly** (s.33) | *"detects only the face but not other keypoints… useful for copying the face only"* | Only the face matters |
| **OpenPose_hand** (s.34) | *"detects the keypoint as OpenPose and the **hands and fingers**"* | Hand gestures matter |
| **OpenPose_full** (s.35) | *"detects everything openPose face and openPose hand do"* | You want it all |
| **Canny (Edge detector)** (s.36) | *"a general-purpose, old-school edge detector. It **extracts the outlines** of an image. It is useful for **retaining the composition** of the original image."* | Keep the exact layout/outline |
| **Depth** (s.37–38) | *"The depth preprocessor **guesses the depth information** from the reference image."* | Keep 3-D structure / spatial arrangement |

The UI **Control Type** radio row (s.29) lists: `All, Canny, Depth, Normal, OpenPose, MLSD, Lineart, SoftEdge, Scribble, Seg, Shuffle, Tile, Inpaint, IP2P, Reference, T2IA`.

**Multi-ControlNet (s.39):** *"More than one ControlNet"* — the UI has **ControlNet Unit 0 / Unit 1 / Unit 2** tabs (s.26). The example stacks **OpenPose (from a photo of a seated man)** + **Depth (from a mountain-lake photo)** → an anime girl sitting in that exact pose in that exact landscape.

**ControlNet settings (s.41):**

| Setting | Slide value | Meaning |
|---|---|---|
| **Preprocessor / Model** | `openpose` / `kohya_controlllite_xl_openpose_anir…` | Thai note: *เลือก Preprocessor และ Model **ให้สอดคล้องกัน*** — **the preprocessor and the model must match** |
| **Control Weight** | 1.5 | Thai note: *ปรับ Weight สำหรับ Control* — how strongly the control map is enforced |
| **Starting Control Step** | 0 | When control begins (fraction of the sampling schedule) |
| **Ending Control Step** | 1 | When control ends |
| **Resolution** | 512 | Preprocessor output resolution |
| **Control Mode** | Balanced / My prompt is more important / ControlNet is more important | Who wins in a conflict |
| **Resize Mode** | Just Resize / Crop and Resize / Resize and Fill | How the reference is fitted |

**Workflow (s.42–43, Thai):** *นำภาพต้นแบบมาใส่* (insert the reference image) → *Preview ผลลัพธ์* (preview the preprocessor output; JSON pose can be edited) → *ทดสอบผลลัพธ์ที่ได้* (test the result), with the warning:
> *(*** ประสิทธิภาพ ขึ้นอยู่กับ **Checkpoint + ControlNet model**)* — **performance depends on the combination of Checkpoint + ControlNet model.**

#### L. Regional Prompt / Forge Couple (s.44–55)

**Motivation (s.44–45):**
- *"Let's say you want to generate a man and a woman in the same image. Using the simple prompt: **a man and a woman**"* → you get *some* man and *some* woman, uncontrolled.
- *"But what if you want to be more specific? Like generating **a man with black hair and a woman with blonde hair**? Naturally, you write that in the prompt: `a man with black hair, a woman with blonde hair`"* → the results (s.45) show **attribute bleeding**: both people end up blonde, or the hair colours swap, or the man gets the woman's hair.
- **This is the classic failure mode that regional prompting fixes: attributes leak across subjects because the whole prompt attends to the whole image.**

**Setup (s.46, verbatim):**
1. Unfold the **Regional Prompter** section on the **txt2img** page.
2. Check **Active** to activate the regional prompter.
3. Set parameters:
   - **Divide mode: Horizontal**
   - **Generation mode: Attention**
   - **Divide Ratio: 1, 1**
4. Click **visualize and make template**.
5. Put prompt:
   ```
   a man and a woman, a man with black hair
   BREAK
   a man and a woman, a woman with blonde hair
   ```
   (Note how the *shared* context "a man and a woman" is repeated in **both** regions.)

**Tips — `Use common prompt` (s.48):** if you tick **Use common prompt**, the **first** block becomes a **common prompt** applied to *all* regions, so you write it only once:
```
a man and a woman        ← common (applies everywhere)
BREAK
a man with black hair    ← region 0
BREAK
a woman with blonde hair ← region 1
```
Other UI fields: **Generation mode: Attention | Latent**, **Base Ratio: 0.2**, checkboxes *Use base prompt* / *Use common prompt* / *Use common negative prompt*, tabs **Matrix / Mask / Prompt**, **Split mode: Horizontal | Vertical | Random**, **Divide Ratio**, and a **template** box that fills with `ADDCOMM` / `ADDCOL`.

**Divide-Ratio semantics (s.49) — the rule you must not get backwards:**
> *"The **first number in each row** represents the **height of the row**. The **subsequent numbers** represent the **width of the regions**."*

| Notation | Layout produced |
|---|---|
| `Horizon (1,1,1)` | one row split into **3 equal columns** (regions 0,1,2) |
| `Horizon (1,2,1)` | one row, 3 columns with the **middle twice as wide** |
| `Vertical (1,1,1)` | **3 equal rows** stacked |
| `Vertical (1,2,1)` | 3 rows, middle row twice as tall |
| `Horizon (1,1,1; 2,1,1)` | **2 rows**: row 1 has height 1 and 2 columns (regions 0,1); row 2 has height **2** and 2 columns (regions 2,3) → 4 regions |
| `Horizon (1,1,1,1; 2,1,2)` | 2 rows: row 1 (height 1) split into **3** columns (0,1,2); row 2 (height 2) split into 2 columns of width 1 and 2 (3,4) → 5 regions |

**Worked example (s.50–51):** layout `Horizon (1,1,1; 2,1,1)` → 4 regions, with **Use common prompt** on:
```
a witch, highly detailed face, half body, studio lighting, dramatic lighting,
highly detailed clothing, looking at you, mysterious, dramatic lighting   ← common
BREAK
(full moon:1.3)          ← region 0 (top-left)
BREAK
                         ← region 1 (top-right) — intentionally empty
BREAK
                         ← region 2 (bottom-left) — intentionally empty
BREAK
(beautiful fire magic: 1.2)   ← region 3 (bottom-right)
```
Result (s.51): a witch, with the **moon in the upper-left** and **fire on the lower-right**, exactly where they were placed. Note the **empty BREAK blocks** — they are how you say "nothing extra here".

**Practical settings for a full picture (s.54, Thai):** *เลือก **[Use common prompt]** → ภาพรวม* (pick Use common prompt for the overall scene) · *ปรับขนาดภาพให้ถูกต้อง* (set the correct image size — slide shows 1024×1024) · *เลือก **Overlay Ratio** ตามที่ต้องการ* (slide value **0.1**) · *Visualize and make template*.
**Writing the prompt (s.55, Thai):** *เขียน Prompt ตาม Template* (follow the template) · *แบ่งวรรคด้วย `<Keyword>`* (separate blocks with the keyword) · *สามารถใช้ **BREAK** แทนได้* (you may use `BREAK` instead).
Example (s.55): `2girls, white background, BREAK 1girl, blonde hair, medium hair, hair, black shirt, denim shorts, BREAK 1girl, black hair, long hair, white tank top, pink dolphin shorts,` → the two girls reliably keep their own hair colour and clothing.

#### M. img2img — "Edit your image with A.I." (s.56–61)

The `img2img` tab (s.57) sits next to `txt2img`, with sub-tabs **img2img / Sketch / Inpaint / Inpaint sketch / Inpaint upload / Batch**.

| Mode | What it does (verbatim) | Key control |
|---|---|---|
| **[1] Img2Img with Text** (s.58) | Feed an existing image + a new prompt (`1girl, yellow eyes, blonde hair, long hair, black tank top,`) → the model re-renders it | **Denoising strength = 0.95** on the slide; *Resize by* Scale = 1 (816×1024 → 816×1024). Low denoise ⇒ stays close to the original; high denoise ⇒ freer re-interpretation |
| **[2] Img2Img with Sketch** (s.59) | *"It helps the AI focus on your masked area."* Steps: **[1] Select specific brush color · [2] Masking it… · [3] Prompts & Generate** | Brush colour + prompt (example adds round glasses) |
| **[3] Img2Img with Inpaint** (s.60) | *"This tool lets you **add, remove, or enhance any part** of the uploaded image."* Example prompt: `blue frilled dress,` — the masked white top becomes a blue frilled dress | The mask |
| **[4] Img2Img with Inpaint-Sketch** (s.61) | *"it is a **combination of the tools Sketch and Inpaint**. You can mask any area of the uploaded image **with a specific color**, bringing your drawing to life on the image."* ⚠ *"However, to use it, you should have **proper painting knowledge**."* | Mask **+** colour (red glasses + pink dress drawn crudely → rendered properly) |

Closing slide (s.62): **"Learning by doing…"**

### 5.4 Terminology and Definitions

| Term | Definition | Simple Explanation | Source |
|---|---|---|---|
| AUTOMATIC1111 | The Stable Diffusion web-UI used in this course | The app you actually click in | s.2 |
| CFG (Classifier Free Guidance) | Comparison of noise prediction **including** the prompt vs **without** the prompt; scale controls prompt adherence | "How obedient should the model be?" 0 = ignores, 20 = strict | s.3 |
| Seed | The random-number-generator state | Which particular random start you get; **−1 = random** | s.5–6 |
| Sampling steps | Number of loops for denoising | How many clean-up passes; 20–60 usually enough | s.7 |
| Sampler / Sampling method | *"A rule that control how we denoising the image in each iteration"* | The recipe for each denoise step (Euler a, Heun, DPM++ SDE Karras, DDIM) | s.8–9 |
| Attention / emphasis | Prompt syntax that multiplies a term's weight | `(word)` = ×1.1, `[word]` = ÷1.1, `(word:1.5)` = ×1.5 | s.12 |
| X/Y/Z Plot | Script that sweeps parameters across rows/columns/batch | An automatic comparison grid | s.13–17 |
| Prompt S/R | **Search/Replace**: first list entry is the keyword, replaced by the others | Swap one word across a sweep | s.16 |
| LoRA weight | The number in `<lora:name:weight>`; **can be negative** | Slider strength for the LoRA | s.17–19 |
| ControlNet | *"a neural network model for controlling Stable Diffusion models"*; adds **one more conditioning** besides text | Copy a pose/outline/depth from a reference image | s.23 |
| Preprocessor / annotation | Converts the reference image into a control map (pose skeleton, edges, depth). **Original image is then discarded** | The "translator" from photo → control map | s.24–28 |
| Pixel Perfect | ControlNet uses the txt2img height/width to build the preprocessed image | Avoids resolution mismatch artefacts | s.28 |
| Control Weight | How strongly ControlNet is enforced | Slide example: 1.5 | s.41 |
| Control Mode | Balanced / My prompt is more important / ControlNet is more important | Tie-breaker between prompt and control map | s.41 |
| OpenPose | Keypoint preprocessor (nose, neck, shoulder, elbow, wrist, knees, ankles…) | Stick-figure pose copier | s.31 |
| Canny | *"general-purpose, old-school edge detector… extracts the outlines… useful for retaining the composition"* | Outline copier | s.36 |
| Depth | *"guesses the depth information from the reference image"* | 3-D layout copier | s.37 |
| Regional Prompter / Forge Couple | Extension that assigns different prompt blocks to different **regions** of the canvas | "This half of the picture gets this prompt" | s.44–55 |
| BREAK | Separator between regional prompt blocks | The region delimiter | s.46, 48, 55 |
| Use common prompt | First block becomes a shared prompt for **all** regions | Write the shared scene once | s.48 |
| Divide Ratio | Region layout: **first number = row height**, following numbers = **region widths** | The grid recipe | s.49 |
| Denoising strength | How much img2img is allowed to change the input | 0 = unchanged, 1 = ignore the input | s.58 |
| Inpaint | Add/remove/enhance a **masked** part of an image | Local edit | s.60 |
| Inpaint-Sketch | Inpaint **+** colour drawing in the mask | Draw crudely, let AI render it | s.61 |

### 5.5 Formulas and Calculations

Lecture 2 has **no physics/maths formulas**, but it has **arithmetic rules that are exam-testable**:

**Rule 1 — Emphasis weight (s.12)**

| Expression | Resulting weight |
|---|---|
| `(word)` | 1.1 |
| `((word))` | 1.1 × 1.1 = **1.21** |
| `(((word)))` | 1.1³ = **1.331** *(extrapolated from the stated rule)* |
| `[word]` | ÷1.1 (≈ 0.909) |
| `(word:N)` | **N** |
| `(word:0.25)` | 0.25 → "decrease by a factor of **4**" because 1 / 0.25 = 4 |

- **Conditions for use:** applies to the prompt text in AUTOMATIC1111; nesting multiplies; explicit `:N` overrides.
- **Common mistakes:** thinking `[word]` deletes the word (it only weakens it); thinking `(word:0.25)` means "25 % more"; forgetting that the emphasis multiplier compounds with nesting.

**Rule 2 — X/Y/Z range expansion (s.15)**
- `A-B` → every integer from A to B.
- `A-B (+s)` → from A stepping by **+s**; `A-B (-s)` → stepping **down**.
- `A-B [n]` → exactly **n** values evenly spread from A to B (inclusive).
- **Worked check:** `0.0-1.0 [6]` → 6 values → step = (1.0 − 0.0)/(6 − 1) = 0.2 → **0.0, 0.2, 0.4, 0.6, 0.8, 1.0** ✓ (matches the slide).
- **Worked check:** `1-10 [5]` → step = (10 − 1)/(5 − 1) = 2.25 → the slide gives **1, 3, 5, 7, 10** (rounded to integers, last snapped to the endpoint). *This rounding behaviour is what the slide shows; do not "correct" it.*

**Rule 3 — Region count from a Divide Ratio (s.49)**
Number of regions = **sum of the number of width entries in each row**.
- `(1,1,1)` → 1 row × 2 widths? **No** — read it as: row-height 1, then widths 1 and 1 → but the slide's picture for `Horizon (1,1,1)` shows **3 columns**. So for a **single-row** ratio the leading number is the height and **all remaining numbers are widths**: `(1, 1,1)` → hmm, that yields 2 columns, yet the figure shows 3.
  ⚠ **Needs further verification** — see §17, item 4. The safe, figure-consistent reading of the *single-row* examples is: `Horizon (1,1,1)` = **3 equal columns**, `Horizon (1,2,1)` = **3 columns with the middle double-width**; the "first number = row height" rule is demonstrated unambiguously only in the **multi-row** forms (`1,1,1; 2,1,1` → row heights **1** and **2**, each with 2 columns → 4 regions), which match their figures exactly.

### 5.6 Processes and Procedures

**Procedure A — Tune a generation (s.2–10)**
1. Pick/replace the **checkpoint** (biggest single effect on style).
2. Write the **prompt**; refine with **emphasis** syntax; add **LoRA** if a specific concept/style is needed.
3. Set **CFG ≈ 8–14**, **steps ≈ 20–60**, choose a **sampler**.
4. Fix the **seed** (not −1) when you want to compare fairly.
5. Sweep one variable at a time with an **X/Y/Z Plot**.
6. If still wrong → **manual re-touch** (img2img / inpaint).

**Procedure B — Use ControlNet (s.26, 28, 41–43)**
1. Install ControlNet; open the ControlNet Unit.
2. Upload the reference image; tick **Enable** (and **Allow Preview**, optionally **Pixel Perfect**).
3. Choose a **Control Type / Preprocessor**, then a **matching Model** (*ให้สอดคล้องกัน*).
4. Click the **explosion icon** → inspect the preview (the original image is discarded from here on).
5. Set **Control Weight**, **Starting/Ending Control Step**, **Control Mode**, **Resize Mode**.
6. Generate; iterate. Remember: **result quality = f(checkpoint, ControlNet model)**.

**Procedure C — Regional prompting (s.46, 48–50, 54–55)**
1. Open **Regional Prompter** → tick **Active**.
2. Choose **Split/Divide mode** (Horizontal / Vertical / Random) and **Generation mode** (Attention / Latent).
3. Enter the **Divide Ratio** (rows separated by `;`).
4. Click **visualize and make template** → confirm the region map and its indices.
5. Tick **Use common prompt** if there is a shared scene description.
6. Write the prompt with `BREAK` between blocks — **one block per region**, in index order; leave a block **empty** if a region needs nothing extra.
7. Set image **Width/Height** and **Overlay Ratio** (e.g. 0.1) to soften region seams.

**Procedure D — img2img editing (s.58–61)**
1. Send the image to `img2img`.
2. Choose the sub-mode: plain (whole-image restyle), **Sketch** (colour hint), **Inpaint** (masked edit), **Inpaint-Sketch** (masked colour drawing).
3. Write the prompt describing **what the region should become**.
4. Tune **Denoising strength** — low = subtle, high = drastic.
5. Generate; repeat locally rather than regenerating the whole picture.

### 5.7 Code Examples

Lecture 2 contains **no Python code**, but it defines **prompt-language syntax**, which is the "code" of this lecture:

```text
# Emphasis (AUTOMATIC1111 prompt syntax)
a (word)          # weight × 1.1
a ((word))        # weight × 1.21
a [word]          # weight ÷ 1.1
a (word:1.5)      # weight = 1.5
a (word:0.25)     # weight = 0.25  (a 4× reduction, since 1/0.25 = 4)

# LoRA invocation (weight may be negative)
<lora:Long legs slider2_alpha16.0_rank32_full_last:-1.5>

# X/Y/Z value fields
1-5            -> 1, 2, 3, 4, 5
1-5 (+2)       -> 1, 3, 5
10-5 (-3)      -> 10, 7
1-3 (+0.5)     -> 1, 1.5, 2, 2.5, 3
1-10 [5]       -> 1, 3, 5, 7, 10
0.0-1.0 [6]    -> 0.0, 0.2, 0.4, 0.6, 0.8, 1.0

# Prompt S/R
prompt : a man holding an apple, 8k clean,
S/R    : an apple, a watermelon, a gun
=> a man holding an apple, 8k clean
   a man holding a watermelon, 8k clean
   a man holding a gun, 8k clean

# Regional Prompter, 2 regions, with [Use common prompt] ticked
a man and a woman
BREAK
a man with black hair
BREAK
a woman with blonde hair

# Regional Prompter, layout Horizon (1,1,1; 2,1,1) = 4 regions, common prompt on
a witch, highly detailed face, half body, studio lighting, dramatic lighting,
highly detailed clothing, looking at you, mysterious, dramatic lighting
BREAK
(full moon:1.3)
BREAK
BREAK
BREAK
(beautiful fire magic: 1.2)
```

**Expected input/output, errors, improvements**
- *Input:* a prompt string + UI parameter values. *Output:* image(s), or a labelled grid if X/Y/Z Plot is used.
- *Common errors:* S/R keyword not present in the prompt (nothing changes); number of `BREAK` blocks ≠ number of regions (blocks silently mis-assigned); preprocessor and ControlNet model mismatched (garbage or no effect); forgetting that `Use common prompt` shifts every region index by one block.
- *[AI-added] improvement, not from the lecture:* keep a fixed seed while sweeping any other axis, otherwise you cannot attribute the change to the variable you tested.

### 5.8 Examples from the Lecture

1. **CFG × Seed grid, fried rice (s.4).** Proves CFG is *the* prompt-adherence knob and that its effect is far larger than the seed's.
2. **Seed sweep, `1girl, kimono, sakura tree,` seeds 360/777/55 (s.5).** Same semantic content, three different samples.
3. **Steps sweep 5→30 on three subjects (s.7).** Diminishing returns after ~20.
4. **Sampler comparison Euler a / Heun / DPM++ SDE Karras (s.9).** Same prompt, different look.
5. **X/Y/Z grid: colour × CFG × background (s.14).** How to present a parameter study — this is the format expected for the workshop.
6. **LoRA "Long legs slider" at −1.5 / 0.0 / +1.5 (s.18–19).** Negative weights invert the concept.
7. **ControlNet: dancing man → Canny edges → new dancer (s.24); → OpenPose skeleton → jumping woman (s.25).** Same pose, completely different subject.
8. **ControlNet Reference example (s.27):** one reference photo of a woman in white holding a hat → four wildly different characters (mage, dragon-tamer, falconer, man in a suit) **all preserving the same arm-raised composition**.
9. **Multi-ControlNet (s.39):** seated man (OpenPose) + mountain lake (Depth) → anime girl seated in that pose in that landscape.
10. **Regional Prompt failure → fix (s.44–47, 51–52, 55).** Attribute bleeding, then correct separation; the witch/moon/fire composition; a four-season landscape strip; two girls with distinct hair and clothes.
11. **img2img chain (s.58–61):** hair recolour → add glasses (sketch) → replace top with a blue frilled dress (inpaint) → red glasses + pink frilled dress drawn by hand (inpaint-sketch).

### 5.9 Important Tables, Figures, and Diagrams

| Slide | Visual | Lesson |
|---|---|---|
| s.4 | CFG × Seed grid | Low CFG ⇒ the prompt is ignored entirely |
| s.6, 8 | AUTOMATIC1111 parameter panel | Where Sampling method / Steps / Width / Height / **CFG Scale** / **Seed** / Batch live |
| s.10 | Five-lever cheat sheet | The one slide to revise before an exam |
| s.12 | Emphasis cheat sheet | Weight arithmetic |
| s.14, 17 | X/Y/Z grid + script UI | How to run and present a sweep |
| s.24–25 | ControlNet block diagram | Where the extra conditioning enters |
| s.29 | ControlNet UI with Control Type radios | The full preprocessor menu |
| s.31–35 | OpenPose variants on the same photo | What each variant actually detects |
| s.41 | ControlNet settings panel | Weight / start / end / mode / resize |
| s.46, 48 | Regional Prompter panel + template | `ADDCOMM` / `ADDCOL`, Base Ratio 0.2 |
| s.49 | Six region-layout diagrams | **The Divide-Ratio semantics** |
| s.50–51 | 4-region witch example + result | Empty `BREAK` blocks; placement really works |
| s.58–61 | img2img four modes | Which tool for which edit |

### 5.10 Common Mistakes and Important Warnings

- **CFG too low → the image ignores the prompt** (s.3–4). **CFG too high → over-saturated, "fried" images.** Stay in **8–14** unless you have a reason.
- **Leaving Seed = −1 while comparing settings.** You then cannot tell whether the change came from your parameter or from a new random start (s.6).
- **Chasing quality with more steps.** Beyond ~20–60 you mostly buy compute time, not quality (s.7, s.10).
- **Misreading emphasis syntax.** `[word]` ≠ delete; `(word:0.25)` = weight 0.25 = a **4×** reduction (s.12).
- **Prompt S/R keyword missing from the prompt** → the sweep silently does nothing (s.16).
- **Forgetting that the preprocessor discards the original image** (s.28) — whatever the preview shows *is* the control signal. If the pose preview is wrong, the output will be wrong.
- **Mismatching preprocessor and ControlNet model** (s.41: *ให้สอดคล้องกัน*). An `openpose` preprocessor needs an *openpose* ControlNet model.
- **Expecting a ControlNet result to be independent of the checkpoint.** s.43 explicitly warns: *ประสิทธิภาพ ขึ้นอยู่กับ Checkpoint + ControlNet model.*
- **Attribute bleeding in multi-subject prompts** (s.45) — the reason regional prompting exists. Writing "a man with black hair, a woman with blonde hair" in one prompt is *not* reliable.
- **Mismatch between the number of `BREAK` blocks and the number of regions**, especially after enabling **Use common prompt** (which consumes the first block) (s.46 vs s.48).
- **Reading Divide Ratio backwards** — the first number in a row is the **row height**, the rest are **widths** (s.49).
- **img2img denoising strength too high** → the model throws away the input image; too low → nothing changes (s.58).
- **Inpaint-Sketch without painting skill** — the lecture itself warns: *"you should have proper painting knowledge"* (s.61).

### 5.11 Easy-to-Understand Summary

Lecture 1 told you the engine exists; Lecture 2 hands you the steering wheel. There are five knobs: **which model** you load, **what you write**, **what extras you bolt on**, **which numbers you set**, and **what you fix by hand afterwards**.

Of the numbers, four matter: **CFG** decides how strictly the picture obeys your words (0 = ignores you, 20 = slavishly literal; live around 8–14); **Seed** decides *which* random starting point you got (fix it whenever you want to compare anything fairly); **Steps** is how many denoising passes you run (20–60 is plenty — more just costs time); and the **Sampler** is the rule used in each of those passes.

Words alone, though, cannot describe a picture — *"one image stands for many words"*. So when you need an exact pose, outline or 3-D layout, you attach an image-shaped control signal with **ControlNet**: it converts a reference photo into a skeleton (**OpenPose**), an outline (**Canny**) or a depth map (**Depth**), throws the photo away, and feeds that map to the model *in addition to* your prompt. And when several subjects must each keep their own attributes, you carve the canvas into regions with the **Regional Prompter** and give each region its own prompt block, separated by `BREAK`.

Finally, when a generated image is *almost* right, you do not start over — you **re-touch** it: `img2img` re-renders it with a new prompt, `Sketch` hints with colour, `Inpaint` edits a masked area, and `Inpaint-Sketch` lets you crudely paint what you want and have the model render it properly.

### 5.12 Source References

- Five tuning levers: **s.2** · CFG: **s.3–4** · Seed: **s.5–6** · Steps: **s.7** · Sampler: **s.8–9** · Cheat sheet: **s.10**
- Attention/emphasis: **s.11–12**
- X/Y/Z Plot (concept, example, range syntax, UI): **s.13–15, 17** · Prompt S/R: **s.16** · LoRA slider sweep: **s.17–19** · Workshop: **s.20**
- ControlNet: title **s.21**, motivation **s.22**, definition **s.23**, block diagrams **s.24–25**, usage **s.26**, reference example **s.27**, preprocessor concept **s.28**, UI/control types **s.29**, results **s.30**
- OpenPose family: **s.31–35** · Canny: **s.36** · Depth: **s.37–38** · Multi-ControlNet: **s.39** · Settings & workflow: **s.41–43**
- Regional Prompt: motivation **s.44–45**, setup **s.46**, results **s.47**, tips/common prompt **s.48**, divide-ratio semantics **s.49**, worked example **s.50–51**, seasons example **s.52**, matrix settings **s.54**, template/BREAK **s.55**
- img2img: overview **s.56–57**, with Text **s.58**, with Sketch **s.59**, with Inpaint **s.60**, with Inpaint-Sketch **s.61**, closing **s.62**

---
## 6. File 3: `Lecture 3 - Human Visual Perception.pdf`

### 6.1 File Overview

59 slides. **The file name is misleading: this PDF contains two separate decks.** The footer changes at slide 13, which is where the second deck begins.

| Slides | Deck (per the slide footer) | Block |
|---|---|---|
| 1–12 | **Human Visual Perception** | The human eye; eye vs. camera lens; liquid lenses; animal eyes; optical illusions |
| 13–17 | **Fundamental Operation** | What a digital image *is* to a computer: grayscale, arrays, RGB channels |
| 18–22 | **Fundamental Operation** | Python setup: PIP, NumPy, OpenCV; virtual environments (`venv`, `pyenv`, `conda`/`mamba`) |
| 23–30 | **Fundamental Operation** | OpenCV/NumPy basics: read/write/show, image attributes, per-pixel access, data types |
| 31–49 | **Fundamental Operation** | Image acquisition optics: pinhole, camera obscura, history, lenses, Snell's law, aberrations, distortion |
| 50–59 | **Fundamental Operation** | Choosing a camera: FOV mathematics, CCD vs CMOS, classwork |

The intellectual arc: **the eye is a camera you cannot trust → so build a camera you understand → and represent what it sees as numbers you can compute on.**

### 6.2 Main Topics

1. **Why study the eye in an image-processing class?** (s.2–3)
2. **Eye lens vs camera lens — what is the big difference?** (s.4–5)
3. **Liquid lenses** — could we build a camera lens that works like the eye? (s.6–7)
4. **Animal eyes** (s.8)
5. **"Can we trust our eyes?"** — optical illusions (s.9–12)
6. **Digital image representation** — grayscale, N-dimensional arrays, RGB channels (s.14–17)
7. **Python environment setup** (s.18–22)
8. **OpenCV / NumPy fundamentals** (s.23–30)
9. **Image acquisition** — pinhole → lens → aberrations → distortion (s.31–49)
10. **How to choose a camera for an image-processing project** + FOV maths + CCD vs CMOS (s.50–59)

### 6.3 Important Concepts and Theories

#### (a) The human eye (s.2–3) — verbatim from the slides

> **Cornea:** "A tough, transparent tissue that covers the anterior surface of the eye."
> **Lens:** "Makes up of concentric layers of fibrous cells and contains **60-70% of water**. To focus on objects near or far the eye, the controlling muscles cause the lens to be **thicker or thinner**."
> **Retina:** "innermost membrane lines the inside of the wall's entire posterior portion. Retina contains **cones and rods**."

**The key contrast (s.4–5 asks it as a question; AI states the answer plainly):** the eye focuses by **deforming a soft, water-filled lens**; a camera focuses by **physically moving a rigid glass lens**. Same job, opposite mechanism.

#### (b) Liquid lens (s.6–7)

s.6 asks *"Why could we design our camera lens like our eyes?"* and gives one clue on the slide: **"Water & Oil"**. s.7 shows this is already a shipping product:

> **Xiaomi Mi Mix Fold** (available in China only) — "telephoto and macro **by the same liquid lens**", "Using **C1 professional imaging chip**", "Mass production of mobile phone with liquid lenses."

**AI explanation:** a liquid lens changes its curvature (and therefore its focal length) by deforming a water/oil interface with an applied voltage — the engineering imitation of the eye's ciliary muscle. One physical element can then act as both a telephoto and a macro lens.

#### (c) "Can we trust our eyes?" (s.9–12) — *the philosophical core of the whole course*

The slides show the **Koffka ring** (s.9–10, credited to `http://persci.mit.edu/gallery`) and further illusion figures on s.11–12.

**Why this matters (AI):** the human visual system reports **relative**, context-dependent brightness, not absolute intensity. Two patches with the *identical* pixel value look different when their surroundings differ. Therefore *"this image looks too dark"* is not a statement a computer can act on. This is precisely the gap that **Lecture 4** closes with the **histogram** — an objective, measurable description of intensity. Lecture 4 s.23 asks the same question from the other side: *"We know, this image too dark right? But how can we tell computer?"*

#### (d) What a digital image is (s.14–17)

* **Grayscale (s.14–15):** *"We see 'image' like this."* vs *"But, this is what computer see."* — a grid of numbers from **0 to 255**.
* **Array (s.16):** `Digital Image ➔ Array (N-dimensions)`; **Rows = Height**, **Columns = Width**, addressed as **`(r, c)`**, zero-indexed from `(0,0)` at the top-left. Thai caption: *การจัดการ "ภาพ" ด้วย Python*.
* **Colour (s.17):** the **RGB model** — the image is three stacked planes, `Channel : Red / Green / Blue`.

> ⚠️ **Trap (AI, but grounded in s.16):** the array index order is **`img[row, column]` = `img[y, x]`** — *y first*. This is the opposite of the `(x, y)` order people expect from maths. Every code example in the lecture obeys it (see `img[y,x] = 255` in Example #3).

#### (e) Image acquisition — from a hole to a lens (s.31–49)

| Idea | What the slide says | Slide |
|---|---|---|
| **Pinhole camera** | A barrier with a tiny hole projects an inverted image onto the film / image plane. The diagram marks the **virtual image**, the **pinhole**, and **f** on both sides. | s.32–33, 41 |
| **Camera obscura** | "the beginnings of photograph" | s.34–35 |
| **Louis Daguerre** | "Lens focus light" · "Better chemical ➔ **10 – 12 min**" (exposure time) | s.37 |
| **Nimrud lens** | Found by **Sir Austen Henry Layard** (English traveller) among Assyrian palace reliefs, ancient Assyrian states (Iraq) — a possible ancient lens | s.38 |
| **Alhazen (Ḥasan Ibn al-Haytham)** | 10th–11th century (**c. 965 – 1040 CE**). Wrote **"Kitab al-Manazir" (Book of Optics)**. Proved **light travels in straight lines**; explained **reflection and refraction**; used a **convex lens to magnify**; laid the foundations of the **camera obscura**. | s.39 |
| **Lens focusing** | "A lens focuses light onto the film — Rays passing through the **center are not deviated** — All **parallel rays converge to one point** on a plane located at the **focal length f**" | s.42 |
| **Circle of confusion** | "There is a **specific distance** at which objects are 'in focus' [other points project to a **'circle of confusion'** in the image]" | s.43 |
| **Why multi-element lenses?** | "Why do we use complex, multi-element designs and large lens housings if a single lens will also provide an image for much cheaper?" → the slide contrasts **Real Glass** with the **Approximate (Thin lens)** model | s.44–45 |
| **Snell's law** | `n₁ sin α₁ = n₂ sin α₂` — α₁ = incident angle, α₂ = refraction angle, nᵢ = index of refraction | s.46 |
| **Spherical aberration** | "Rays farther from the optical axis focus closer" *(แถวๆ ขอบเลนส์จะโฟกัสใกล้กว่า)* | s.47–48 |
| **Chromatic aberration** | "Lens has different refractive indices for different wavelengths: causes **colour fringing**" | s.47–48 |
| **Distortion** | Three cases drawn: **No distortion** · **Pin cushion** · **Barrel (fisheye lens)** — "Image magnification decreases with distance from the optical axis". Caption: "**Deviations are most noticeable for rays that pass through the edge of the lens**" | s.49 |

**AI synthesis — why this optics detour exists in a programming course:** every defect above is a *systematic error baked into your data before a single line of code runs*. Barrel distortion bends straight lines, so an edge detector will report curves. Chromatic aberration paints false colour at high-contrast edges, so a colour-based segmenter will mis-classify. The lecture's message is the same as slide 5 of Lecture 1: **fix the acquisition first**, because no algorithm can recover information the optics destroyed.

#### (f) Choosing a camera (s.50)

> **How to choose camera? (for image processing project)**
> `[1]` Data type (Still Image or Video) ➔ **CCD or CMOS**
> `[2]` Coverage area (**Field of View** / Size of Object)
> `[3]` Resolution of image / Frame rate (Detection / Identify)
> `[4]` Connectivity / Hardware Memory
> `[5]` Reasonable price

#### (g) CCD vs CMOS (s.57)

| | **CCD** | **CMOS** |
|---|---|---|
| Resolution | Up to 100+ Megapixels | Up to 100+ Megapixels |
| Frame rate | Low frame rates | **High frame rates** |
| Noise figure | **Low noise floor** | High noise floor |
| Sensitivity of intensity | **More sensitive at low intensity** | Less sensitive at low intensity |
| Shutter type | **Global** | **Rolling** |
| Skew | **No** | **Yes** |

**AI explanation of the last two rows — this is the row that decides the choice.** A **global** shutter exposes every pixel at the same instant. A **rolling** shutter exposes row by row, so a fast-moving object is captured at slightly different times down the frame and comes out **skewed** (leaning). If your project photographs anything moving quickly — a conveyor belt, a spinning part — a CMOS rolling shutter will bend it. That is why `[1]` on s.50 ties "Still Image or Video" directly to "CCD or CMOS".

### 6.4 Terminology and Definitions

| Term | Definition as given in the lecture | Slide |
|---|---|---|
| **Cornea** | Tough, transparent tissue covering the anterior surface of the eye | s.2–3 |
| **Lens (eye)** | Concentric layers of fibrous cells, 60–70 % water; muscles make it thicker/thinner to focus | s.2–3 |
| **Retina** | Innermost membrane lining the posterior wall; contains **cones and rods** | s.2–3 |
| **Liquid lens** | A lens using **Water & Oil**, able to do telephoto and macro with the same element | s.6–7 |
| **Koffka ring** | An optical illusion used to ask "Can we trust our eyes?" | s.9–10 |
| **Channel** | One of the Red / Green / Blue planes of a colour image | s.17 |
| **Virtual environment** | "A Python environment such that the Python interpreter, libraries and scripts installed into it are **isolated from other**" | s.19 |
| **`uint8`** | Unsigned integer, **0 to 255** — the natural type of an 8-bit image | s.28 |
| **Camera obscura** | "the beginnings of photograph" — a darkened room/box with a pinhole | s.34–35 |
| **Focal length (f)** | The distance at which parallel rays converge to a point | s.42 |
| **Circle of confusion** | The blur disc formed by points that are not at the in-focus distance | s.43 |
| **Thin lens** | The simplifying approximation used instead of real multi-element glass | s.45 |
| **Index of refraction (n)** | The `n` in Snell's law | s.46 |
| **Spherical aberration** | Rays farther from the optical axis focus closer | s.47 |
| **Chromatic aberration** | Different refractive indices per wavelength → colour fringing | s.47 |
| **Barrel / Pin cushion distortion** | Straight lines bow outwards / inwards; magnification varies with distance from the optical axis | s.49 |
| **Angle of view (θ)** | Derived from sensor size and focal length | s.53, 55 |
| **Field of view (FOV)** | Derived from angle of view and distance to the object | s.53, 55 |
| **Global / Rolling shutter** | Whole sensor exposed at once / row-by-row (causes **skew**) | s.57 |

### 6.5 Formulas and Calculations

**Formula 1 — Snell's law (s.46), exactly as printed:**

```
n₁ sin α₁ = n₂ sin α₂

α₁ = incident angle
α₂ = refraction angle
nᵢ = index of refraction
```

**Formula 2 — Angle of view (s.55), exactly as printed:**

```
        ⎛ sensor size ⎞
θ = 2 tan⁻¹⎜ ─────────── ⎟
        ⎝     2f      ⎠
```

**Formula 3 — Field of view (s.55), exactly as printed:**

```
FOV = 2 ( S₀ · tan(θ/2) )        S₀ = distance to object
```

**The two-step procedure (s.53):** *"Find 'Angle of view' from Focal length & Sensor size"* → *"Find 'Field of view' from Angle of view & Distance to Obj."*

**Worked setup printed on s.56:**

```
θ   = 2 tan⁻¹( 35mm / (2 × 50mm) )
FOV = 2 ( 5m · tan(θ/2) )
```

> **Unit warning, verbatim (s.56):** *ข้อแนะนำ: ควรระมัดระวังเรื่องการใช้หน่วยวัด (ให้ใช้หน่วยวัดเดียวกันจะได้ไม่สับสน)* — "Be careful with units of measurement (use the same unit so you don't get confused)."
> And: *Field of view (FOV) จะได้ผลลัพธ์เป็นหน่วย เมตร (m) ตามหน่วยของระยะห่างวัตถุถึงเลนส์* — "The FOV comes out in **metres (m)**, following the unit of the object-to-lens distance."

**AI-completed arithmetic** (the slide sets up the numbers but does not print the answer):
θ = 2·tan⁻¹(35 / 100) = 2 × 19.29° = **38.58°**
FOV = 2 × 5 m × tan(19.29°) = 2 × 5 × 0.35 = **3.5 m**

**AI shortcut worth memorising:** substituting Formula 2 into Formula 3, the tangents cancel:

```
FOV ≈ S₀ × (sensor size / f)
```
Check: 5 m × (35 / 50) = **3.5 m** ✓ — same answer, no trigonometry. Use the exact formulas when asked to *show work*; use this to sanity-check the result.

### 6.6 Processes and Procedures

**Procedure 1 — Set up Python for image processing (s.18):**
1. Check Python version
2. Install **PIP**
3. Install libraries **NumPy** & **OpenCV**
*(the slide also links a guide: "How to install PIP in macOS")*

**Procedure 2 — Virtual environment with `venv` (s.19–20):**
```bash
python -m venv <virtual-environment-name>   # 1) create
env/Scripts/activate.bat                    # 2) activate  (as printed on the slide)
pip freeze > requirements.txt               # 3) save the package list
pip install -r requirements.txt             # 4) install from the list
```
> ⚠️ The activate path printed on s.19 (`env/Scripts/activate.bat`) is the **Windows** form. macOS/Linux use `source env/bin/activate` — **not stated on the slide**; see §17.

**Procedure 3 — `pyenv` + `pyenv-virtualenv` (s.21)** — "for managing many Python versions + env"; supports Mac/Linux well, and Windows via WSL or Git Bash:
```bash
pyenv install 3.10.13                       # install Python 3.10
pyenv virtualenv 3.10.13 myproject-env      # create the environment
pyenv activate myproject-env                # use it
```

**Procedure 4 — `conda` / `mamba` (s.22)** — "suits Data Science / Windows users"; `mamba` is a faster version of `conda` (**the slide recommends it**); good for people working with NumPy, SciPy, TensorFlow:
```bash
conda create -n myenv python=3.9            # new environment with Python 3.9
conda activate myenv                        # enter it
conda install numpy pandas                  # install libraries
```

**Procedure 5 — Choose a camera (s.50):** the 5-point checklist in §6.3(f).

**Procedure 6 — Compute the FOV (s.53, 55–56):** ① sensor size + focal length → θ ② θ + object distance → FOV ③ check your units.

### 6.7 Code Examples

All code below is **transcribed verbatim from the slide screenshots**. Filenames are the ones visible in the editor title bars.

**Example #1 — Read / Write / Show image (s.23–24, `Demo02_Read-Write-Show.py`)**
```python
import cv2 as cv

# Read the image
img = cv.imread("pic/B.bmp")

print("Data type of image (OpenCV): ", type(img))

# Display the image
cv.imshow("Example1 - imshow", img)

# Save the image
cv.imwrite("out.png", img)

# Wait for a key press
cv.waitKey(0)

# Clean up
cv.destroyAllWindows()
```
Console output shown on the slide: `Data type of image (OpenCV):  <class 'numpy.ndarray'>`
Thai annotations on s.24, line by line: read the image file at the given path into the variable `img` · display the image in `img` in a window · save the image to the given path · **wait for any key press (if you omit this, the window closes by itself)** · after the key press, close all windows.

**Example #2 — Access image attributes (s.25–26, `Demo02_02_Grayscale.py`)**
```python
import cv2 as cv

# Read the image
img = cv.imread("pic/C.jpg", cv.IMREAD_GRAYSCALE)

print("Data type of image (OpenCV): ", type(img))
print("number of dimension: ", img.ndim)
print("size of each dimension: ", img.shape)
print("image height: ", img.shape[0])
print("image width: ", img.shape[1])

# Display the image
cv.namedWindow('Example1 - imshow', cv.WINDOW_NORMAL)
cv.imshow('Example1 - imshow', img)

# Wait for a key press
cv.waitKey(0)

# Clean up
cv.destroyAllWindows()
```
Console output shown on the slide:
```
Data type of image (OpenCV):  <class 'numpy.ndarray'>
number of dimension:  2
size of each dimension:  (1440, 1080)
image height:  1440
image width:  1080
```
> **Read the output carefully:** `.ndim` is **2** because the image was loaded with `cv.IMREAD_GRAYSCALE` (a colour image would be 3). `.shape` is `(1440, 1080)` = **(height, width)** — height first, matching the `img[y, x]` convention from s.16. `cv.WINDOW_NORMAL` makes the window resizable, which is what lets a 1440-pixel-tall image fit on screen.

**Example #3 — Access / Modify each pixel (s.27–29, `Demo02_03_DrawRect.py`)**
```python
import numpy as np
import cv2 as cv

# Create empty image
img = np.zeros([200, 300], dtype = np.uint8)

for y in range( 75, 125 ):
    for x in range( 50, 250 ):
        img[y,x] = 255

# Display the image
cv.imshow('Drawing', img)

# Wait for a key press
cv.waitKey(0)

# Clean up
cv.destroyAllWindows()
```
Result shown on s.29: a black 300 × 200 image with a **white rectangle** — 200 px wide (x from 50 to 249) and 50 px tall (y from 75 to 124).

**NumPy array creation (s.27):**
```python
numpy.empty(shape, dtype)   # uninitialized array of the given shape and dtype
numpy.zeros(shape, dtype)   # new array of the given size, filled with zeros
numpy.ones(shape, dtype)    # new array of the given size and type, filled with ones
```

**NumPy data types (s.28)** — 15 rows are listed (`bool_`, `int8`, `int16`, `int32`, `int64`, `uint8`, `uint16`, `uint32`, `uint64`, `float_`, `float32`, `float64`, `complex`, `complex64`, `complex128`). The one that matters for 8-bit images:

| # | Data type | Description (verbatim) |
|---|---|---|
| 6 | **`uint8`** | **Unsigned integer (0 to 255)** |
| 2 | `int8` | Byte (-128 to 127) |
| 7 | `uint16` | Unsigned integer (0 to 65535) |
| 11 | `float32` | Single precision float: sign bit, 8 bits exponent, 23 bits mantissa |
| 12 | `float64` | Double precision float: sign bit, 11 bits exponent, 52 bits mantissa |

### 6.8 Examples from the Lecture

* **The Koffka ring** (s.9–10) — the illusion that motivates the whole "don't trust your eyes" argument.
* **Xiaomi Mi Mix Fold** (s.7) — a real, mass-produced phone with a liquid lens; telephoto and macro from one element.
* **Louis Daguerre's 10–12 minute exposure** (s.37) — what photography cost before fast optics.
* **The Nimrud lens** (s.38) and **Alhazen's Book of Optics** (s.39) — the pre-history of the camera.
* **The three Demo02 scripts** (s.23–29) — read/show/save, inspect, and draw a rectangle pixel by pixel.
* **The 35 mm / 50 mm / 5 m FOV example** (s.56).

**Classwork set on s.59 (verbatim, translated):**
> * Check the properties of *your* camera: **Focal Length · Sensor Size · Field of View · Resolution (Pixel per Inch)**
> * At a distance of **1 metre**, how big is the Field of View (width × length)? Check the units too (cm or m).
> * Does the image taken by your camera have **distortion**? (check straight lines)
> * Do the **colours** from your camera differ from those of the other members of your group?
> * Make **one summary file per group**, submitted by one person (**.pdf**)

### 6.9 Important Tables, Figures, and Diagrams

| Slide | Figure / Table | What to take from it |
|---|---|---|
| s.14–15 | "We see image like this / this is what computer see" | An image is a grid of numbers, 0–255 |
| s.16 | Row/column array diagram, `(r, c)` | Indexing is **`[row, column] = [y, x]`** |
| s.17 | RGB three-plane diagram | Colour = 3 stacked channels |
| s.28 | NumPy data-type table (15 rows) | `uint8` = 0–255 is *the* image type |
| s.41 | Pinhole camera (image plane, pinhole, virtual image, f) | The image is inverted; geometry is pure similar triangles |
| s.43 | "Circle of confusion" diagram | Only one distance is truly in focus |
| s.45 | Real Glass vs Approximate (Thin lens) | Why the simple formulas are an approximation |
| s.46 | Snell's law diagram (α₁, α₂, n₁, n₂) | Refraction is the reason lenses work at all |
| s.47–48 | Spherical vs chromatic aberration | Edge rays focus early; colours focus differently |
| s.49 | No distortion / Pin cushion / Barrel | The three shapes to recognise in your own photos |
| s.53 | Angle of view / Field of view / Focal length diagram | The picture that makes the FOV formulas obvious |
| s.57 | **CCD vs CMOS comparison table** | Global vs rolling shutter, skew — the deciding row |

### 6.10 Common Mistakes and Important Warnings

**Printed in the lecture (s.30, "What will happen if…"), verbatim:**
> ❑ *จะเกิดอะไรขึ้นถ้ากำหนดให้ค่าในภาพมีค่าที่ไม่ได้อยู่ในช่วง 0 – 255 ???* — What happens if you assign a pixel a value **outside 0–255**?
> ❑ *ถ้ามีการวนลูปออกนอกบริเวณภาพจะเกิดอะไรขึ้น* — What happens if your **loop runs outside the image bounds**?

And "**Try this…**" (s.30):
> ❑ Split an RGB colour image into its Red, Green, Blue planes
> ❑ Write a function to adjust the **brightness** of an image
> ❑ Try `hconcat` / `vconcat` to place images side by side

**AI answers to the lecture's two questions** (the slide poses them; it does not answer them):
* Assigning outside 0–255 to a `uint8` array **wraps around** (256 → 0, −1 → 255), so an over-bright pixel turns *black*. This is exactly the bug that Lecture 4's **clamping** (s.32) exists to prevent.
* Looping past the bounds raises an `IndexError` on read — but note that a **negative** index does *not* raise: `img[-1]` silently reads the last row.

**Other warnings:**
* **The unit trap (s.56)** — mixing mm and m in the FOV formula is the single most common numerical error here.
* **Don't trust the eye (s.9–12)** — never conclude "this image needs enhancement" by looking; measure it (Lecture 4).
* **Rolling-shutter skew (s.57)** — a CMOS sensor will bend fast-moving objects.
* **Optics defects are unrecoverable (s.47–49)** — barrel distortion, colour fringing and blur are baked in at capture time.

### 6.11 Easy-to-Understand Summary

Your eye is a brilliant camera with a soft, water-filled lens that changes shape to focus — and it *lies to you* about brightness (that's what the Koffka ring proves). A camera is the opposite: a rigid lens that moves, and a sensor that records honest numbers. To a computer an image is just a grid of integers from 0 to 255 — `img[y, x]`, **row first** — and colour is three such grids stacked (R, G, B). Before you write any code you must get the physics right: a lens focuses parallel rays at the focal length **f**, only one distance is genuinely sharp (everything else lands as a "circle of confusion"), and real glass adds defects — edge rays focus early (**spherical**), colours focus differently (**chromatic**), and straight lines bow (**barrel / pin cushion**). Choose your camera deliberately: work out the **angle of view** from the sensor size and **f**, then the **field of view** from the angle and the distance — and keep your units consistent. Finally, CCD gives you a **global** shutter (no skew, low noise, slow), CMOS gives you a **rolling** shutter (fast, but it bends moving objects).

### 6.12 Source References

* Human eye (cornea / lens / retina): **s.2–3** *(ref. printed on slide: opentextbooks.org.hk)*
* Eye vs camera lens: **s.4–5** *(ref: sciencelearn.org.nz)*
* Liquid lens (Water & Oil; Xiaomi Mi Mix Fold): **s.6–7**
* Animal eyes: **s.8** · Koffka ring / illusions: **s.9–12** *(ref: persci.mit.edu/gallery)*
* Digital image — grayscale **s.14–15**, array **s.16**, RGB **s.17**
* Python setup **s.18** · `venv` **s.19–20** · `pyenv` **s.21** · `conda`/`mamba` **s.22**
* Code Example #1 **s.23–24** · #2 **s.25–26** · #3 **s.27–29** · NumPy dtypes **s.28** · "What will happen if…" **s.30**
* Image acquisition: film **s.31**, pinhole **s.32–33, 41**, camera obscura **s.34–35**, Daguerre **s.37**, Nimrud lens **s.38**, Alhazen **s.39**
* Lens: focusing **s.42**, circle of confusion **s.43**, multi-element vs thin lens **s.44–45**, Snell's law **s.46**
* Aberrations **s.47–48** · Distortion **s.49**
* Choosing a camera **s.50** · FOV **s.51–56** · CCD vs CMOS **s.57** · Classwork **s.59**

---

## 7. File 4: `Lecture 4 - Point Operation.pdf`

### 7.1 File Overview

103 slides — the largest file, and **it contains three separate decks**. The footer changes twice.

| Slides | Deck (per the slide footer/title) | Block |
|---|---|---|
| 1–10 | **Point Operation** | What intensity transformation is; the transformation-curve chart; the mapping table |
| 11–22 | **Point Operation** (section "Tools") | Power-law/gamma, log transform, piecewise-linear contrast stretching |
| 23–34 | **Point Operation** | Histograms, dynamic range, brightness/contrast, clamping, automatic contrast adjustment |
| 35–50 | **Point Operation** | Histogram equalization; histogram specification (matching) |
| 51–56 | **Class Project (LUMA)** | The project brief, the distributed system, the team split |
| 57–67 | **Web Application** | Front-end / back-end / full-stack; popular tech stacks; roadmaps |
| 68–103 | **Web Development with Flask** | Flask, routes, debug mode, HTTP status codes, Jinja templates, project milestones |

**This is the file that explains why the working folder is called `Web_App`** — the second half of it *is* the web-development course, and it defines the LUMA class project that is worth **40 %** of the grade (Lecture 1, s.6).

### 7.2 Main Topics

1. **Intensity transformation** — what it is, when you need it, how to choose a method (s.3–8)
2. **The standard transformation curves** — Negative, Log, Inverse log, nth power, nth root, Identity (s.7–8)
3. **Power-law (gamma) transformation** and **gamma correction** (s.12–18)
4. **Logarithmic transformation** (s.19)
5. **Piecewise-linear contrast stretching** (s.20–22)
6. **The histogram** as the objective measuring tool (s.23–29)
7. **Dynamic range** (s.30–31)
8. **Brightness / contrast, clamping, automatic contrast adjustment** (s.32–34)
9. **Histogram equalization** (s.36–43)
10. **Histogram specification / matching** (s.44–50)
11. **The LUMA class project** and its **distributed system** (s.51–56)
12. **Web application concepts** — front/back/full-stack, tech stacks (s.57–67)
13. **Flask** — routes, parameters, debug mode, status codes (s.68–90)
14. **Jinja templates** (s.91–101)
15. **The five project milestones** (s.103)

### 7.3 Important Concepts and Theories

#### (a) The central equation (s.7)

```
g(x,y) = T[ f(x,y) ]

f(x,y) : input image
g(x,y) : output image
```

**What makes it a *point* operation (AI):** `T` looks at **one pixel at a time** and depends on *nothing else* — not the neighbours, not the position. Change a pixel's value, and only that pixel changes. This is why a point operation can be pre-computed as a **mapping table** (s.8):

| Input | Output |
|---|---|
| 0 | 0 |
| 1 | 25 |
| 2 | 33 |
| 3 | 56 |
| … | … |
| 255 | 255 |

**Consequence:** a point operation on an 8-bit image is a 256-entry lookup table. That is why it is fast, and why it can *never* remove noise or blur (those need neighbours).

#### (b) The transformation-curve chart (s.7, repeated s.43)

The slide plots six curves on axes `Input intensity level` (0 … 127 … 255) vs `Output intensity level`:

* **Identity** — the diagonal; changes nothing
* **Negative** — top-left to bottom-right; inverts
* **Log** and **nth root** — bow *above* the diagonal → **brighten dark regions, compress bright ones**
* **Inverse log** and **nth power** — bow *below* the diagonal → **darken, expand bright regions**

**AI reading of the chart — the one rule that matters:** *above the diagonal = brighter; below = darker.* Where the curve is **steep**, contrast is **stretched** (differences become visible); where it is **flat**, contrast is **crushed** (differences are lost). Every point operation is a trade: you buy contrast in one intensity band by spending it in another.

#### (c) "When do we need intensity transformation?" (s.4–6)

> "It depend on your problem.
> ➢ What **Goal** do you aim for?
> ➢ What **Feature** your algorithm used?"

Illustrated (s.5–6) with **Sea Bass (ปลากะพงขาว)** vs **Salmon** — two fish whose separation depends on which feature you intend to measure.

#### (d) Power-law (gamma) transformation (s.12–18)

**As printed (s.12):**
```
s = c · r^γ

where c and γ are positive constants
    r = input intensity levels
    s = output intensity levels

Sometimes this equation is written as
    s = c (r + ε)^γ
to account for offsets (that is, a measurable output when the input is zero).
```

**Gamma correction (s.13), verbatim:**
> "The response of many devices used for image capture, printing, and display **obey a power law**. By convention, the exponent in a power-law equation is referred to as **gamma (γ)**. The process used to correct these power-law response phenomena is called **gamma correction**."
> "**Cathode Ray Tubes (CRTs) are Nonlinear**"

**AI explanation:** a CRT's light output is not proportional to its input voltage — it follows a power law. If you send it a linear image, it displays a too-dark one. Gamma correction pre-distorts the image with the *inverse* exponent so the two power laws cancel and the eye sees the right thing. Note the direction: **γ < 1 brightens** (it lifts dark tones), **γ > 1 darkens**.

#### (e) Logarithmic transformation (s.19)

**As printed:**
```
s = c log(1 + r)     where c is a constant, and r ≥ 0
```
Application shown on the slide: **Fourier spectrum display**.

**AI explanation:** the `1 +` exists so that `r = 0` maps to `0` rather than to `log(0) = −∞`. The log curve is extremely steep near zero and very flat at the top, so it **massively expands dark detail and compresses highlights** — which is exactly what a Fourier spectrum needs, since its DC term is orders of magnitude larger than everything else.

#### (f) Contrast and contrast stretching (s.20–22)

**Contrast, as defined on s.20:**
```
              I_max − I_min
contrast = ─────────────────
              I_max + I_min
```
*(This is the **Michelson** definition — the slide gives the formula without naming it.)*

**AI note:** the value is bounded between 0 and 1 for non-negative intensities. `I_min = 0` gives contrast = 1 regardless of `I_max`, which is why a single stray black pixel makes this metric optimistic. The **piecewise-linear** stretch (s.21–22, code in §7.7) fixes this properly by mapping a chosen input band `[r₁, r₂]` onto a wider output band `[s₁, s₂]`.

#### (g) The histogram — the answer to "how can we tell the computer?" (s.23–29)

s.23 poses the problem exactly:
> "We know, this image **too dark** right? But how can we **tell computer**?"

s.24 answers:
> "We will begin with a basic tool. **Histogram**. It is simple to conclude if an image is **properly exposed** by visual inspection of its histogram."

**The crucial caveat (s.25):** *"Three very different images with **identical histograms**"* — the histogram counts *how many* pixels have each value, and throws away *where* they are. It is a **summary**, not a description. Two completely different photographs can share one histogram.

**Histograms are 1-D signals (s.27),** so they can be described with: **Mean · Variance · Skewness · Kurtosis · etc.**

#### (h) Dynamic range (s.30–31), verbatim

> "The dynamic range of an image is, in principle, understood as **the number of distinct pixel values in an image**. In the ideal case, the dynamic range encompasses all **K usable pixel values**, in which case the value range is completely utilized."

The slides contrast a **High dynamic range** histogram (values spread across the whole axis) with a **Low dynamic range** one (values bunched together).

#### (i) Modifying image intensity (s.32–34)

The slides name four operations in sequence:
1. **Contrast and Brightness** (s.32–33) — the linear pair
2. **Limiting the Results by Clamping** (s.32) — force the result back into 0…255
3. **Automatic Contrast Adjustment** (s.32) — stretch using the image's own min and max
4. **Modified Automatic Contrast Adjustment** (s.34)

**AI explanation of why "modified" exists:** plain automatic contrast adjustment anchors on the *absolute* darkest and brightest pixels — so a single hot pixel or one dead black pixel dictates the whole mapping. The *modified* version ignores a small percentage at each end (a percentile-based stretch) and is therefore robust to outliers. **`Needs further verification`: the exact percentile/quantile formula on s.34 is presented as a figure; the numeric parameters are not legible in the extracted text.**

#### (j) Histogram equalization (s.36–43)

**Motivation (s.36), verbatim:** "A frequent task is to adjust two different images in such a way that their resulting intensity distributions are **similar**, for example to use them in a print publication or to make them easier to compare."

**The idea (s.37):** "Basically, we might want to **spread the intensity equally** for each value."

**The mechanism (s.39–40) — this is the whole trick:**
* Build the **histogram**, then the **cumulative histogram**.
* s.40, verbatim: *สร้าง mapping function จาก Cumulative Histogram ไปหา "เส้นตรง"* — **"build the mapping function from the cumulative histogram towards a straight line."**

**AI explanation:** if the intensities were perfectly uniform, the *cumulative* histogram would be a straight diagonal line. So equalization asks: "what transformation would bend my actual cumulative curve into that straight line?" The answer *is* the (normalised) cumulative histogram itself, used as the mapping function.

**Results (s.41–42):**
* *ภาพ Low Contrast (Histogram เกาะกลุ่มกันช่วงค่าสีหนึ่งมากๆ)* — "Low-contrast image (the histogram is clumped tightly into one intensity band)"
* *ภาพ High Contrast (จากการทำ Histogram Equalization)* — "High-contrast image (resulting from histogram equalization)"

**Where we now stand (s.43), verbatim:** "What we know now — **[1] Change intensity based on known equation. [2] Spread it out, uniformity.**"

#### (k) Histogram specification / matching (s.44–50)

**The gap (s.44):** "What if, we **don't know equation** & we **don't want to spread it**" — *"Wanna make left image look like a right image."*

**The construction (s.45–46), exactly as drawn:**

```
 Input  ──H₁──►  (Histogram Equalization)  ──A──►  U₁
 Goal   ──H₂──►  (Histogram Equalization)  ──B──►  U₂          ← s.45

 Input  ──H₁───►  (Histogram Equalization)   ──A───►  U₁
 Goal   ──H₂⁻¹─►  (Inverse Hist. Equalization) ──AB─►          ← s.46
                                                    U₁ ≈ U₂
```

**AI explanation in one line:** equalization is a *universal* destination — **any** image, equalized, lands on the same uniform distribution. So to make image A look like image B: **equalize A to get there, then run B's equalization backwards to come back down into B's shape.** The composition `H₂⁻¹ ∘ H₁` is the histogram-matching transform, and `U₁ ≈ U₂` is the slide's way of saying the two now coincide.

**Experiment (s.47–49):** the slides show `input` → `Draw something` → `output`, with the note: **"With this concept you can *specify* what you want."** — i.e. you can literally *draw* the target histogram you want and force an image into that shape.

### 7.4 Terminology and Definitions

| Term | Definition as given | Slide |
|---|---|---|
| **Point operation / intensity transformation** | `g(x,y) = T[f(x,y)]` — output pixel depends only on the corresponding input pixel | s.7 |
| **Mapping table** | The input→output lookup that a point operation is equivalent to | s.8 |
| **Gamma (γ)** | "By convention, the exponent in a power-law equation is referred to as gamma" | s.13 |
| **Gamma correction** | "The process used to correct these power-law response phenomena" | s.13 |
| **Contrast** | `(I_max − I_min) / (I_max + I_min)` | s.20 |
| **Contrast stretching** | A piecewise-linear transformation that widens a chosen intensity band | s.20–22 |
| **Histogram** | The tool used to judge whether an image is properly exposed | s.24 |
| **Dynamic range** | "the number of distinct pixel values in an image"; ideally all **K** usable values | s.30 |
| **Clamping** | "Limiting the Results by Clamping" — forcing values back into the valid range | s.32 |
| **Automatic contrast adjustment** | Stretching based on the image's own intensity extremes | s.32 |
| **Histogram equalization** | Spreading the intensities uniformly; mapping the cumulative histogram to a straight line | s.37, 40 |
| **Histogram specification** | Matching one image's histogram to another's, via `H₂⁻¹ ∘ H₁` | s.45–46 |
| **LUMA** | **L**earning-based **U**niversal **M**edia **A**rtist — the class project | s.52 |
| **Reverse proxy (Nginx)** | The single entry point in front of the distributed system | s.54, 68 |
| **Micro web framework** | "Flask is a **micro** web framework written in Python"; a minimalistic framework, contrasted with full-stack ones | s.69 |
| **Routing** | "Modern web apps use a technique named routing. This helps the user remember the URLs." | s.78 |
| **Jinja** | "Jinja is a **template engine** for Python" | s.91 |
| **Template engine** | "a library designed to combine templates with a data model to produce documents" | s.91 |

### 7.5 Formulas and Calculations

| # | Formula (as printed) | Slide | Notes |
|---|---|---|---|
| 1 | `g(x,y) = T[f(x,y)]` | s.7 | The definition of a point operation |
| 2 | `s = c · r^γ` | s.12 | Power-law; `c`, `γ` positive constants |
| 3 | `s = c (r + ε)^γ` | s.12 | Power-law with offset ε |
| 4 | `s = c log(1 + r)` | s.19 | Log transform; `r ≥ 0` |
| 5 | `contrast = (I_max − I_min) / (I_max + I_min)` | s.20 | Michelson contrast (not named on the slide) |

**AI-worked numeric examples** (the slides show the formulas and code, not these numbers):

* **Power-law, using the lecture's own code convention (s.16 code normalises first):** `γ = 2`, `r = 100`
  `(100 / 255)² × 255 = 0.3922² × 255 = 0.1538 × 255 ≈ 39` → a mid-dark pixel gets **much darker**. ✔ γ > 1 darkens.
* **Log transform, using the lecture's own code convention (s.18 code):** `c = 255 / ln(1 + 255) = 255 / 5.545 ≈ 45.99`; for `r = 100`:
  `s = 45.99 × ln(101) = 45.99 × 4.615 ≈ 212` → the same mid-dark pixel is **massively brightened**. ✔ log brightens.
* **Contrast (s.20):** an image with `I_max = 200`, `I_min = 50` → `(200 − 50) / (200 + 50) = 150 / 250 = **0.6**`.
* **Piecewise-linear stretch (s.22 code, `r₁=70, s₁=0, r₂=140, s₂=255`):** a pixel of value `100` falls in the middle band →
  `((255 − 0) / (140 − 70)) × (100 − 70) + 0 = 3.643 × 30 ≈ **109**`. A pixel of `50` → `0`; a pixel of `200` → `255`.

### 7.6 Processes and Procedures

**Procedure 1 — Decide whether an image needs an intensity transformation (s.4, 23–24):**
1. State the **goal**, and the **feature** your algorithm will use (s.4).
2. Don't judge by eye — **compute the histogram** (s.24).
3. Read it: bunched to the left = too dark; bunched to the right = too bright; bunched in a narrow band = low contrast / low **dynamic range** (s.30–31).
4. Remember it is only a summary — different images can share a histogram (s.25).

**Procedure 2 — Choose the transformation (s.43–44, AI-organised from the lecture's own logic):**
* You know the equation you want → **power-law** or **log** (s.12–19).
* You want a uniform spread and don't care about the exact shape → **histogram equalization** (s.36–42).
* You want the image to match a *specific* target image or a *specific* shape → **histogram specification** (s.44–50).
* You want to stretch one particular band and leave the rest → **piecewise-linear contrast stretching** (s.20–22).

**Procedure 3 — Histogram equalization (s.39–40):** compute the histogram → compute the cumulative histogram → use it as the mapping function that straightens the cumulative curve into a line → apply.

**Procedure 4 — Histogram specification (s.45–46):** equalize the input (`H₁`) → apply the **inverse** equalization of the goal image (`H₂⁻¹`) → the result has the goal's histogram (`U₁ ≈ U₂`).

**Procedure 5 — Build the first Flask app (s.72–77):** install everything (s.72) → create the Flask application (s.73) → **[Run]** → open `http://127.0.0.1:5000/` (s.74) → the browser shows an error **because no `[Route]` was defined** (s.75) → add the route (s.76) → run again (s.77).

**Procedure 6 — The five project milestones (s.103), verbatim:**

| | Version 1 | Version 2 | Version 3 | Version 4 | Version 5 |
|---|---|---|---|---|---|
| | **All-in-one Flask** | **Flask + SQLite** | **Flask + Forge** | **Separate Frontend** | **Nginx all Service** |

### 7.7 Code Examples

All transcribed **verbatim** from the slide screenshots.

**Log transform, first attempt (s.10, `Demo03 example1 - DIY1.py`)**
```python
img_output = np.log(img_input)
img_max = np.max(img_output)
img_output = img_output * (255 / img_max)
img_output = np.array(img_output, dtype = np.uint8)
```
The slide asks two questions about exactly this code:
> *ถ้าไม่เปลี่ยนเป็น uint8 จะเกิดอะไรขึ้น ?* — What happens if you **don't** convert to `uint8`?
> *ถ้า data type เป็น float ทำงานได้มั้ย ?* — Will it work if the data type is **float**?

**Power-law / gamma (s.16, `Demo03 example2 - PowerLaw.py`)**
```python
gamma = 2
gamma_corrected = (img_in / 255)**gamma
gamma_corrected = gamma_corrected*255
img_out = np.array(gamma_corrected, dtype = 'uint8')
```
> Note the **normalise → power → re-scale** pattern: divide by 255 so `r ∈ [0,1]`, apply the exponent, multiply back. Without the normalisation, `100**2 = 10000` would overflow `uint8` immediately.
> s.17 suggests: convert numbers to text with `str()`, and **write a `for` loop over γ** to save a series of images at different gamma values.

**Logarithmic transformation (s.18, `Demo03 example3 - Log.py`)**
```python
c = 255 / np.log(1 + np.max(image))
log_image = c * (np.log(1 + image))
log_image = np.array(log_image, dtype = np.uint8)
```
> This is formula 4 (`s = c log(1+r)`) with `c` chosen so that the brightest input maps exactly to 255.

**Piecewise-linear contrast stretching (s.22)**
```python
def pixelVal(pix, r1, s1, r2, s2):
    if (0 <= pix and pix <= r1):
        return (s1 / r1)*pix
    elif (r1 < pix and pix <= r2):
        return ((s2 - s1)/(r2 - r1)) * (pix - r1) + s1
    else:
        return ((255 - s2)/(255 - r2)) * (pix - r2) + s2

r1 = 70
s1 = 0
r2 = 140
s2 = 255

pixelVal_vec = np.vectorize(pixelVal)
contrast_stretched = pixelVal_vec(img, r1, s1, r2, s2)
```
> Three straight lines joined at `(r1,s1)` and `(r2,s2)`. `np.vectorize` applies the scalar function to every pixel.

**Histogram (s.28–29)**
```python
img_gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
histogram = cv.calcHist([img_gray], [0], None, [256], [0, 256])
plt.plot(histogram)
plt.show()
```
> Arguments: `[image]`, `[channel]`, `mask` (None = whole image), `[histSize]` = 256 bins, `[range]` = 0–256. s.29 suggests adding labels and a grid to the plot.

**Histogram equalization (s.38)**
```python
img_out = cv.equalizeHist(img)
```

**Histogram specification (s.50) — transcribed exactly as printed:**
```python
histB  = cv.calcHist([imgB], [0], None, [256], [0, 256])
imgAtoB = cv.equalizeHist(imgA, histB)
```
Slide caption: *ใช้ฟังก์ชั่น `equalizeHist( )` โดยกำหนดเป้าหมายเหมือนกัน (ใส่รูป หรือ histogram ที่ต้องการ)* — "use the `equalizeHist()` function by specifying the same target (pass in the image or the histogram you want)."

> ⚠️ **Concern recorded, not corrected (per the source-accuracy rules).** The code above is reproduced exactly as it appears on s.50. In the standard OpenCV Python API, `cv.equalizeHist()` has the signature `equalizeHist(src[, dst])` — it takes **no target-histogram argument** and always equalizes to a uniform distribution. As written, the second argument would be interpreted as the output array, not as a specification target. Achieving true histogram *specification* normally requires building the mapping `H₂⁻¹ ∘ H₁` by hand (or using `skimage.exposure.match_histograms`). **The original slide content is the source of truth and is recorded above; this note is a separate observation.** → `Needs further verification` (§17).

**Flask — the first application (s.73–85)**
```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    return "<h1>Hello Flask Framework</h1>"

@app.route('/user/<name>/<ID>')
def user(name, ID):
    return "<h1>ยินดีต้อนรับ คุณ {} รหัส [{}] เข้าสู่ระบบ</h1>".format(name, ID)

if __name__ == "__main__":
    app.run(debug=True)
```
* `@app.route('/')` binds a URL to a function (s.79–81).
* `<name>` / `<ID>` are **route parameters** — captured from the URL and passed into the function (s.82–85). s.84 notes you may use an **f-string** instead of `.format()`.
* `debug=True` enables **debug mode** (s.86–88): without it, "We cannot find what wrong in our code."

**Jinja template syntax (s.95–101)**
```jinja
{{ Parameter }}                  {# Display a value #}

{% if condition %}               {# Flow control: if / else #}
    Do this if condition is True
{% else %}
    Do this if condition is False
{% endif %}

{% for item in List %}           {# Flow control: for loop #}
    Do this for each item
{% endfor %}
```
* Rendered from Python with **`render_template`** (s.92); the `.html` files live in a folder named **`templates`**.
* s.94: data is passed as keyword arguments — a **variable in Python** becomes a **parameter name for the html file**.
* s.97: you can pass a **dictionary** (key/value) as a group of data.

### 7.8 Examples from the Lecture

* **Sea Bass (ปลากะพงขาว) vs Salmon** (s.5–6) — the goal/feature question made concrete.
* **The mapping table** (s.8) — 0→0, 1→25, 2→33, 3→56, …, 255→255.
* **Three very different images with identical histograms** (s.25) — the histogram's blind spot.
* **Fourier spectrum display** (s.19) — the classic use of the log transform.
* **Low-contrast → high-contrast pair** (s.41–42) — before/after histogram equalization.
* **"Draw something"** (s.48–49) — hand-draw the target histogram and force the image into it.
* **LUMA** (s.52–53) — the full project brief (below).
* **The `student360.cdti.ac.th` URL** (s.78) — a real, ugly query-string URL (`?q=/modules/Planner/units.php&gibbonSchoolYearID=026&viewBy=class&gibbonCourseID=00230626`) used to motivate clean routing.
* **`127.0.0.1:5000/user/krisada`** (s.79) — the route-parameter example.

#### The LUMA project brief (s.52–53), verbatim

**LUMA = Learning-based Universal Media Artist.** *ปรับแต่ง Style ให้เหมาะสมกับผู้ใช้งานแต่ละคน (User Account Control)* — tailor the style to each individual user.

**Key Features:**
* **AI Generation:** Text / Image-to-Image — type prompts to generate or edit still images; *(Optional)* use a **small LLM** to convert plain text into suitable prompts.
* **Smart Canvas:** layout arrangement, colour palettes; automatic **background removal**; automatic object selection (**segmentation**).
* **Asset Hub:** a searchable resource library (tags, search).

**Target Audience (s.53):** CDTI CPE students (2nd-year juniors / 4th-year seniors); Content Creators & YouTubers (fast, high-quality content — covers, cuts, copyright-free generated images); Digital Artists & Designers (brainstorming, mockups/storyboards for clients).
**UI/UX (s.53):** *Minimalist & Flexible Interface* — the interface changes with the active mode so it never looks cluttered.

#### The distributed system (s.54, repeated s.68), verbatim

```
                    Browser (User)
                          │
                 Nginx (Reverse Proxy)
                          │
        ┌─────────────────┼──────────────────┐
        │                 │                  │
   Frontend          AI Server          Backend (Flask)
 (HTML / CSS / JS)   192.168.1.30         192.168.1.20
   192.168.1.10                                │
                                          Database (SQLite)
                                            192.168.1.20
```
Slide notes: *สมาชิกแต่ละคน ใช้ PC แยก IP Address กัน* (each member uses a PC with a separate IP address) · *ให้ใช้ความรู้จากรายวิชา Network เพื่อทำให้ PCs เชื่อมโยงกัน* (use what you learned in the Network course to link the PCs) · *แต่ละเครื่องทำหน้าที่แตกต่างกัน* (each machine has a different job).

#### The team split (s.55) — *"การแบ่งหน้าที่ในกลุ่ม (ตัวอย่าง)"*, an **example** division

| สมาชิก | หน้าที่ | สิ่งที่ส่งมอบ |
|---|---|---|
| คนที่ 1 | UX/UI Frontend | หน้าเว็บ, Bootstrap, JavaScript |
| คนที่ 2 | Flask Backend | Authentication, API, Database, Logging |
| คนที่ 3 | AI Engineer | Image Generation, Image Editing, Model/LoRA, ทดสอบ API, Queue |
| คนที่ 4 | QA / DevOps | ทดสอบระบบ, เขียนคู่มือ, Deployment, Dashboard, Backup |
| **คนที่ 5 (ถ้ามี)** | **Reverse Proxy, Routing** | *(ช่วยงานส่วนอื่น เพราะภาระงานต่ำ)* — helps with other parts, because the workload is light |

> **Cross-reference:** this is the table that the images in the `Learn` folder implement — see `Learn_Knowledge_Base.md`. There the team is **4 people** and the Nginx/reverse-proxy duty of the optional "คนที่ 5" has been absorbed by **คนที่ 4 (QA/DevOps)**, which the lecture explicitly allows (*ถ้ามี* = "if there is one").

#### Number of PCs (s.56)

* **3-computer example:** `Frontend + Nginx` · `Forge AI` · `Flask + SQLite`
* **4-computer example:** `Frontend + Nginx` · `Forge AI` · `Flask` · `PostgreSQL`

#### Web application background (s.57–67)

* **Old-school web development (s.57):** User Interface (UI) → Processing → Database.
* **Front-End Developer (s.61):** "The main responsibility … is the User interface. Simply put, create things that the user sees."
* **Back-End Developer (s.61):** "can develop **server-side** software" — ❑ Program a server (PHP, ASP, Python, or Node) ❑ Program a database (SQL, SQLite, or MongoDB).
* **Full Stack Web Developer (s.62)** — *"very popular in Thailand…"*. Popular stacks, verbatim:

| Stack | Components |
|---|---|
| **LAMP** | JavaScript · Linux · Apache · MySQL · PHP |
| **LEMP** | JavaScript · Linux · **Nginx** · MySQL · PHP |
| **MEAN** | JavaScript · MongoDB · Express · AngularJS · Node.js |
| **MERN** | JavaScript · MongoDB · Express · React.js · Node.js |
| **MEVN** | JavaScript · MongoDB · Express · Vue.js · Node.js |
| **Django** | JavaScript · Python · Django · MySQL |
| **Ruby on Rails** | JavaScript · Ruby · SQLite · Rails |

* Tech-stack directory (s.63): `https://stackshare.io/stacks`
* Roadmaps (s.65–66) and *"Thing you should learn by yourself: **Responsive Web Design**"* (s.67).

#### Flask (s.69–71)

**s.69, verbatim:** "Flask is a **micro** web framework written in Python. A microframework is a term used to refer to minimalistic web application frameworks. It is contrasted with full-stack frameworks. **It lacks most of the functionality** which is common to expect in a full-fledged web application framework, such as:"

| Missing functionality | Extension the slide recommends |
|---|---|
| Accounts, authentication, authorization, roles | **Flask-Login**, **Flask-JET-Extended** *(as printed — see §17)* |
| Database abstraction via an object-relational mapping | **Flask-SQLAlchemy** |
| Input validation and input sanitation | **Flask-WTF** |

**Advantages / disadvantages (s.70):**
* ✔ Easy to understand development · Small, not rely on many library · Very flexible · Easy to test
* ✘ **Not suitable for big applications**
* *What you need to know before:* HTML5 · CSS · Python
* "Flask is good when you want to build simple, innovative use case to be added in existing application."

**Project structure (s.71), verbatim:**
```
<Project name>
    app.py                 ▪ templates/       หน้า page          (the pages)
    .env                   ▪ static/          CSS, JavaScript, Image
    requirement.txt        ▪ logs/            บันทึกการทำงาน     (activity logs)
    templates/             ▪ app.py           WebApp หลัก        (the main WebApp)
        index.html
    static/
        style.css
    logs/
```
*(the file is printed as `requirement.txt`, singular — see §17)*

**HTTP status codes (s.90), verbatim:**
```
200 OK
400 Bad Request
404 Not Found
500 Internal Server Error
```

**Jinja (s.91):** "Jinja is a **template engine** for Python… a library designed to combine templates with a data model to produce documents… **Now, we can insert python source code to HTML.**" *(The slide plays on the word: Jinja (神社) → Shinto shrine → ศาลเจ้า, with a torii gate.)*

### 7.9 Important Tables, Figures, and Diagrams

| Slide | Figure / Table | What to take from it |
|---|---|---|
| s.7, 43 | **The transformation-curve chart** | Above the diagonal = brighter; steep = more contrast |
| s.8 | **Mapping table** (input → output) | Every point operation is a 256-entry lookup table |
| s.13 | CRT non-linearity | *Why* gamma correction exists |
| s.19 | Fourier spectrum before/after log | The log transform's killer application |
| s.25 | **Three different images, identical histograms** | The histogram's fundamental blind spot |
| s.30–31 | High vs low dynamic range histograms | What "needs stretching" looks like |
| s.39–40 | Histogram → **cumulative histogram** → straight line | The mechanism of equalization |
| s.41–42 | Low-contrast → high-contrast | The result of equalization |
| s.45–46 | **H₁ / H₂⁻¹ block diagram** | The mechanism of histogram specification |
| s.54, 68 | **Distributed system diagram** | The architecture of the LUMA project |
| s.55 | **Team split table** | Who does what (5 roles, the 5th optional) |
| s.56 | 3-PC vs 4-PC deployment | Two acceptable hardware layouts |
| s.62 | **Popular stacks table** | LAMP / LEMP / MEAN / MERN / MEVN / Django / Rails |
| s.71 | **Flask project structure** | `app.py`, `.env`, `templates/`, `static/`, `logs/` |
| s.103 | **Milestone table (V1→V5)** | The order in which to build the project |

### 7.10 Common Mistakes and Important Warnings

**Printed in the lecture:**
* **s.10:** *"ถ้าไม่เปลี่ยนเป็น uint8 จะเกิดอะไรขึ้น?"* — what happens if you don't cast back to `uint8`? *"ถ้า data type เป็น float ทำงานได้มั้ย?"* — will it work as `float`? **(The slide asks; it does not answer.)**
  → **AI answer:** OpenCV's `imshow`/`imwrite` expect `uint8` in 0–255. A `float` array is interpreted on a 0.0–1.0 scale, so an un-cast log/gamma result displays as almost pure white or is silently clipped. This is why *every* code example on these slides ends with `np.array(..., dtype = np.uint8)`.
* **s.25:** three very different images can have identical histograms — never conclude anything about *content* from a histogram.
* **s.32:** results must be **clamped** back into the valid range.
* **s.70:** Flask is **not suitable for big applications**.
* **s.75:** the browser shows an error if you forget to define a `[Route]`.
* **s.87:** with debug mode off, "We cannot find what wrong in our code."

**AI-added warnings (not printed, but implied by the material):**
* **γ direction is easy to invert:** γ > 1 **darkens**; γ < 1 **brightens**. Check against a known pixel before trusting a result.
* **Normalise before you exponentiate** (s.16) — `(img/255)**gamma * 255`, not `img**gamma`, which overflows instantly.
* **Histogram equalization is not always desirable.** It amplifies noise in flat regions (it stretches whatever is there, including sensor noise), and it destroys the original tonal *mood*. If you need a *specific* look, use **specification** (s.44–50), not equalization.
* **Contrast = (Imax−Imin)/(Imax+Imin) is outlier-sensitive** — one dead pixel at 0 pins `I_min` to 0.
* **Never run Flask's development server in production** — and note `debug=True` (s.88) **must** be switched off before deployment; it exposes an interactive debugger that can execute code.

### 7.11 Easy-to-Understand Summary

A **point operation** changes each pixel using only that pixel's own value: `g = T[f]`. Because it ignores neighbours, it's really just a 256-entry lookup table — fast, but incapable of removing blur or noise. The classic curves are **log / nth-root** (bow above the diagonal → brighten shadows) and **power-law / nth-power** (bow below → darken), and the exponent in the power law is **gamma**; correcting a display's built-in power law is **gamma correction**. But how do you *know* an image needs fixing? Not by looking — Lecture 3 proved your eyes lie. You compute the **histogram**, and read it: bunched left = too dark; bunched into a narrow band = low **dynamic range**. Just remember it's a summary, so three different pictures can share one histogram. To fix low contrast automatically, **histogram equalization** takes the cumulative histogram and bends it into a straight line, spreading the intensities out. And when you want an image to look like a *particular other image*, you use **histogram specification**: equalize yours, then run the target's equalization backwards. The second half of the file switches to the **LUMA** web app — a Flask backend on `192.168.1.20`, a frontend on `.10`, an AI server on `.30`, all behind an **Nginx reverse proxy** — built in five milestones from an all-in-one Flask app up to a fully separated, Nginx-fronted service.

### 7.12 Source References

* Intensity transformation: intro **s.3–6**, curve chart **s.7**, mapping table **s.8**, before/after **s.9**, log DIY **s.10**
* Power-law: formula **s.12**, gamma correction & CRT **s.13**, monitor calibration **s.14**, examples **s.15–16**, code hints **s.17–18**
* Log transform: **s.19** · Contrast stretching (Michelson + piecewise-linear): **s.20–22**
* Histogram: motivation **s.23**, definition **s.24**, identical-histogram warning **s.25**, interpretation & moments **s.26–27**, OpenCV `calcHist` **s.28**, matplotlib **s.29**
* Dynamic range: **s.30–31** · Brightness/contrast, clamping, automatic contrast adjustment: **s.32–33** · Modified automatic contrast adjustment: **s.34**
* Histogram equalization: motivation **s.36–37**, code **s.38**, concept (cumulative → straight line) **s.39–40**, low/high contrast **s.41–42**, recap **s.43**
* Histogram specification: motivation **s.44**, block diagrams **s.45–46**, results **s.47**, "draw something" experiment **s.48–49**, code **s.50**
* **Class Project (LUMA):** title **s.51**, brief **s.52**, audience/UX **s.53**, distributed system **s.54**, team split **s.55**, PC count **s.56**
* **Web Application:** old-school **s.57**, modern **s.58–60**, front/back-end roles **s.61**, stacks **s.62**, tech stack **s.63–64**, roadmaps **s.65–66**, responsive design **s.67**
* **Flask:** distributed system repeat **s.68**, micro-framework + extensions **s.69**, pros/cons **s.70**, project structure **s.71**, install **s.72**, first app **s.73–77**, routing **s.78–81**, route parameters **s.82–85**, debug mode **s.86–88**, HTTP status codes **s.89–90**
* **Jinja:** intro **s.91**, `render_template` **s.92**, exercise **s.93**, passing data **s.94**, syntax **s.95–96**, dictionaries **s.97**, if/else **s.98–99**, for loop **s.100–101**
* Project kick-off **s.102** · **Milestones V1–V5: s.103**

---

## 8. Connections Between All Lectures

### 8.1 Shared Concepts Across Files

| Concept | L1 | L2 | L3 | L4 |
|---|---|---|---|---|
| **The image-processing pipeline** | Defined (s.7) | — | Acquisition stage in depth (s.31–59) | Enhancement stage in depth (s.1–50) |
| **"Don't trust the eye — measure"** | — | — | Illusions: *Can we trust our eyes?* (s.9–12) | Histogram: *how can we tell computer?* (s.23–24) |
| **Stable Diffusion / LoRA** | Theory: diffusion, U-Net, VAE, cross-attention, LoRA (s.19–49) | Practice: CFG, seed, samplers, LoRA weights, ControlNet (s.1–62) | — | The AI Server in the LUMA architecture (s.54) |
| **Python / NumPy / OpenCV** | — | — | `imread`/`imshow`/`imwrite`, `ndim`/`shape`, `np.zeros`, `uint8` (s.23–29) | `calcHist`, `equalizeHist`, `np.vectorize`, gamma/log code (s.10–50) |
| **`uint8`, range 0–255** | — | — | Data-type table (s.28); "what if the value is outside 0–255?" (s.30) | Every code example casts back to `uint8`; clamping (s.32) |
| **The LUMA Web App project** | 40 % of the grade (s.6) | The image-generation engine it wraps | — | The full brief + architecture (s.51–56, 103) |
| **Nginx reverse proxy** | — | — | — | s.54, 68; LEMP stack s.62 |
| **Workshops / classwork** | Workshops #1–#4 (s.50–58) | Workshop (s.20) | Camera classwork (s.59) | Flask exercises (s.72, 93) |

**The single thread that runs through all four files (AI):** *make the machine see reliably, then make the machine make pictures.* Files 3 → 4 build the **classical** half (acquire honestly, then transform intensities objectively). Files 1 → 2 build the **generative** half (how diffusion works, then how to control it). Lecture 4's second half is the **bridge**: the LUMA web application, where the classical tools and the generative model are wrapped into one product.

### 8.2 Learning Sequence — the order the material actually builds in

```
L1 s.1–13   What is image processing? · the pipeline · how to find a problem · grading (40 % = Web App)
    │
    ├─► L3 s.1–12    Human vision — and why it cannot be trusted
    │      │
    │      └─► L3 s.13–30   What an image is to a computer (arrays, uint8, OpenCV)
    │              │
    │              └─► L3 s.31–59   Acquisition: optics, aberrations, FOV, sensor choice
    │                      │
    │                      └─► L4 s.1–50   Point operations: curves, gamma, log,
    │                                       histogram, equalization, specification
    │                                       ("how can we TELL the computer it's dark?")
    │
    └─► L1 s.19–49   How Stable Diffusion works (diffusion, U-Net, VAE, cross-attention, LoRA)
           │
           └─► L2 s.1–62   How to CONTROL it (CFG, seed, samplers, X/Y/Z, LoRA,
                            ControlNet, Regional Prompter, img2img)
                   │
                   └─► L4 s.51–103   Wrap it all in a web app: LUMA, Flask, Jinja,
                                      the distributed system, milestones V1→V5
```

**Recommended study order:** **L1 → L3 → L4 (first half) → L1 (AI half) → L2 → L4 (second half).**
**Exam-focused order:** L3 + L4 (first half) carry the formulas and code; L1 + L2 carry the concepts and the vocabulary.

### 8.3 Combined Applications — how the files are used *together*

1. **The LUMA project (the 40 % deliverable)** needs *all four*: L1 for the pipeline and the diffusion theory · L2 for the generation controls the app must expose (CFG, seed, sampler, LoRA, ControlNet, img2img/inpaint) · L3 for the image handling and file I/O · L4 for the Flask/Jinja backend, the architecture, and the intensity tools behind "Smart Canvas".
2. **A quality-assessment sub-system** (item 2 of the 5 project sub-systems, L1 s.6): use L3 to acquire the image correctly, then L4's **histogram** to decide *objectively* whether it needs enhancement, then L4's **gamma / log / stretching / equalization** to fix it.
3. **A camera-selection decision** (L3 s.50–57) is driven by the *problem* framing from L1 s.7 (is this a detection task? a counting task? does the object move?).
4. **Image-to-image editing in LUMA** = L2's `img2img` / Inpaint controls (s.56–61) exposed through L4's Flask routes and Jinja templates.
5. **Explainability** (L1 s.15–18, Grad-CAM) is the natural "Evaluation" stage (item 5 of L1 s.6) for any classifier the project ends up training.

### 8.4 Important Differences Between the Files

| | **Lecture 1** | **Lecture 2** | **Lecture 3** | **Lecture 4** |
|---|---|---|---|---|
| **Register** | Survey / motivation | Hands-on tool manual | Physics + programming primer | Mathematics + software engineering |
| **Deliverable it serves** | Choosing a project topic | The generation workshops | The camera classwork (s.59) | The LUMA web app + the exam formulas |
| **What "an image" means** | A thing to be understood | A thing to be *generated* | A grid of `uint8` numbers | A histogram / a distribution |
| **Direction of work** | Image → meaning | Text → image | World → image | Image → better image |
| **Number of decks in the file** | 1 | 1 | **2** | **3** |

**The most important structural fact:** two of the four file *names* under-describe their contents. `Lecture 3 - Human Visual Perception.pdf` is only *20 %* about human visual perception — the remaining 47 slides are **Fundamental Operation** (Python, OpenCV, optics, FOV). `Lecture 4 - Point Operation.pdf` is only *half* about point operations — the other half is the **LUMA class project and the entire Flask/Jinja web-development course**. Anyone searching these files by name will miss most of the syllabus.

### 8.5 Contradictions or Inconsistencies Between Files

Recorded, **not corrected** (per the source-accuracy rules). Details in §17.

| # | The inconsistency | Where |
|---|---|---|
| 1 | **`requirements.txt` vs `requirement.txt`** — L3 s.20 uses the plural (`pip freeze > requirements.txt`, `pip install -r requirements.txt`, which is the form the commands actually require); the Flask project structure on L4 s.71 prints the singular **`requirement.txt`**. | L3 s.20 vs L4 s.71 |
| 2 | **`Flask-JET-Extended`** (L4 s.69) — the extension for JWT authentication is universally published as **Flask-JWT-Extended**, and the `Learn` folder's own tool table (`5.jpg`) writes it as **Flask-JWT-Extended**. Recorded as printed. | L4 s.69 |
| 3 | **Team size: 5 vs 4.** L4 s.55 lists five roles, the fifth (**Reverse Proxy, Routing**) marked *ถ้ามี* — "if there is one" — with a light workload. The `Learn` images document a **4-person** team in which QA/DevOps absorbs the Nginx work. These are consistent *only because* the lecture marks role 5 as optional. | L4 s.55 vs `Learn/1.jpg`, `Learn/9.jpg` |
| 4 | **`cv.equalizeHist(imgA, histB)`** (L4 s.50) does not match the documented OpenCV signature `equalizeHist(src[, dst])`. | L4 s.50 |
| 5 | **Windows-only activation path.** L3 s.19 gives `env/Scripts/activate.bat` with no macOS/Linux equivalent, even though s.18 links a *macOS* PIP guide. | L3 s.18 vs s.19 |
| 6 | **Divide-Ratio reading** in the Regional Prompter (L2 s.49): the stated rule ("the first number is the row height, the rest are the region widths") is unambiguous for the multi-row examples but reads ambiguously for the single-row case `Horizon (1,1,1)`, which produces three columns. | L2 s.49 vs s.50–54 |

**No outright factual contradiction exists between the four files' *technical content*.** Every item above is a typo, an optional-role difference, or a platform omission — not two files teaching opposite things.

---

## 9. Master Formula Reference

Every formula that appears anywhere in the four lectures, with its source.

| # | Formula | Meaning | Variables (as defined in the lecture) | Source |
|---|---|---|---|---|
| 1 | `g(x,y) = T[ f(x,y) ]` | **Point operation** — output pixel = a function of the input pixel alone | `f` = input image, `g` = output image | **L4 s.7** |
| 2 | `s = c · r^γ` | **Power-law (gamma) transformation** | `r` = input intensity, `s` = output intensity, `c` & `γ` positive constants | **L4 s.12** |
| 3 | `s = c (r + ε)^γ` | Power-law **with offset** (a measurable output when the input is zero) | `ε` = offset | **L4 s.12** |
| 4 | `s = c · log(1 + r)` | **Logarithmic transformation** | `c` = constant, `r ≥ 0` | **L4 s.19** |
| 5 | `contrast = (I_max − I_min) / (I_max + I_min)` | **Contrast** (Michelson form; the name is not given on the slide) | `I_max`, `I_min` = brightest / darkest intensity | **L4 s.20** |
| 6 | Piecewise-linear: `(s1/r1)·p` · `((s2−s1)/(r2−r1))·(p−r1)+s1` · `((255−s2)/(255−r2))·(p−r2)+s2` | **Contrast stretching** — three joined line segments | `p` = pixel, `(r1,s1)` & `(r2,s2)` = the break points | **L4 s.22 (code)** |
| 7 | `n₁ sin α₁ = n₂ sin α₂` | **Snell's law** — refraction at a boundary | `α₁` incident angle, `α₂` refraction angle, `nᵢ` index of refraction | **L3 s.46** |
| 8 | `θ = 2 · tan⁻¹( sensor size / 2f )` | **Angle of view** | `f` = focal length | **L3 s.55** |
| 9 | `FOV = 2 · ( S₀ · tan(θ/2) )` | **Field of view** | `S₀` = distance to object | **L3 s.55** |
| 10 | *(AI shortcut, not on any slide)* `FOV ≈ S₀ × (sensor size / f)` | Formulas 8 + 9 composed; the tangents cancel | — | **AI-derived from L3 s.55** |
| 11 | Emphasis: `(word)` = ×1.1 · `((word))` = ×1.21 · `[word]` = ÷1.1 · `(word:1.5)` = ×1.5 · `(word:0.25)` = ÷4 | **Prompt attention weighting** (AUTOMATIC1111) | — | **L2 s.11–12** |
| 12 | Latent tensor `4 × 64 × 64` vs pixel tensor `3 × 512 × 512` | The **48× compression** of latent space | 16,384 vs 786,432 values → ratio 48 | **L1 s.31, s.41** |
| 13 | Embedding = a **768-value** vector per token | Text conditioning | — | **L1 s.36** |

> **Reading note:** formulas 1–6 are the examinable *point-operation* mathematics; 7–10 are the examinable *acquisition* mathematics. Formulas 11–13 are numeric facts from the generative-AI half, not equations to manipulate.

---

## 10. Master Terminology Reference

| Term | Short definition | Source |
|---|---|---|
| **Digital image processing** | Using computer algorithms to manipulate images (enhancement, detection, segmentation, …) | L1 s.1 |
| **Image → Image / Image → Descriptor / Image → Recognition** | The three possible outputs of an image-processing system | L1 s.2 |
| **The pipeline** | Visual Problem Domain → Image Acquisition → Image Enhancement → Feature Extraction → Object Recognition → Image Understanding | L1 s.7 |
| **The 5 project sub-systems** | Acquisition · Quality Assessment & Enhancement · Segmentation · Feature Extraction → Classification/Analysis · Evaluation | L1 s.6 |
| **Diffusion model** | A generative deep-learning model; forward diffusion adds noise, reverse diffusion removes it | L1 s.21–25 |
| **Drift / Random motion** | The two parts of every diffusion process | L1 s.26 |
| **Noise predictor** | The network that predicts how much noise was added — **a U-Net** | L1 s.27 |
| **Latent diffusion / latent space** | Stable Diffusion compresses the image first; the latent space is **48× smaller** | L1 s.31 |
| **VAE (Variational Autoencoder)** | Encoder compresses to latent space; decoder restores the image | L1 s.33 |
| **Conditioning** | Steering the noise predictor so the result is what you asked for | L1 s.35 |
| **Tokenizer / token / embedding** | Prompt word → number → **768-value vector** | L1 s.36 |
| **Cross-attention** | Where the prompt meets the image inside the U-Net | L1 s.38 |
| **Checkpoint / base model** | The large trained model (SD v1.5, SDXL, Flux.1 dev) | L1 s.46 |
| **LoRA** | Small add-on that patches the **cross-attention layers** — customises style without huge files | L1 s.47 |
| **Textual inversion / LyCORIS / hypernetwork** | The other non-checkpoint model types | L1 s.47 |
| **CFG scale** | How strictly the image must obey the prompt (0–20; **use 8–14**) | L2 |
| **Seed** | The random-tensor selector; **−1 = random** | L2 |
| **Sampling steps** | How many denoise iterations (typically 20–60) | L2 |
| **Sampler** | The denoising algorithm (Euler a, Heun, DPM++ SDE Karras, DDIM, …) | L2 |
| **ControlNet** | Conditions generation on a reference structure (OpenPose, Canny, Depth) | L2 s.21–43 |
| **Regional Prompter** | Splits the canvas into regions, each with its own prompt (BREAK, Divide Ratio) | L2 s.44–55 |
| **img2img / Inpaint** | Generate from an existing image / regenerate only a masked part | L2 s.56–61 |
| **Denoising strength** | How far img2img is allowed to depart from the source image | L2 s.56–61 |
| **Cornea / Lens / Retina** | The eye's front cover / the 60–70 % water focusing element / the sensor containing cones and rods | L3 s.2–3 |
| **Liquid lens** | Water & oil lens; telephoto + macro from one element | L3 s.6–7 |
| **Koffka ring** | The illusion proving that perceived brightness is relative | L3 s.9–10 |
| **`(r, c)` / `img[y, x]`** | Image indexing: **row first, column second** | L3 s.16 |
| **Channel** | One of the R / G / B planes | L3 s.17 |
| **Virtual environment** | An isolated Python interpreter + libraries per project | L3 s.19 |
| **`uint8`** | Unsigned 8-bit integer, **0–255** — the image data type | L3 s.28 |
| **Pinhole camera / camera obscura** | The simplest imaging device: a hole projects an inverted image | L3 s.32–35 |
| **Focal length (f)** | Where parallel rays converge | L3 s.42 |
| **Circle of confusion** | The blur disc from points not at the focus distance | L3 s.43 |
| **Thin lens** | The approximation used in place of real multi-element glass | L3 s.45 |
| **Spherical / chromatic aberration** | Edge rays focus early / colours focus differently (colour fringing) | L3 s.47 |
| **Barrel / pin-cushion distortion** | Straight lines bow out / in | L3 s.49 |
| **Angle of view / Field of view** | Derived from sensor+f / from angle+distance | L3 s.53–56 |
| **CCD vs CMOS** | Global shutter, low noise, slow / rolling shutter, fast, **skew** | L3 s.57 |
| **Point operation** | `g = T[f]`, pixel-by-pixel, no neighbours | L4 s.7 |
| **Mapping table** | The 256-entry lookup a point operation reduces to | L4 s.8 |
| **Gamma / gamma correction** | The power-law exponent / correcting a device's power-law response | L4 s.13 |
| **Contrast stretching** | Piecewise-linear widening of a chosen intensity band | L4 s.20–22 |
| **Histogram** | The count of pixels at each intensity — the objective exposure tool | L4 s.24 |
| **Dynamic range** | The number of distinct pixel values actually used | L4 s.30 |
| **Clamping** | Forcing results back into the legal range | L4 s.32 |
| **Automatic / Modified automatic contrast adjustment** | Stretch using the image's own extremes / a robust, outlier-tolerant version | L4 s.32, 34 |
| **Histogram equalization** | Map the cumulative histogram to a straight line → uniform spread | L4 s.37–40 |
| **Histogram specification (matching)** | `H₂⁻¹ ∘ H₁` — make image A take on image B's histogram | L4 s.45–46 |
| **LUMA** | Learning-based Universal Media Artist — the class project | L4 s.52 |
| **Reverse proxy (Nginx)** | The single public entry point in front of the three PCs | L4 s.54 |
| **Micro web framework** | Flask — minimal by design; extensions add the rest | L4 s.69 |
| **Routing / route parameter** | URL → function binding / `<name>` captured from the URL | L4 s.78–85 |
| **Jinja / template engine** | Combines templates with a data model to produce HTML | L4 s.91 |
| **`{{ }}` / `{% %}`** | Jinja: display a value / flow control | L4 s.95 |

---

## 11. Problem-Solving Framework

**A general procedure for any problem posed by this course, assembled from the lectures' own rules.**

### Step 1 — Frame the problem (L1 s.5, s.7)
> *"ถ้าโจทย์ปัญหายาก ให้ใช้วิธีกำหนดเงื่อนไข, ขอบเขตของงาน, แบ่งเป็นงานย่อย"* (L1 s.5)
> **If the problem is hard: impose conditions, bound the scope, split it into sub-tasks.**

Ask L4 s.4's two questions before anything else:
* **What goal am I aiming for?**
* **What feature will my algorithm use?**

### Step 2 — Decide which stage of the pipeline you are in (L1 s.7)
`Visual Problem Domain → Image Acquisition → Image Enhancement → Feature Extraction → Object Recognition → Image Understanding`
Most exam and homework questions live in **Acquisition** (L3) or **Enhancement** (L4).

### Step 3 — Fix acquisition before you write code (L3)
* Control the scene — the moulting case study only worked because a **lighting enclosure** was built first (L1 s.10).
* Choose the sensor from the 5-point checklist (L3 s.50); if the subject moves, **CCD/global shutter**, not CMOS/rolling (L3 s.57).
* Compute the **FOV** to confirm the object actually fits in frame (L3 s.55) — and check your units (L3 s.56).
* Check for **distortion** and **colour fringing** in a test shot (L3 s.49, s.59).

### Step 4 — Measure, don't look (L3 s.9–12 → L4 s.23–24)
Compute the **histogram**. Read it:

| Histogram shape | Diagnosis | Fix |
|---|---|---|
| Bunched at the left | Under-exposed / too dark | Log transform, or γ < 1 |
| Bunched at the right | Over-exposed / too bright | γ > 1 |
| Bunched in a narrow band anywhere | Low **dynamic range** / low contrast | Contrast stretching, or histogram equalization |
| Spread across the full 0–255 | Properly exposed | Leave it alone |
| Needs to match another image | — | **Histogram specification** |

### Step 5 — Apply the transformation, then re-measure
1. Convert to the right type; **normalise before exponentiating** (L4 s.16).
2. Apply the point operation.
3. **Clamp** (L4 s.32) and cast back to **`uint8`** (L3 s.28; every L4 code example).
4. **Plot the histogram again** — it is the evidence that the fix worked (L4 s.33: *"Try to plot and see Histogram by yourself :)"*).

### Step 6 — Evaluate (L1 s.6, item 5)
Every project must include **Evaluation**. In the moulting case study that meant a chart of the measured feature over time for both classes (L1 s.13) — a plot that *proves the feature separates the classes*. Do the equivalent.

### For a generative-AI problem instead (L1 → L2)
1. Choose the **base model** (SD v1.5 / SDXL / Flux.1 dev) — L1 s.46.
2. Write the prompt; use **emphasis syntax** to weight it — L2 s.11–12.
3. Set **CFG** (8–14) and **sampling steps** (20–60); fix the **seed** to make results reproducible — L2.
4. Need a *specific pose or composition*? → **ControlNet** (OpenPose / Canny / Depth) — L2 s.21–43.
5. Need *different things in different areas*? → **Regional Prompter** — L2 s.44–55.
6. Need to *edit an existing image*? → **img2img / Inpaint**, and tune **denoising strength** — L2 s.56–61.
7. Need a *consistent character or style*? → **LoRA** — L1 s.47, L2 s.17–19.
8. Sweep a parameter systematically with the **X/Y/Z plot** rather than guessing — L2 s.13–17.

### For a web-app problem (L4 s.51–103)
1. Which milestone are you on? V1 all-in-one → V2 +SQLite → V3 +Forge → V4 separate frontend → V5 Nginx (s.103).
2. Which machine owns the work? Frontend `.10` · Backend `.20` · AI `.30` (s.54).
3. New page → a **route** (`@app.route`) + a **template** (`render_template` + Jinja) (s.79, s.92).
4. Something broken? Turn on **debug mode** (s.88) and read the **HTTP status code** (s.90).

---

## 12. Common Mistakes and Misconceptions

| # | Mistake | Why it's wrong | Source |
|---|---|---|---|
| 1 | **"The image looks too dark, so I'll brighten it."** | Your eyes report *relative* brightness — the Koffka ring proves it. Judge by **histogram**, not by looking. | L3 s.9–12; L4 s.23–24 |
| 2 | **Forgetting to cast back to `uint8`.** | A float result is interpreted on a 0.0–1.0 scale by OpenCV and displays as near-white/clipped. Every lecture code example ends with `np.array(..., dtype=np.uint8)`. | L3 s.28; L4 s.10, 16, 18 |
| 3 | **Exponentiating raw pixel values** (`img**gamma`). | Overflows `uint8` instantly. The lecture's own code **normalises first**: `(img/255)**gamma * 255`. | L4 s.16 |
| 4 | **Assuming values outside 0–255 are "just clipped".** | In `uint8` they **wrap around** — 256 becomes 0, so an over-bright pixel turns *black*. That is what **clamping** is for. | L3 s.30; L4 s.32 |
| 5 | **Indexing `img[x, y]`.** | NumPy/OpenCV images are **`img[row, column] = img[y, x]`**, and `.shape` is `(height, width)`. | L3 s.16, s.25–26 |
| 6 | **Getting the gamma direction backwards.** | **γ > 1 darkens; γ < 1 brightens.** Verify against one known pixel before trusting the whole image. | L4 s.12–16 |
| 7 | **Concluding things about image *content* from a histogram.** | "Three very different images with identical histograms" — the histogram discards all spatial information. | L4 s.25 |
| 8 | **Using histogram equalization for everything.** | It forces a *uniform* spread, amplifies noise, and destroys the original tonal intent. If you need a specific look, use **specification**. | L4 s.36–50 |
| 9 | **Thinking a point operation can remove noise or blur.** | `g = T[f]` sees one pixel at a time. Noise and blur are *neighbourhood* phenomena. | L4 s.7 |
| 10 | **Mixing units in the FOV calculation.** | The lecture warns explicitly; the FOV comes out in the unit of the **object distance**. | L3 s.56 |
| 11 | **Choosing CMOS for fast-moving subjects.** | Rolling shutter ⇒ **skew**. Global shutter (CCD) does not skew. | L3 s.57 |
| 12 | **Believing optics defects can be fixed later.** | Barrel distortion, chromatic fringing and out-of-focus blur are baked in at capture. Fix the lighting, the lens and the framing *first*. | L3 s.43–49; L1 s.5, s.10 |
| 13 | **Forgetting to define a route in Flask.** | The browser returns an error — the lecture shows exactly this failure. | L4 s.75 |
| 14 | **Leaving `debug=True` on in production.** | Debug mode is a development aid; the lecture only frames it as "we cannot find what's wrong without it" (s.87), but shipping it exposes an interactive debugger. *(AI-added warning.)* | L4 s.86–88 |
| 15 | **Assuming the file names describe the files.** | `Lecture 3` is mostly *Fundamental Operation*; `Lecture 4` is half *web development*. | §8.4 |

---

## 13. Quick Decision Guide

| If you need to… | Use | Where |
|---|---|---|
| Decide whether an image needs enhancing at all | **Histogram** (+ mean/variance/skew/kurtosis) | L4 s.24–27 |
| Brighten dark detail (huge dynamic range, e.g. a Fourier spectrum) | **Log transform** `s = c·log(1+r)` | L4 s.19 |
| Brighten or darken with a single tunable knob | **Power-law / gamma** `s = c·r^γ` (γ<1 brightens, γ>1 darkens) | L4 s.12 |
| Correct a display's or camera's non-linear response | **Gamma correction** | L4 s.13 |
| Widen one specific intensity band and keep the rest | **Piecewise-linear contrast stretching** | L4 s.20–22 |
| Spread intensities out automatically, no parameters | **Histogram equalization** (`cv.equalizeHist`) | L4 s.36–42 |
| Make image A look like image B (or like a drawn target) | **Histogram specification** (`H₂⁻¹ ∘ H₁`) | L4 s.44–50 |
| Stop values escaping 0–255 | **Clamping** + cast to `uint8` | L4 s.32; L3 s.28 |
| Know how much of the scene fits in frame | **θ = 2 tan⁻¹(sensor/2f)** then **FOV = 2·S₀·tan(θ/2)** | L3 s.55 |
| Photograph something that moves fast | **CCD / global shutter** (CMOS rolling shutter skews) | L3 s.57 |
| Photograph in low light with minimal noise | **CCD** (low noise floor, more sensitive at low intensity) | L3 s.57 |
| Get high frame rates cheaply | **CMOS** | L3 s.57 |
| Create an empty image to draw on | `np.zeros([h, w], dtype=np.uint8)` | L3 s.27–29 |
| Read / show / save an image | `cv.imread` / `cv.imshow` / `cv.imwrite` (+ `cv.waitKey(0)`) | L3 s.23–24 |
| Generate an image from text | **txt2img** with a base model | L1 s.40–43 |
| Reproduce an earlier generation exactly | Fix the **Seed** (−1 = random) | L2 |
| Make the model obey the prompt more strictly | Raise **CFG** (use 8–14) | L2 |
| Enforce a specific pose / outline / depth | **ControlNet** (OpenPose / Canny / Depth) | L2 s.21–43 |
| Put different subjects in different parts of the canvas | **Regional Prompter** (BREAK, Divide Ratio) | L2 s.44–55 |
| Edit an existing image | **img2img** (Sketch / Inpaint / Inpaint-Sketch) + denoising strength | L2 s.56–61 |
| Keep one consistent character or art style | **LoRA** (`<lora:name:weight>`) | L1 s.47; L2 s.17–19 |
| Compare many parameter values at once | **X/Y/Z Plot** | L2 s.13–17 |
| Serve a web page from Python | **Flask** + `@app.route` + `render_template` | L4 s.79, s.92 |
| Put Python data into HTML | **Jinja**: `{{ value }}`, `{% if %}`, `{% for %}` | L4 s.95–101 |
| Let one address reach three machines | **Nginx reverse proxy** | L4 s.54, 68 |
| Decide what to build next in the project | The **milestones**: V1→V2→V3→V4→V5 | L4 s.103 |

---

## 14. Review Questions and Answers

> Every question in this section is an **`AI-generated practice question based on the lecture content`**. The questions were written by AI; the **answers are traceable to the slides cited**. None of these questions appeared on any slide.

### 14.1 Basic Recall

**Q1.** *`AI-generated practice question based on the lecture content`* — What are the three possible outputs of an image-processing system?
**A.** **Image → Image**, **Image → Descriptor**, and **Image → Recognition/Classification**. *(L1 s.2)*

**Q2.** *`AI-generated practice question based on the lecture content`* — State the six stages of the image-processing pipeline in order.
**A.** Visual Problem Domain → Image Acquisition → Image Enhancement → Feature Extraction → Object Recognition → Image Understanding. *(L1 s.7)*

**Q3.** *`AI-generated practice question based on the lecture content`* — How is the course assessed?
**A.** Homework and in-class problems **30 %**, the image-processing project (**Web App**) **40 %**, final exam **30 %**. *(L1 s.6)*

**Q4.** *`AI-generated practice question based on the lecture content`* — What data type does an 8-bit grayscale image use, and what is its range?
**A.** **`uint8`** — unsigned integer, **0 to 255**. *(L3 s.28)*

**Q5.** *`AI-generated practice question based on the lecture content`* — In OpenCV, what does `img.shape` return for a grayscale image, and in what order?
**A.** A tuple of **(height, width)** — height first. In the lecture's example it prints `(1440, 1080)`, i.e. height 1440, width 1080. *(L3 s.25–26)*

**Q6.** *`AI-generated practice question based on the lecture content`* — Which neural-network architecture is the **noise predictor** in Stable Diffusion?
**A.** A **U-Net**. *(L1 s.27)*

**Q7.** *`AI-generated practice question based on the lecture content`* — What are the two parts of every diffusion process?
**A.** **(1) Drift** *(แนวโน้มทิศทางเฉพาะ)* and **(2) Random motion** *(การเคลื่อนแบบสุ่ม)*. *(L1 s.26)*

**Q8.** *`AI-generated practice question based on the lecture content`* — Name the five sub-systems into which the class project divides an image-processing system.
**A.** Image Acquisition · Quality Assessment & Enhancement · Segmentation · Feature Extraction → Classification/Analysis · Evaluation. *(L1 s.6)*

### 14.2 Conceptual Understanding

**Q9.** *`AI-generated practice question based on the lecture content`* — Lecture 3 spends twelve slides on optical illusions. What does this have to do with programming?
**A.** It establishes that human brightness perception is **relative and unreliable** (the Koffka ring, L3 s.9–10). Therefore "this image looks too dark" is not something a computer can act on. Lecture 4 s.23 asks the follow-up directly — *"We know, this image too dark right? But how can we tell computer?"* — and answers it with the **histogram** (s.24). The illusions are the motivation for objective measurement.

**Q10.** *`AI-generated practice question based on the lecture content`* — Why can a point operation never remove blur or noise?
**A.** By definition `g(x,y) = T[f(x,y)]` (L4 s.7): the output pixel depends **only on the corresponding input pixel**, never on its neighbours. Blur and noise are relationships *between* neighbouring pixels, so no pixel-wise lookup can address them. This is also why a point operation reduces to a 256-entry **mapping table** (L4 s.8).

**Q11.** *`AI-generated practice question based on the lecture content`* — Explain in your own words how histogram equalization works.
**A.** Build the histogram, then the **cumulative** histogram. If the intensities were perfectly uniform, that cumulative curve would be a straight diagonal. Equalization uses the cumulative histogram itself as the mapping function, which **bends the actual curve into that straight line** — the lecture's own phrasing on L4 s.40: *สร้าง mapping function จาก Cumulative Histogram ไปหา "เส้นตรง"*. The effect is to spread a clumped, low-contrast histogram (s.41) across the full range (s.42).

**Q12.** *`AI-generated practice question based on the lecture content`* — What problem does histogram **specification** solve that equalization cannot?
**A.** Equalization always lands on the *same* uniform distribution — you cannot choose the destination. Specification lets you target **a particular image's histogram** (L4 s.44: *"Wanna make left image look like a right image"*). It works by equalizing the input (`H₁`), then applying the **inverse** equalization of the goal image (`H₂⁻¹`), so that `U₁ ≈ U₂` (L4 s.45–46). L4 s.48–49 shows you can even hand-draw the target.

**Q13.** *`AI-generated practice question based on the lecture content`* — Why is Stable Diffusion called a **latent** diffusion model, and what does that buy?
**A.** Instead of denoising in the high-dimensional pixel space, it first compresses the image into a **latent space that is 48× smaller** using the **VAE encoder**, denoises there, then decodes back with the **VAE decoder** (L1 s.31–34). The payoff is speed and memory: the un-compressed version "is computationally very, very slow. You won't be able to run on any single GPU" (L1 s.31).

**Q14.** *`AI-generated practice question based on the lecture content`* — Where exactly does the text prompt "meet" the image inside Stable Diffusion?
**A.** In the **cross-attention** layers of the U-Net (L1 s.38: *"That's where the prompt meets the image"*). The prompt is tokenized, each token becomes a **768-value embedding**, the text transformer processes them, and the U-Net consumes the result via cross-attention (L1 s.36–38). This is also *why* **LoRA** works by patching precisely those cross-attention layers (L1 s.47).

**Q15.** *`AI-generated practice question based on the lecture content`* — What is the practical difference between a global and a rolling shutter?
**A.** A **global** shutter (CCD) exposes the whole sensor at the same instant; a **rolling** shutter (CMOS) exposes row by row, so a fast-moving subject is captured at slightly different times down the frame and appears **skewed**. The CCD/CMOS table lists exactly this: Shutter type Global vs Rolling, Skew **No** vs **Yes** (L3 s.57).

**Q16.** *`AI-generated practice question based on the lecture content`* — Why is Flask called a *micro* framework, and what follows from that?
**A.** Because it is deliberately minimal and "**lacks most of the functionality** which is common to expect in a full-fledged web application framework" (L4 s.69). What follows is that you must add the missing pieces yourself via extensions: **Flask-Login / Flask-JET-Extended** for auth, **Flask-SQLAlchemy** for the ORM, **Flask-WTF** for validation (s.69). Its stated weakness is that it is "**not suitable for big applications**" (s.70). *(The extension name is reproduced as printed on the slide; see §17.)*

### 14.3 Calculation

**Q17.** *`AI-generated practice question based on the lecture content`* — A camera has a 36 mm sensor dimension and a 50 mm lens. (a) What is the angle of view? (b) What is the field of view at 2 m?
**A.** Using L3 s.55:
(a) `θ = 2·tan⁻¹(36 / (2×50)) = 2·tan⁻¹(0.36) = 2 × 19.80° = **39.60°**`
(b) `FOV = 2·(2 m · tan(19.80°)) = 2 × 2 × 0.36 = **1.44 m**`
*Sanity check with the shortcut `FOV ≈ S₀ × sensor/f` = 2 × 36/50 = 1.44 m ✔.* Note the answer is in **metres**, because the object distance was in metres (L3 s.56).

**Q18.** *`AI-generated practice question based on the lecture content`* — An image has `I_max = 200` and `I_min = 50`. Compute its contrast.
**A.** Using L4 s.20: `(200 − 50)/(200 + 50) = 150/250 = **0.6**`.

**Q19.** *`AI-generated practice question based on the lecture content`* — Apply the lecture's power-law code (L4 s.16) with `γ = 2` to a pixel of value 100. What is the output?
**A.** The code normalises first: `(100/255)² × 255 = 0.3922² × 255 = 0.1538 × 255 ≈ **39**`. The pixel gets much darker — confirming that **γ > 1 darkens**.

**Q20.** *`AI-generated practice question based on the lecture content`* — Apply the lecture's log-transform code (L4 s.18) to the same pixel (value 100), assuming the image's maximum is 255.
**A.** `c = 255 / ln(1 + 255) = 255 / 5.545 ≈ 45.99`; then `s = 45.99 × ln(1 + 100) = 45.99 × 4.615 ≈ **212**`. The same pixel is strongly brightened — the log transform lifts dark tones.

**Q21.** *`AI-generated practice question based on the lecture content`* — Using the contrast-stretching parameters from L4 s.22 (`r1=70, s1=0, r2=140, s2=255`), what do pixels of value 50, 100 and 200 become?
**A.**
* `50` → first segment: `(0/70) × 50 = **0**`
* `100` → middle segment: `((255−0)/(140−70)) × (100−70) + 0 = 3.643 × 30 ≈ **109**`
* `200` → third segment: `((255−255)/(255−140)) × (200−140) + 255 = **255**`
Everything below 70 is crushed to black, everything above 140 to white, and the 70–140 band is stretched across the full range.

**Q22.** *`AI-generated practice question based on the lecture content`* — Verify the "48× smaller" claim for Stable Diffusion's latent space.
**A.** A pixel-space image is `3 × 512 × 512 = 786,432` values; the latent tensor is `4 × 64 × 64 = 16,384` values (L1 s.31, s.41). `786,432 / 16,384 = **48**` ✔.

**Q23.** *`AI-generated practice question based on the lecture content`* — In AUTOMATIC1111 prompt syntax, what weight does `((sunset))` carry, and how would you write the same weight explicitly?
**A.** Each pair of parentheses multiplies by 1.1, so `((sunset))` = `1.1 × 1.1` = **×1.21**. Written explicitly: `(sunset:1.21)`. *(L2 s.11–12)*

### 14.4 Application

**Q24.** *`AI-generated practice question based on the lecture content`* — You must photograph bottles moving quickly along a conveyor belt and check each label is present. Which sensor do you choose, and why?
**A.** **CCD (global shutter)**. A CMOS rolling shutter exposes row by row, so fast-moving bottles would come out **skewed** (L3 s.57) and a label-alignment check would produce false failures. Then follow the rest of L3 s.50: compute the required **FOV** so the whole bottle fits (s.55), pick the resolution needed to *identify* (not merely detect) the label, and — following L1 s.5 and s.10 — build a **controlled lighting enclosure** first, because that is what made the moulting case study work at all.

**Q25.** *`AI-generated practice question based on the lecture content`* — An X-ray image is very dark; nearly all its histogram mass is squeezed against 0, but the few bright values span a huge range. Which transformation, and why?
**A.** The **log transform** `s = c·log(1+r)` (L4 s.19). Its curve is steepest near zero, so it **expands the dark detail** while compressing the few very bright values — exactly the property the lecture demonstrates on the **Fourier spectrum display**, which has the same enormous-dynamic-range problem. Set `c = 255/ln(1+max)` so the brightest input maps to 255 (L4 s.18 code), then cast back to `uint8`.

**Q26.** *`AI-generated practice question based on the lecture content`* — You have 200 photographs of the same subject taken by different students' phones. They must be visually consistent for a report. What do you do?
**A.** This is exactly the motivating scenario on L4 s.36 ("adjust two different images in such a way that their resulting intensity distributions are similar… to use them in a print publication"). Two options: **histogram equalization** on every image (uniform spread, no reference needed, L4 s.38), or better — pick one good reference image and apply **histogram specification** to the other 199 so they all take on *its* histogram (L4 s.44–46). Specification is the right choice here because it preserves a chosen *look*, whereas equalization forces a uniform distribution on everyone.

**Q27.** *`AI-generated practice question based on the lecture content`* — In LUMA, a user uploads a photo and asks for the same pose with a different character. Which tools?
**A.** **ControlNet + OpenPose** to extract and re-impose the skeleton from the uploaded photo (L2 s.31–35), with the new character described in the prompt — optionally locked in by a **LoRA** (L1 s.47; L2 s.17–19). If they want to keep parts of the original picture, use **img2img** and tune the **denoising strength** (L2 s.56–61); if they want to replace only a region, use **Inpaint** (L2 s.60). Architecturally the request goes Browser → **Nginx** (`192.168.1.10`) → **Flask** (`.20`) → **AI Server** (`.30`) (L4 s.54).

**Q28.** *`AI-generated practice question based on the lecture content`* — Your Flask page must greet a user by name from the URL `.../user/somchai/6412345`. Write the route.
**A.**
```python
@app.route('/user/<name>/<ID>')
def user(name, ID):
    return "<h1>ยินดีต้อนรับ คุณ {} รหัส [{}] เข้าสู่ระบบ</h1>".format(name, ID)
```
The `<name>` and `<ID>` placeholders are **route parameters**, captured from the URL and passed as function arguments (L4 s.82–85). An f-string works equally well (s.84).

### 14.5 Analysis

**Q29.** *`AI-generated practice question based on the lecture content`* — Two images have identical histograms. Can you conclude they look the same? What does this imply about using histograms as a quality metric?
**A.** No — L4 s.25 shows explicitly *"Three very different images with identical histograms."* The histogram counts **how many** pixels hold each value but discards **where** they are, so all spatial structure is invisible to it. The implication: a histogram is a reliable tool for judging **exposure and dynamic range** (which is precisely what L4 s.24 and s.30 use it for), but it is worthless as a measure of **content, sharpness or structure**. Any pipeline that verifies its output *only* by histogram is verifying almost nothing.

**Q30.** *`AI-generated practice question based on the lecture content`* — Compare the eye and the camera as imaging systems, and explain what the liquid lens is trying to achieve.
**A.** Both project light through a lens onto a light-sensitive surface (retina / sensor). The **mechanism of focus is opposite**: the eye's lens is soft, 60–70 % water, and the ciliary muscles make it **thicker or thinner** (L3 s.2–3); a camera focuses by **physically moving rigid glass**. The eye's approach needs no moving assembly and is compact. A **liquid lens** (water & oil, L3 s.6) imitates it by deforming a fluid interface electrically — which is why the Xiaomi Mi Mix Fold can do **telephoto *and* macro with the same lens** (L3 s.7). The camera's approach, in turn, wins on optical quality: a multi-element glass design (L3 s.44–45) corrects the **spherical** and **chromatic aberrations** (s.47) that a single simple lens cannot.

**Q31.** *`AI-generated practice question based on the lecture content`* — Histogram equalization is automatic and parameter-free. Why not simply apply it to every image?
**A.** Three reasons drawn from the material. **(1)** It forces a *uniform* distribution, which is a specific aesthetic choice, not a neutral one — L4 s.36 frames it as a tool for making images *comparable*, not universally better. **(2)** It stretches whatever is in the histogram, **including sensor noise** in flat regions — so a noisy dark image becomes a noisy, *visibly* noisy image. **(3)** If you actually want a particular look, **specification** (s.44–50) gives you control that equalization by construction cannot: equalization has exactly one destination, and you don't get to choose it. *(Point 2 is an AI-added observation; the lecture does not state it.)*

**Q32.** *`AI-generated practice question based on the lecture content`* — The lecture insists on fixing acquisition before writing algorithms. Defend that position using the case study.
**A.** The moulting case study (L1 s.8–13) began with two hard problems — a **24 × 7 workload** (s.8) and the need for **skilled, trained workers** (s.9). The solution did not start with a clever algorithm: it started by building a **controlled indoor tank with dedicated overhead lighting in a dark enclosure** (s.10). *Because* the scene was controlled, a very simple pipeline sufficed — crop → enhance → binary mask → clean → contour (s.11) — and a single scalar feature (the **percentage of detected area**, s.12) separated the classes cleanly: the moulting series climbs to ≈ 95–97 % while the non-moulting series oscillates around 0 (s.13). That separation is a property of the *scene design*, not of the code. This is the concrete payoff of the rule stated on L1 s.5: **impose conditions, bound the scope, decompose**.

### 14.6 Integrated (across multiple lectures)

**Q33.** *`AI-generated practice question based on the lecture content`* — Trace one photograph through the entire course: from choosing the camera to displaying an enhanced version on the LUMA website. Name the lecture and slide behind each decision.
**A.**
1. **Frame the problem** — state the goal and the feature (L4 s.4); if it's hard, impose conditions and decompose (L1 s.5). Locate yourself in the pipeline (L1 s.7).
2. **Choose the camera** — the 5-point checklist (L3 s.50); CCD vs CMOS by whether the subject moves (L3 s.57).
3. **Frame the shot** — `θ = 2 tan⁻¹(sensor/2f)`, then `FOV = 2·S₀·tan(θ/2)`; keep the units consistent (L3 s.55–56).
4. **Check the optics** — inspect a test shot for barrel/pin-cushion distortion and colour fringing (L3 s.49, s.59).
5. **Load it** — `cv.imread`; it becomes a `uint8` NumPy array indexed `img[y, x]` (L3 s.16, s.23–28).
6. **Measure, don't look** — `cv.calcHist` and plot it; your eyes are unreliable (L3 s.9–12 → L4 s.24, s.28).
7. **Diagnose** — clumped histogram = low **dynamic range** (L4 s.30–31).
8. **Transform** — gamma / log / stretching / equalization / specification as the diagnosis dictates (L4 s.12–50); **normalise before exponentiating**, then **clamp and cast back to `uint8`** (L4 s.16, s.32).
9. **Re-measure** — plot the histogram again as evidence (L4 s.33).
10. **Serve it** — a Flask **route** returns a **Jinja** template that displays the result (L4 s.79, s.92, s.95); the request arrives through the **Nginx reverse proxy** at `192.168.1.10` and is handled by the backend at `192.168.1.20` (L4 s.54).
11. **Evaluate** — item 5 of the five sub-systems: prove it works with a measurement, as the case study did with its area-vs-time chart (L1 s.6, s.13).

**Q34.** *`AI-generated practice question based on the lecture content`* — The LUMA app must let a user type "a knight in a forest, cinematic", get an image, then remove the background. Which parts of which lectures does each step draw on?
**A.**
* **Typing the prompt → an image:** the txt2img pipeline — random latent tensor (seeded), U-Net noise predictor conditioned by the 768-value text embeddings via cross-attention, repeated for N sampling steps, then decoded by the VAE (**L1 s.36–43**). Exposed to the user as **CFG (8–14)**, **seed**, **sampling steps (20–60)** and **sampler** (**L2**).
* **Making it look the way they want:** prompt emphasis syntax, LoRA for style, ControlNet for structure, Regional Prompter for composition (**L2 s.11–55**).
* **Removing the background:** LUMA's **Smart Canvas** feature list explicitly includes *Background Removal* and *Segmentation* (**L4 s.52**) — and segmentation is sub-system 3 of the five (**L1 s.6**).
* **Delivering it:** the request path Browser → Nginx → Flask → AI Server, the SQLite database, and whichever milestone the team is on (**L4 s.54, s.103**).

**Q35.** *`AI-generated practice question based on the lecture content`* — Lectures 3 and 4 both revolve around the same question, asked twice. What is it, and what are the two halves of the answer?
**A.** The question is **"can you trust what you see?"**
* **L3 s.9–12** answers *no* — the **Koffka ring** and the other illusions prove that human brightness perception is contextual and relative. You cannot judge an image by looking at it.
* **L4 s.23–24** turns that into an engineering problem — *"We know, this image too dark right? But how can we tell computer?"* — and supplies the objective replacement: the **histogram**, plus its statistics (mean, variance, skewness, kurtosis, L4 s.27) and the concept of **dynamic range** (s.30).
Together they form the course's central methodological rule: **replace perception with measurement.** And L4 s.25 immediately adds the caveat that keeps you honest — the measurement is a *summary*, so three different images can share one histogram.

---

## 15. AI Usage Instructions

**Rules for any AI (including future sessions of me) using this knowledge base.**

1. **The four PDFs in `/Users/winter/Desktop/Web_App/Lecture/` are the final source of truth.** This document is a faithful reorganisation of them. Where this file and a slide disagree, **the slide wins** — go and re-read it.
2. **Cite the slide.** State facts as "L4 s.20 defines contrast as…", never as bare assertion. Every section above carries its slide numbers so this is always possible.
3. **Never invent a slide number, a formula, a citation, or a piece of lecture content.** If it is not in §9 (formulas), §10 (terminology), or a cited section above, then say it is **not covered by these lectures** rather than filling the gap from general knowledge.
4. **Keep source and AI commentary separated,** exactly as this document does. Verbatim slide content is quoted or marked "as printed"; anything else is labelled **(AI)**, "AI explanation", or "AI-added".
5. **Do not silently correct the lectures.** Items like `cv.equalizeHist(imgA, histB)` (L4 s.50), `Flask-JET-Extended` (L4 s.69) and `requirement.txt` (L4 s.71) are recorded **as printed**, with the concern noted separately in §17. Follow the same discipline for anything new you find: **record first, flag second, never overwrite.**
6. **Respect the `Needs further verification` markers in §17.** Do not resolve them by guessing. If a task depends on one, surface the ambiguity to the user.
7. **Preserve the instructor's terminology and notation** — `g(x,y) = T[f(x,y)]`, `s = c·r^γ`, `H₂⁻¹`, `S₀`, *คนที่ 1…5*, "Fundamental Operation", "Point Operation". Do not substitute synonyms from other textbooks; the exam will use the lecture's words.
8. **Use the lecture's own code conventions when generating code:** `import cv2 as cv`, normalise before exponentiating, always cast back with `np.array(..., dtype = np.uint8)`, index as `img[y, x]`, end interactive scripts with `cv.waitKey(0)` and `cv.destroyAllWindows()`.
9. **When asked "which method should I use?", go through §13 (Quick Decision Guide) and §11 (Problem-Solving Framework)** rather than reaching for the first technique that comes to mind. Both are built from the lectures' own decision logic.
10. **For any question about the project, remember the file names lie** (§8.4): the LUMA brief, the distributed system, Flask and Jinja are all inside `Lecture 4 - Point Operation.pdf` (s.51–103), and the Python/OpenCV/optics material is inside `Lecture 3 - Human Visual Perception.pdf` (s.13–59).
11. **Cross-reference `Learn_Knowledge_Base.md`** for the project's *implementation* details (the 4-person team split, the API endpoints, the database schema, the deployment plan). The lectures give the *theory and the brief*; the `Learn` images give the *team's build plan*. Say which one you are drawing on.
12. **Do not modify, rename, move or delete the original lecture PDFs.** They are read-only source material.
13. **When the lecture asks a question but does not answer it** (L3 s.30, L4 s.10), say so explicitly, then give the answer as **AI-supplied**, not as lecture content.
14. **Prefer the exam-relevant framing.** The examinable mathematics is concentrated in **L4 s.7–50** (point operations) and **L3 s.46–57** (optics/FOV/sensors); the examinable concepts are spread across all four. Weight your explanations accordingly.
15. **When you genuinely do not know, say so.** These four lectures do not cover: convolution/filtering, edge detection algorithms, morphology, thresholding algorithms (Otsu etc.), the Fourier transform itself, training a CNN, or SQL. If asked about them, state plainly that they are **outside the scope of these four files** — do not improvise course content.

---

## 16. Quick Revision Summary

**The one-page version. If you remember nothing else, remember this.**

**The frame (L1).** Image processing = computer algorithms applied to pictures, producing one of three things: **a better image**, **a descriptor**, or **a label**. The pipeline is *acquire → enhance → extract features → recognise → understand*. Grading: **30 / 40 / 30** — and the **40 % is the Web App**. If a problem is too hard: **impose conditions, bound the scope, decompose**.

**The generative half (L1 → L2).** Diffusion models add noise, then learn to reverse it. The noise predictor is a **U-Net**; every diffusion has **drift + random motion**. Stable Diffusion is a **latent** diffusion model — the **VAE** compresses the image into a latent space **48× smaller** (a `4×64×64` tensor), all the denoising happens there, and the VAE decoder brings it back. The prompt enters through the **tokenizer → 768-value embedding → text transformer → cross-attention**, and that is exactly where **LoRA** patches the model. Control it with **CFG (8–14)**, **seed (−1 = random)**, **steps (20–60)**, samplers, **ControlNet** (pose/edges/depth), **Regional Prompter** (different prompts in different areas) and **img2img/Inpaint**.

**The eye (L3).** The eye focuses by **squeezing a soft, 60–70 %-water lens**; the camera focuses by **moving rigid glass**. The **liquid lens** (water & oil) is the engineering imitation. And critically: **you cannot trust your eyes** — the Koffka ring proves brightness perception is relative.

**The image (L3).** To a computer an image is a grid of **`uint8`** values, **0–255**, indexed **`img[y, x]`** (row first), and colour is three stacked **channels** (R/G/B). Create with `np.zeros(...)`, read with `cv.imread`, and **always cast back to `uint8`**.

**The camera (L3).** A lens converges parallel rays at the **focal length f**; only one distance is truly sharp (everything else is a **circle of confusion**). Real glass adds **spherical** (edge rays focus early) and **chromatic** (colour fringing) aberration, plus **barrel / pin-cushion** distortion. Choose the camera by the 5-point checklist, compute
**θ = 2 tan⁻¹(sensor / 2f)** then **FOV = 2·S₀·tan(θ/2)** *(watch your units!)*,
and pick **CCD (global shutter, no skew, low noise)** or **CMOS (rolling shutter, fast, skews moving objects)**.

**The transformations (L4).** A **point operation** is `g(x,y) = T[f(x,y)]` — one pixel at a time, so it's just a 256-entry lookup table, and it can *never* fix blur or noise. Above the diagonal = brighter, below = darker; steep = more contrast.
* **Power-law:** `s = c·r^γ` — **γ > 1 darkens, γ < 1 brightens**. Correcting a device's power law is **gamma correction** (CRTs are non-linear).
* **Log:** `s = c·log(1+r)` — massively lifts dark detail (used for the **Fourier spectrum**).
* **Contrast:** `(I_max − I_min)/(I_max + I_min)`; widen a band with **piecewise-linear stretching**.

**The measurement (L4).** *"We know this image is too dark — but how do we tell the computer?"* → the **histogram**. Bunched left = dark; bunched narrow = low **dynamic range**. But beware: **three very different images can have identical histograms**. Fix a clumped histogram with **equalization** (map the *cumulative* histogram onto a straight line); match a *specific* target with **specification** (`H₂⁻¹ ∘ H₁`, giving `U₁ ≈ U₂`). Always **clamp** and cast back to `uint8`.

**The project (L4).** **LUMA** = Learning-based Universal Media Artist: AI Generation + Smart Canvas + Asset Hub. Architecture: **Browser → Nginx reverse proxy → Frontend `192.168.1.10` / Flask backend `192.168.1.20` (+ SQLite) / AI Server `192.168.1.30`**. **Flask** is a *micro* framework (add Flask-Login, Flask-SQLAlchemy, Flask-WTF; not for big apps); routes are `@app.route('/user/<name>')`; templates are **Jinja** (`{{ }}` to display, `{% %}` for flow control). Build it in five milestones: **V1 all-in-one Flask → V2 +SQLite → V3 +Forge → V4 separate frontend → V5 Nginx all services.**

---

## 17. Unclear or Missing Information

Everything below is recorded because it is ambiguous, illegible, internally inconsistent, or absent. **Per the source-accuracy rules, nothing here has been silently corrected — the original is recorded first, and the concern is stated separately.**

| # | Item — recorded **as it appears in the lecture** | Concern (stated separately) | Location | Status |
|---|---|---|---|---|
| 1 | **`imgAtoB = cv.equalizeHist(imgA, histB)`** | The documented OpenCV Python signature is `equalizeHist(src[, dst])` — it accepts **no target histogram** and always equalizes to a uniform distribution; a second positional argument is treated as the *output array*. True histogram *specification* normally requires building `H₂⁻¹ ∘ H₁` manually. The slide's own block diagram (s.45–46) describes the correct algorithm; the code line appears not to implement it. | **L4 s.50** | `Needs further verification` |
| 2 | **`Flask-JET-Extended`** | The JWT-authentication extension is published as **Flask-JWT-Extended**; the `Learn` folder's own backend tool table (`5.jpg`) writes it that way. Very likely a typo for JWT. | **L4 s.69** | `Needs further verification` |
| 3 | **`requirement.txt`** (singular) in the Flask project structure | L3 s.20 uses the plural **`requirements.txt`**, which is what the commands `pip freeze > requirements.txt` and `pip install -r requirements.txt` actually produce and consume. | **L4 s.71** vs **L3 s.20** | `Needs further verification` |
| 4 | **`env/Scripts/activate.bat`** as *the* activation command | This is the **Windows** path. macOS/Linux require `source env/bin/activate`. No macOS/Linux form is given, even though the previous slide links a *macOS* PIP installation guide. | **L3 s.19** (cf. s.18) | `Needs further verification` |
| 5 | **The species in the case study is never named in the slide text.** Slides 8–13 are image-only; the Thai label on the chart is *มีการลอกคราบ / ไม่มีการลอกคราบ* = "moulting / not moulting". | The photographs show a moulting crustacean held in a basket grid, but no slide text identifies the animal. Any species name (shrimp, crab, …) would be an **inference, not a citation**. | **L1 s.8–13** | `Needs further verification` |
| 6 | **The experiment table's minute-4 and minute-5 values are not readable.** The first table shows minutes 1–3 (15.02, 15.14, 15.51) before being **overlapped by a second table** that resumes at minute 6 (25.57, 27.34, 29.60, 29.28, 29.09). | Two data points are hidden behind the overlapping table graphic. The trend is still unambiguous from the chart on s.13. | **L1 s.12** | `Needs further verification` |
| 7 | **Two slides render as solid black frames** with no extractable text. | Almost certainly embedded video that does not render in a static export. Their content could not be analysed. | **L3 s.40, s.58** | `Needs further verification` |
| 8 | **The OpenPose keypoint list appears to print "eyes" twice** ("eyes, nose, eyes, neck, …"). | Probably a slide typo (the standard OpenPose set distinguishes left/right eyes and ears), but it is reproduced as printed. | **L2 s.31** | `Needs further verification` |
| 9 | **Divide Ratio semantics for a single row.** The rule as stated is "the first number is the row height, the remaining numbers are the region widths", yet the example `Horizon (1,1,1)` yields **three columns**. | The multi-row examples (s.50–54) are unambiguous; the single-row reading is not. Do not rely on the single-row interpretation without testing it. | **L2 s.49** vs **s.50–54** | `Needs further verification` |
| 10 | **The parameters of "Modified Automatic Contrast Adjustment"** are presented as a figure; no numeric percentile/quantile values are extractable from the slide text. | The *concept* (a robust, outlier-tolerant version of automatic contrast adjustment) is clear; the exact formula and its constants are not. | **L4 s.34** | `Needs further verification` |
| 11 | **Team roles: five on the slide, four in practice.** L4 s.55 lists **คนที่ 5 (ถ้ามี) — Reverse Proxy, Routing**, marked *"if there is one"* with a light workload. | The `Learn` folder documents a **4-person** team where QA/DevOps absorbs the Nginx duty. Consistent *only* because the lecture marks role 5 as optional — but a reader of the slide alone would expect five people. | **L4 s.55** | Resolved by cross-reference; noted |
| 12 | **No textbook, reading list, or bibliographic citation** is given for the point-operation mathematics (formulas 1–6). | Some slides carry web links (OpenCV docs, wikiHow, tutorialspoint, stackshare), but the formulas themselves are uncited. Do **not** attribute them to a specific textbook. | **L4, throughout** | Absent from source |
| 13 | **No dates, deadlines, or submission details** for the homework, the workshops, the classwork or the project appear anywhere in the four files (beyond "1 group, 1 person submits, .pdf" on L3 s.59). | If a task depends on a deadline, it must come from outside these files. | All four files | Absent from source |
| 14 | **Several slides are image-only** (title cards, photographs, illusion figures) and carry no text layer. | Their content has been described from the visuals; where a figure's fine detail was not legible it is flagged individually above. | L1, L2, L3, L4 | Noted |

---

## 18. Final Readiness Assessment

### Coverage

| File | Slides | Read in full? | Captured in this knowledge base |
|---|---|---|---|
| `Lecture 1 - Introduction to Image Processing.pdf` | 58 | ✅ all 58, visually + text layer | §4 (12 sub-sections) |
| `Lecture 2 - Control and Fine-tune.pdf` | 62 | ✅ all 62, visually + text layer | §5 (12 sub-sections) |
| `Lecture 3 - Human Visual Perception.pdf` | 59 | ✅ all 59, visually + text layer | §6 (12 sub-sections) |
| `Lecture 4 - Point Operation.pdf` | 103 | ✅ all 103, visually + text layer | §7 (12 sub-sections) |
| **Total** | **282** | **✅ 282 / 282** | **§§1–18** |

### Quality checks

| Check | Result |
|---|---|
| Exactly 4 files found in `Lecture/` | ✅ Confirmed |
| Every slide inspected; none skipped | ✅ 282/282 |
| All formulas transcribed with their source slide | ✅ §9 — 13 entries |
| All code transcribed verbatim from the slides | ✅ §4.7, §5.7, §6.7, §7.7 |
| Original terminology and notation preserved | ✅ `g(x,y)=T[f(x,y)]`, `H₂⁻¹`, `S₀`, *คนที่ 1–5*, Thai retained with translations |
| Source content separated from AI explanation | ✅ Quoted/"as printed" vs "(AI)" throughout |
| Possible errors recorded, **not** silently corrected | ✅ §17 — 14 items, original first, concern second |
| Uncertain items marked `Needs further verification` | ✅ 10 of the 14 items in §17 |
| No fabricated citations, page numbers or content | ✅ Every claim carries a slide number that was verified against the PDF |
| Original lecture files unmodified | ✅ Read-only access; nothing renamed, moved or deleted |

### Readiness by task type

| Task | Ready? | Where to look |
|---|---|---|
| Answer conceptual questions | ✅ | §§4–7 (`.3` sub-sections), §10 |
| Solve calculation problems | ✅ | §9, §14.3 |
| Explain a concept simply | ✅ | The `.11` "Easy-to-Understand Summary" of each file section, §16 |
| Generate code in the lecture's style | ✅ | §4.7, §5.7, §6.7, §7.7; conventions in §15 rule 8 |
| Choose a method for a new problem | ✅ | §11, §13 |
| Debug a student's mistake | ✅ | §12, and each `.10` sub-section |
| Prepare for the exam | ✅ | §9, §10, §14, §16 |
| Work on the LUMA web app | ✅ | §7.3(k)–§7.8, §7.12 — **and `Learn_Knowledge_Base.md` for the team's implementation plan** |
| Anything about filtering, edges, morphology, Otsu, CNN training, SQL | ❌ | **Not covered by these four lectures** — see §15 rule 15 |

### Verdict

**This knowledge base is complete and ready for use as the primary AI reference for the course 310-3311 Image Processing.** All 282 slides across all 4 files have been read and captured. The 14 open items in §17 are documented, bounded, and none of them affects the core examinable material (the point-operation formulas, the histogram methods, the optics/FOV mathematics, or the Flask/Jinja fundamentals). Where the lectures contain probable typos, the original text has been preserved and the concern recorded separately, exactly as required.

---

*End of `Lecture_Knowledge_Base.md`. Source of truth: the 4 PDF files in `/Users/winter/Desktop/Web_App/Lecture/` (282 slides).*
