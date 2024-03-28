Install Homebrew on your Mac by going to the url https://brew.sh and run the curl script within your terminal window.

Check for Homebrew
Check if Homebrew is installed:

$ brew
If Homebrew is not installed, you will see:

zsh: command not found: brew


Brew install
Homebrew provides an installation script you can download and run with a single command (check that it hasn't changed at the Homebrew site). This is the easiest way to install Homebrew.

$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
The Homebrew installation script will ask you to enter your Mac user password. This is the password you used to sign into your Mac.

Password:
You won't see the characters as you type. Press enter when you are done.



Open terminal and enter the below command to install Homebrew:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Add Homebrew shell configuration

```
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verify Homebrew installation
After you've installed Homebrew, check that Homebrew is installed properly.

$ brew doctor
You should see:

Your system is ready to brew.

Listing installed packages
As you use Homebrew, it is helpful to see a list of all the packages you've installed:

$ brew list
You can also see a diagram of packages and dependencies.

$ brew deps --tree --installed
Right now, immediately after installation, these commands show nothing is installed.
