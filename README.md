Styleint for pre-commit
========================

Mirror of stylelint package for pre-commit.

For pre-commit: see https://github.com/pre-commit/pre-commit

For stylelint: see http://stylelint.io/


### Using styleint with pre-commit

Add this to your `.pre-commit-config.yaml`:

```yaml
   -   repo: https://github.com/awebdeveloper/pre-commit-stylelint
       sha: '' # Use the sha or tag you want to point at like 0.0.1
       hooks:
       -   id: stylelint
           additional_dependencies: ['stylelint@7.10.1', 'stylelint-config-standard@16.0.0']
 ```


