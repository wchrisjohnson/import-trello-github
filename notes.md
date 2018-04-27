## Overview


## Caveats
You cannot create an "Urgent" label - it's reserved.

## Preparation
Get set to run by setting up a virtualenv.
<!--  https://python-guide-cn.readthedocs.io/en/latest/dev/virtualenvs.html -->
```
virtualenv -p python3 .venv
source .venv/bin/activate
pip3 install -r requirements.txt
```

Run following to understand how to format command:
```
(.venv) » python3 import-issues.py --help
usage: import-issues.py [-h] [--loglevel {DEBUG,INFO,WARNING,ERROR,CRITICAL}]
                        [--dryrun DRYRUN] [--statedir STATEDIR]
                        [--githubroot GITHUBROOT] [--labelmaps LABELMAPS]
                        trello_json github_owner github_repo github_user
                        github_password

Import Trello cards JSON into GitHub issues

positional arguments:
  trello_json           JSON file exported from Trello
  github_owner          Owner of the GitHub repo
  github_repo           Repo in GitHub
  github_user           Your GitHub username
  github_password       Your GitHub password

optional arguments:
  -h, --help            show this help message and exit
  --loglevel {DEBUG,INFO,WARNING,ERROR,CRITICAL}
                        Set the minimum level to show logs for
  --dryrun DRYRUN       Dryrun mode. Don't make any changes.
  --statedir STATEDIR   Directory to store change state
  --githubroot GITHUBROOT
                        Root for the GitHub API
  --labelmaps LABELMAPS
                        Map Trello labels to GitHub labels
(.venv) »
```

## Run the conversion
Get a Personal Access Token to use as a password:
```
export TOKEN="<token>"
```

Run conversion for Cedar:
```
python3 ./import-issues.py --loglevel DEBUG \
                   --statedir state \
                   --labelmaps ./mappings.cedar.json \
                   ./trello.cedar.json heroku chrisj-trello-import \
                   wchrisjohnson@gmail.com $TOKEN
```

*Note: If you need to run the conversion while testing it out multiple times, it would be wise to `rm -rf` the state folder between runs to clean up after each run.*
