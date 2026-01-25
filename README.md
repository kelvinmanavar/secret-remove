Case-I We have commited two files .env and demo.txt, While .env file having api key which was commited by mistake.

git remote -v
git remote add origin git@github.com:kelvinmanavar/secret-remove.git
pip install git-filter-repo
git filter-repo --path .env --invert-paths
git push -u origin master --force --tags
