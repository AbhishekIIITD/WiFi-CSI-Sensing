# WiFi-CSI-Sensing

# WiFi Sensing using Channel State Information (CSI)  

This repository contains the implementation and analysis for **Assignment 4: WiFi Sensing through Channel State Information (CSI)** for the Wireless Network course. The goal of this project was to explore the effectiveness of WiFi sensing under varied conditions using few-shot learning techniques.  

## Project Objective  

WiFi sensing uses Channel State Information (CSI) to monitor environmental changes and human activities. This project evaluates WiFi sensing robustness in diverse experimental settings, including variations in participants and obstacles. Few-shot learning techniques were applied to improve sensing adaptability under unseen settings.

## Dataset  

The CSI data contains 7 head gesticulations captured under three obstacle types:  
- **Fiber**  
- **Wood**  
- **Glass**  

For each obstacle, the dataset includes files labeled by participant IDs (`P26-P30`) and head gestures:  
1. Looking forward  
2. Looking down  
3. Looking up  
4. Looking left  
5. Looking right  
6. Nodding  
7. Shaking  

### Preprocessing Steps  

1. Removed the first 128 columns (legacy header CSI data).  
2. Removed pilot and null subcarriers.  
3. Computed the amplitude for each subcarrier using:  
   \[
   \text{Amplitude} = \sqrt{\text{real}^2 + \text{imaginary}^2}
   \]  
4. Denoised the data using the following filters:  
   - Hampel filter  
   - 1-D wavelet transform filter  
   - Savitzky-Golay filter  

### Training Strategy  

- **Few-shot learning**: CSI files from two obstacle types were used for training, while the third obstacle type was reserved for testing.  
- Prepared separate training and testing datasets for each material combination.  

### Model Evaluation  

The trained model was evaluated on unseen data. Few samples were selected for retraining to observe its impact on testing accuracy.  

#### Key Metrics Reported  

- Number of retraining samples  
- Testing samples  
- Retraining time (s)  
- Testing time (s)  
- Testing accuracy  

A graph was plotted to visualize the trade-off between retraining samples and accuracy.

### Experiment Results  

Retraining yielded marginal accuracy improvements, with varying retraining sample sizes showing the following results:  

| Retraining Samples | Testing Accuracy | Retraining Time (s) | Testing Time (s) |  
|--------------------|------------------|---------------------|------------------|  
| 1000              | 37.57%          | 4.76               | 11.87           |  
| 5000              | 37.56%          | 34.94              | 11.74           |  
| ...               | ...             | ...                | ...             |  

(*Refer to the full report for more details.*)

---

## Repository Structure  

- `data/`: Preprocessed CSI files and folders categorized by participant IDs and obstacle types.  
- `src/`: Source code for preprocessing, training, and evaluation.  
- `results/`: Graphs, accuracy tables, and other visualizations.  
- `report.pdf`: Detailed analysis and findings.  

## Usage Instructions  

1. Clone this repository:  
   ```bash  
   git clone https://github.com/your-username/wifi-sensing-csi.git  
   ```  
2. Install the required dependencies:  
   ```bash  
   pip install -r requirements.txt  
   ```  
3. Preprocess the dataset using:  
   ```bash  
   python src/preprocess.py  
   ```  
4. Train and evaluate the model:  
   ```bash  
   python src/train.py  
   ```  

## Findings  

1. Small retraining sample sizes are computationally efficient but offer limited accuracy improvement.  
2. Larger sample sizes improve accuracy but at the cost of increased computational time and potential overfitting.  

---
