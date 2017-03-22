Styleint for pre-commit
========================

Mirror of stylelint package for pre-commit.

For pre-commit: see https://github.com/pre-commit/pre-commit

For stylelint: see http://stylelint.io/


### Using styleint with pre-commit

Add this to your `.pre-commit-config.yaml`:

    -   repo: git://github.com/awebdeveloper/pre-commit-stylelint
        sha: ''  # Use the sha or tag you want to point at
        hooks:
        -   id: stylelint
