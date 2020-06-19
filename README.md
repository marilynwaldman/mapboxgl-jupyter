# Install mapboxgl jupyter on on AWS

## ssh to your  aws instance

1.  Obtain your aws security key and place it in your home directory on your local computer
2.  Change the permissions on the key
    
    `chmod 400 myaws.pem`
    
    Note:  You may place this key in your .ssh directory and make the proper adjustments when
    you ssh to your aws instance

1.  ssh into your instance - obtain addresses from AWS administrator

`ssh -i "myaws.pem" ubuntu@ec2-34-221-171-5.us-west-2.compute.amazonaws.com`

## Install Anaconda
2.  Install Anaconda on your aws instance.
    Per this article
    https://analyticsindiamag.com/setting-up-a-completely-free-jupyter-server-for-data-science-with-aws/

3.  Within the aws instance create a Downloads directory and cd to it

     ```
        mkdir Downloads
        cd Downloads
    ```
     
4.  Download the Anaconda code

`wget https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh`  

5.  Unpack the shell installer - this will install Anaconda

`bash Anaconda3-2019.03-Linux-x86_64.sh`   

## Set up Jupyter notebooks with an empty password

6.    cd to your home directory, then set the Jupyter password to the empty string

   `cd`
   
   enter the python interrupter and create the password.
   
   ```$xslt
      from IPython.lib import passwd
      passwd()
```

SAVE THE PASSWORD HASH!!!  It looks like:

sha1:057a582a99999:92684a48df8b4396bc27a81995541f930499999

7.  Generate a Jupyter configuration file

`jupyter notebook --generate-config`

8.  Edit the configuration file and add the following lines.  Replace the password hash with
the hash created in step 7.

`vim ~/.jupyter/jupyter_notebook_config.py`

```
c = get_config()
#Kernel config
c.IPKernelApp.pylab = 'inline'  #Enables plotting support by default
#Notebook config
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.open_browser = False  #Setting it to False will not let the Notebook attempt to open up in a native browser.(AWS server has no browsers or GUI)
c.NotebookApp.password = u'sha1:057a582a99999:92684a48df8b4396bc27a81995541f930499999'  #The encrypted password to log in to jupyter notebook
#Setting the default port for Jupyter Notebook
c.NotebookApp.port = 8888
```

9.  You can now load your notebooks from http.

`http://ec2-34-210-8-158.us-west-2.compute.amazonaws.com:8888`

REPLACE THE ec2... with the ip for your instance.

## Install node

10.  Node is used everywhere.  Let's install it now.

`conda install -c conda-forge nodejs`

11.`








