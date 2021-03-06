# Mac OSX

Almost everything that follows below needs to be dine by typing in commands in your terminal. There's plenty of steps that needs to be finished before your development environment is set up. See this as a learning experience - a big part of a programmers job is to use third party tools and tweak his own, or a remote system.

#### Atom
At the beginning of the course (week 1 - 6) we'll be using a text editor to write code. There are many editors out there we can use. [Sublime](http://www.sublimetext.com/) is one, [TextMate](https://macromates.com/) is another, but our editor of choice for this course is [Atom](https://atom.io). It is brought to us by the good people of GitHub and comes with over 3000 extension packages - all open sourced.

*"Atom is a text editor that's modern, approachable, yet hackable to the core — a tool you can customize to do anything but also use productively without ever touching a config file."* - https://atom.io
![Atom.io - Download for OS X](../images/atom_io_landing_page.png)

Download and install Atom by following the instructions on their [web site](). Once that's done you can browse around for some packages you might find useful. Or you wait with that until you actually know what '*useful*' is in the context of coding. If you want to find out more about how to install Atom packages head over to their excellent [documentation](https://atom.io/docs/v1.2.4/using-atom-atom-packages) site. Also, read through this blog post about some Atom extensions that might prove useful: http://www.sitepoint.com/10-essential-atom-add-ons/

For now, what you really want to do is to set Atom as the default editor fir Git (trust me, you are going to need it):

```shell
$ git config --global core.editor "atom --wait"
```

#### Xcode Command Line Tools
[Xcode](https://developer.apple.com/xcode/) is an integrated development environment (IDE) with a suite of tools for developing software for OS X and iOS. But Xcode is more than what just meets the eye. Ruby gems often use so called "native extensions", that connects them with other non-Ruby components on your machine. Without Xcode installed, you don't have the necessary code compilers installed and can not use those extensions. While installing Xcode you also install LLVM, GCC, and many other developer tools. 

For the purpose of this course, we are going to install Xcode Command Line Tools, a part of the Xcode IDE, without installing the entire Xcode package. 

Check if Xcode Command Line Tools are installed by typing in the following command in your terminal:
```shell
$ xcode-select -p
```

Install:
```shell
$ xcode-select --install
```
Work your way through the dialog screens presented by the installer. Complete the process and verify installation:

```shell
$ xcode-select -p
/Library/Developer/CommandLineTools
# or: 
/Applications/Xcode.app/Contents/Developer
```

Also, verify that LLVM-GCC is installed:

```shell
$ gcc --version
Configured with: --prefix=/Applications/Xcode.app/Contents/Developer/usr --with-gxx-include-dir=/usr/include/c++/4.2.1
Apple LLVM version 7.0.0 (clang-700.1.76)
Target: x86_64-apple-darwin14.5.0
Thread model: posix
```
#### Homebrew
[Homebrew](http://brew.sh/) is “the missing package manager for OSX” written in Ruby. It allows you to easily install hundreds of open-source tools. Homebrew complements OSX. Install your gems with `gem install`, and their dependencies with `brew install`.

In your terminal, run the following command:
```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once the installation is successful, run the following command:

```shell
$ brew doctor
```
If you get the response `Your system is ready to brew`, you're all set.

#### RVM

Ruby Environment Manager (RVM) is a tool that allows you to install, manage and work with multiple ruby environments. RVM lets you deploy each project with its own completely self-contained and dedicated environment, from the specific version of ruby, all the way down to the precise set of required gems to run your application.

To install RVM, run the following command in your terminal:

```shell
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
$ curl -L https://get.rvm.io | bash -s stable --auto-dotfiles --autolibs=enable --ruby
```

> Note: If you get the following error after running the `gpg` command
```shell
-bash: gpg: command not found
```
You need to install gpg on your system:
```shell
brew install gnupg gnupg2
```

Once the installation is complete you must load RVM to make RVM available in your current session. Otherwise you'll need to restart your terminal. Run the following command in terminal:

```shell
$ source ~/.rvm/scripts/rvm
```

Verify your install:

```shell
$ type rvm | head -1
rvm is a function
```

If you get the response `rvm is a function` it means you're all good.

Now you can check what ruby version/versions you have installed on your machine with the `list` command:

```shell
$ rvm list
```

And install new rubies with:
```shell
$ rvm install 2.2.3  # or whatever version you need
```

To switch between Ruby versions make use of the `use` command:

```shell
$ rvm use 2.2.3
```
Read the [RVM documentation](https://github.com/rvm/rvm#action) to see all the different actions you can use.

#### Bundler
Bundler is a program for managing gem dependencies in your Ruby projects. With Bundler you can specify which gems your program needs, what versions they should be at, it can help you install them, load them at runtime and distribute them with your software.

*"Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed."* - http://bundler.io/

You install it with a terminal command:

```shell
$ gem install bundler
```

Now, you can keep control of which gems your programs are using by adding them to a file called `Gemfile` in your project folder (Please note the capital 'G'). 

An example `Gemfile` can look like this:
```ruby
source 'https://rubygems.org'
gem 'rack'
gem 'rspec'
gem 'mail'
```

To install those gems and their dependencies, you run the following command in your terminal:
```shell
$ bundle install
```

We'll be covering `bundler` and gems more extensively later on when we work with our challenges. 


#### Git
Git is a version control system that we'll be using extensively during the course. Version Control lets you track your files, changes and avoid general chaos over time. 

With Homebrew, installing Git is easy:

```shell
$ brew install git
```
And verify your installation: 

```shell
$ git --version
git version 2.4.4
```

Next, let's tell git who we are.
```shell
$ git config --global user.name "you name"
$ git config --global user.email "your@email.com"
```
Now, you are ready to use Git. 

#### Git Autocomplete

Install bash-completion: `brew install brew install bash-completion` 

Add bash-completion to your `~/.bash_profile`.

```
$ atom ~/.bash_profile
```

```
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi
```

#### Terminal prompt
When you work with git and version control it is a good idea to set up your prompt that displays some useful information such as:
- What branch are you currently on
- What is your current status compared to your GitHub repository (`origin`)

There is a very nice modification made available on GitHub called [Bash Git Prompt](https://github.com/magicmonty/bash-git-prompt). You an install it using Homebrew with these steps:

```shell
$ brew install bash-git-prompt
```

Once the installation is complete, you need to open the `.bash_profile` file:

```bash
$ atom ~/.bash_profile
```

This should open the file in your newly installed text editor.

Now add the following configuration at the bottom of the file and save. 

```bash
# ~/.bash_profile

if [ -f "$(brew --prefix)/opt/bash-git-prompt/share/gitprompt.sh" ]; then
    export __GIT_PROMPT_DIR="$(brew --prefix bash-git-prompt)/share/"
    source "$(brew --prefix)/opt/bash-git-prompt/share/gitprompt.sh"
fi
```
Once you save and close `.bash_profile`, you can close Atom and go back to your terminal and reload the file to make the changes you've made visible.:

```shell
source ~/.bash_profile
```

Your terminal prompt will now show a lot more useful information that will help you in your coding. 


#### That's it!
You are all set up, you have your necessary compilers (with Xcode CLT) to be able to effectively use ruby gems, your package managers (RVM, Bundler and Homebrew) are in place, you have your Ruby versions installed, a version control system (Git) and you have a text editor. In your terminal, where you will be spending most of your time, you have a prompt that tells you all you need to know about where you are in your version control process.  

**You are all good!**












