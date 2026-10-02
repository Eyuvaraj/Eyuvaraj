# Comment Category Prediction

**Repository:** [comment-category-prediction](https://github.com/Eyuvaraj/comment-category-prediction)

## One-line summary

Solo multiclass machine learning project for predicting one of four categories assigned to online comments using comment text, engagement signals, timestamps, discussion metadata, emoticon indicators, hidden platform features, and identity/topic indicators, developed for the IIT Madras BSCS2008P Machine Learning Practice Project on Kaggle.

## Project Context

Developed as part of **BSCS2008P: Machine Learning Practice Project** in the **IIT Madras BS in Data Science and Applications** program during the January to April 2026 term.

The project was conducted through the private Kaggle competition **Comment Category Prediction Challenge**.

The course project is intended to apply the complete machine learning lifecycle to a real-world dataset, including data understanding, preprocessing, feature engineering, model development, evaluation, and prediction on unseen data.

**Competition period:** January 17, 2026 to March 31, 2026
**Problem type:** Supervised multiclass classification
**Target:** `label`
**Number of target classes:** 4

## Dataset

The competition provides:

* `train.csv` containing input features and the target `label`
* `test.csv` containing the same predictive features without the target
* `sample_submission.csv` defining the required Kaggle submission format

Each row represents a comment posted to an online discussion platform.

### Input Features

**Text**

* `comment`: raw text content of the user comment

**Temporal / identifier**

* `created_date`: date and time at which the comment was posted
* `post_id`: identifier linking the comment to its discussion thread or parent post

**Engagement**

* `upvote`: number of positive reactions
* `downvote`: number of negative reactions

**Emoticon indicators**

* `emoticon_1`
* `emoticon_2`
* `emoticon_3`

These indicate the presence of symbols belonging to three internal emoticon groups.

**Hidden/internal platform features**

* `if_1`
* `if_2`

The semantic meaning of these features is intentionally hidden by the competition.

**Topic / identity indicators**

* `race`
* `religion`
* `gender`
* `disability`

These indicate whether the platform detected references associated with the corresponding topic.

**Target**

* `label`: one of four categories assigned to the comment by the platform

## Machine Learning Problem

The task is to learn a mapping:

`comment + metadata + platform signals -> label`

Unlike a pure NLP classification task, the dataset combines **unstructured text** with **structured numerical, categorical, binary, temporal, and identifier-based features**.

This makes the project a mixed-feature multiclass classification problem.

Potential predictive information can therefore come from both:

1. the semantic or lexical content of the comment, and
2. non-textual signals such as engagement, platform indicators, and metadata.

## ML Workflow

The notebook implements an end-to-end competition workflow built around the standard supervised machine learning cycle.

### Data Loading and Inspection

The training and test datasets are loaded and examined for:

* dimensions
* column types
* missing values
* feature distributions
* target distribution
* consistency between training and test schemas

This stage establishes which features require text processing, numeric preprocessing, categorical handling, or datetime transformation.

### Exploratory Data Analysis

Exploration focuses on understanding the relationship between the available features and the four-class target.

Relevant areas include:

* class balance
* comment characteristics
* upvote and downvote distributions
* emoticon indicators
* identity/topic indicators
* hidden platform variables
* temporal information
* relationships between comments and `post_id`

The objective is to identify useful predictive signals and preprocessing requirements before model training.

### Preprocessing

The dataset contains heterogeneous feature types that cannot be passed directly to most machine learning models.

The workflow therefore separates and prepares:

* raw text
* numeric variables
* binary indicators
* datetime-derived information
* identifiers or categorical variables where applicable

Training and test transformations are kept consistent so that the feature representation used during training is reproducible at inference time.

### Text Representation

The `comment` field is transformed from raw natural-language text into a numerical representation that can be consumed by machine learning algorithms.

The text pipeline is treated separately from structured metadata before the resulting features are combined for classification.

This is a central part of the project because the raw comment itself contains substantially different information from the accompanying numerical and platform-generated attributes.

### Feature Engineering

The project investigates information available beyond the raw comment text.

Candidate feature groups include:

* comment-derived features
* engagement signals from `upvote` and `downvote`
* combinations or relationships between positive and negative reactions
* datetime-derived features from `created_date`
* discussion/thread information from `post_id`
* emoticon-group indicators
* hidden internal features
* race, religion, gender, and disability indicators

The objective is to represent useful patterns in a form that improves classification performance while avoiding inconsistent transformations between the training and test sets.

### Model Development

Multiple machine learning configurations can be evaluated against the same validation strategy.

The development loop consists of:

`preprocessing -> feature representation -> model training -> validation -> comparison -> refinement`

The final model is trained using the selected preprocessing and feature configuration before generating predictions for the competition test set.

## Validation and Evaluation

Because this is a supervised Kaggle competition, model development requires separating local model evaluation from the final hidden test evaluation.

The notebook uses the available labelled training data to compare candidate approaches before producing predictions for `test.csv`.

The Kaggle leaderboard then provides an external evaluation of the submitted predictions against labels unavailable to participants.

This distinction is important:

* local validation is used for development and model selection
* Kaggle evaluation measures generalization against the competition's hidden labels

## Prediction Pipeline

The final inference process follows:

`test.csv`

→ apply the same preprocessing used during training

→ transform text and structured features

→ run the trained classifier

→ predict one of four labels per comment

→ construct the submission dataframe

→ export predictions in `sample_submission.csv` format

The generated submission can then be uploaded to Kaggle for evaluation.

## Repository Structure

```text
comment-category-prediction/
├── README.md
├── comment_category_prediction.ipynb
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── data/
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
│
└── outputs/
    └── submission.csv
```

The notebook is the primary project artifact and contains the complete analytical and modeling workflow.

## Technology Stack

**Language**

* Python

**Data manipulation**

* NumPy
* Pandas

**Machine learning**

* Scikit-learn

**Visualization**

* Matplotlib

**Development environment**

* Jupyter Notebook
* Kaggle Notebooks

**Competition platform**

* Kaggle

## Architecture

This is a notebook-driven machine learning project rather than an application or service architecture.

The main logical pipeline is:

```text
Raw CSV data
    |
    v
Data inspection / EDA
    |
    v
Preprocessing
    |
    +----------+
    |          |
    v          v
Text       Structured
features   features
    |          |
    +----+-----+
         |
         v
Combined feature representation
         |
         v
Multiclass classifier
         |
         v
Validation / evaluation
         |
         v
Final test predictions
         |
         v
Kaggle submission
```

The key architectural concern is maintaining exactly the same learned preprocessing transformations between training and inference.

## Key Technical Characteristics

* **Mixed-modality tabular problem:** combines free-form natural-language comments with numerical, binary, categorical, temporal, and identifier-like features.

* **Four-class supervised classification:** each comment must be assigned exactly one of four target labels.

* **Text + metadata modeling:** the problem is not restricted to NLP. Platform-generated metadata and interaction signals can contribute predictive information alongside text.

* **Train/test transformation consistency:** preprocessing learned from the training set must be applied unchanged to unseen test data.

* **Competition-style evaluation:** model development occurs using labelled training data, while final generalization is measured against hidden Kaggle labels.

* **End-to-end workflow:** covers data exploration, preprocessing, feature engineering, model experimentation, validation, inference, and submission generation.

## Scale Signals

The dataset contains:

* 1 primary free-text feature
* 1 datetime feature
* 1 discussion/post identifier
* 2 engagement-count features
* 3 emoticon indicators
* 2 hidden internal platform features
* 4 identity/topic-reference indicators
* 1 four-class target variable

This gives **14 predictive columns** in the provided schema before any derived or encoded features are created.

The effective feature space can become substantially larger after text vectorization and feature engineering.

## Key Highlights

1. Built an end-to-end multiclass machine learning workflow for categorizing online comments into four platform-defined classes.

2. Worked with heterogeneous data containing raw text, engagement metrics, temporal data, thread identifiers, emoticon indicators, hidden system features, and topic-reference signals.

3. Designed preprocessing so text and structured metadata could be transformed independently and combined into a single predictive representation.

4. Applied feature engineering and exploratory analysis to identify useful signals beyond the raw comment text.

5. Evaluated machine learning configurations using labelled training data before generating predictions for an unseen Kaggle test set.

6. Implemented the complete competition workflow from raw CSV ingestion through preprocessing, model training, inference, and submission-file generation.

7. Gained practical experience with the full machine learning lifecycle in a Kaggle-based academic project rather than working only with isolated model-training exercises.

## Skills Demonstrated

* Supervised machine learning
* Multiclass classification
* Text classification
* Natural language processing
* Exploratory data analysis
* Feature engineering
* Mixed structured/unstructured data
* Data preprocessing
* Model validation
* Scikit-learn workflows
* Pandas / NumPy data processing
* Kaggle competition workflow
* Reproducible notebook-based experimentation

## Course

**BSCS2008P: Machine Learning Practice Project**
**Indian Institute of Technology Madras**
**BS in Data Science and Applications**
**Term:** January to April 2026

The project course focuses on applying machine learning techniques to real-world datasets and completing the full ML lifecycle from data analysis through predictive modeling and evaluation.