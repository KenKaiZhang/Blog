# 8 User Management

Users are just numbers defined by an unsigned 32-bit integer called the UID

System defines an API that maps UID numbers back and forth into more complete sets of information about users

**/etc/passwd** defines a list of users recognized by the user and contains 7 fields seperated by `:`

1. Login name
2. Encrypted password
3. UID
4. Default GID
5. Full name, office, extension, home phone
6. Home directoyr
7. Login shell

Login names must be an unqiue 32 character word

- no colons or newlines allowed

**/etc/pam.d/common-passwd** defines the hashing algorithm used to encrypt passwords

- users must manually update their passwords before changes to the algorithm is made

**`chage -d 0 username`** will invalidate an user's password and force an update

Users should typically have UID of 1000+ and should not use a previously used UID

A simple scheme is to assign users to groups and then let those groups manage the range of IDS users can have within those groups

GID are defined in the **/etc/group** file and the one in **/etc/passwd** determines the default upon login

**`chfn`** allows users to change their personal information in **/etc/passwd**

**/etc/shadow** is a more indepth file of user passwords

- has no relation to **/etc/passwd**, just holds password information
- contains 9 fields sperated by `:`
  1. Login name
  2. Encrypted password
  3. Date of last password change
  4. Minimum days between password changes
  5. Maximum days between passwrod changes
  6. Number of days in advance ot warn users about password expiration
  7. Days after password expiration that account will be disabled
  8. Account expiration date
  9. Reserved for future (always empty)

The **/etc/group** file contains the names of UNIX groups and a list of its members and contains 4 fields:

1. Group name,
2. Encrypted password or a placeholder
3. GID number
4. List of members seperated by `,`

**/etc/password** is the source of truth for what group user belongs in

## Adding Users

Required:

- Edit **passwd** and **shadow** files to define the user
- Add the user to the **/etc/group** file
- Set an initial password
- Create `chown` and `chmod` the user's home directory
- Configure roles and permissions

Use high level tools such as

- **`useradd`**
- **`adduser`**
- **`usermod`**
- **`pw`**
- **`chsh`**

Use **`vipw`** command to edit **passwd** and **shadow** files and **`vigr`** for the **group** file

Set a password for user using the **`passwd`** command

- you will be prompted for a password

Home directories should be created for you when `useradd` and `adduser` is ran

- still make sure that permissions are properly set by letting users try
- **`sudo chown -R newuser:newgroup ~newuser`** should set ownerships properly

New users should have a startup file starting with a `.` and ending with a `rc`

Using `useradd` makes life easier

- `sudo useradd -c "Ken Zhang" -d /home/staff/ken -g ken -G staff -m -s /bin/bash ken`
  - this will create a new user `ken` in group `ken` and `staff` with home dirctory of `/home/staff` if does not exist

You can use **`newusers`** to create multiple users at once

Use **`userdel`** and **`rmuser`** to delete users properly

- use **`sudo find filesystem -xdev -nouser`** to check if old UID still owns any files on the system
