## RoleFitAPI

RoleFitAPI is a specialized resume analysis engine designed to evaluate the alignment between a candidate's background and specific job profiles. The system utilizes natural language processing (NLP) to extract skills, perform lemmatized token matching, and generate weighted relevance scores to assist in automating the initial screening process.

### Features

*   **NLP-Powered Extraction**: Utilizes the spaCy library for advanced text cleaning, stop-word removal, and lemmatization.
*   **Intelligent Token Overlap**: Implements a threshold-based matching algorithm to identify skills even when phrased differently in the source text.
*   **Weighted Scoring Model**: Calculates relevance based on specific category weights, including clinical skills (35%), technical skills (35%), certifications (20%), and soft skills (10%).
*   **Structured Data Output**: Returns a detailed JSON response featuring role-wise matches and specific skill breakdowns.
*   **FastAPI Integration**: Exposes core functionality through a FastAPI endpoint for easy integration into HR-tech ecosystems.

### Project Structure

RoleFitAPI/  
├── utils/  
│ ├── parser.py # Logic for reading various file formats  
│ ├── role\_profile.py # Skill definitions and role configurations  
│ └── skills\_extractor.py # Core NLP logic and scoring engine  
├── main.py # FastAPI entry point and routes  
├── requirements.txt # Project dependencies  
└── LICENSE # Project license  

### Installation

#### 1\. Clone the Repository

git clone https://github.com/yourusername/RoleFitAPI.git  
cd RoleFitAPI  

#### 2\. Configure Virtual Environment

python -m venv venv  
source venv/bin/activate # On Windows: venv\\Scripts\\activate  

#### 3\. Install Dependencies

pip install -r requirements.txt  
python -m spacy download en\_core\_web\_sm  

### Usage

#### Starting the Server

Run the FastAPI server using Uvicorn:

uvicorn main:app --reload  

#### API Reference

**Endpoint:** POST /analyze

**Request Body:**

JSON

{  
"resume\_text": "Insert raw resume text here"  
}  

**Example Response:**

JSON

{  
"Software Engineer": {  
"score": 82.5,  
"skills": {  
"technical\_skills": \[\["python", 4\], \["api design", 1\]\],  
"soft\_skills": \[\["leadership", 1\]\]  
}  
}  
}  

### Technical Methodology

The analysis follows a three-stage pipeline:

1.  **Preprocessing**: Text is converted to lowercase and cleaned of punctuation and stop-words. Every word is lemmatized to its root form to ensure "developing" matches "developer".
2.  **Overlap Calculation**: The system compares resume tokens against predefined role requirements. A match is confirmed if the overlap ratio meets the defined threshold.
3.  **Normalized Scoring**: A final score (out of 100) is calculated by multiplying the match ratio of each category by its assigned weight.

### Contributing

Contributions are welcome. Please follow the standard fork-and-pull-request workflow.

1.  Fork the Project.
2.  Create a Feature Branch.
3.  Commit Changes.
4.  Push to the Branch.
5.  Open a Pull Request.
