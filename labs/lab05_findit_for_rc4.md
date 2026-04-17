# Lab 5: FindIT for RC4

## Objective
Modify the FindIT example to work with the RC4 encryption algorithm. This lab focuses on understanding stream ciphers, RC4 implementation, and cryptographic analysis techniques.

## Prerequisites
- Python 3.x installed
- Understanding of stream cipher algorithms
- Basic knowledge of RC4 encryption
- Familiarity with cryptographic key-value operations

## Background
RC4 is a stream cipher that was widely used in protocols such as SSL and WEP. This assignment demonstrates RC4 encryption/decryption and applies the FindIT methodology to analyze RC4-encrypted data.

## Assignment Requirements

### Task 1: RC4 Implementation
Use the provided RC4 algorithm implementation:
- Understand the key scheduling algorithm (KSA)
- Understand the pseudo-random generation algorithm (PRGA)
- Implement encryption and decryption using the same function

### Task 2: FindIT Modification
Modify the FindIT example to:
- Work with RC4 encryption instead of the original algorithm
- Use the same keys and examples from the FindIT exercise
- Demonstrate encryption and decryption capabilities
- Validate that decryption produces the original plaintext

### Technical Requirements
- Implement proper RC4 encryption/decryption
- Handle different key lengths appropriately
- Include proper error handling
- Provide clear output showing encryption and decryption results

## Reference RC4 Implementation

```python
# Implementation of RC4 algorithm
# Copyright (c) 2016, Jurriaan Bremer
def rc4(data, key):
    S, j, out = list(range(256)), 0, []

    for i in range(256):
        j = (j + S[i] + ord(key[i % len(key)])) % 256
        S[i], S[j] = S[j], S[i]

    i = j = 0
    for ch in data:
        i = (i + 1) % 256
        j = (j + S[i]) % 256
        S[i], S[j] = S[j], S[i]
        out.append(chr(ord(ch) ^ S[(S[i] + S[j]) % 256]))

    return "".join(out)
```

## Deliverables

Submit a **ZIP file** containing:
- **CSCI61-[Section]-[StudentID]-[LastName]-FindIT.py**
- **requirements.txt** (if additional packages are needed)

**ZIP file naming convention**:
`CSCI61-[Section]-[StudentID]-[LastName]-Lab05.zip`

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

Lab 5: FindIT for RC4
Student: [Your Name]
Student ID: [Your ID]
Email: [Your Email]
"""

# Add your imports here

def rc4(data, key):
    """
    RC4 encryption/decryption algorithm
    
    Args:
        data (str): Data to encrypt or decrypt
        key (str): Encryption key
        
    Returns:
        str: Encrypted or decrypted data
    """
    # Your implementation here
    pass

def findit_rc4():
    """
    FindIT implementation using RC4
    Demonstrates encryption and decryption with various keys and examples
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

**Total: 25 points**

- RC4 implementation (8 points)
- FindIT modification and integration (8 points)
- Encryption/decryption demonstration (5 points)
- Code quality and documentation (4 points)

### Deduction Criteria
- Missing Certificate of Authorship: -5 points
- Incorrect file naming: -5 points
- Including virtual environments: -10 points
- Late submission: As per course policy

## Hints
- RC4 is symmetric: the same function encrypts and decrypts
- Test with the example: "The quick brown foxes are jumping over the lazy dogs" with key "password"
- RC4 uses XOR operations for encryption
- The key scheduling algorithm initializes the state array
- Proper key handling is essential for correct encryption/decryption
