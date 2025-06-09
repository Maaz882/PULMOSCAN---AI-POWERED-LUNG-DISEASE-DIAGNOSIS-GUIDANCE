# Lung Disease Detection with Deep Learning and GUI

A deep learning-powered system to detect lung diseases from chest X-ray images with a user-friendly graphical interface.
It also recommends nearby hospitals based on detected disease and user location.

## Features

 Train a deep learning model (Xception-based) on chest X-ray images
 GUI for loading X-ray images and viewing predictions
 Location-based hospital recommendations using geolocation APIs
 Stores user profile and history in MySQL database
 Displays maps and distances to recommended hospitals

 ## Screenshots
 
![Screenshot 1 165602](https://github.com/user-attachments/assets/cb8c310a-8a67-4bc3-97f2-8ba17ec9c322)
![Screenshot 2 165620](https://github.com/user-attachments/assets/ade189dd-d8a0-4a07-8cb5-8964bdd49e89)
![Screenshot 3 165729](https://github.com/user-attachments/assets/ba8982c8-d326-403a-8c48-83997c457d6d)
![Screenshot 4 165749](https://github.com/user-attachments/assets/b6b9ff03-a676-44fb-8c78-ae68b78404c2)
![Screenshot 5 165827](https://github.com/user-attachments/assets/dbaad71a-2748-4abc-bc7d-37ab319cd325)

## Install Required Libraries

```bash
pip install tensorflow==2.15 keras==2.15 opencv-python matplotlib customtkinter mysql-connector-python geopy folium Pillow requests
```
## Usage Instructions

### 1.**Model Training**

 -**Open trainingmodel1.ipynb in Jupyter Notebook or VS Code.
 -**Configure your dataset paths.
 -**Run the notebook to:
 -**Preprocess data
 -**Train the model (Xception-based)
 -**Save the trained model as best_lung_disease_model.h5

### 2.***Launch the GUI**

-**Open GUI3.7.ipynb in Jupyter Notebook or VS Code.
-**Modify model path if required:
```bash
tf.keras.models.load_model('best_lung_disease_model.h5')
```
-**Configure your MySQL database connection inside the notebook.
-**Run the notebook to launch the GUI window:
  -**Upload an X-ray image.
  -**View detected disease.
  -**View top recommended hospitals near you (based on stored locations).
  -**Map is generated with Folium.

## MySQL Database Setup

Create a database and table to store:

### Create the database:

```sql
CREATE DATABASE lung_disease_detection;
USE lung_disease_detection;
```

### Table: `users`

Stores user profile and location data.

```sql
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    user_name VARCHAR(255) UNIQUE NOT NULL,
    location VARCHAR(255),
    latitude DECIMAL(35,15),
    longitude DECIMAL(35,15)
);
```

### Table: `diseases`

Stores disease information, symptoms, cure, and prescriptions.

```sql
CREATE TABLE diseases (
    name VARCHAR(100) PRIMARY KEY,
    info TEXT,
    symptoms TEXT,
    cure TEXT,
    prescription TEXT
);
```
### Table: `history`

Stores prediction history for each user.

```sql
CREATE TABLE history (
    history_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    image_path TEXT,
    predicted_class VARCHAR(255),
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);
```
### Table: `hospitals`

Stores hospital details, specialties, doctor info, and geolocation data.

```sql
CREATE TABLE hospitals (
    hospital_id INT PRIMARY KEY,
    name VARCHAR(255),
    address TEXT,
    latitude DECIMAL(35,15),
    longitude DECIMAL(35,15),
    specialties TEXT,
    doctor_name VARCHAR(255),
    contact_info VARCHAR(255)
);
```


