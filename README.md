Pre-commit hook for Styleint  
=============================

This is the Stylelint hook for [pre-commit](https://github.com/pre-commit/pre-commit). This prevents git commits unless the checks pass. 


### Using styleint with pre-commit

- To use this you first need to install pre-commit(see links below). 
- Then create a pre-commit config file and also a stylelint config file in the root of your project. 
- Run `pre-commit install` from the root of your project

Finally add this to your `.pre-commit-config.yaml`:

```yaml
-   repo: https://github.com/awebdeveloper/pre-commit-stylelint
    rev: '' # Use the sha or tag you want to point at like 0.0.1
    hooks:
    -   id: stylelint
        additional_dependencies: ['stylelint@13.2.1', 'stylelint-config-standard@20.0.0'] //specify the latest version
 ```
PS: These are for version 2.3.0 visit https://pre-commit.com/#2-add-a-pre-commit-configuration for latest config syntax or for config syntax specific to your version

 Now everytime you commit a scss/css file. It will run stylelint on this and prevent commit if the checks fail.
 
 ### Links
 - For pre-commit: see https://github.com/pre-commit/pre-commit

 - For stylelint: see http://stylelint.io/


