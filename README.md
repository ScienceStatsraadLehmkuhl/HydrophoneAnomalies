
## 1\. Setting Up the `HydrophoneAnalysis` Conda Environment

First, you need to create a Conda environment named `HydrophoneAnalysis` and install all the necessary Python libraries.

1.  **Create the Environment**: Open your terminal or Anaconda Prompt and run the following command to create a new environment with Python 3.9 (a stable choice for these libraries):

    ```bash
    conda create -n HydrophoneAnalysis python=3.9 -y
    ```

2.  **Activate the Environment**: You must activate the environment each time you want to run the script.

    ```bash
    conda activate HydrophoneAnalysis
    ```

3.  **Install Libraries**: Now, install the required packages. The most critical step is installing PyTorch, as its version depends on whether you have a CUDA-enabled GPU.

      * **Install PyTorch & Torchaudio**: For the most reliable installation, go to the [PyTorch official website](https://pytorch.org/get-started/locally/) and select your system's specifications (e.g., OS, Package: Conda, and your CUDA version or CPU). Copy the command they provide. For a standard CPU-only setup, the command is usually:
        ```bash
        conda install pytorch torchaudio cpuonly -c pytorch
        ```
      * **Install other core packages**: Run this command to install the remaining data science and audio libraries from the `conda-forge` channel, which ensures better compatibility.
        ```bash
        conda install -c conda-forge librosa scikit-learn matplotlib -y
        ```
      * **Install `panns_inference`**: This package is best installed using `pip`.
        ```bash
        pip install panns-inference
        ```

-----

## 2\. Configuring the Script

Before running the analysis, you **must** edit the `config` dictionary at the top of the script to match your system's file paths.

  * **`audio_folder_path`**: Change this to the full path where your `.wav` hydrophone files are stored.
  * **`output_folder`**: Change this to the full path where you want all the results (CSVs, plots, audio clips) to be saved.

Your modified configuration might look something like this:

```python
# --- Configuration ---
config = {
    # --- Paths ---
    "audio_folder_path": "D:/My_Research/Project_Azores/Hydrophone_Data",
    "output_folder": "D:/My_Research/Project_Azores/Analysis_Results",
    # ... other settings remain the same ...
}
```

You can also tune other parameters in this section, like `high_pass_filter_hz` or `dbscan_eps`, to adjust the analysis.

-----

## 3\. Running the Analysis

With the environment set up and the script configured, you can run the analysis using one of two methods.

### Method A: Direct Execution (Command Line)

This is the most straightforward way to run the script.

1.  Save the code into a file named `analyze_hydrophone.py`.
2.  Open your terminal and activate the environment:
    ```bash
    conda activate HydrophoneAnalysis
    ```
3.  Navigate to the directory where you saved the file:
    ```bash
    cd path/to/your/script
    ```
4.  Execute the script using Python. The analysis will start, printing progress directly to your terminal.
    ```bash
    python analyze_hydrophone.py
    ```

### Method B: Jupyter Notebook

Running the script in a Jupyter Notebook is great for interactive analysis and debugging.

1.  **Install Jupyter**: If you haven't already, install Jupyter in your environment.
    ```bash
    # Make sure your 'HydrophoneAnalysis' environment is active
    conda install jupyter -y
    ```

    ```bash
    conda activate HydrophoneAnalysis
    ```
2.  **Launch Jupyter Notebook**: From your terminal, start the Jupyter server.
    ```bash
    jupyter notebook
    ```
3.  **Run the Code**: Your web browser will open the Jupyter interface.
      * Click **New** -\> **Notebook** (and select the `HydrophoneAnalysis` kernel if prompted).
      * Copy the entire script and paste it into the first cell of the notebook.
      * Run the cell by pressing **Shift + Enter**. The analysis will begin, and the output will appear below the cell.


## 4\. Acknowledgement of AI usage

This Readme was written with Gemini

Main Author of the code is Thomas Rost, Code itself was supported by AI (SHOULD be acknowledged in the files themselves but.. better safe than sorry)

=======
# HydrophoneAnomalies
An acoustic anomaly detection script for hydrophone recordings from the Statsraad Lehmkuhl. It uses PANNs embeddings and DBSCAN clustering to automatically find interesting sounds (e.g., marine life 🐋), while filtering out pings from the ship's own scientific instruments. The system saves clips and spectrograms of detected events for review.
