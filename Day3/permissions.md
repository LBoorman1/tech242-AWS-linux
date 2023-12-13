# File ownership and permissions

# File ownership

Either user, group or others. Groups are identified by group Id of GID.

# File permissions

Has permissions RWX. Read, write execute. can use `chmod` to change the permissions of a file.

read - 4
write - 2
execute - 1

Have to add these values together to get the permissions you want. 

read + write = 4 + 2 = 6
read + write + execute = 4 + 2 + 1 = 7

To change the permissions for each user group, you can do `chmod 777` to add all permissions to all user groups.