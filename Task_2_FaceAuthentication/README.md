## Task 2 — Face Authentication

A FastAPI service that compares two face images using deep embedding similarity.

**How it works:**
1. Accepts two face images via a POST request
2. Detects faces and extracts embeddings using InsightFace
3. Computes cosine similarity between the two embeddings
4. Returns the verification result, similarity score, and bounding boxes

**Endpoint:** `POST /verify`
**Structure**

```
Task_2_FaceAuthentication/
│
├── __pycache__/
├── image_samples/
├── models/
│   └── face_model.pkl
├── uploads/
├── venv/
│
├── .gitignore
├── app.py
├── predict.py
├── README.md
├── requirements.txt
└── train.py
```

**Sample response:**
```json
{
  "verification_result": "same person",
  "similarity_score": 0.70,
  "bounding_box_image1": [x1, y1, x2, y2],
  "bounding_box_image2": [x1, y1, x2, y2]
}
```

**Tech stack:** FastAPI · InsightFace · OpenCV · NumPy · ONNX Runtime

---

## Setup

Install all dependencies:

```bash
pip install -r requirements.txt
```

Start the face authentication server:

```bash
cd Task2
python train.py
uvicorn app:app --reload
```
```bash
Open the interactive API explorer:
http://127.0.0.1:8000/docs
```