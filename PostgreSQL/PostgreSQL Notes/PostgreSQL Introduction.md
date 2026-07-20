Installing PostgreSQL on a Debian-based system is straightforward using the official PostgreSQL Apt repository.

```
sudo apt install postgresql
```

#### Step 1: Check PostgreSQL Service Status
After installation, verify that it's working correctly:
```
sudo systemctl status postgresql
```
If the output includes `active (running)`, the service is running.
If it's not running, start it with:
```
sudo systemctl start postgresql
```
To ensure it automatically starts after every system reboot:
```
sudo systemctl enable postgresql
```
#### Step 2: Switch to the `postgres` User
PostgreSQL automatically creates a system user named `postgres` by default. Database management is performed through this user.
To switch to this user, use the following command:
```
sudo -i -u postgres
```
`-i` stands for 'login' or 'initial'.
`-u` stands for 'user'.

You are now inside the `postgres` user's shell.

**Note:**
Run the following command to see switches:
```
psql --help
```
#### Step 3: Enter the PostgreSQL Command-Line Interface (psql)
Now enter the interactive PostgreSQL environment with:
```
psql
```
You'll see the prompt change to:
```
postgres=#
```
This means you're in the `psql` environment and can execute SQL commands.
