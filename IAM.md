## IAM
http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
### Users

```shell
# list all user's info
aws iam list-users

# list all user's usernames
aws iam list-users --output text | cut -f 6

# list current user's info
aws iam get-user

# list current user's access keys
aws iam list-access-keys

# crate new user
aws iam create-user \
    --user-name UserName

# create multiple new users, from a file
allUsers=$(cat ./user-names.txt)
for userName in $allUsers; do
    aws iam create-user \
        --user-name $userName
done

# list all users
aws iam list-users --no-paginate

# get a specific user's info
aws iam get-user \
    --user-name UserName

# delete one user
aws iam delete-user \
    --user-name UserName

# delete all users
# allUsers=$(aws iam list-users --output text | cut -f 6);
allUsers=$(cat ./user-names.txt)
for userName in $allUsers; do
    aws iam delete-user \
        --user-name $userName
done
```


### Access Keys

http://docs.aws.amazon.com/cli/latest/reference/iam/

```shell
# list all access keys
aws iam list-access-keys

# list access keys of a specific user
aws iam list-access-keys \
    --user-name UserName

# create a new access key
aws iam create-access-key \
    --user-name UserName \
    --output text | tee UserName.txt

# list last access time of an access key
aws iam get-access-key-last-used \
    --access-key-id AKIZNAA7RKZY4EXAMPLE

# deactivate an acccss key
aws iam update-access-key \
    --access-key-id AKIZNAA7RKZY4EXAMPLE \
    --status Inactive \
    --user-name UserName

# delete an access key
aws iam delete-access-key \
    --access-key-id AKIZNAA7RKZY4EXAMPLE \
    --user-name UserName
```


### Groups, Policies, Managed Policies

http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html
http://docs.aws.amazon.com/cli/latest/reference/iam/

```shell
# list all groups
aws iam list-groups

# create a group
aws iam create-group --group-name GroupName

# delete a group
aws iam delete-group \
    --group-name GroupName

# list all policies
aws iam list-policies

# get a specific policy
aws iam get-policy \
    --policy-arn <value>

# list all users, groups, and roles, for a given policy
aws iam list-entities-for-policy \
    --policy-arn <value>

# list policies, for a given group
aws iam list-attached-group-policies \
    --group-name GroupName

# add a policy to a group
aws iam attach-group-policy \
    --group-name GroupName \
    --policy-arn arn:aws:iam::aws:policy/AdministratorAccess

# add a user to a group
aws iam add-user-to-group \
    --group-name GroupName \
    --user-name UserName

# list users, for a given group
aws iam get-group \
    --group-name GroupName

# list groups, for a given user
aws iam list-groups-for-user \
    --user-name UserName

# remove a user from a group
aws iam remove-user-from-group \
    --group-name GroupName \
    --user-name UserName

# remove a policy from a group
aws iam detach-group-policy \
    --group-name GroupName \
    --policy-arn arn:aws:iam::aws:policy/AdministratorAccess

# delete a group
aws iam delete-group \
    --group-name GroupName
```
<br/><br/><br/>