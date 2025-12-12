# 😷 Face Mask Detection (Haar Cascade Implementation)

![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green?style=for-the-badge&logo=opencv)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?style=for-the-badge&logo=windows)

A real-time computer vision application that detects face masks using **Haar Cascade Classifiers**. Unlike heavy deep learning models, this project uses a lightweight "negative detection" logic—determining if a person is masked by checking for the *absence* of nose and mouth features.

---

## 📖 Table of Contents
- [How It Works](#-how-it-works)
- [Technical Configuration](#-technical-configuration)
- [Installation & Setup](#-installation--setup)
- [Project Structure](#-project-structure)
- [Limitations & Known Issues](#-limitations--known-issues)
- [Future Scope](#-future-scope)

---

## 🚀 How It Works

The system processes the video feed in three stages:
1.  **Face Detection**: Scans the frame for a frontal face using standard Haar features.
2.  **Region of Interest (ROI)**: Isolates the detected face area to reduce processing power.
3.  **Feature Logic**:
    * Scans the ROI for a **Nose** and a **Mouth**.
    * **Assumption**: If a face is present but the nose and mouth are *not* detected, they are likely covered by a mask.
    * **Result**: 
        * `No Nose + No Mouth` = 🟢 **"Masked Person"**
        * `Nose OR Mouth Detected` = 🔴 **"UnMasked Person"**

---

## ⚙️ Technical Configuration

The script uses specific tuning parameters for the Haar Cascades to balance speed and accuracy:

| Classifier | Scale Factor | Min Neighbors | Description |
| :--- | :--- | :--- | :--- |
| **Face** | Default | `5` | Base detection for the face region. |
| **Nose** | `1.3` | `5` | High scale factor to detect prominent nose shapes. |
| **Mouth** | `1.25` | `5` | Adjusted to detect mouth regions within the face ROI. |

*Note: The code logic flips the webcam feed horizontally (`cv2.flip(img, 1)`) for a mirror-like experience.*

---

## 💻 Installation & Setup

### Prerequisites
* Python 3.x
* A working webcam

### 1. Clone the Repository
```bash
git clone <repository-url>
cd mask-detection-haar-cascades-only
2. Create a Virtual Environment (Windows)
It is recommended to use a virtual environment to manage dependencies.

Bash

python -m venv venv
.\venv\Scripts\activate
3. Install Dependencies
Bash

pip install opencv-python
4. Run the Application
Ensure the .xml cascade files are in the same folder as the notebook/script.

Bash

# If running via Jupyter Notebook
jupyter notebook mask.ipynb
Press q on your keyboard to close the webcam window and stop the program.

📂 Project Structure
Plaintext

├── .vscode/
│   └── settings.json          # VS Code environment configuration
├── haarcascade_frontalface_default.xml  # Pre-trained face model
├── haarcascade_mcs_mouth.xml            # Pre-trained mouth model
├── haarcascade_mcs_nose.xml             # Pre-trained nose model
├── mask.ipynb                 # Main application logic
└── README.md                  # Project documentation
⚠️ Limitations & Known Issues
Lighting Sensitivity: Haar cascades struggle in low-light environments, which may lead to failure in detecting the face entirely.

Occlusion False Positives: Covering your mouth with your hand may be interpreted as "Masked" because the algorithm only looks for feature absence.

Side Profiles: The frontalface classifier does not detect faces turned to the side.

🔮 Future Scope
To improve robustness, future versions of this project could include:

Deep Learning Integration: Replacing Haar Cascades with MobileNetV2 or MTCNN for better accuracy in complex lighting.

Mask Type Classification: Distinguishing between N95, surgical, and cloth masks.

Distance Estimation: Alerting users if they are too close to the camera while unmasked.