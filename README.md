# temp

```bash

import requests
from requests.auth import HTTPBasicAuth

def get_project_repo_names(workspace, project_key, bitbucket_auth, max_repos=100):
    """
    Fetches up to `max_repos` repository names from a Bitbucket project.

    Args:
        workspace (str): Bitbucket workspace ID.
        project_key (str): Bitbucket project key.
        bitbucket_auth (str): Base64-encoded "username:app_password".
        max_repos (int): Maximum number of repo names to return.

    Returns:
        List[str]: List of repository slugs.
    """
    import base64
    decoded_auth = base64.b64decode(bitbucket_auth).decode('utf-8')
    username, app_password = decoded_auth.split(':', 1)

    repo_names = []
    url = f"https://api.bitbucket.org/2.0/repositories/{workspace}"
    params = {
        'q': f'project.key="{project_key}"',
        'pagelen': 50
    }

    while url and len(repo_names) < max_repos:
        response = requests.get(url, auth=HTTPBasicAuth(username, app_password), params=params)
        if response.status_code != 200:
            raise Exception(f"Error fetching repos: {response.status_code}, {response.text}")

        data = response.json()
        for repo in data.get('values', []):
            repo_names.append(repo['slug'])
            if len(repo_names) >= max_repos:
                break

        url = data.get('next')

    return repo_names
```
