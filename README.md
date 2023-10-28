## Github Actions Notes

### Setup Branch Protection
Prevent directly pushing commits on main branch, instead they will pull request.
```
Git Repository->Settings->Branch
                Branch Name Pattern = main
                Pull Request before merging
                          -> Require approvals = check 
                Require Status Check to pass before merging
                          -> Require branches to be up to date before mergin = check
```
### Create Workflow 
```
$cd my_repository or $git clone <remote repository>
$mkdir .github 
$cd .github
$mkdir workflows
$touch demo_workflow.yml
```
```

```
### References
[Github Actions](https://www.youtube.com/watch?v=UEOtZvTCmDo)
