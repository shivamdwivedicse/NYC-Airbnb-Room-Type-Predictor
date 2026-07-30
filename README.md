<div align="center">

![Header Banner](https://capsule-render.vercel.app/api?type=waving&color=0:1e3c72,100:2a5298&height=180&section=header&text=NYC%20Airbnb%20Room%20Type%20Predictor&fontSize=36&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Entire%20Home%20%7C%20Private%20Room%20%7C%20Shared%20Room&descAlignY=58&descSize=18)

<img src="https://readme-typing-svg.demolab.com?font=Space+Grotesk&size=20&pause=1000&color=F7931E&center=true&vCenter=true&width=600&lines=Predicting+room+types+from+listing+data...;Random+Forest+%7C+FastAPI+%7C+scikit-learn;85.9%25+accuracy+%C2%B7+0.76+macro-F1" alt="Typing SVG" />

### Predict a listing's room type from its price, location & reviews — served live via FastAPI

[![Python](https://img.shields.io/badge/Python-3.13-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Render](https://img.shields.io/badge/Deployed%20on-Render-46E3B7?style=for-the-badge&logo=render&logoColor=white)](https://render.com/)

![GitHub last commit](https://img.shields.io/github/last-commit/shivamdwivedicse/NYC-Airbnb-Room-Type-Predictor?style=flat-square&color=blueviolet)
![GitHub repo size](https://img.shields.io/github/repo-size/shivamdwivedicse/NYC-Airbnb-Room-Type-Predictor?style=flat-square&color=orange)
![GitHub stars](https://img.shields.io/github/stars/shivamdwivedicse/NYC-Airbnb-Room-Type-Predictor?style=flat-square&color=yellow)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

**[🔴 Live Demo](https://nyc-airbnb-room-type-predictor-1-unp5.onrender.com)** &nbsp;·&nbsp; **[📓 Notebook](./NYC_Airbnb_roomType_Classification.ipynb)** &nbsp;·&nbsp; **[🔌 API Docs](#-api-reference)**

</div>

---

> Give the model a listing's location, price, availability, and review stats — it predicts whether the listing is an **Entire home/apt**, **Private room**, or **Shared room**, along with a full confidence breakdown. The frontend renders this as a tiny NYC skyline, where each room type is a building and its lit windows glow according to the model's confidence.

<div align="center">

```
 ┌──────────┐   ┌──────────┐   ┌──────────┐
 │ ▢▢ ▢▢ ▢▢ │   │ ▢▢ ▢▢    │   │ ▢▢       │
 │ ▢▢ ▢▢ ▢▢ │   │ ▢▢ ▢▢    │   │ ▢▢       │
 │ ▢▢ ▢▢ ▢▢ │   │ ▢▢ ▢▢    │   └──────────┘
 │ ▢▢ ▢▢ ▢▢ │   └──────────┘    Shared Room
 └──────────┘   Private Room
 Entire home/apt
```

</div>

---

## ✨ What it does

Give the model a listing's location, price, availability, and review stats — it predicts the most likely room type along with the full probability breakdown across all three classes.

The frontend visualizes this as a mini NYC skyline: each room type is a building, and its "lit windows" represent the model's confidence in that class.

---

## 🧠 The Model

Trained on the classic [NYC Airbnb Open Data (2019)](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data) dataset from Kaggle.

**Pipeline:**
- Preprocessing via `ColumnTransformer` — median imputation + scaling for numeric features, one-hot encoding for categorical features (`neighbourhood_group`, `neighbourhood`).
- Four candidate models were benchmarked with 3-fold stratified cross-validation, using `class_weight="balanced"` to handle the strong class imbalance (Shared Room listings are rare):

| Model | Accuracy | F1 (macro) |
|---|---|---|
| Logistic Regression | 0.663 | 0.526 |
| Decision Tree | 0.783 | 0.649 |
| **Random Forest** | **0.853** | **0.719** |
| Gradient Boosting | 0.850 | 0.708 |

- **Random Forest** won, and was further tuned with `RandomizedSearchCV` (`f1_macro` scoring, 3-fold CV):
  - Best params: `n_estimators=200`, `max_depth=None`, `min_samples_split=10`
  - Best CV macro-F1: **0.733**

**Final held-out test performance:**
- **Accuracy: 85.9%**
- **F1 (macro): 75.6%**

The final pipeline (preprocessing + model) is serialized with `joblib` as `Model_Pipeline.pkl`.

---

## ⚙️ Tech Stack

<div align="center">

| Layer | Tech |
|---|---|
| 🧠 Modeling | ![scikit-learn](https://img.shields.io/badge/-scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white) ![Pandas](https://img.shields.io/badge/-Pandas-150458?style=flat-square&logo=pandas&logoColor=white) ![Joblib](https://img.shields.io/badge/-Joblib-4B8BBE?style=flat-square) |
| ⚡ API | ![FastAPI](https://img.shields.io/badge/-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Pydantic](https://img.shields.io/badge/-Pydantic-E92063?style=flat-square&logo=pydantic&logoColor=white) ![Uvicorn](https://img.shields.io/badge/-Uvicorn-2A308B?style=flat-square) |
| 🎨 Frontend | ![HTML5](https://img.shields.io/badge/-HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/-CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/-JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) |
| 🚀 Deployment | ![Render](https://img.shields.io/badge/-Render-46E3B7?style=flat-square&logo=render&logoColor=white) |

</div>

---

## 📂 Project Structure

```
├── NYC_Airbnb_roomType_Classification.ipynb   # EDA, model comparison & tuning
├── Model_Pipeline.pkl                         # Trained sklearn pipeline
├── main.py                                    # FastAPI inference service
├── index.html / style.css / script.js         # Frontend UI
├── requirements.txt
└── runtime.txt
```

---

## 🚀 Running Locally

### 1. Clone & install
```bash
git clone https://github.com/<your-username>/NYC-Airbnb-Room-Type-Predictor.git
cd NYC-Airbnb-Room-Type-Predictor
pip install -r requirements.txt
```

### 2. Start the API
```bash
uvicorn main:app --reload
```
API will be live at `http://127.0.0.1:8000`. Interactive docs at `http://127.0.0.1:8000/docs`.

### 3. Open the frontend
Just open `index.html` in your browser (update `API_BASE_URL` in `script.js` to point at your local server), or serve it with any static file server.

---

## 🔌 API Reference

### `POST /predict`

**Request body:**
```json
{
  "latitude": 40.7484,
  "longitude": -73.9857,
  "price": 120,
  "minimum_nights": 2,
  "number_of_reviews": 84,
  "reviews_per_month": 2.3,
  "calculated_host_listings_count": 1,
  "availability_365": 210,
  "neighbourhood_group": "Manhattan",
  "neighbourhood": "Midtown"
}
```

**Response:**
```json
{
  "Predicted_room_type": "Entire home/apt",
  "Probability": [0.71, 0.24, 0.05]
}
```

All inputs are validated with Pydantic (e.g. latitude/longitude bounds, positive price, 0–365 day ranges), returning clear `422` errors on invalid input.

---

## 🗺️ Roadmap / Ideas

- [ ] Add SHAP-based explainability to show *why* a listing was classified a certain way
- [ ] Dockerize the API for easier deployment
- [ ] Add a `/batch-predict` endpoint for CSV uploads
- [ ] CI pipeline with automated model evaluation on new data

---

## 📜 License

This project is open source — feel free to fork, learn from it, and build on top of it.

---

<div align="center">

**⭐ If this project helped you, consider giving it a star!**

[⬆ Back to top](#-nyc-airbnb-room-type-predictor)

![Footer Banner](https://capsule-render.vercel.app/api?type=waving&color=0:2a5298,100:1e3c72&height=100&section=footer)

</div>
