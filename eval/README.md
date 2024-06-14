# Running evaluation


## Overview
This folder is designed to evaluate various models on a range of evaluation datasets using specific evaluation modes. It supports evaluating models with different data modes such as absolute, relative, or both, depending on the model and dataset compatibility. The core functionality includes running inference on model outputs, parsing and scoring these outputs, and generating detailed evaluation reports.

## Requirements

This project is configured using Poetry, a tool for dependency management and packaging in Python. It specifies package versions to ensure compatibility and reproducibility of the environment.

The required Python version is between 3.11 and 3.13. Here's a list of the main dependencies:

- `openai` for using OpenAI's APIs.
- `tqdm` for progress bars.
- `transformers` and `datasets` from Hugging Face for model interactions and data handling.
- Various utilities like `python-dotenv` for environment variable management, and `openpyxl` for Excel file interactions.
- `nvitop` for NVIDIA GPU monitoring.
- Specialized libraries like `llm-blender`, `litellm`, `google-generativeai`, and `anthropic` for specific model operations and AI tasks.
- Visualization and data analysis libraries like `plotly`, `seaborn`, and `statsmodels`.
- `google-cloud-aiplatform` for interactions with Google Cloud's AI Platform.

## Installation

#### Using Poetry

1. Install Poetry:
   ```bash
   curl -sSL https://install.python-poetry.org | python3 -
   ```
   or on Windows, use PowerShell:
   ```powershell
   (Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -
   ```

2. Clone the project repository:
   ```bash
   git clone https://yourrepositoryurl.com
   cd eval
   ```

3. Install the project dependencies:
   ```bash
   poetry install
   ```

This will create a virtual environment and install all required dependencies as specified in the `pyproject.toml` file.

#### Using Conda

If you prefer using Conda for managing environments, follow these steps:

1. Install Anaconda or Miniconda if not already installed:
   - Download from [Anaconda](https://www.anaconda.com/products/distribution) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html).

2. Create a new Conda environment:
   ```bash
   conda create --name eval_env python=3.11
   ```

3. Activate the new environment:
   ```bash
   conda activate eval_env
   ```

4. Install the dependencies:
   - While not all dependencies might be available via Conda, most can be installed through PyPI within a Conda environment.
   ```bash
   conda install pip
   pip install openai==1.9.0 tqdm transformers datasets scipy loguru numpy seaborn statsmodels plotly
   pip install git+https://github.com/yuchenlin/LLM-Blender.git
   # Add more packages as required.
   ```

5. Proceed with the use of the environment in your development or deployment.

This setup ensures that you are working in a Python environment tailored to the specific needs and dependencies of the project.

## Usage
To run the script, you can use the command line interface providing the necessary arguments. Here's how to use it:

```bash
python -m eval.run_evaluate --model_name YOUR_MODEL_CHECKPOINT --eval_data_names DATASET_NAME_1 DATASET_NAME_2 [--rerun]
```

#### Arguments
- `--model_name`: The checkpoint or identifier for the model you want to evaluate. This should be a path to or an identifier of a pretrained model that is compatible with the Hugging Face Transformers library.
- `--eval_data_names`: A list of names of the evaluation datasets to be used. Multiple datasets can be provided separated by spaces.
- `--rerun`: Optional flag to force rerun of evaluations even if the outputs already exist.

#### Examples
Run an evaluation on a model with multiple datasets:
```bash
python -m eval.run_evaluate --model_name "mistralai/Mistral-7B-Instruct-v0.2" --eval_data_names hhh_alignment_eval flask_eval --rerun
```

#### Detailed Description of Modules

1. **Main Evaluation Flow**:
   - Initializes the model and tokenizer based on the provided model name.
   - Loads evaluation data and parameters.
   - Executes evaluation runs as per the specified modes and datasets.
   - Collects and aggregates feedback and scores.
   - Outputs detailed reports and logs.

2. **Feedback and Scoring**:
   - Parses model outputs to extract feedback and scores.
   - Handles retries for failed model outputs.
   - Aggregates results across multiple evaluation runs.

3. **Utilities**:
   - Includes functions to prepare input data according to the mode (absolute, relative) and tokenize using a specified tokenizer.
   - Provides utilities for loading and handling evaluation data.

4. **Debugging and Error Handling**:
   - Includes optional debugging capabilities to simplify tracing and resolving issues during development or evaluation.
   - Error handling to ensure robust execution even with problematic inputs or unexpected failures.