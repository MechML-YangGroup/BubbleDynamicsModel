# Bubble Dynamics Transformer (BDT) — Web Apps (Hugging Face)

This project provides **browser-based** tools for analyzing **bubble dynamics** data and inferring material properties using **Bubble Dynamics Transformer (BDT)** models.  
No local installation is required — everything runs directly in your browser via **Hugging Face Spaces**.

---

## 🌐 Live Web Apps

### ✅ BDT (Joint Inference: **G & μ**)
**Link:** https://huggingface.co/spaces/lehuaaa/BDT  

- Predicts **shear modulus** \(G\) and **viscosity** \(\mu\)
- Includes data processing, ML inference, validation, and export

---

### ✅ BDT — Viscosity Only (Inference: **μ only**)
**Link:** https://huggingface.co/spaces/lehuaaa/BDT_Viscosity_Only  

- Predicts **viscosity** \(\mu\) only  
- \(G\) is treated as a constant in this version (model/app workflow)

---

## ✨ Features

- 📂 **Data Loading**: Upload and analyze `.mat` files containing bubble dynamics data  
- ⚙️ **Data Processing**: Clean and interpolate experimental R–t curves  
- 🤖 **ML Prediction**: Predict material properties using trained BDT models  
- ✅ **Validation**: Compare experimental vs physics-based simulation results  
- 📊 **Export**: Download processed data, prediction summaries, and simulations  

---

## 🚀 Quick Start Workflow (End-to-End)

### 1) Open a Web App
Choose the correct platform:

- **BDT (G & μ):** https://huggingface.co/spaces/lehuaaa/BDT  
- **BDT_Viscosity_Only (μ only):** https://huggingface.co/spaces/lehuaaa/BDT_Viscosity_Only  

---

### 2) Upload Experimental Data (`.mat`)
Navigate to **📂 Data Loading** and upload your experimental `.mat` file.

✅ **Important:** Your `.mat` file must follow the required format below.

---

### 3) Process Data (Interpolation)
Navigate to **⚙️ Data Processing**:

1. Select one dataset/curve  
2. Choose interpolation range and time step  
3. Click **🔄 Process Data**

The app will automatically:
- Replace NaNs (if any) with valid values  
- Remove invalid points (Inf)  
- Sort time points and remove duplicates  
- Generate an interpolated R–t curve suitable for inference/validation  

---

### 4) Upload the Trained ML Model
Navigate to **🤖 ML Prediction** and upload the trained model.

The trained models are hosted in this GitHub repo:

👉 **BubbleDynamicsModel:** https://github.com/MechML-YangGroup/BubbleDynamicsModel  

Inside that repository:

- `BDT/` → trained model for **joint inference (G & μ)**  
- `BDT_viscosity_only/` → trained model for **viscosity-only inference (μ)**  

✅ Supported model formats:
- `.h5` *(recommended)*
- `.keras`
- `.zip` (SavedModel format zipped as a folder)

Optional:
- `model_config.npy` (if provided in the repo)

---

### 5) Run ML Inference
In **🤖 ML Prediction**, you can either:

✅ **Option A (recommended): Use current processed data**
- Click **📊 Use Current Processed Data**

✅ **Option B: Upload test curve**
- Upload a `.txt` file containing a processed/interpolated curve

Then click:
- **🚀 Predict G & μ** (BDT Space)
- **🚀 Predict μ** (BDT_Viscosity_Only Space)

---

### 6) Validate Prediction by Simulation
Navigate to **✅ Validation** and click:

✅ **🚀 Run Validation Simulation**

The validation compares:
- **Experimental curve** (processed + interpolated)  
vs.  
- **Physics-based simulation** using the predicted properties  

Outputs include:
- Comparison plot (R–t overlay)
- Error metrics (RMSE / MAE / Max Error)

---

### 7) Export Results
Navigate to **📊 Results & Export** to download:

- ✅ Interpolated experimental curve  
- ✅ ML prediction summary  
- ✅ Simulation curve data  
- ✅ Visual comparison results  

---

## 📁 Required `.mat` Data Format

Your uploaded `.mat` file must contain the following variables:

### Required
- `R_nondim_All`  
- `t_nondim_All`

### Recommended
- `lambda_max_mean` (scalar)

---

### ✅ Expected Structure
`R_nondim_All` and `t_nondim_All` are typically MATLAB **cell arrays** with shape:

- `(1, N)` where `N` is the number of datasets/curves  
- each cell contains a **1D array** (one curve)

Example (MATLAB):
```matlab
R_nondim_All{1,i} = [ ... ]   % non-dimensional radius curve
t_nondim_All{1,i} = [ ... ]   % non-dimensional time curve
lambda_max_mean   = 5.99      % scalar (recommended)
```

---

## 🧪 Test Data for Users

The training repository includes **test data** for quick verification:

👉 https://github.com/MechML-YangGroup/BubbleDynamicsModel  

Users can upload the provided test `.mat` file(s) into the web app to run the full workflow:
**Data Loading → Processing → Prediction → Validation → Export**

---

## 🔧 Troubleshooting

### ❓ Upload `.mat` fails
Ensure your `.mat` contains:
- `R_nondim_All`
- `t_nondim_All`

If either is missing, the app will display an error.

---

### ❓ Processed curve looks wrong
Common causes:
- NaN/Inf values in raw input
- duplicated time points
- too few valid points after cleaning

Try:
- selecting a different dataset index
- re-exporting the `.mat` file with clean values

---

### ❓ Model loading fails
Make sure you upload a supported model file:
- `.h5` / `.keras` (recommended)
- `.zip` must contain a valid `saved_model.pb`

If using SavedModel:
- zip the **entire folder**, not just individual files

---

## 📌 Model Repository (Training + Test Data)

👉 https://github.com/MechML-YangGroup/BubbleDynamicsModel  

- `BDT/` → joint inference model (**G & μ**)  
- `BDT_viscosity_only/` → viscosity-only model (**μ**)  
- test data included for users  

---

## 📬 Contact
For questions, bug reports, or collaboration, please contact the maintainers from **MechML – Yang Research Group**.
