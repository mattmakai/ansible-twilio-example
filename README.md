# Ansible Twilio example
This project is an example for how to use the Twilio module in 
Ansible core notifications package which is part of the upcoming 
Ansible 1.6 release.

*Note*: this playbook requires the 
[Ansible devel](https://github.com/ansible/ansible) branch until 1.6 is
officially released.


## Walkthrough
Check the tags 
[example-step-1](https://github.com/makaimc/ansible-twilio-example/tree/example-step-1), 
[example-step-2](https://github.com/makaimc/ansible-twilio-example/tree/example-step-2) and
[example-step-3](https://github.com/makaimc/ansible-twilio-example/tree/example-step-3) 
to see each progressive addition to the playbook.

Copy set\_envs.sh.template to set\envs.sh and fill in your environment variables. Note this file
changes between example-step-1 and example-step-2 tags with new Twilio environment variables.


### Step 1: Playbook with get\_url module
Step 1 is a playbook that uses the get\_url module to download a remote file
and save it to the local node. We'll use this tag as a base for adding the
Twilio module in step 2 for notifications.


### Step 2: Add Twilio module for notifications
In step 2 we add the Twilio module to notify us in case our download does
not work properly. We'll simulate this by "fat-fingering" the site\_tarball
URL variable in the group\_vars/all file to have an extra character. That
will cause GitHub to return an HTTP 404 status code which will indicate
to Ansible that the download failed.

*Note*: if you run this step when the download file already exists on the
node from a previous playbook exection then Ansible will assume the get\_url
step was successful. To simulate the failure, make sure to delete the file
before a new playbook execution. 


### Step 3: Fix errors, now Twilio module is bypassed
In step 3 we just fix the site\_tarball URL and we see that when the download
is successful the error notification does not send a message because
that step is skipped.

