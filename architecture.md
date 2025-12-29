Technical Architecture Detail

The Smart Agriculture Advisor (SAA) is built on a robust, scalable, and auditable infrastructure using Google Cloud Platform. The architecture follows the Medallion (Bronze/Silver/Gold) pattern to ensure data lineage and model reproducibility.

1. Data Foundation (BigQuery & GCS)

We use a multi-tiered storage approach to handle both structured and unstructured data:

Bronze Layer (Raw): * Cloud Storage: Stores raw satellite rasters (NDVI, SMAP) in GeoTIFF format and vendor-provided CSVs for IMD/NASA weather data.

BigQuery Raw: Ingests raw district-level crop history and soil health records without transformation.

Silver Layer (Curated): * Data is cleaned using Cloud Dataflow. We standardize district IDs, unify crop nomenclatures, and perform temporal alignment (matching daily weather to seasonal cycles).

Gold Layer (Analytical):

Final materialized views in BigQuery optimized for model training. This includes calculated features like "Monsoon Delay Days" or "3-Year Average Yield Delta."

2. Vertex AI Modeling Workflow

The ML lifecycle is managed via Vertex AI Pipelines (Kubeflow-based):

Ingestion & Validation: TFX components check for data anomalies (e.g., pH values out of range).

Feature Retrieval: The pipeline pulls "point-in-time" correct features from the Vertex Feature Store to avoid data leakage.

Training: * Tabular: XGBoost models optimized via Vertex Hyperparameter Tuning jobs.

Time-Series: Prophet or TFT (Temporal Fusion Transformer) for market price and climate forecasting.

Evaluation: Models are evaluated against a "Challenger" model. If the RMSE (Root Mean Square Error) is 10% lower, the model is promoted.

Model Registry: Validated artifacts are stored with full lineage tracking, linking the model to the specific BigQuery snapshot used for training.

3. Real-Time Feature Store & Serving

To bridge the gap between training and real-time inference:

Vertex Feature Store: Stores pre-computed features (e.g., 10-year soil carbon average) for sub-second retrieval during online prediction.

Online Serving: Models are deployed to Vertex AI Endpoints. These endpoints handle autoscaling and provide built-in monitoring for "Prediction Drift."

4. The Recommendation Engine (Logic Layer)

Predictions are passed through a custom business logic layer hosted on Cloud Run:

Constraint Checking: Filters crops based on soil pH and historical rotation rules (to prevent soil depletion).

Risk weighting: Calculates a "Confidence Interval." If the weather forecast is highly uncertain, the system prioritizes low-risk, drought-resistant crops (e.g., Millet) over high-yield, high-water crops.

Local Language Translation: Uses Cloud Translation API or pre-defined templates to convert numerical output into actionable advice in Hindi, Telugu, or Marathi.

5. Security & Privacy

IAM: Strict least-privilege access using Service Accounts for all Vertex AI and BigQuery operations.

Data Residency: All data is stored in localized GCP regions (e.g., asia-south1) to comply with local data sovereignty regulations.
