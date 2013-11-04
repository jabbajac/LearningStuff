# Telepathik

***

## <a name='toc'>Table of Contents</a>

---

1. [Todo](#todo)
2. [Roadmap](#roadmap)
3. [App Requirements](#appreq)
4. [Setting up your environment](#envsetup)


## Tempory stuff 

---

* logo <http://d.pr/i/kOPQ>
* google app id
  * lunar-bonus-385

## Todo 

---

* google omniauth
  - [x] set up google account dev secret and key
  - [ ] check authentication
* twitter omniauth
  - [x] set up twitter account dev secret and key
  - [ ] check authentication
* facebook omniauth
  - [x] set up fb account dev secret and key
  - [ ] check authentication
* Telepathik API
  - [ ] user login API
  - [ ] user link feed API
  - [ ] friends top links feed API
  - [ ] overal top links feed API
  - [ ] relink a link API
  - [ ] retrieve info on users/links API

**[[^]](#toc)**

---

## Roadmap 

### MVP 

---

1. Users are able to share links via the dashboard, either to general or to specific friends
  * Users can sign in using twitter/facebook/google
  * uses Devise gem for account creation if user wants to create a seperate account (this is still on the table as a maybe)
2. Links will have a link score dependent on age, relinks, views
3. Dashboard will show:
  * Main section will show all links you've submitted (refreshes upon refresh)
  * Sidebar to show top 10 aggregated links from all user's friends (hourly persist)
  * top 10 links of all time (hourly persist)
4. Links will have tags, users can search by tag
5. All major transactions will be done via API built into Ruby framework

---

### v 1.0 

---

1. All features from MVP
2. Browser plugins (firefox/chrome)
3. Release API for general public use?

---

### v 2.0 

---

1. All features from v 1.0
2. Implement user groups, will probably add a third feed for groups only
3. Mobile Apps? (iOS/android/wm8)

**[[^]](#toc)**

---

## <a name='appreq'>App Requirements</a>

DB handling: MongoDB  
Dashboard: Ruby on Rails   
Bookmarklets: TBD (most likely javascript), maybe browser extensions instead?  
Authentication: OpenAuth (allows login using fb, twitter, google)  

#### Objective: 

---

Link sharing upgraded, capabilities include:

* Share to feed, share to friends, or share to group
    + share directly to friends/group without sharing to feed
    + feed can be sorted by link score (asc desc), date linked (newest to oldest)
    + friend feed shows top ten (or any other number) highest links from all friends
    + top links show top ten (or any other number) highest links from link db
* Shared links ranked based upon relinks and views
* Link score calculated based on relinks and views and days since last link
   + algorithm: ((3\*relink + 2\*views)\*(1-(days since last relink)/100))
   + relinks are weighed more than views
   + links that are not relinked after 100 days will fade 
   + links that are not relinked after a full day will start to lose link score ensuring newer links have a better chance of making it to the top


#### DB:

* Database objects and sample queries in telepathikdatamodel.txt

**[[^]](#toc)**

## <a name='envsetup'>Setting up the Environment</a>

---

* Installing GIT and checking out the project
  1. Install git, using git bash on windows will make the rest of the commands pretty much universal
  2. Once git is installed you should set up the git configs
    * use the command `git config global user.name "[your username]"`. Replace [your username] with your username for bitbucket.
    * use the command `git config gloabl user.email [your email]`. Replace [your email] with your email address. 
  3. Go to your working directory
  4. Execute `git clone https://[your username]@bitbucket.org/jwelker/telepathik.git` to clone the project off of bitbucket into your directory
  5. Currently we're working on the MVP so you should run `ggit fetch && git checkout MVP` to check out the MVP changes
  6. After you are done making changes to the code, if you have files to add use the command `git add .` to add any files you added
  7. After you add the files you need to commit them. At this point you should also add a comment to your commit to describe your changes. You commit using `git commit -am "[comments]"` fill in [comments] with your comments on changes you've made
  8. You can then push the project back up to bitbucket using `git push origin [branch]`. In the current case code should be pushed up to do the MVP branch so your command should be `git push origin MVP`

* Vagrant and the dev VM
  1. Follow instructions to install Vagrant from [http://docs.vagrantup.com/v2/installation/index.html](http://docs.vagrantup.com/v2/installation/index.html)
  2. In terminal or windows change directory to source directory. 
  3. vagrant up --provision  <-- this command will bring up the VM
    * I've remapped the port 80 on your host to match port 3000 on the guest OS so you can hit the RoR app just by going to [127.0.0.1](127.0.0.1)
    * You can ssh into the machine either by using 'vagrant ssh' no quotes or ssh into 127.0.0.1 port 2222, default username and password for now is vagrant  
    * You can launch the app by going to /vagrant/telepathik, runt 'bundle install', and then run 'rails s'
  5. You can shut down the vm with 'vagrant halt' or delete the VM with 'vagrant destroy'

**[[^]](#toc)**