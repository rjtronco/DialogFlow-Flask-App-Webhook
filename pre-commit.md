## Pre-commit

Added `pre-commit` to repo. 
To setup pre-commit
  - Install pre-commit: pip install pre-commit
  - Add pre-commit to requirements.txt (or requirements-dev.txt)
  - Define .pre-commit-config.yaml with the hooks you want to include.
  - Execute pre-commit install to install git hooks in your .git/ directory.


To test if `pre-commit` is working, just push to your repo by doing the following:
- `git add .`
- `git commit -m <commit_message>`
- `git push`

The pre-commit hooks should run after the `git commit` command as show here:

<img src="https://github.com/rjtronco/DialogFlow-Flask-App-Webhook/blob/main/pre-commit-test.png" width="800px" margin-left="-5px">
<br>
