
# Secret Remove from Git code

If the secrets are commited in to the git repository, you should assume they are compromised (even if the repo is private). 

Here’s what you should do step-by-step:

## Step-1 Rotate / Revoke the Secrets (MOST IMPORTANT)

Immediately go to wherever the secrets are used and regenerate them:

API keys (AWS, Azure, GCP, etc.)
DB passwords
Tokens (JWT secrets, OAuth secrets, etc.)

Example:

In AWS → rotate IAM user keys , DB passwords

Note: Do this before anything else. Removing from Git is not enough.

## Step-2 Remove .env from Git (Latest Commit)
If it’s only in the latest commit:

## Process

```bash
git rm --cached .env
echo ".env" >> .gitignore
git commit -m "Remove .env file"
git push
```


## Step-3 Remove Secrets from Git History (IMPORTANT)
Even after deleting, secrets still exist in history. So, we require to clear that from history. 

## Case-1 
We have commited two files .env and demo.txt, While .env file having api key which was commited by mistake. Remove .env file with git history.

```bash
git remote -v
git remote add origin git@github.com:kelvinmanavar/secret-remove.git
pip install git-filter-repo
git filter-repo --path .env --invert-paths
git push -u origin master --force --tags
```


## Case-2
If we do not want to remove .env file but replace api key value with dummy value then use below process.

```bash
Create a file replace.txt with value API_KEY = sdbf46nwhgdwk8739nfbsn4jy==>API_KEY=test
git filter-repo --replace-text replace.txt
git remote add origin git@github.com:kelvinmanavar/secret-remove.git
git push origin master --force --tags
```
## Step-4 Notify Your Team
Ask everyone to re-clone the repo OR reset:

```bash
git fetch
git reset --hard origin/master
```
## Step-5 Prevent This in Future
Add .env to .gitignore
