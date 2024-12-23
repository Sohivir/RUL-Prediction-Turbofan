# Turbofan Degradation Prediction Using LSTM

## 1. What are Turbofans?
Turbofans are a type of jet engine widely used in aviation. They combine the benefits of turbojet engines and propellers, providing a high thrust-to-weight ratio and fuel efficiency. Turbofan engines operate by drawing in air, compressing it, mixing it with fuel for combustion, and expelling the exhaust to generate thrust. Over time, these engines degrade due to wear and tear, making it essential to predict their Remaining Useful Life (RUL) to ensure safety and optimize maintenance.

---

## 2. NASA Turbofan Degradation Dataset
The **NASA CMAPSS Dataset** (Commercial Modular Aero-Propulsion System Simulation) is a benchmark dataset used for predictive maintenance of turbofan engines. 

![image](https://github.com/user-attachments/assets/70ccd721-5786-4ff5-98c2-800403348f55)
### Dataset Overview:
- **Features:**
  - 3 operational settings: `setting_1`, `setting_2`, `setting_3`.
  - 21 sensor readings: `s_1` to `s_21` (given in the image).
- **Columns:**
  - `unit_nr`: The unit ID of the engine.
  - `time_cycles`: The operational cycles of the engine.
  - Target column: **RUL (Remaining Useful Life)** for each engine.
- **Train Data:** Data up to engine failure.
- **Test Data:** Data up to the last recorded operational cycle, with RUL values provided in a separate file.

### Dataset Usage:
The dataset captures how engine sensors behave as the engine approaches failure, making it ideal for RUL prediction using time-series models like LSTMs.

---

## 3. LSTM Architecture for RUL Prediction
The model leverages a Long Short-Term Memory (LSTM) network, a type of recurrent neural network (RNN) well-suited for time-series data.

### Model Architecture:
1. **Input Layer:**
   - A sliding window of size 30 is used to feed sequential time-series data (24 features per time step).

2. **LSTM Layer:**
   - A single LSTM layer with 64 neurons captures temporal dependencies between sensor readings over the time window.

3. **Dense Layer:**
   - A fully connected layer processes the output of the LSTM layer.

4. **Output Layer:**
   - A single neuron outputs the predicted RUL.

### Key Parameters:
- **Loss Function:** Mean Squared Error (MSE).
- **Optimizer:** Adam.
- **Batch Size:** 64.
- **Sliding Window Size:** 30.

---

## 4. Project Highlights
### Challenges Faced:
- Scaling the features while ensuring consistency across train and test datasets.
- Predicting RUL for engines in the test dataset based on the last 30 operational cycles.
- Understanding the contribution of each feature to the model's predictions.

### Solutions:
- MinMaxScaler was applied consistently to both train and test datasets.
- The model was trained on sliding windows of data, and predictions for the test dataset were made using the last 30 rows for each engine.
- Feature importance was derived using **SHAP (SHapley Additive exPlanations)** to analyze the impact of each sensor on RUL predictions.

---

## 5. How to Run the Code
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/turbofan-lstm-rul.git
   cd turbofan-lstm-rul
