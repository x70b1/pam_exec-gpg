# pam_exec-gpg

[![Codecheck](https://github.com/x70b1/pam_exec-gpg/workflows/Codecheck/badge.svg?branch=master)](https://github.com/x70b1/pam_exec-gpg/actions)
[![GitHub contributors](https://img.shields.io/github/contributors/x70b1/pam_exec-gpg.svg)](https://github.com/x70b1/pam_exec-gpg/graphs/contributors)
[![license](https://img.shields.io/github/license/x70b1/pam_exec-gpg.svg)](https://github.com/x70b1/pam_exec-gpg/blob/master/LICENSE)

Unlock GnuPG keys keys on login using PAM.

[pam-gnupg](https://github.com/cruegge/pam-gnupg) is an awesome project too.


## Installation

For Arch Linux users is already a [pam_exec-gpg](https://aur.archlinux.org/packages/pam_exec-gpg/) package in the AUR.

Otherwise just copy the script, set the permissions and install `pam`.

```sh
cp pam_exec-gpg /usr/bin/pam_exec-gpg
chown root:root /usr/bin/pam_exec-gpg
chmod 755 /usr/bin/pam_exec-gpg
```


## Configuration

You need a running `gpg-agent`.
The agent have to be started before you login.
Take a look at the wiki how to [configure gpg-agent](https://wiki.archlinux.org/title/GnuPG#gpg-agent).

A file `~/.gnupg/pam_exec-gpg` should contain the keygrip.

Add the PAM call to your config:

```
auth		optional	pam_exec.so expose_authtok /usr/bin/pam_exec-gpg
```

To make sure that your keys are locked again you can restart your `gpg-agent`.
A good time to do this is when you lock your screen.
This means all keys are locked when you leave your device but the agent is still prepared for the next use.
