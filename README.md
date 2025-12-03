# 🧠 Tesseract OCR API – Docker Container  
Local FastAPI-based Optical Character Recognition (OCR) service optimized for numeric CAPTCHAs

<p align="center">
  <img src="images/tesseract-ocr-api-logo.png" alt="Tesseract OCR API Logo" width="220" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tesseract%20OCR-API-blue?style=for-the-badge&logo=tesseract-ocr" />
  <img src="https://img.shields.io/badge/Docker-Container-2496ED?style=for-the-badge&logo=docker" />
  <img src="https://img.shields.io/badge/FastAPI-High%20Performance-009688?style=for-the-badge&logo=fastapi" />
</p>

---

## 📌 Overview

**Tesseract OCR API** is a lightweight, high-performance **Dockerized OCR service** built using:

- 🧠 **Tesseract OCR** (digit-only, high-accuracy mode)
- 🚀 **FastAPI** + **Uvicorn** for ultra-fast HTTP processing
- 🖼️ Aggressive image preprocessing for maximum CAPTCHA accuracy
- 🔒 100% offline — no cloud services involved

This container is ideal for:

- Automated CAPTCHA solving  
- Integrations requiring numeric OCR (e.g., RAR ITP Checker)  
- High-throughput, low-latency local OCR  
- Private homelab environments  

---

## ✨ Features

| Feature | Description |
|--------|-------------|
| 🚀 FastAPI backend | Async endpoints with excellent performance |
| 🔢 Digits-only OCR | Perfect for CAPTCHAs and numeric codes |
| 🖼️ Smart preprocessing | Thresholding, sharpening, denoising, resizing |
| 📤 File upload support | OCR images sent directly via multipart/form-data |
| 🌐 URL support | OCR images downloaded directly from remote URLs |
| 🧪 Health endpoint | Simple monitoring endpoint `/health` |
| 🐳 Dockerized | Portable, lightweight container |

---

## 🐳 Docker Usage

### 🔧 Pull the image

```bash
docker pull <your-dockerhub-username>/tesseract-ocr-api:latest
```

Or build locally:

```bash
docker build -t tesseract-ocr-api .
```

---

### ▶️ Run the container

```bash
docker run -d   -p 8000:8000   --name tesseract-ocr-api   tesseract-ocr-api
```

The API will now be available at:

```text
http://localhost:8000
```

---

## 🚀 API Endpoints

### 🩺 Health Check

```http
GET /health
```

Response:

```json
{ "status": "ok" }
```

---

### 📤 OCR from File Upload

```http
POST /ocr/file?expected_length=4
```

Example:

```bash
curl -F "file=@captcha.png"   "http://localhost:8000/ocr/file?expected_length=4"
```

Response:

```json
{
  "text": "8372",
  "length": 4,
  "expected_length": 4,
  "filename": "captcha.png"
}
```

---

### 🌐 OCR from Image URL

```http
POST /ocr/url
```

Body:

```json
{
  "url": "https://example.com/captcha.png",
  "expected_length": 4
}
```

Response:

```json
{
  "text": "4921",
  "length": 4,
  "expected_length": 4
}
```

---

## 🔍 Internals & Behavior

- Uses **Tesseract PSM 7 / PSM 8** for best numeric detection  
- Applies heavy preprocessing for noisy images:
  - grayscale → normalized
  - resize × 2
  - blur
  - threshold
  - denoise  
- Extracts ONLY digits (0–9)  
- Async, thread-safe, and optimized for server use  



> Place your logo at `images/tesseract-ocr-api-logo.png` to match the path used above.

---

## 🛠 Development

Run locally with hot reload:

```bash
uvicorn app:app --reload --host 0.0.0.0 --port 8000
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## 📝 License

MIT License — free for personal & commercial use.

---

## 👤 Maintainer

**(kosztyk)**  
Homelab • Imaging • Integrations • Automation  

---

## ⭐ Support

If you find this container useful, please **star the repository** on GitHub — it helps a lot!
