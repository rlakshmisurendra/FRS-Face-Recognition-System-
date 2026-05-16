# Face Recognition Attendance System

A Python-based attendance tracker that uses face recognition to mark daily attendance from a webcam feed and store records in SQLite.

## Project Structure

```text
.
├── app.py                            # Flask UI to view attendance by date
├── attendance_taker.py               # Live webcam recognition + attendance marking
├── features_extraction_to_csv.py     # Builds face embeddings CSV from saved face images
├── get_faces_from_camera_tkinter.py  # Tkinter app to collect and register face images
├── templates/index.html              # Flask template for attendance viewer
├── requirements.txt                  # Python dependencies
└── data/
    └── data_dlib/
        ├── dlib_face_recognition_resnet_model_v1.dat
        └── shape_predictor_68_face_landmarks.dat
```

## Features

- Register face images with a GUI (`Tkinter` + webcam)
- Extract 128D face embeddings and save them to `data/features_all.csv`
- Recognize faces in real-time using dlib and OpenCV
- Mark attendance once per person per day in `attendance.db`
- View attendance records by date from a simple Flask web interface

## Prerequisites

- Python 3.8+ recommended
- Webcam access
- System dependencies needed by OpenCV/dlib

> This repository already includes required dlib model files under `data/data_dlib/`.

## Installation

1. Clone the repository.
2. Create and activate a virtual environment (recommended).
3. Install dependencies:

```bash
pip install -r requirements.txt
```

## End-to-End Usage

Run scripts from the repository root in this order:

### 1) Register faces

```bash
python get_faces_from_camera_tkinter.py
```

In the GUI:
- **Step 1**: (Optional) Clear existing face photos
- **Step 2**: Enter a person name and create a folder
- **Step 3**: Save multiple face images for that person

Registered images are saved under `data/data_faces_from_camera/`.

### 2) Extract features

```bash
python features_extraction_to_csv.py
```

This creates `data/features_all.csv` used by the recognizer.

### 3) Start attendance recognition

```bash
python attendance_taker.py
```

- Webcam opens and recognized faces are marked present in `attendance.db`
- Press **q** to quit

### 4) View attendance records

```bash
python app.py
```

Open the local Flask URL shown in terminal (typically `http://127.0.0.1:5000`) and select a date to view attendance.

## Data Files Generated at Runtime

- `data/data_faces_from_camera/` — captured face images grouped by person
- `data/features_all.csv` — face embeddings database
- `attendance.db` — SQLite attendance records (`name`, `time`, `date`)

## Troubleshooting

- **`features_all.csv` not found**: run `get_faces_from_camera_tkinter.py` and then `features_extraction_to_csv.py`.
- **No webcam input**: ensure camera permissions are enabled and not used by another app.
- **Poor recognition accuracy**: capture more clear, front-facing images per person.

## Contributing

Issues and pull requests are welcome.
