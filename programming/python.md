# Python

## Virtual Environments

### Manual Way

        python -m venv venv
        source venv/bin/activate
        echo $VIRTUAL_ENV
        deactivate

### Pipenv

        pip3 install pipenv
        pipenv install requests
        pipenv --venv
        pipenv shell
        exit
        pipenv install
        pipenv install --ignore-pipfile
        pipenv graph
        pipenv update --outdated
