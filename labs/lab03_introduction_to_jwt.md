# Lab 3: Introduction to JWT

## Objective
Build a Python application that authenticates with a JWT-based API and creates a new user. This lab focuses on understanding JSON Web Tokens (JWT), API authentication, and HTTP request handling in Python.

## Prerequisites
- Python 3.x installed
- Understanding of HTTP requests and responses
- Basic knowledge of JSON Web Tokens (JWT)
- Familiarity with REST API concepts

## Background
JSON Web Tokens (JWT) are a compact, URL-safe means of representing claims between two parties. This assignment demonstrates JWT authentication flow and API interaction using Python.

## Assignment Requirements

### Task 1: JWT Authentication
Create a Python script that:
- Authenticates with the provided API using login credentials
- Obtains a JWT token from the authentication endpoint
- Handles authentication errors appropriately

### Task 2: User Creation
The script should:
- Use the obtained JWT token to authenticate API requests
- Create a new user with your student email address
- Handle API responses and errors properly

### Technical Requirements
- Use proper HTTP libraries (not curl wrappers)
- Implement JWT token handling
- Include proper error handling for API failures
- Validate API responses appropriately

## API Information

**Base URL and Credentials**: Available on Canvas

**Endpoints**:
- Authentication: `/api/v1/users/login`
- User Creation: `/api/v1/users`

## Deliverables

Submit a **ZIP file** containing:
- **CSCI61-[Section]-[StudentID]-[LastName]-JWT-Intro.py**
- **requirements.txt** (if additional packages are needed)

**ZIP file naming convention**:
`CSCI61-[Section]-[StudentID]-[LastName]-Lab03.zip`

**Python file format example**:
```python
"""
Certificate of Authorship:
I have not discussed the Python language code in my program with anyone 
other than my instructor or the teaching assistants assigned to this course.
I have not used Python language code obtained from another student, 
or any other unauthorized source, either modified or unmodified.
If any Python language code or documentation used in my program 
was obtained from another source, such as a textbook or course notes, 
that has been clearly noted with a proper citation in the comments of my program.

Lab 3: Introduction to JWT
Student: [Your Name]
Student ID: [Your ID]
Email: [Your Email]
"""

# Add your imports here

def get_jwt_token():
    """
    Authenticate with API and obtain JWT token
    
    Returns:
        str: JWT token if successful, None otherwise
    """
    # Your implementation here
    pass

def create_user(token, email):
    """
    Create new user using JWT token
    
    Args:
        token (str): JWT authentication token
        email (str): Student email address
        
    Returns:
        bool: True if user created successfully, False otherwise
    """
    # Your implementation here
    pass

if __name__ == "__main__":
    # Your main execution code here
    pass
```

**Note**: This is a sample skeleton. You are **expected** to add any other variables, constants, and utility functions as needed for your implementation.

## Important Submission Guidelines

### Virtual Environment Restrictions
**CRITICAL**: Do **NOT** include virtual environments in your submission. Including virtual environment directories (venv/, env/, .venv/, etc.) will result in **automatic point deductions**.

### File Structure
Your ZIP submission should contain **only**:
- Your Python script file
- requirements.txt (if needed)
- No additional directories or files

## Grading

**Total: 50 points**

- JWT authentication implementation (15 points)
- Token handling and storage (10 points)
- User creation API call (15 points)
- Error handling and validation (10 points)

### Deduction Criteria
- Missing Certificate of Authorship: -5 points
- Incorrect file naming: -5 points
- Including virtual environments: -10 points
- Late submission: As per course policy

## Hints
- Use `requests` library for HTTP operations
- JWT tokens are typically sent in Authorization header as "Bearer {token}"
- API endpoints may require specific Content-Type headers
- Handle HTTP status codes appropriately
- Store JWT token securely during script execution
