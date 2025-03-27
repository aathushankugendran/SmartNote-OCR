# 📝 SmartNote OCR – AI-Powered Note-Taking App

SmartNote OCR is a full-stack web application that allows users to create, manage, and upload handwritten or printed notes. Using integrated OCR (Optical Character Recognition), it extracts text from image-based notes and evaluates readability metrics such as OCR Accuracy and Clarity Score.

> ⚡ Built with React, Ruby on Rails, PostgreSQL, and OCR AI models.

---

## 🚀 Features

- ✍️ Create, edit, delete, and search text-based notes.
- 📷 Upload scanned or photographed notes (JPEG, PNG, PDF).
- 🤖 Integrated OCR pipeline extracts text using PyTorch/Transformers.
- 📊 Get instant readability scores and OCR accuracy metrics to ensure scanned notes are clear, accessible, and study-ready.
- ☁️ Frontend hosted on Netlify, backend on Heroku, OCR module runs on Databricks.

---

## 🛠️ Tech Stack

| Layer             | Tech Stack                             |
|------------------|----------------------------------------|
| Frontend          | React, TypeScript, TailwindCSS         |
| Backend           | Ruby on Rails (API mode)               |
| Database          | PostgreSQL                             |
| OCR Engine        | PyTorch, HuggingFace Transformers      |
| Metrics           | `jiwer`, `textstat`, custom logic      |
| Infrastructure    | Databricks (Spark 3.5, Scala 2.12)     |
| Hosting           | Netlify (FE), Heroku (BE), AWS S3      |

---

## 📸 OCR & Readability Metrics

OCR integration extracts text and calculates:

- **OCR Accuracy Score** using `jiwer` (compares OCR output to user-corrected content).
- **Readability Score** using `textstat` (Flesch-Kincaid Grade, Reading Ease, etc.).
- **Clarity Score** – Custom metric combining image resolution + model confidence.

> 📈 These metrics help ensure that digitized notes are accessible, high-quality, and suitable for studying, archiving, or assistive technologies.

---

## ✅ Setup Instructions

### 🧩 Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/smartnote-ocr.git
   cd smartnote-ocr
   ```

2. **Start the Backend (Rails API)**
   ```bash
   cd backend
   bundle install
   rails db:create db:migrate
   rails s
   ```

3. **Start the Frontend (React App)**
   ```bash
   cd frontend
   npm install
   npm start
   ```

4. **Run the OCR Module (Python)**
   ```bash
   cd ocr
   pip install -r requirements.txt
   python ocr_pipeline.py
   ```

---

## 🧠 Usage

### 🖼️ 1. Convert PDF to Image
```python
pdf_image = pdf_to_image("example.pdf")
pdf_image.save("note_page.png")
```

### 🧠 2. Run OCR Model
```python
model = Qwen2VLForConditionalGeneration.from_pretrained("Qwen/Qwen2-VL-2B-Instruct", torch_dtype=torch.bfloat16, device_map="auto")
```

### 📤 3. Extract Text and Generate Metrics
```python
inputs = processor(text=prompt, images=optimized_image, return_tensors="pt").to(device)
output = model.generate(**inputs)
ocr_text = processor.batch_decode(output, skip_special_tokens=True)[0]

readability = textstat.flesch_reading_ease(ocr_text)
accuracy = wer(reference_text, ocr_text)
```

---

## 📈 Example JSON Output

```json
{
  "ocr_text": "Extracted note content...",
  "Character Error Rate (%)": 0.84,
  "Word Error Rate (%)": 8.35,
  "OCR Accuracy (%)": 99.16
}
```

---

## 🔥 Databricks Cluster Configuration

| Setting                | Value                                        |
|------------------------|----------------------------------------------|
| Cluster Owner          | Aathushan Kugendran                          |
| Access Mode            | Dedicated (Single User)                      |
| Runtime Version        | 15.4 LTS ML (Apache Spark 3.5.0, Scala 2.12) |
| Node Type              | Standard_E8ads_v5                            |
| Specs                  | 64 GB RAM, 8 Cores                           |
| Termination Timeout    | 30 minutes of inactivity                     |
| DBU Consumption        | ~2.75 DBU/hour                               |
| Photon Acceleration    | Disabled                                     |
| Cost Center Tag        | 8604                                         |

---

## 🚀 Performance Optimizations

- ✅ **bfloat16 precision**: Memory-efficient inference with near-float32 accuracy.
- ✅ **Auto Device Mapping**: Automatically maps computations to CPU/GPU.
- ✅ **Torch Compilation**: Speeds up inference by optimizing graph execution.
- ✅ **Databricks Optimization**: Configured for 64GB RAM / 8-core compute with low DBU cost, balancing performance and scalability.

---

## 🔒 License

This project is licensed under the MIT License.
