# Lab 1: Python SSH Assignment

## Objective
Build an SSH Crawler that remotely connects to a Linux SSH server and extracts directory contents. This lab focuses on establishing SSH connections, remote file system operations, and data processing using Python.

## Prerequisites
- Working Linux environment with SSH configured
- Python 3.x installed
- SSH server access (local or remote)
- Basic understanding of SSH protocols and Python programming

## Environment Setup
Ensure you have:
1. A working Linux and Python environment
2. SSH configured in your Linux environment
3. Access to an SSH server for testing

## Assignment Requirements

### Task 1: SSH Connection and Data Extraction
Create a Python script that:
- Remotely connects to your Linux SSH server
- Extracts the contents of the `/usr/bin` directory
- Collects file name and modification date for each file
- Uses configurable HOSTNAME and PORT as function arguments

### Task 2: Data Processing and Display
The script should generate two tables:
1. **Table 1**: Display name and modification date sorted by file name in ascending order
2. **Table 2**: Display name and modification date sorted by modification date from newest to oldest

### Technical Requirements
- Implement proper error handling for connection failures
- Make HOSTNAME and PORT configurable as function arguments
- Include proper documentation and comments

## Deliverables

Submit a **ZIP file** containing:
- **CSCI61-[Section]-[StudentID]-[LastName]-SSHCrawler.py**
- **requirements.txt** (if additional packages are needed)

**ZIP file naming convention**:
`CSCI61-[Section]-[StudentID]-[LastName]-Lab01.zip`

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

Lab 1: Python SSH Assignment
Student: [Your Name]
Student ID: [Your ID]
Email: [Your Email]
"""

# Add your imports here

def ssh_crawler(hostname, port=22):
    """
    Connect to SSH server and extract /usr/bin directory contents
    
    Args:
        hostname (str): SSH server hostname or IP
        port (int): SSH server port (default: 22)
    
    Returns:
        list: List of tuples containing (filename, modification_date)
    """
    # Your implementation here
    pass

def display_tables(file_data):
    """
    Display two sorted tables of file data
    
    Args:
        file_data (list): List of tuples containing (filename, modification_date)
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

- SSH connection implementation (15 points)
- Directory content extraction (15 points)
- Table 1: Filename sorting (10 points)
- Table 2: Date sorting (10 points)

### Deduction Criteria
- Missing Certificate of Authorship: -5 points
- Incorrect file naming: -5 points
- Including virtual environments: -10 points
- Late submission: As per course policy

## Hints
- You can use the `paramiko` Python library for SSH connections
- Consider using `stat` command or similar for file modification dates
- Handle SSH authentication properly (keys or password)
- Test your connection before implementing the full crawler

## Resources
- [Paramiko Documentation](https://docs.paramiko.org/)
- Python `datetime` module for date formatting
- SSH key authentication best practices
