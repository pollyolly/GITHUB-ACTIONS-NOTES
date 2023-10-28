## Github Actions Notes

### Setup Branch Protection
Prevent directly pushing commits on main branch, instead they will pull request.
```vim
Git Repository->Settings->Branch
                Branch Name Pattern = main
                Pull Request before merging
                          -> Require approvals = check 
                Require Status Check to pass before merging
                          -> Require branches to be up to date before mergin = check
```
### Setup Environment Variables (For values inside .env )
To hide sensitive environment variables
```
Git Repository->Settings->Environment
                New Environment->Add = "dev"
                                 Environment secrets->Add secrets
                                                      Name  = "DB"
                                                      Value = "http://localhost:9000/"
```
### Create Workflow 
```vim
$cd my_repository or $git clone <remote repository>
$mkdir .github 
$cd .github
$mkdir workflows
$touch demo_workflow.yml
```
```yml
name: Sample App
on:
  pull_request:
    branches:
      -  main

jobs:
  test:
    runs-on: [ubuntu-latest, centos-latest]
    defaults:
      run:
        working-directory: ./app/

    strategy:
      matrix:
        python-version: [3.8, 3.9]

    env:
      MODE: ${{ secrets.MODE }}

    steps:
      -  uses: actions/checkout@v3

      -  name: Set up Python
         uses: actions/setup-python@v4
         with:
           python-version: ${{ matrix.python-version }}
      
      -  name: Install dependencies
         run: |
           python -m pip install --upgrade pip
           pip install -r ../requirements.txt

      - name: Test App Code
        run: python ./main_test.py
```
### References
[Github Actions](https://www.youtube.com/watch?v=UEOtZvTCmDo)

[Github Checkout@v4](https://github.com/actions/checkout)
