# License Plate Detection and Traffic Violation Reporting System
![LOGO](https://github.com/user-attachments/assets/3232c311-4448-4f3b-af6e-e5965c19d22b)

This project implements an end-to-end system for detecting traffic violations and automatically sending email notifications with evidence. Using a combination of YOLOv8 for object detection, an OCR model for license plate recognition, and an email notification system, the project aims to streamline traffic violation reporting.

## Project Overview
The system detects traffic violations such as *No Helmet* and *Entering Red Lane*, extracts the license plate number (in both Arabic and English), checks the license plate in a database for contact information, and sends an email notification to the violator. An image showing the violation is attached to the email.

## Key Features:
### 1. License Plate Detection and OCR:
- **YOLOv8 Model**: The system uses a fine-tuned YOLOv8 model to detect motorbikes, helmets, and lanes in input images. This model is pre-trained to identify motorbikes violating traffic rules, such as driving without a helmet or entering a restricted lane.
- **GOT-OCR Transformer**: The license plates detected by YOLOv8 are passed to the GOT-OCR2_0 transformer model for character recognition. This model supports both Arabic and English characters commonly found on Saudi Arabian license plates.
   
### 2. Data Preprocessing and Image Manipulation:
- **Image Preprocessing**: Input images are processed using OpenCV and converted to PIL format for text overlaying and image manipulation.
- **Text Overlay**: The `draw_text_pil` function overlays the detected license plate number (in Arabic or English) on the original image for better visualization.

### 3. License Plate Text Processing:
- **Text Filtering**: The OCR-extracted text is cleansed using the `filter_license_plate_text` function to remove unwanted characters and ensure proper formatting.
- **Conversion to Arabic**: The system can convert English characters on license plates to Arabic for better readability and compliance with local standards using the `convert_to_arabic` function.

### 4. Traffic Violation Detection:
- The system supports multiple traffic violation types:
  - No Helmet
  - Entering Red Lane
  - Combination of both (No Helmet + Entering Red Lane)
- Based on the detected violation, the system automatically generates a notification with all the necessary details.

### 5. Email Notification System:
- **Automated Email Sending**: The `send_email` function sends an email to the violator using the violator's contact information retrieved from a **license plate database**. The email includes:
  - The violation type (in Arabic)
  - The detected license plate number (in Arabic or English)
  - An attached image of the violation

## Techniques and Libraries Used:
### 1. Object Detection:
- **YOLOv8**: Pre-trained and fine-tuned to detect motorbikes, helmets, and lane violations with bounding boxes around the objects of interest.
   
### 2. Optical Character Recognition (OCR):
- **GOT-OCR2_0 Transformer**: A transformer-based OCR model capable of recognizing Arabic and English characters from license plates.

### 3. Image Manipulation:
- **OpenCV** and **Pillow (PIL)**: Used for image processing, conversion between formats, and adding visual elements such as text overlays.

### 4. Regular Expressions:
- **Text Filtering**: Regular expressions are used to filter and format OCR-extracted license plate text.

### 5. Email Automation:
- **SMTP**: Python's `smtplib` is used to send email notifications automatically, including dynamically generated email content and image attachments.

### 6. Database Lookup:
- **License Plate Database**: The system checks the detected license plate in a pre-existing database to retrieve the contact information of the vehicle owner. This information is used to send the violation email. 

## Setup and Usage

### Prerequisites:
- **Python 3.x**
- Required libraries:
  - `transformers`
  - `opencv-python`
  - `Pillow`
  - `re`
  - `smtplib`
  - `email`
  - YOLOv8 (pre-trained model)
  - A database for storing license plate contact information

You can install the necessary packages using pip:

```bash
pip install transformers opencv-python Pillow smtplib email
