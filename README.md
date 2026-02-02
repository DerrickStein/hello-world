ID Card OCR and Face Verification Pipeline

This project provides a complete pipeline for extracting text from ID cards and verifying faces from ID images against selfies. It combines OCR, face detection, and similarity measurements using multiple methods.

**Features**

1. OCR Extraction

2. Uses EasyOCR to extract text from ID cards.

3,. Returns structured text data and optionally displays detected text with bounding boxes.

**Face Extraction**

1. Detects and extracts the largest face from images using OpenCV Haar Cascades.

2. Face Similarity

**Provides three similarity measures between faces:**

1. Histogram-based similarity

2. LBP (Local Binary Patterns) similarity

3. DeepFace similarity (using Facenet model)

4. Returns the highest similarity score as the face match percentage.

5. Structured Data Extraction

**Uses Google Colab AI to extract structured fields from OCR text:**

1. Full Name

2. Personal ID Number

3. Date of Birth

4. Expiry Date

5. Combines all extracted information with face match percentage in a dictionary.

**Installation**

**Install required Python libraries:**

1. pip install easyocr
2. pip install opencv-python numpy face-recognition
3. pip install deepface

**Usage**

1. OCR Extraction

2. full_text = extract_text_from_image('sample_data/sample_id.jpg')


**Face Extraction**

1. face_id = extract_face(img_id)
2. face_selfie = extract_face(img_selfie)


**Compute Face Similarity**

1. sim_hist = face_similarity_histogram(face_id, face_selfie)
2. sim_lbp  = face_similarity_lbp(face_id, face_selfie)
3. sim_df   = face_similarity_deepface(face_id, face_selfie)

4. face_match_percentage = round(max(filter(None,[sim_hist, sim_lbp, sim_df])), 4)


**Generate Structured Data**

1. import google.colab.ai as ai

2. fullname = ai.generate_text(f"Get just full name from this: {full_text}")
3. id_number = ai.generate_text(f"Get just Personal ID number from this: {full_text}")
4. date_of_birth = ai.generate_text(f"Get just date of birth from this: {full_text} with a date format")
5. expiry_date = ai.generate_text(f"Get just expiry date from this: {full_text} with a date format")

6. data = {
    "name": fullname,
    "id_number": id_number,
    "date_of_birth": date_of_birth,
    "expiry_date": expiry_date,
    "face_match_percentage": face_match_percentage
}

7. print("Final extracted data:", data)

8. Output Example
{
  "name": "John Doe",
  "id_number": "AB1234567",
  "date_of_birth": "1990-01-01",
  "expiry_date": "2030-01-01",
  "face_match_percentage": 0.89
}
