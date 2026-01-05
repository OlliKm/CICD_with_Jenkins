# CICD Pipelines & Jenkins
- [CICD Pipelines \& Jenkins](#cicd-pipelines--jenkins)
      - [](#)
- [Step 1 setting up your Github Key](#step-1-setting-up-your-github-key)
    - [How to make the Key](#how-to-make-the-key)
- [Jenkins setup](#jenkins-setup)
    - [Jenkins Job 1 - Setup app](#jenkins-job-1---setup-app)
      - [Setting up your key in GitHub](#setting-up-your-key-in-github)
      - [Setting up credentials to link github with jenkins](#setting-up-credentials-to-link-github-with-jenkins)
- [Jenkins Job 2 Merging branches](#jenkins-job-2-merging-branches)
- [Jenkins Job 3 - app deploy](#jenkins-job-3---app-deploy)

#### Click to learn about CICD Pipelines 
[Link to Learning](/cicd-with-jenkins/README.md)

# Step 1 setting up your Github Key

### How to make the Key
1. open a git bash terminal and cd into your ```.ssh``` folder
   
2. you then want to run the command, replacing it with your email ```ssh-keygen -t rsa -b 4096 -C "email address"```
3. you will then be prompted to name the key, make sure not to backspace or back arrow key when typing in the Keys name:
4. Name the key something like: ```name-github-key```
5.  you now want to run agent on terminal window so it has permissions using the command ``` eval `ssh-agent -s```
6. we now want to register the private key to the terminal to do this we use the command ```ssh-add "private-key-name"```
7. Finally to check connection to github we will run ```ssh -T git@github.com ``` 

* Do be advised **AGENT** only runs in the terminal window you ran it on

----
# Jenkins setup 

 ![alt text](/images/jenkinshomepage.png)

### Jenkins Job 1 - Setup app 

* Setting up the Job
1. on Jenkins 
2. click new item 
3. name the item name-sparta-app-job1-ci-test 
4. click freestyle project 
5. click ok

 ![alt text](/images/jenkins-make.png)

---- 
* Setting up the configuration
1. click into the configurations and scroll down till you see the tick box setting for linking a github project  to the job

2. you then want to input the link to your github repo and remove '.git' at the end of it.


2. inside your job configuration settings scroll down to the bottom to the source code management area

3. click git and then you want to paste the SSH URL you get from your github repo (make sure this is SSH not HTTPS)

<br>

#### Setting up your key in GitHub

1. on your github repo click setting and then on the left hand side should be a option bar
2. select deploy keys - we then want to be click **Add deploy key** which will ask for a title and key.
3. for the title we want to paste the file name of the key and then paste the actual key itself into the Key section
#### Setting up credentials to link github with jenkins
1.  in the credentials option in settings clikc add credential "add jenkins"
2.  we want to select the type to be the **ssh username with private key**
3.  Once completed set the username to the key's name we made earlier "name"-2-github-key 
4.  add a  description: to explain what it does
5.   it will then ask you to put in the private key, we cant to click to type/paste it in.
6. to get the private key we need to go into the terminal and run ```cat "name""-2-github-key``` This will provide us with the encrypted key,
7. from there we want to copy and paste the whole key starting from the 5 hyphens to the last 5 hyphens.
<br>
1. we now want to scroll down and set the default branch to ```*/main```
2. In the build environment section selection the option to provide a Node &NPM bin folder
3.  for this we will be using version 20 of NodeJS 
<br>
1.  and finally we want to scroll all the way to the bottom, and within build steps select **Execute Shell** 
2.  Within the the shell we want to type in 3 commands:
```
cd app
npm install
npm test
```
1.  once you have typed in the commands you are finished so can now
2. save the job build

## How Webhooks work
 ![alt text](/images/webhook.png)
**What is a Webhook?**
* A webhook is a an automated message sent from one app to another when a specific event triggers. 
**How did I use them?**
* I used webhooks to make Github Notify Jenkins when a push occurs on the github repo, 
* this sends a message to jenkins which then once received initiates Job 1
**Key Benefits**
- Delivers data instantly in real time
- efficient as it reducing server load from both sender and receiver.
- Works automatically meaning its seamless

# Jenkins Job 2 Merging branches
**Setting up step 2- merging dev branch to main branch** 

* **Issues I faced initially:**
my  GitHub wasn't receiving the updates most likely due to me not **GIT PUSH** when in the DEV branch I only ```git add .``` and ```git commit``` which may be why it was getting pushed onto the GitHub when using Jenkins
* **Fix**
1. for the merge job I made sure that the GitHub hook was disabled and made sure in the **build environments** I had SSH agent turned on linking it to the key we made, 

2. I sorted this by just moving on for the moment and using git publisher plugin within jenkins, using the settings :
* tick both of these:
- [x] Push Only If Build Succeeds?
- [x] Merge Results?

the under **Branches** you want to put:

**"Main"** Under the branch to push section &
**"origin"** under the target remote name

* I tested whether this worked my adding text into my README.md file and git: adding,committing and pushing on dev branch. then checking the github repo.

* I also made sure in the configure "source code management " section I added to the **branch specifier** with ```*/main``` & ```*/dev ```

# Jenkins Job 3 - app deploy

1. On jenkins make a job that clones the step 2 job and name it under the pretext of deployment.
2. Tick the option in the build environment for **SSH AGENT** and click ==Add==
3. Make a new new ssh key and for the aws .pem file you have copying the file name and the private key.
4. once created select it as the ssh credential in the drop down list.
5. you then want to go down to the build steps and add a **Execute shell** this is where we will be adding the code so jenkins can ssh into the instance and scp the app code.
6. for this we will be using the code below:
```
rsync -av --delete -e "ssh -o StrictHostKeyChecking=no" \
  ./ ubuntu@54.229.71.203:/home/ubuntu/app/

ssh -o StrictHostKeyChecking=no ubuntu@54.229.71.203 << 'EOF'
  cd /home/ubuntu/app/app
  npm install
  pm2 restart all || pm2 start app.js
EOF
```
* this will ssh into the instance ignoring the host key checking to save time and input, we then specify where we are wanting to go which is the inside the app folder in the app instance we use the public ip of the instance to ssh in.
<br>

* we then are inside the VM where we are cd into the apps app and running npm install and then starting the app through pm2

#### If you havent read about the basics of CICD Pipelines yet I advise you click the link
[Link to CICD Pipelines Learning](/README.md)