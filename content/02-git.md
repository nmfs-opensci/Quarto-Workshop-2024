---
title: Authenticating and Installing
---

## Installing Git

Ask IT to install Git or GitHub Desktop. The later is more useful since you will get a good Git GUI and Git bundled together.

## Git and RStudio

In order for RStudio to use Git, it needs to know where your Git binary is installed. Instructions: <https://happygitwithr.com/rstudio-see-git>

**Find Git binary**

1. In RStudio, Tools > Terminal > New Terminal
2. At the command line (in the new terminal), type `which git` if on a Mac and `where git` if in Windows.  
3. Copy that path. It probably doesn't matter which one you use if there are multiple listed.

**Tell RStudio the Git binary location**

1. In RStudio, Tools > Global Options > Git/SVN
2. There is a box at top that asks for the location of the Git binary.  
3. Paste that path in.

## Authenticating

### GitHub Desktop

No tokens needed. 

1. Sign in under GitHub Desktop > Settings (or Options) > Account.
2. Fill out your user info on GitHub Desktop > Settings (or Options) > Git.

**Help! I signed up for GitHub Enterprise and GitHub Desktop will not authenticate!!** 
Log out of GitHub Desktop under GitHub Desktop > Settings (or Options) > Account and log back in.

### R users with RStudio

Install the `usethis` and `credentials` packages. Then run this code.

```
## set your user name and email:
usethis::use_git_config(user.name = "YourName", user.email = "your@mail.com")

## create a personal access token for authentication:
usethis::create_github_token() 
```
Copy the token. It is really long. Copy that into `YourPAT` in code below.
```
## set personal access token:
credentials::set_github_pat("YourPAT")
```

Note for Linux users:
`credentials::set_github_pat()` might store your PAT in a memory cache that expires after 15 minutes or 
when the computer is rebooted. You thus may wish to do extend the cache timeout to match the PAT validity period:
`usethis::use_git_config(helper="cache --timeout=2600000")`

### With a Personal Access Token

1. Go to <https://github.com/settings/tokens>
2. Click generate new token. 
3. For most uses, set the scope to "repo". Definitely do not click all the scopes!
4. Copy the token that it generates.

Open a terminal window and type
```
git config --global user.email "<your email>"
git config --global user.name "<your name>"
git config --global pull.rebase false
```
Next in the terminal window type one of these

* Unix: `git config --global credential.helper store`
* Max: `git config --global credential.helper osxkeychain`
* Windows: `git config –global credential.helper manager-core`


