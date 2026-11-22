# Diamond Price Prediction

Predicts the price of a diamond from its attributes (carat, cut, color, clarity, depth, table, dimensions) using a trained CatBoost regressor served through a Flask web app.

## Project Structure

- `application.py` — Flask app with prediction form (`/` and `/predict`)
- `src/pipelines/` — training and prediction pipelines
- `src/components/` — data ingestion, transformation, model training, monitoring
- `artifacts/` — trained model and preprocessor pickles, train/test CSVs
- `data/gemstone.csv` — source dataset (53,940 diamonds)
- `notebooks/` — EDA and model training notebooks

## Data Source

By default the training pipeline reads `data/gemstone.csv`. To pull from MongoDB instead, set a `host` env var (or `.env` file) pointing at your Mongo instance with a `Diamond_Price_Prediction.data` collection.

## Setup

```bash
python3 -m venv .venv
.venv/bin/pip install flask pandas scikit-learn==1.3.1 numpy==1.24.4 \
    xgboost catboost pymongo tqdm python-dotenv joblib
```

Note: the pickled artifacts require `scikit-learn==1.3.1`, `pandas==2.0.3`, `numpy==1.24.4`.

## Run the App

```bash
PORT=5001 .venv/bin/python application.py
```

Then open http://localhost:5001 and go to the prediction page.

## Retrain the Model

```bash
.venv/bin/python src/pipelines/training_pipeline.py
```

This regenerates `artifacts/model.pkl` and `artifacts/preprocessor.pkl`.
