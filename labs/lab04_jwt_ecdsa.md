# Lab 4: JWT ECDSA

## Objective
Extend your JWT implementation from Lab 3 to include JWT signature validation using ECDSA public key cryptography. This lab focuses on understanding JWT signature verification, public key cryptography, and security implications of JWT tokens.

## Prerequisites
- Completed [Lab 3: Introduction to JWT](lab03_introduction_to_jwt.md)
- Python 3.x installed
- Understanding of public key cryptography
- Basic knowledge of ECDSA (Elliptic Curve Digital Signature Algorithm)

## Background
JWT tokens are signed to ensure their integrity and authenticity. This assignment demonstrates how to validate JWT signatures using ECDSA public key cryptography, building upon your previous JWT authentication implementation.

## Assignment Requirements

### Task 1: Extend Previous Implementation
Starting from your Lab 3 code:
- Use the same JWT authentication functionality
- Maintain the user creation capability
- Add JWT signature validation functionality

### Task 2: JWT Signature Validation
Implement a function that:
- Takes a JWT token as input
- Uses the provided ECDSA public key to validate the token signature
- Returns validation result (valid/invalid)
- Handles validation errors appropriately

### Task 3: Analysis and Documentation
In your code comments, provide detailed answers to:
1. Is it safe to share this public key with you? Why or why not?
2. Can this key be used to generate a valid JWT token? Expound on your answer.
3. How can this be used in real-world application development?

## API Information

**Base URL and Credentials**: Available on Canvas

**Endpoints**:
- Authentication: `/api/v1/users/login`
- User Creation: `/api/v1/users`

**Public Key**: Available on Canvas

## Deliverables

Submit a **ZIP file** containing:
- **CSCI61-[Section]-[StudentID]-[LastName]-JWT-ECDSA.py**
- **requirements.txt** (if additional packages are needed)

**ZIP file naming convention**:
`CSCI61-[Section]-[StudentID]-[LastName]-Lab04.zip`

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

Lab 4: JWT ECDSA
Student: [Your Name]
Student ID: [Your ID]
Email: [Your Email]

Guide Questions Analysis:

1. Is it safe to share this public key with you? Why or why not?
   Answer: [Answer]

2. Can this key be used to generate a valid JWT token? Expound on your answer.
   Answer: [Answer]

3. How can this be used in real-world application development?
   Answer: [Answer]
"""

# Add your imports here

def get_jwt_token():
    """
    Authenticate with API and obtain JWT token
    (From Lab 3 implementation)
    
    Returns:
        str: JWT token if successful, None otherwise
    """
    # Your implementation from Lab 3
    pass

def validate_jwt_signature(token):
    """
    Validate JWT token signature using ECDSA public key
    
    Args:
        token (str): JWT token to validate
        
    Returns:
        bool: True if signature is valid, False otherwise
    """
    # Your implementation here
    pass

def create_user(token, email):
    """
    Create new user using JWT token
    (From Lab 3 implementation)
    
    Args:
        token (str): JWT authentication token
        email (str): Student email address
        
    Returns:
        bool: True if user created successfully, False otherwise
    """
    # Your implementation from Lab 3
    pass

if __name__ == "__main__":
    # Your main execution code here
    # Include JWT validation in your workflow
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

- JWT signature validation implementation (20 points)
- Integration with Lab 3 functionality (10 points)
- Guide question analysis (15 points)
- Error handling and code quality (5 points)

### Deduction Criteria
- Missing Certificate of Authorship: -5 points
- Incorrect file naming: -5 points
- Including virtual environments: -10 points
- Missing or incomplete guide question answers: -10 points
- Late submission: As per course policy

## Hints
- JWT tokens have three parts: header, payload, and signature
- ECDSA public keys can verify signatures but cannot create them
- Public key cryptography enables secure signature verification
- Consider the security implications of public vs private keys
