# End2End-PricePredictionSystem
End to End ML Project from Scratch for Price Prediction

## Project Setup with ZenML and MLflow Integration

This project is built using ZenML and requires setting up ZenML integrations for MLflow for experiment tracking and model deployment. Follow the steps below to set up and run the project.

## Prerequisites

Make sure the following are installed on your machine:

- Python 3.8 or higher
- Virtualenv (optional but recommended)
- Git (to clone the project)
- ZenML

## Steps to Set Up the Project

### 1. Clone the Repository

First, clone the source code from the repository to your local machine. Navigate to the project directory:

```bash
git clone <repository-url>
cd <project-directory>
```

### 2. Create and Activate Virtual Environment

It is recommended to set up a virtual environment to manage project dependencies. Follow the steps in this video guide or use the instructions below to create and activate a virtual environment:

```bash
# Create a virtual environment
python3 -m venv venv

# Activate the virtual environment
# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Project Dependencies
Once the virtual environment is activated, install the project dependencies by running:

```bash
pip install -r requirements.txt
```
### 4. Install ZenML
ZenML is an MLOps framework that simplifies model management and experiment tracking. Install ZenML using the following command:

```bash
# pip install zenml
pip install 'zenml[server]==0.64.0'
```

### 5. Install MLflow Integration with ZenML
MLflow is used for experiment tracking and model deployment in this project. You can install MLflow integration using ZenML by running:

```bash
zenml integration install mlflow -y
```

### 6. Configure ZenML Stack with MLflow Components
ZenML uses stacks to manage different components required for MLOps workflows. In this project, we need to configure an MLflow experiment tracker and model deployer. Follow the steps below to register these components:

```bash
# Register MLflow experiment tracker
zenml experiment-tracker register mlflow_tracker --flavor=mlflow

# Register MLflow model deployer
zenml model-deployer register mlflow --flavor=mlflow

# Register a ZenML stack with MLflow components
zenml stack register local-mlflow-stack -a default -o default -d mlflow -e mlflow_tracker --set

```

### 7. Run the Pipeline Script
Now that the stack is configured, you can run the deployment script:

```bash
python run_pipeline.py
```

Once pipeline is running, then you can see its runs and performances to inspect your experiment runs within the mlflow UI.


### 8. Run the Deployment Script
Now that the stack is configured, you can run the deployment script:

```bash
python run_deployment.py
```


Note: Make sure that your virtual environment is active when running the script.

**Ensure the MLflow Tracking URI is Set:**  
If you’re using a local MLflow tracking server or a specific backend URI, make sure that the tracking URI is correctly set in your environment or within your code.

You can set the tracking URI programmatically:

```bash
mlflow.set_tracking_uri("file:/Users/macbook/Library/Application Support/zenml/local_stores/0c0eaca7-9783-48c1-8bbc-4c39005e05f9/mlruns")
```


Also Set Path in training_pipeline for running the code without error for the datafile.
```bash
file_path="/Users/macbook/Downloads/PricePredictionSyste_End2End/data/archive.zip" #give your file path
```

To get ZenML Dashboard:

```bash
zenml init
zenml up
```

**Set the Environment Variable**  
You need to set the environment variable OBJC_DISABLE_INITIALIZE_FORK_SAFETY to YES in your terminal.

```bash
export OBJC_DISABLE_INITIALIZE_FORK_SAFETY=YES
```

get dashboard at ```http://127.0.0.1:8237```

**Further: MLflow Server Configuration:**
- Confirm that the server is running and accessible at http://127.0.0.1:8000/invocations. You can do this by checking if the daemon process is still running.
- You can also stop and restart the server using the --stop-service flag and then restart it to ensure everything is properly configured.


### Additional Information
#### ZenML Stacks
- Experiment Tracker: MLflow is used to track experiments in this project. It records parameters, metrics, and artifacts, allowing you to compare different experiment runs.
- Model Deployer: The MLflow model deployer component in ZenML allows models to be served directly after being trained.

#### ZenML Documentation
For more information about ZenML, visit the ZenML documentation.

##### Troubleshooting
If you face any issues during the setup or while running the project, ensure the following:

- All dependencies are installed.
- You are using the correct versions of Python and ZenML.
- The virtual environment is activated when executing scripts.

For further troubleshooting, refer to the ZenML documentation at https://docs.zenml.io/ or the official MLflow documentation for more details.


