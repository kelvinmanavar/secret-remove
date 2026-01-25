Case-I We have commited two files .env and demo.txt, While .env file having api key which was commited by mistake. Remove .env file with git history.

git remote -v
git remote add origin git@github.com:kelvinmanavar/secret-remove.git
pip install git-filter-repo
git filter-repo --path .env --invert-paths
git push -u origin master --force --tags

Case-II If we do not want to remove .env file but replace api key value with dummy value then use below

Create a file replace.txt with value API_KEY = sdbf46nwhgdwk8739nfbsn4jy==>API_KEY=test
git filter-repo --replace-text replace.txt
git remote add origin git@github.com:kelvinmanavar/secret-remove.git
git push origin master --force --tags
