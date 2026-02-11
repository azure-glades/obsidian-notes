
Dissimilarity matrix - one mode

Data matrix - 2 modes

types of data in clustering analysis
- interval scaled var
- binary var
- nominal, ordinal and ratio vars
- vars of mixed types

Intervalued data
standardize it, get var and std dev
use distances to cluster - euclidean, manhatta, minkowski

Binary data



Goal: Code repository management.
You have a repository. I store information on who made it, who has access to make change to it, a table storing commit history (just the commit messages and time) and issues that are raised on the repository

What r we trying to do:
basically, we need to use sql db and nosql db.

person inits a repo. Pushes it to an external server (remote) . tables are updated.

person commits changes to repo and pushes to remote. remote will see if person has permissions (role table) and commit changes if they have permission. it will store this event in access log (this person tried to commit but succeeded/failed)

another person raises an issue for a repo. their message/issue is stored in nosql db. other people can comment/message under this issue and it also gets seen

for nosql db -> we need to store issue threads as objects in nosql and make a way to show this to examiner

for sql db -> we need to store roles, users, repo details (for now only 1 repository) and access-log and show how tables are updated/referred etc etc.


