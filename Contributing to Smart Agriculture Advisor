Contributing to Smart Agriculture Advisor

Welcome! We are thrilled that you want to contribute to a project that directly impacts the livelihoods of smallholder farmers.

This project is a multidisciplinary effort. Whether you are a Data Scientist, an Agronomist, or a Software Engineer, your expertise is needed.

🛠️ Technical Setup

1. Development Environment

We recommend using Vertex AI Workbench or a local VS Code setup with the Google Cloud SDK installed.

# Set your active project
gcloud config set project [YOUR_PROJECT_ID]

# Create a virtual environment
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt


2. Mock Data

For security reasons, production BigQuery datasets are restricted. Use the scripts in /data/mock_generators/ to create a local SQLite or small BigQuery sandbox for testing.

🧪 Contribution Workflows

For Data Scientists (Models & Features)

New Features: Add feature engineering logic in features/definitions.py. Ensure you include a unit test verifying the math for seasonal aggregates.

Model Improvements: Use the notebooks/experiments/ folder for prototyping. Once a model shows improvement, port the logic to a Vertex Pipeline component in models/pipelines/.

For Developers (API & Infrastructure)

API Changes: All API changes should be reflected in the /api/swagger.yaml file.

Integration: When adding a new delivery channel (e.g., Telegram), ensure it follows the abstract Notifier class in api/notifications/base.py.

For Agronomists (Domain Logic)

Rule Engine: Update crop suitability matrices in data/agronomy/suitability_rules.json.

Translations: Help us refine the "Explainability" strings in local languages to ensure they are culturally appropriate and easy to understand.

📬 Pull Request (PR) Process

Branching: Use feature/ or fix/ prefixes for your branches.

Testing: All PRs must pass the CI/CD pipeline which checks for:

Linting (PEP 8)

Unit tests

Model performance regression (for ML changes)

Review: At least one maintainer and one domain expert (e.g., an agronomist for rule changes) must approve the PR.

💬 Communication

Slack/Discord: Join our #saa-dev channel for real-time discussions.

Bi-Weekly Sync: Join our "Field-to-Cloud" sync every other Thursday to discuss pilot feedback and technical roadblocks.

📜 Code of Conduct

We follow the Contributor Covenant. Please be respectful, inclusive, and collaborative. Our goal is impact, not ego.
