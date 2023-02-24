# Configure Github with ssh

[![](https://naasai-public.s3.eu-west-3.amazonaws.com/open\_in\_naas.svg)](https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas\_Configure\_Github\_with\_ssh.ipynb)\
\
[Template request](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=\&template=template-request.md\&title=Tool+-+Action+of+the+notebook+) | [Bug report](https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=\&labels=bug\&template=bug\_report.md\&title=Naas+-+Configure+Github+with+ssh:+Error+short+description)

**Tags:** #naas #git #github #jupyterlab #operations #snippet

**Author:** [Maxime Jublou](https://linkedin.com/in/maximejublou)

**Description:** This notebook provides instructions on how to configure Github with SSH for secure access to the Naas platform.

### Input

#### Import needed libraries

```python
import os
```

#### Create an SSH key pair to use with Github

The first thing we need to do is to generate a key pair to be able to interact with Github.

You can follow the instructions on [this link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) or execute the next cell to do that.

```python
if not (os.path.isfile('/home/ftp/.ssh/id_rsa') and os.path.isfile('/home/ftp/.ssh/id_rsa.pub')):
    print(f'💡 We need to create an SSH key.')
    !mkdir -p /home/ftp/.ssh/
    !ssh-keygen -b 2048 -t rsa -f /home/ftp/.ssh/id_rsa -q -N ""
else:
    print('✅ All good you already have an RSA key pair.')
```

#### Copy your public key.

Now we need to copy the public key (the one you can share with the world) into our clipboard.

You need to copy everything: ssh-rsa .... ftp@jupyter...

```python
!cat /home/ftp/.ssh/id_rsa.pub
```

#### Add the public key to Github

Simply go here and add a "New ssh key": https://github.com/settings/keys

&#x20;

### Model

#### Let's clone a project to test that it works.

We will clone [awesome-notebooks](https://github.com/jupyter-naas/awesome-notebooks) for this example.

&#x20;&#x20;

We can also clone from the terminal like so:

```python
! git clone git@github.com:jupyter-naas/awesome-notebooks.git
```

It will use your new rsa key by default. (The default one is always stored at `~/.ssh/id_rsa` (`~` means "Your home directory", here it's `/home/ftp`))

### Output

#### Cloned repo is present in Jupyterlab



#### 🎉 Congratulations, you now know how to:

* Create an SSH key pair.
* Add it to your Github account.
* Clone a repository using SSH.

This knowledge is not only applicable on naas.ai but also on any other linux based machine.
