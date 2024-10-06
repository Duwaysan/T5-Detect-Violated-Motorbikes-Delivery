# Final Project: License Plate Detection and Traffic Violation Reporting
![LOGO](https://github.com/user-attachments/assets/9d031d62-00fa-4f74-b870-4d62e9d39eeb)
## Project Overview
This notebook implements a complete pipeline for detecting traffic violations, recognizing license plates, and sending automated email notifications for violations. The project leverages techniques in computer vision, optical character recognition (OCR), and automated email notification systems. The system aims to detect license plates from vehicles, identify violations such as "No Helmet" or "Entering Red Lane," and send a violation notification along with image evidence.


## Key Components

### 1. License Plate Detection and OCR
- **YOLOv8 Model**: A pre-trained YOLOv8 model is used to detect motorbikes and their license plates from input images. The model is fine-tuned for detecting various types of violations, such as riding without a helmet and entering restricted lanes.
- **GOT-OCR Transformer**: The detected license plates are passed through the `GOT-OCR2_0` model, a transformer-based model for Optical Character Recognition (OCR). This model extracts both Arabic and English characters from the license plates.

### 2. Data Preprocessing and Image Manipulation
- **Image Preprocessing**: Input images are converted from OpenCV format to PIL format for processing text overlays.
- **Text Overlay on Images**: The `draw_text_pil` function uses the Python Imaging Library (PIL) to overlay Arabic or English text on images, drawing the license plate number onto the detected motorbike in the image.

### 3. License Plate Text Processing
- **Text Filtering**: The `filter_license_plate_text` function cleanses the OCR-extracted text by removing unwanted characters and ensuring the license plate is in the correct format.
- **Conversion to Arabic**: The `convert_to_arabic` function converts English license plate characters into Arabic using a predefined dictionary mapping, ensuring compliance with local standards.

### 4. Traffic Violation Detection
- **Violation Types**: The notebook supports multiple types of violations, including:
  - No Helmet
  - Entering Red Lane
  - Combination of both (No Helmet + Entering Red Lane)

  Based on the detected violation type, the system automatically generates an email notification.

### 5. Email Notification System
- **Automated Email Notification**: The `send_email` function sends an email notification to the violator. The email includes:
  - The violation type (in Arabic)
  - The detected license plate number (in Arabic or English)
  - An image of the violation as an attachment

  The function supports multiple types of violations and constructs the email body accordingly, including the attachment of the violation image.

## Techniques and Libraries Used

### 1. Object Detection
- **YOLOv8**: Used for detecting motorbikes, helmets, and lanes from input images. This model provides accurate bounding boxes around objects of interest.

### 2. Optical Character Recognition (OCR)
- **GOT-OCR2_0**: A transformer-based OCR model that recognizes both Arabic and English license plates. This model extracts text directly from images of license plates and processes it for reporting.

### 3. Image Manipulation
- **OpenCV and PIL**: Used for image manipulation, including converting between image formats and drawing text onto images for visualization purposes.

### 4. Regular Expressions
- **Text Filtering**: Regular expressions are used to clean the OCR-extracted text, ensuring that only valid license plate formats are recognized.

### 5. Email Automation
- **SMTP**: The notebook uses Python's `smtplib` to automate the process of sending violation notifications via email. The email includes dynamically generated content based on the type of violation and the license plate detected.

## Setup and Usage

### Prerequisites
To run the notebook, you will need the following:

- Python 3.x
- Required libraries:
  - `transformers`
  - `opencv-python`
  - `Pillow`
  - `re`
  - `smtplib`
  - `email`
  - YOLOv8 (pre-trained model)

You can install the necessary packages using pip:

```bash
pip install transformers opencv-python Pillow smtplib email
