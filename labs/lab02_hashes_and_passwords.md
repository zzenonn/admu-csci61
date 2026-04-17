# Lab 2: Hashes and Passwords

## Objective
Build a Python application that validates user passwords against Kali Linux password file entries. This lab focuses on understanding password hashing, salt mechanisms, and secure password verification techniques.

## Prerequisites
- Python 3.x installed
- Linux environment (Kali Linux recommended)
- Understanding of cryptographic hashing algorithms
- Basic knowledge of Linux password storage mechanisms

## Background
Linux systems store password hashes in the shadow file (`/etc/shadow`) using various hashing algorithms with salt values. This assignment simulates the password verification process used by Linux authentication systems.

## Assignment Requirements

### Task 1: Password Hash Analysis
Create a Python script that:
- Contains a hardcoded password line from Kali Linux shadow file format
- Prompts the user to enter a password (use secure input method)
- Extracts the salt and hashing algorithm from the shadow entry
- Applies the proper hashing algorithm with salt to the user input

### Task 2: Password Verification
The script should:
- Compare the computed hash with the stored hash
- Display whether the password matches or not
- Handle errors appropriately

### Technical Requirements
- Implement proper salt extraction from shadow file format
- Use appropriate tools for password hashing
- Include proper error handling for invalid inputs
- Provide clear user feedback on verification results

## Deliverables

Submit a **ZIP file** containing:
- **CSCI61-[Section]-[StudentID]-[LastName]-HashesAndPasswords.py**
- **requirements.txt** (if additional packages are needed)

**ZIP file naming convention**:
`CSCI61-[Section]-[StudentID]-[LastName]-Lab02.zip`

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

Lab 2: Hashes and Passwords
Student: [Your Name]
Student ID: [Your ID]
Email: [Your Email]
"""

# Add your imports here

# Sample shadow file entry (use actual hash from Kali Linux)
stored_hash = "$y$j9T$salt$hash"

def verify_password(password):
    """
    Verify password against stored hash
    
    Args:
        password (str): Plain text password to verify
        
    Returns:
        bool: True if password matches, False otherwise
    """
    # Your implementation here
    pass

if __name__ == "__main__":
    # Your main execution code here
    pass
```

**Note**: This is a sample skeleton. You are **expected** to add any other variables, constants, and utility functions as needed for your implementation.

## Important Submission Guidelines

### Individual Assignment
This is an **individual assignment**. Collaboration is not permitted.

### Virtual Environment Restrictions
**CRITICAL**: Do **NOT** include virtual environments in your submission. Including virtual environment directories (venv/, env/, .venv/, etc.) will result in **automatic point deductions**.

### File Structure
Your ZIP submission should contain **only**:
- Your Python script file
- requirements.txt (if needed)
- No additional directories or files

## Grading

**Total: 50 points**

- Shadow file parsing and salt extraction (15 points)
- Hash generation implementation (15 points)
- Password verification logic (10 points)
- Error handling and user interface (10 points)

### Deduction Criteria
- Missing Certificate of Authorship: -5 points
- Incorrect file naming: -5 points
- Including virtual environments: -10 points
- Late submission: As per course policy

## Hints
- Linux shadow files use format: `username:$algorithm$salt$hash:...`
- Modern Kali Linux uses yescrypt algorithm (`$y$`)
- Use `getpass` module for secure password input
- The `mkpasswd` utility can generate hashes with specific salts
- Salt extraction requires parsing the hash string properly
- Consider using system utilities for hash generation
