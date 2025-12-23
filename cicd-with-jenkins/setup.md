# CICD Pipelines

# How to setup your github key
```
#make key 
ssh-keygen -t rsa -b 4096 -C "email address"
#name it
name-github-key
```
* run agent on terminal window 
> eval `ssh-agent -s`

* adds private key to terminal
ssh-add "private-key-name"

> ssh -T git@github.com # check connection 

* when you have made your key in the terminal window as the agent will only be registered on that terminal window its best to stay in that window, if you need to move folders just cd back out of your .ssh and go to your desired file path **within the same terminal window that you started agent on** 
----
# Jenkins setup
Jenkins -> click new item -> name: name-sparta-app-job1-ci-test -> click freestyle project -> click ok
 
1. general -> github project tick > **link to github repo** but remove '.git' at the end.

2. tech515-sparta-test-app-cicd/ -> source code management > click git -> URL: **The SSH Github link** (make sure this is SSH not HTTPS)-> 
3. add credential -> add -> jenkins -> kind: ssh username with private key -> id&username: ""name"-2-github-key -> description: to read/write to repo -> private key -> enter directly (```cat "name""-2-github-key``` in github - copy and paste)-> add -> then add this key to credentials drop down -> branch -> 
4. set default branch to */main -> build environment -> click provide node & npm bin/ folder to PATH -> specify NodeJS version 20 -> build steps -> select **execute shell** -> we are now in github repo -> add the commands
```
cd app
npm install
npm test
```
5. save > build

# Jenkins merge branches
**Setting up step 2- merging dev branch to main branch** 

* **Issues I faced:**
my  GitHub wasn't receiving the updates most likely due to me not **GIT PUSH** when in the DEV branch I only ```git add .``` and ```git commit``` which may be why it was getting pushed onto the GitHub when using Jenkins

for the merge job I made sure that the GitHub hook was disabled and made sure in the **build environments** I had SSH agent turned on linking it to the key we made, 

I sorted this by just moving on for the moment and using git publisher plugin within jenkins, using the settings :

* tick both of these:
- [x] Push Only If Build Succeeds?
- [x] Merge Results?

the under **Branches you want to put:
**Main** Under the branch to push section &
**origin** under the target remote name

I tested whether this worked my adding text into my README.md file and git: adding,committing and pushing on dev branch. then checking the github repo.

I also made sure in the configure "source code management " section I added to the **branch specifier** with ```*/main``` & ```*/dev ```

# Jenkins app deploy

1. On jenkins make a job that clones the step 2 and name it under the pretext of deployment.
2. tick the option in the build environment for **SSH AGENT** and click ==Add==
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
