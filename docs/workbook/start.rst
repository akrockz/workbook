Create AWS Account
------------------

* Do the below for workshop learning.

1. Go to below training account.

https://abc-training.signin.aws.amazon.com/console


2. Login with provided username and password with details from `here <http://abc.com:8190/download/attachments/account-cred.txt?api=v2>`_

* (Or do the below only for your own learning. Not necessary for the workshop)

1. `Create AWS Account <https://aws.amazon.com/getting-started/>`_
2. `Create Default VPC <https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html#create-default-vpc>`_

Create Workspace
-----------------
1. Create a Cloud9 Environment

	https://ap-southeast-1.console.aws.amazon.com/cloud9/home?region=ap-southeast-1

2. Select **Create environment**
3. Name it **ws**, and take all other defaults
4. When it comes up, customize the environment by closing the welcome tab and lower work area, and opening a new terminal tab in the main work area
5. If you like this theme, you can choose it yourself by selecting **View / Themes / Solarized / Solarized Dark** in the Cloud9 workspace menu.

.. image:: images/getting-started/cloud9-interface.png
    :width: 100%
    :align: center

.. note::

	If there is a pop up from Cloud9, Select the below option to disable AWS managed credential option

.. image:: images/getting-started/note-1.png
    :width: 50%
    :align: center

.. image:: images/getting-started/note-2.png
    :width: 50%
    :align: center
    
Environment Setup
-----------------

Type below commands in your Cloud9 terminal window.

.. code-block:: bash

	# Install python3 and pip3
	sudo yum remove -y python36   
	sudo yum -y install https://centos6.iuscommunity.org/ius-release.rpm
	sudo yum -y install python36u
	sudo yum -y install python36u-pip
	sudo pip3.6 install requests
	sudo pip3.6 install bs4
	sudo pip3.6 install boto3
	sudo pip3.6 install pypac

Get "scripts" for SAML authentication. **On your Local Terminal**:

.. code-block:: bash
	
	curl -O http://abc.com:8190/download/attachments/scripts.zip
	unzip scripts.zip
	rm scripts.zip
	

Switch back to your Cloud9 workspace.

* Upload local files to Cloud9

.. image:: images/getting-started/upload-1.png
    :width: 50%
    :align: center

.. image:: images/getting-started/upload-2.png
    :width: 100%
    :align: center

Git config 
----------

Edit your git config. Type below command in your Cloud9 terminal window.

.. code-block:: bash

 sudo git config --edit --system

Modify it with below contents in your git config. Replace with your respective username and email.

.. code-block:: bash

	[user]
	       name = "<user name>"
	       email = <email>
	[push]
	       default=simple
	[color]
	       ui = auto
	[core]
	       autocrlf = input
	       editor = vim
	       askpass =
	[rerere]
	       enabled = 1
	[credential]
	       helper = !aws --profile=saml codecommit credential-helper $@
	       UseHttpPath = true
	[merge]
	       ff = false

After modification, the git config file should look like below.

.. image:: images/getting-started/gitconfig.png
    :width: 75%
    :align: center

* Run SAML authentication script to get the temporary token which is active only for 8 hours. Username is your win2k_id and the password is PIN + 6 digit token number since Cloud9 environment does not go through proxy2. 

.. code-block:: bash

	cd ~/environment/scripts/
	python3.6 samlauth.py

* Once validated, it will ask you to choose the role. Choose the below role.

.. code-block:: bash

	abc-auto arn:aws:iam:35545:role/DEMO_DEVOPS


Clone
-----

Clone the required repos.

.. code-block:: bash

  mkdir ~/environment/cloud
  cd ~/environment/cloud
  git clone https://git-codecommit.ap-southeast-1.amazonaws.com/v1/repos/devops
  
