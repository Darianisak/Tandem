# Tandem: A Linux upgrade client for Discord
## What is Tandem?

*Tandem* is a *[dpkg]* based upgrade client for [Discord]'s Linux desktop app.

## Motivation

*Tandem* was born from a minor annoyance: Discord's Linux app *does not*
auto update.

*Tandem* streamlines the client update process, making a multi-click operation
achievable with a single command.

## Using Tandem

If you're *not* planning on poking around with *Tandem's* source code, then
you can use the pre-built executable, which can be downloaded [here][Releases].

Once you've downloaded the executable, it can be run:

``` bash
cd ~/Downloads

./tandem --help

"""
usage: tandem [-h] [-v] [--dpkg-verbose] [--dry-run]

A Discord upgrade client for Linux.

options:
  -h, --help      show this help message and exit
  -v, --verbose   Enables verbose logging.
  --dpkg-verbose  Enables dpkg verbose logging.
  --dry-run       Toggle whether Discord will be updated.

Authored by <culver.darian@gmail.com>, licensed under GPL v3.
"""
```

## Using Tandem *during* development

Using *Tandem* during development is easy, *but* it does assume you have a
few things installed:

* dpkg
* git
* Python
* Python's pip module
* Python's venv module
* Discord's package dependencies
  * libasound2
  * libatomic1
  * libnotify4
  * libnspr4
  * libnss3
  * libxss1
  * libxtst6

Once these are installed, you're ready to go!

### 1: Checking out the project

First, checkout *Tandem*'s source code:

``` bash
mkdir /tmp/tandem
cd /tmp/tandem
git clone git@github.com:Darianisak/Tandem.git --depth=1
```

### 2: Creating a Virtual Environment

Then, we'll create a virtual environment to prevent *Tandem* from interfering
with other projects, and/or system packages:

``` bash
cd /tmp/tandem
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 3: Running Tandem

And then we'll run *Tandem* to install or update Discord:

``` bash
python3 update_discord.py

"""
INFO - Installed version: 0.0.108
INFO - Upstream version: 0.0.108
INFO - Installed version is up to date!
"""
```

We'll then check that Discord has been installed with:

``` bash
apt policy discord
```

For further details about *Tandem*, or the options that it can take, refer to
the help dialog:

``` bash
python3 update_discord.py --help

"""
usage: tandem [-h] [-v] [--dpkg-verbose] [--[here][Releases].dry-run]

A Discord upgrade client for Linux.

options:
  -h, --help      show this help message and exit
  -v, --verbose   Enables verbose logging.
  --dpkg-verbose  Enables dpkg verbose logging.
  --dry-run       Toggle whether Discord will be updated.

Authored by <culver.darian@gmail.com>, licensed under GPL v3.
"""
```

## Building Tandem

*Tandem* binaries are built using [PyInstaller] and distributed via GitHub.

*Assuming* you already have the project checked out under `/tmp/tandem`, the
next step would be to create a virtual environment:

``` bash
cd /tmp/tandem
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Then, we'll run the build process:

``` bash
pyinstaller update_discord.py --onefile --name tandem
```

Alongside a number of build artifacts, this will produce a single
executable file:

``` bash
cd dist

./tandem --help

"""
usage: tandem [-h] [-v] [--dpkg-verbose] [--dry-run]

A Discord upgrade client for Linux.

options:
  -h, --help      show this help message and exit
  -v, --verbose   Enables verbose logging.
  --dpkg-verbose  Enables dpkg verbose logging.
  --dry-run       Toggle whether Discord will be updated.

Authored by <culver.darian@gmail.com>, licensed under GPL v3.
"""
```

## FAQ
### What distributions has this been tested with?

*Tandem* has been tested with:

* Ubuntu Noble (Ubuntu 24.04 LTS)
* Debian Bookworm (Debian 12).

### What if I already have Discord installed?

*Tandem* will not attempt to update Discord *unless* your installed version
*is* older than the most recent version of Discord.

*If* you have the most recently version already, *Tandem* will not make
any changes.

<!-- Links -->

[dpkg]: https://man7.org/linux/man-pages/man1/dpkg.1.html
[Discord]: https://discord.com/
[PyInstaller]: https://pyinstaller.org/en/stable/index.html
[Releases]: https://github.com/Darianisak/provisioning/releases
