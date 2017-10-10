[Back to Guides](../README.md)
# Python Virtual Environment Cheatsheet
---
[Source: Python Docs](https://docs.python.org/3/tutorial/venv.html)

### What the heck is this?

> Python Docs Said:
> Python applications will often use packages and modules that don’t come as part of the standard library. Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.
> This means it may not be possible for one Python installation to meet the requirements of every application. If application A needs version 1.0 of a particular module but application B needs version 2.0, then the requirements are in conflict and installing either version 1.0 or 2.0 will leave one application unable to run.


Basically virtual environments allow us to use different versions (Django 1.8 and Django 1.10) in different projects all one on computer. YOU SHOULD USE THIS! 

### Ok, how the heck do I install it?

Glad you asked! It's super easy as long as you have Python and Pip install. Remember that your pip version corresponds to your python version. So if you have type 'python3' to launch your python interpreter, you probably also have to use 'pip3' to install packages for that version of python.

```shell
$ pip install virtualenv
-or-
$ pip3 install virtualenv
```
On linux/mac you may get an error that talks about permission, in this case add 'sudo' at the start of the command. Keep this in mind as this may be a common problem.

```shell
$ sudo pip install virtualenv
```

### Umm, I think it worked. How can I tell?

Pip has a cool command that tells you all the packages you have installed.

``` shell
$ pip freeze
virtualenv==15.10
```

Try this command to see some more things you can do with pip

```shell
$ pip --help
```

### So I'm guessing I need to create one now?

You guess right! It's simple to do just CD (remember that means Change Directory using your terminal) into a directory where you want the virtual environment to live, we suggest in your workspace/venvs directory. Then just type 'virtualenv <some name>'.

```shell
$ cd ~/Desktop/workspace/venvs
$ virtualenv myFirstVirtualEnvironment
```

It may take a minute. All that stuff you're seeing on your terminal is the new virtualenv being created in a directory corresponding to the name of the virtual environment. You now have your own isolated python install. 

### OHHHHHHH YEAHHHHHH! How do I use it?

You need to 'activate' it. In the directory that was just created there is a 'bin' directory. In that directory there is a script called activate. We need to use that. All we do is:

```shell
CD into the virtual enviroment.
$ cd ~/Desktop/workspace/venvs/myFirstVirtualEnvironment
Activate On BASH (LINUX/MAC):
$ source /bin/activate
Activate on Command Prompt (WINDOWS):
$ Scripts\activate
```

### Check if its working

Now that you activated it, you should see the name of the virtual environment prepended (at the beginning) of your prompt. You can also check by typing pip freeze again, which shouldn't print anything because you are on a new python install (not the one you installed the virtualenv package on earlier).

Keep in mind that if you previously had to type 'python3' or 'pip3' previously, now you only have to type 'python' or 'pip'.

```shell
(myFirstVirtualEnvironment) $ 
```

### Deactivate it

Super Simple! Just enter the command 'deactivate' into your terminal.

```shell
(myFirstVirtualEnvironment) $ deactivate
$ 
```



