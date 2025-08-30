# BugsInPy
BugsInPy: A Database of Existing Bugs in Python Programs to Enable Controlled Testing and Debugging Studies.
The objective of this work is to support reproducible research on real-world Python projects. 

# Steps to set up BugsInPy
1. Clone BugsInPy:
    - `git clone https://github.com/soarsmu/BugsInPy`
2. Add BugsInPy executables path:
    - `export PATH=$PATH:<bugsinpy_path>/framework/bin`

# BugsInPy Command
Command | Description
--- | ---
info | Get the information of a specific project or a specific bug
checkout | Checkout buggy or fixed version project from dataset
compile | Compile sources from project that have been checkout
test | Run test case that relevant with bug, single-test case from input user, or all test cases from project
coverage | Run code coverage analysis from test case that relevant with bug, single-test-case from input user, or all test cases
mutation | Run mutation analysis from input user or test case that relevant with bug
fuzz | Run a test input generation from specific bug

# Example BugsInPy Command
- Help usage from checkout command:
    - `bugsinpy-checkout --help`
- Checkout a buggy source code version (youtube-dl, bug 2, buggy version):
    - `bugsinpy-checkout -p youtube-dl -v 0 -i 2 -w /temp/projects`
- Compile sources and tests, and run tests from current directory:
    - `bugsinpy-compile`
    - `bugsinpy-test`

# My own examples
## Example 1: tqdm
`export PATH=$PATH:<bugsinpy_path>/framework/bin` (always needed. You can set it permanent.)
`bugsinpy-info -p tqdm`\
`bugsinpy-checkout -p tqdm -i 1` (We are cloning the github repo for the first bug)  
`cd framework/bin/temp/tqdm`\
(Note that you can do docker here, or create a virtual env installing the required packages)\
`cd ../../../../projects/tqdm/bugs/1`\
`pip install -r requirements.txt` (Go back to the project bug folder and install the env for testing. 'pkg-resources==0.0.0' can be skipped if throws error)
`cd ../../../../framework/bin/temp/tqdm/`\
`python3 -m pytest tqdm/tests/tests_contrib.py::test_enumerate` (We come back and run the testing script)
`bugsinpy-compile`\
`bugsinpy-test`