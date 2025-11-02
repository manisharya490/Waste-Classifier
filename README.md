# ♻️ Smart Waste Classifier

The **Smart Waste Classifier** is an intelligent web application designed to promote sustainable waste management by automatically identifying and categorizing waste materials using **Deep Learning** and **Computer Vision**. [cite_start]Users can capture a live photo or upload an image of a waste item, and the system provides an instant, highly accurate classification result[cite: 5, 20, 413].



---

## ✨ Features

* [cite_start]**Intelligent Classification:** Uses a fine-tuned **MobileNetV2 CNN** model, leveraging Transfer Learning, to classify waste into 10 categories (e.g., Plastic, Metal, Glass, Paper, Biological, etc.)[cite: 7, 23, 374].
* [cite_start]**High Accuracy:** The model achieves a robust **validation accuracy of over 90%**[cite: 36, 78, 416].
* [cite_start]**Automatic Object Cropping:** The **Flask** backend uses **OpenCV** to detect the largest contour of the waste item, cropping the image to remove background noise and ensure the model receives a clean, focused input for better prediction accuracy[cite: 40, 41, 167, 369, 370].
* [cite_start]**Real-Time Interface:** The frontend is built with HTML, CSS, and JavaScript, enabling live camera access and instantaneous display of the predicted waste category and confidence score[cite: 50, 51, 57, 145].
* [cite_start]**API Communication:** Uses a **Flask REST API** (`/predict` endpoint) to handle image reception, preprocessing, and model inference, with **Flask-CORS** enabled for seamless cross-origin communication[cite: 43, 44, 48, 159, 174].

---

## 🛠️ Technology Stack

This project is a full-stack ML application split into a Python backend and a JavaScript frontend.

### Backend (Python API - Deployed on **Render**)
| Component | Purpose |
| :--- | :--- |
| **Python** | [cite_start]Core programming language (3.8+) [cite: 108] |
| **Flask** | [cite_start]Web framework for the API server [cite: 109] |
| **TensorFlow/Keras** | [cite_start]Deep Learning library for model building and inference [cite: 110] |
| **MobileNetV2** | [cite_start]Base CNN model used for classification [cite: 33] |
| **OpenCV** | [cite_start]Image preprocessing and object cropping [cite: 39, 111] |
| **`flask-cors`** | [cite_start]Enables cross-origin requests [cite: 119] |
| **`gunicorn`** | Production WSGI server for Render deployment |

### Frontend (Web UI - Deployed on **Netlify**)
| Component | Purpose |
| :--- | :--- |
| **HTML5** | [cite_start]Structure of the web interface [cite: 114] |
| **CSS3** | [cite_start]Styling and responsive design [cite: 115] |
| **JavaScript (ES6)** | [cite_start]Client-side scripting, camera access, and API calls [cite: 116] |

---

## 🚀 Setup & Deployment Guide

This project requires a two-part deployment: the **API Backend** on Render and the **Static Frontend** on Netlify.

### 1. Local Setup (Development)

1.  **Clone the Repository:**
    ```bash
    git clone [YOUR_REPO_URL]
    cd Smart-Waste-Classifier
    ```
2.  **Install Dependencies:**
    * Ensure all necessary libraries are installed (TensorFlow, Flask, OpenCV, etc.).
    * If using a `requirements.txt` file (recommended):
        ```bash
        pip install -r requirements.txt
        ```
3.  [cite_start]**Download Model:** Place the pre-trained model file (`waste_classifier_model.h5` [cite: 37]) in your root directory.
4.  **Run the Backend:**
    ```bash
    python app.py
    # This will typically run on [http://127.0.0.1:5000/](http://127.0.0.1:5000/)
    ```
5.  **View Frontend:** Open the main HTML file (e.g., `index.html`) in your browser. (Note: You may need to update the API endpoint in the JS file to `http://127.0.0.1:5000/predict` for local testing).

---

### 2. Deployment on Render (Backend API)

1.  **Prepare for Render:** Ensure your `app.py` is configured for deployment (uses `gunicorn` in the start command and listens on `0.0.0.0` with the correct environment `PORT`).
2.  **Create New Web Service:** Connect your GitHub repository to Render.
3.  **Configuration:**
    * **Runtime:** Python 3
    * **Build Command:** `pip install -r requirements.txt`
    * **Start Command:** `gunicorn app:app` (Assuming your main Flask app instance is named `app` in `app.py`)
4.  **Save the Render URL:** Once deployed, copy the public URL (e.g., `https://[app-name].onrender.com`).

### 3. Deployment on Netlify (Static Frontend)

1.  **Update Frontend API Call:** In your main JavaScript file, update the `fetch` API call to use the absolute URL from Render (e.g., `const API_URL = 'https://[your-render-app].onrender.com/predict';`).
2.  **Create New Site:** Connect your GitHub repository to Netlify.
3.  **Configuration:**
    * **Build Command:** (Leave blank or `echo "No build step"`)
    * **Publish Directory:** Specify the folder containing your HTML, CSS, and JS (e.g., `static` or `templates`).
4.  **Deploy:** Netlify will host your static frontend, which will communicate with your Render backend.

---
