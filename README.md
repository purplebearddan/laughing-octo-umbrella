# Git and GitHub

## Git Workflow

### Clone a git repository (with ssh)

This will copy the `repo` contents to your computer.

```sh
git clone git@GitHub.com:username/repo-name.git
```

### Add new files

If you add a new file or rename a file you will have to run this com

```sh
git add .

# or 

git add -A
```

### Commit changes to all your files

Push your committed changes to GitHub

```sh
git push
```

## Setting up your SSH Key on GitHub

### Step 1 - Check if you have any SSH keys

Check if you have an existing SSH key that you'd like to use. It is better if you create a new SSH key for GitHub; however, if you want to know if you have any SSH keys run the following command in your terminal on MacOS or Git Bash on Windows:

```sh
ls -al ~/.ssh
```

If you have a `.ssh` folder then you should see some keys with a `.pub` extension which is your public key.

If you see the error message `ls: .ssh: No such file or directory` or the above command doesn't display any files then that is alright as the `.ssh` folder gets created once we generate a new key

### Step 2 - Generate a new SSH key

Open the terminal on MacOS or Git Bash on Windows

Enter the command shown below which will begin the process to generate an SSH key

```sh
# Change this to use your GitHub email address, keep the quotes!
ssh-keygen -t rsa -b 2048 -C "here@there.co.uk" -f ~/.ssh/id_rsa_GitHub
```

When presented with `Enter passphrase (empty for no passphrase):` just hit enter which is an empty passphrase

When presented with `Enter same passphrase again:` just hit enter again

You will then see some text displayed on your terminal which indicates that your SSH key has been successfully generated.

You can check your new key in the `.ssh` folder by running this command which will display files like `id_rsa` and `id_rsa_GitHub.pub`

```sh
ls -al ~/.ssh
```

### Step 3 - Pair your SSH key with your GitHub account

Open `Terminal` on MacOS or `Git Bash` on Windows

Run the following command

```sh
eval $(ssh-agent -s)
```

You *should* see something like `Agent pid <number>` displayed on your terminal

Run the following command to open your config file in VSCode.

```sh
code ~/.ssh/config
```

> :bulb: Heads Up:  If you're on mac and `code` does not work please follow these [instructions](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line "Running Visual Studio Code on macOS")

Add these settings to your file. If the file has some data then add this to the end of the file

```text
Host GitHub.com
    HostName GitHub.com
    User git
    IdentityFile ~/.ssh/id_rsa_GitHub
```

### Step 4 - Add an SSH key to your GitHub account

#### On macOS

Open `Terminal` and run this command to copy your `public key`

```sh
pbcopy < ~/.ssh/id_rsa_GitHub.pub
```

#### On Windows

Run the command below to copy your `public key`

```sh
cat ~/.ssh/id_rsa_GitHub.pub | clip
```

#### Then

- Sign in to [GitHub](https://GitHub.com/login)
- When logged in, In the top right corner select your `avatar`/`display picture`
- Select `Settings`
- From the left sidebar, select `SSH and GPG Keys`
- Click on the button that says `New SSH Key`
- In the `Title` text box, type a description, like `Work Laptop` or `Home Workstation`
- Make sure the `Key Type` drop down is set to `Authentication Key`
- In the `Key` box, paste the contents of your public key.

It should look something like this:

```text
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q== username@laptop
```

> :bulb: Warning: If you manually copied the key, make sure you copy the entire key, which starts with `ssh-ed25519` or `ssh-rsa`, and may end with a comment, in the example above this is `username@laptop`

- Click the `Add SSH key` button to add the key

### Step 5 - Verify your connection is working

Open `Terminal` on MacOS or `Git Bash` on Windows

Run the following command to ensure you can connect to the GitHub instance

```sh
ssh -T git@github.com
```

> :bulb: Heads up: If this is the first time you connect, you'll see this message.

```text
# this may be slightly different on your computer
The authenticity of host 'github.com (35.231.145.151)' can't be established.
ECDSA key fingerprint is SHA256:HbW3g8zUjNSksFbqTiUWPWg2Bq1x8xdGUrliXFzSnUw.
Are you sure you want to continue connecting (yes/no)?
```

> :bulb: Heads up: If you see a message like above then type `yes` and hit `[Enter]`, this just means you are adding GitHub to your list of known SSH connections

```text
Warning: Permanently added 'github.com' (ECDSA) to the list of known hosts.
```

Run the command again and you should see a Welcome message with your GitHub username

```text
$ ssh -T git@github.com
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

> 🎊 You are now setup to use github, I'd keep this guide handy just in-case.
