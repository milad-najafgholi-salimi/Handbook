**Git** is a **distributed version control system (VCS)** used to track changes in files, especially source code, so multiple people can collaborate efficiently and safely on a project.

# How to start using Git
### Step 1: Install Git

Before you can use Git, you need to install it on your computer. The process is slightly different depending on your operating system.

- **On Windows**: The best way is to download the installer from the official website, [git-scm.com](https://git-scm.com/). Run the installer and accept the default options unless you have a specific reason to change them. This will also install **Git Bash**, a command-line program that we'll use for Git commands.
    
- **On macOS**: Git might already be installed. To check, open the **Terminal** app (found in Applications > Utilities) and type `git --version`. If it's not installed, running this command for the first time will usually prompt your system to install the command line developer tools, which include Git. You can also download an installer from [git-scm.com](https://git-scm.com/).
    
- **On Linux**: You can install Git using your distribution's package manager. For example, on Ubuntu or Debian, you would open your terminal and run `sudo apt install git -y`.
    

To verify the installation was successful, open your terminal (or Git Bash on Windows) and run:
```
git --version
```
You should see the installed Git version number printed on the screen.
### Step 2: Introduce Yourself to Git

Git needs to know who you are to label the changes (commits) you make. This is a one-time setup. Open your terminal and run the following commands, replacing the name and email with your own.
```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
The `--global` flag means you're setting this identity for all your Git projects on your computer.
### Step 3: Use Git

| Scenario                                       | Your Goal                                                                                                    | Command to Use                        |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------- |
| **Start from scratch (Local First)**           | You have an existing project folder on your computer and want to start tracking its history with Git.        | `git init` inside that project folder |

#### If You're Starting from Scratch (Using `git init`)

Let's say you have a project folder called `my-project` on your desktop.

1. **Navigate to your project**: Open your terminal and use the `cd` (change directory) command to go into your project folder.
```
cd Desktop/my-project
```
2. **Initialize the repository**: Run the `init` command.
```
git init
```
You'll see a message like:
`Initialized empty Git repository in /path/to/your/project/.git/`

Git has created a hidden `.git` folder inside your project, which is where it stores all its tracking information.

3. **Check the status**: It's good practice to see what Git sees.
```
git status
```
This will list your project files in red, meaning they are "untracked" (Git isn't saving their history yet).

4. **Make your first commit**: Now, you'll take a snapshot of your files.

- First, tell Git which files to include in the snapshot. To add all files in the current directory, use:
```
git add -A
```
- Now, permanently store this snapshot with a message describing it.
```
git commit -m "Initial commit"
```
The `-m` flag lets you add a commit message directly in the command line.

You are now successfully tracking your project with Git!
