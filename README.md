# LicensePlate Detection and Traffic Violation Reporting System
![LOGO](https://github.com/user-attachments/assets/a1e397ad-2b6c-4d79-ba72-cc902868c788)

This project implements an end-to-end system for detecting traffic violations and automatically sending email notifications with evidence. Using a combination of YOLOv8 for object detection, an OCR model for license plate recognition, and an email notification system, the project aims to streamline traffic violation reporting.
## TEAM
- Khaled Alduwaysan      [Github](https://github.com/khaled-alduwaysan)  |  [Linkedin](https://www.linkedin.com/in/kduwaysan/)
- Abdulrahman Alghamdi   [Github](https://github.com/AbdulrhmanBakrgh)  |  [Linkedin](https://linkedin.com/in/abdulrahman-alghamdi)
- Nasser Alsaqer         [Github](https://github.com/NasserAlsaqer)  |  [Linkedin](https://www.linkedin.com/in/nasser-alsaqer/)
- Fares Altoukhi         [Github](https://github.com/TheKnight909)  |  [Linkedin](https://www.linkedin.com/in/fares-altoukhi/)
- Alhanouf Alhumid       [Github](https://github.com/alhanoufalh)  |  [Linkedin](https://www.linkedin.com/in/alhanouf-alhumid-40a7391b0/?originalSubdomain=sa)
## Project Overview
The system detects traffic violations such as *No Helmet* and *Entering Red Lane*, extracts the license plate number (in both Arabic and English), checks the license plate in a database for contact information, and sends an email notification to the violator. An image showing the violation is attached to the email.

## Process Overview:

![process_flow](https://github.com/user-attachments/assets/a539e6fb-ef62-4f4f-a75e-3e898daeec1c)

1. **Raw Image**: The process starts with an image of the motorbike captured from a traffic camera.
2. **YOLOv8 Detection**: YOLOv8 is used to detect the motorbike, the license plate, and whether the rider is wearing a helmet.
3. **Lane Boundary Detection**: The system checks whether the motorbike is in a restricted lane, like the red lane, where bikes are not allowed.
4. **OCR Detection**: The GOT-OCR2_0 model extracts the license plate characters in both Arabic and English.
5. **Database Integration**: The detected license plate is cross-referenced with a database that stores the violator's contact details, such as email and phone number.
6. **Email Integration**: A violation report is generated and sent via email to the violator with an image of the violation and license plate details.

## Demo

### Video Demo:

[Watch the full system demo here](https://youtu.be/LgCqOEWqY0A?feature=shared)

- **YOLOv8 Detection**: Detects motorbikes, helmets, and lanes in real time.
- **OCR in Action**: Recognizes both Arabic and English characters from license plates.
- **Violation Detection**: Identifies and logs violations like "No Helmet" and "Entering Red Lane."
- **Email Notification**: Automatically sends a violation report with an attached image of the offense.

![Lane_violation](https://github.com/user-attachments/assets/5da05a03-e676-4ffd-8b8c-6424977d1c74)



### Steps to Run the Demo:

1. **Upload Images**: Upload images or video frames to the system.
2. **YOLOv8 Model**: The model detects motorbikes, helmets, and restricted lanes.
3. **OCR**: The system extracts the license plate number using GOT-OCR2_0 and cross-references the database.
4. **Violation Report**: A report is generated and sent via email, containing details of the violation, the license plate, and the attached image.

## Key Features:
### 1. License Plate Detection and OCR:
- **YOLOv8 Model**: The system uses a fine-tuned YOLOv8 model to detect motorbikes, helmets, and lanes in input images. This model is pre-trained to identify motorbikes violating traffic rules, such as driving without a helmet or entering a restricted lane.
- **GOT-OCR Transformer**: The license plates detected by YOLOv8 are passed to the GOT-OCR2_0 transformer model for character recognition. This model supports English characters commonly found on Saudi Arabian license plates.
   
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
- **GOT-OCR2_0 Transformer**: A transformer-based OCR model capable of recognizing English characters from license plates.

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
  - `torch`
  - `datasets`
  - `ultralytics`
  - `numpy`
  - `matplotlib`

You can install the necessary packages using pip:

```bash
pip install transformers opencv-python Pillow smtplib email torch datasets yolov5 numpy matplotlib
