# DentalVLM-Seg

An early scaffold for a dental X-ray analysis API that would pair image segmentation with an automatically drafted radiology report.

> **This is not a working AI system.** No model has been trained or loaded. The segmentation step returns fixed, simulated findings and the report is a text template. Do not use it for any clinical purpose or treat its output as a real reading of an image.

## The idea

1. **Segment** panoramic and bitewing X-rays into teeth, caries, restorations and bone loss with an Attention U-Net (MONAI).
2. **Describe** the findings in a short draft report for a dentist to review, using a vision-language model.

## What exists today

| Part | State |
| --- | --- |
| `backend/main.py` | Working FastAPI app: `POST /api/v1/analyze` accepts an image, `GET /health` |
| `core/models/segmentation.py` | MONAI `AttentionUnet` is defined (5 classes) but has no weights and is not run. `predict()` returns hard-coded example findings |
| `core/vlm/report_generator.py` | Placeholder. Builds the report from a fixed template; the Hugging Face model call is commented out |
| `Dockerfile`, `docker-compose.yml` | Container setup for the API |

## Run the scaffold

```bash
pip install -r requirements.txt
uvicorn backend.main:app --reload
```

Then open `http://localhost:8000/docs` and try `/api/v1/analyze` with any image. You will always get the same example output, whatever the image shows.

With Docker:

```bash
docker-compose up --build
```

## Project layout

```
backend/main.py                   FastAPI app
core/models/segmentation.py       Segmentation model definition (untrained)
core/vlm/report_generator.py      Report generation placeholder
Dockerfile, docker-compose.yml
requirements.txt
```

## Roadmap

- [ ] Choose and connect a public dataset (for example UFBA-UESC Dental Images or the Tufts Dental Database)
- [ ] Write the training loop and train the segmentation model
- [ ] Replace the simulated findings with real model output
- [ ] Fine-tune a lightweight vision-language model on dental annotations
- [ ] Evaluate on held-out images before any claims about accuracy

## Author

Dr. Enosh A Paulson. [LinkedIn](https://linkedin.com/in/dr-enosh) · [GitHub](https://github.com/DrEnosh)
