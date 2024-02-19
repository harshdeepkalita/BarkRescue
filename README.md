# Bark Rescue App:

## Introduction

The "Bar Rescue App" leverages artificial intelligence to support animal rescue operations. By analyzing user-submitted images, the app predicts:

- **Presence of dogs:** Determines if a dog is present in the image.
- **Dog's emotions:** Identifies the emotional state of the dog (e.g., scared, happy), if present.

This analysis facilitates the notification of relevant animal control centers for potential rescue actions.

## Tech Stack

- **Front-End:** HTML (JavaScript is optional for basic validation)
- **Back-End:** Spring Boot
- **Model Inference:** TorchServe (deployed on cloud platforms like Google Cloud AI Platform, Amazon SageMaker)
- **Machine Learning Models:**
  - **EfficientNet-B0:** For dog detection (classification)
  - **YOLOv5:** For bounding box detection (if a dog is detected)
  - **MobileNetV2:** For emotion recognition (if a dog is detected)

## Functionalities

1. **User submits image:** Through a simple HTML form.
2. **Preprocessing:** Images are resized and normalized for analysis.
3. **Dog Detection (Model 1):**
   - Utilizes the EfficientNet-B0 model, served via TorchServe, to calculate the probability of a dog's presence in the image.
4. **Conditional Processing:**
   - If the score is >= 0.5 (indicating a dog):
     - **Bounding Box (Model 2):**
       - YOLOv5 predicts a bounding box around the detected dog.
       - The image is preprocessed based on the bounding box coordinates.
     - **Emotion Recognition (Model 3):**
       - MobileNetV2 predicts the dog's emotional state from the cropped image.
   - If unlikely a dog, it skips to the next steps.
5. **Decision-Making:**
   - Emotion scores, especially negative ones like scared or anxious, are analyzed.
   - Contact (Email) is made with an animal control center based on the highest negative emotion score:
     - **< 0.4:** Considered non-threatening, and a nearby animal control center is contacted.
     - **> 0.4:** Considered potentially needing help, and the nearest possible animal control center is contacted.
6. **Notification:**
   - An automated notification, including user location and image of the dog is sent to the selected animal control center.
7. **Secure Communication:**
   - Implements HTTPS and encryption for all data transfers.
