# Installation & Deployment Guide
## Medical Image-Based Disease Detection and Classification System

---

## 1. System Requirements

Ensure the deployment environment meets the following specifications before initiating the installation process:

### 1.1 Hardware Specifications
- **GPU Accelerator:** NVIDIA GPU (Ampere architecture or newer recommended) with a minimum of **8GB VRAM** to support deep learning classification model loading.
- **System Memory:** Minimum **16GB System RAM**.
- **Persistent Storage:** Minimum **100GB of Solid State Drive (SSD)** space for operating system binaries, database records, preprocessed pixel archives, and DICOM caches.
- **CPU:** Quad-core 2.4GHz or higher processor.

### 1.2 Software Dependencies
- **Operating System:** Ubuntu 22.04 LTS (recommended for production) or Windows 10/11 (for local evaluation).
- **Python Runtime:** Python 3.10+ (specifically version 3.10 or 3.11).
- **GPU Acceleration Framework:** NVIDIA CUDA Toolkit 11.8+ and corresponding cuDNN drivers.
- **Package Manager:** `pip` and `virtualenv` installed locally.

---

## 2. Installation Steps

Follow this CLI execution sequence to configure the software dependencies.

### Step 2.1: Clone codebase
Clone the repository files to the target deployment host server directory:
```bash
git clone https://github.com/alirezakavianifar/Medical-Image-Based-Disease-Detection-and-Classification-System.git
cd Medical-Image-Based-Disease-Detection-and-Classification-System
```

### Step 2.2: Setup Python Virtual Environment
Initialize a clean virtual workspace environment to isolate Python package requirements:
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment (Linux/macOS)
source venv/bin/activate

# Activate virtual environment (Windows PowerShell)
.\venv\Scripts\Activate.ps1
```

### Step 2.3: Install Package Dependencies
Install the required application library payloads using `pip`:
```bash
pip install --upgrade pip
pip install pydicom torch torchvision numpy fastapi uvicorn reportlab python-dotenv
```

---

## 3. Configuration Setup

The application backend retrieves environment parameters from a `.env` configuration file in the project root.

### 3.1 Environment Configuration Template
Create a file named `.env` in the root directory and define the following variables:
```ini
# Server Configuration
HOST=0.0.0.0
PORT=8000

# Security Credentials
JWT_SECRET=super_secret_key_change_in_production_9872
JWT_EXPIRATION_MINUTES=15

# Database Persistence
SQLITE_DB_PATH=./data/clinical_cache.db

# Storage Directories
UPLOAD_DIR=./data/uploads
PREPROCESSED_DIR=./static/preprocessed
REPORTS_DIR=./static/reports

# Deep Learning Weight Paths
MODEL_WEIGHTS_PATH=./data/models/disease_classifier_weights.pth
```

### 3.2 Create Storage Directories
Run this command to initialize storage directory folders:
```bash
mkdir -p data/uploads data/models static/preprocessed static/reports
```

---

## 4. Database Schema Initialization

To establish relational tables (users, images, results, reports) and indices, execute the schema database migration script. 

Create a bootstrap script `init_db.py` under the root workspace containing:
```python
import sqlite3
import os

db_path = "./data/clinical_cache.db"
os.makedirs(os.path.dirname(db_path), exist_ok=True)

conn = sqlite3.connect(db_path)
cursor = conn.cursor()

# Enable Foreign Key support in SQLite session
cursor.execute("PRAGMA foreign_keys = ON;")

# Create tables and indices
# (Database tables follow the schemas documented in SDD Section 5)
```

Run the initialization script:
```bash
python init_db.py
```

---

## 5. Services Launch & Deployment

### 5.1 Mount Pre-trained Model Weights
Place the pre-trained neural model binary file (`disease_classifier_weights.pth`) in the target path directory configured in the `.env` file:
```text
./data/models/disease_classifier_weights.pth
```

### 5.2 Start Backend Application Node
Launch the ASGI API web server utilizing `uvicorn`:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 1
```
*Note: We restrict work threads to 1 worker to ensure CUDA GPU resource handles are not locked by concurrent subprocess bindings.*

---

## 6. System Verification Checks

Execute the following verification queries to ensure that uvicorn service threads are correctly serving routing requests and database queries:

### 6.1 API Health Check Query
Run a curl query against the health routing endpoint:
```bash
curl http://localhost:8000/api/health
```
**Expected Response:**
```json
{
  "status": "healthy",
  "gpu_available": true,
  "database_connected": true
}
```

### 6.2 Log Verification Check
Examine the console output terminal log for the following verification startup tags:
- `[INFO] Connection to SQLite Database succeeded.`
- `[INFO] GPU Model detected: NVIDIA GeForce RTX... (CUDA active)`
- `[INFO] Pre-trained AI model weights loaded successfully into VRAM.`
- `[INFO] Uvicorn server running on http://0.0.0.0:8000`
