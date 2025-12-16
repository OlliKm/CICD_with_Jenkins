# CICD Pipelines

#make key 
ssh-keygen -t rsa -b 4096 -C "email address"
#name it
name-github-key

* run agent on term iwndow 
> eval `ssh-agent -s`

ssh-add private-key-name # adds priv key 

ssh -T git@github.com # check connection 

* when you have made your key in the terminal window as the agent will only be registered on that terminal window its best to stay in that window, if you need to move folders just cd back out of your .ssh and go to your desired file path **within the same terminal window that you started agent on** 
