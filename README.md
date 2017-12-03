# Task Lights

Like music, light (color) is an excellent source of information that the brain can process in the background. A more structured signal, like a clock or count down timer (24:13 minutes) requires our eyes to first shift focus to the location of the information, and then perform a further mental calculation to reason about the time you’ve spent on a task. All that extra thinking can be disruptive of our work.

Simply having the light on is a strong and constant environmental cue that you have a task that you need to complete. The color helps you be aware of your state: (getting started, need to really work, ok — wrap it up time is almost done). Fun trick, try reading this text and see the light in the picture below. Now, what about that 24:13 timer?

![demo](https://media.giphy.com/media/vQsEfQegkAl8s/giphy.gif)

## Hardware

The LED light is a [blink(1)](https://blink1.thingm.com/).

## Instructions for installing on Linux (tested on 14.04 LTS 64-bit):

1. #### Setting up environment
  * Seting up basic requirements:
  ``` bash
  sudo apt-get update
  sudo apt-get install git make vim python-dev python-pip
  sudo apt-get install build-essential libssl-dev
  ```

  * Setting up USB library:
  ``` bash
  sudo apt-get install libudev-dev libusb-1.0-0-dev libfox-1.6-dev
  ```

  If using Debian/Ubuntu:
  ```
  sudo apt-get install libasound2-dev
  ```

2. #### Installing Node.js:
  * See [tutorial here](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-an-ubuntu-14-04-server) for other ways:
  ``` bash
  curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh
  source ~/.profile
  nvm ls-remote
  nvm install v6.9.4
  nvm use 6.9.4
  node -v
  # See where installed
  which node
  ```

  You may want to add `nvm use 6.9.4` add the end of your .bashrc/.profile or change (nvm alias)[https://github.com/creationix/nvm#listing-versions] to set 6.9.4 be your default version:
    `nvm alias default 6.9.4`

3. #### Change directory to src and do:
  ```npm install```

  
4. #### To get the web-server to work:
  Change directory to `/src/controllers/web` and do
  ```npm install```
  and to start the local-server do the following and go to `http://localhost:5000/` in your browser:
  ```node app.js```


## Instructions for installing on Windows (tested on win 7, 10):

1. #### Setting up environment
  * Installing Node.js:
    * Download and install: [Node.js 6.9.4 64-bit](https://nodejs.org/dist/v6.9.4/node-v6.9.4-x64.msi)
    * For 32-bit Windows see Node.js (website)[https://nodejs.org/en/download/]

2. #### Installing    
  * Automaticlly install
    * Run the shell as administer
    * Change directory to src and do:
      ```bash
      npm install --global --production windows-build-tools
      ```
    * do: 
      ```
      npm install
      ```
    
  
  * If automaticlly install does not work, try manually install
    * Setting up basic requirements:
      * Install Microsoft Visual Studio (community/express versions are enough)
      * Or use (this one-liner)[https://github.com/felixrieseberg/windows-build-tools] if you just want the build tools.
      
      You may want to add `PATH/TO/NODE-NPM` to your environment path (if it was not added automatically).

    * Change directory to src and do:
      ```
      npm install --global --production windows-build-tools
      ```
    * do: 
      ```
      npm install
      ```  

3. #### To get the web-server to work:
  * Change directory to `/src/controllers/web` and do
    ```
    npm install --global --production windows-build-tools
    ```
  * do: 
    ```
    npm install
    ```
  
  * To start the local-server do the following:
    * Change directory to `/src/controllers/web` and do:
    ```node app.js```
    
    
    * Go to `http://localhost:5000/` in your browser

4. #### To track your focus: 
   Create a git repository and update `src/settings.json` with your information.<br>
   Content of `settings.json` should look like:
   ```
   { 
     	"remote": "Remote url of the repository you just created",
     	"username": "Your GitHub username",
     	"repo_name": "Name of the repository you just created"
   }
   ```
   
   Then you will be able to see a heatmap of your TaskLights sessions at: 
      * {Your GitHub username}.github.io/{Name of the repo you made}
      * Example: [ssmirr.github.io/FocusDash](https://ssmirr.github.io/FocusDash/)

   Or a json of your sessions in master branch of the repository that you created.

<br/>

## Command line arguments
##### Run "node blink.js --help" for help page:
1. Type:
     * `--solid`  or `-s`
     * `--linear` or `-l`
     * `--exponential` or `-e`
2. Length:
     * `--length 10` (in minutes)
3. Lightness (optional):
     * `--lightness 0.7`
4. Pomodoro (25 min linear session):
     * `--pomodoro` or `-p`
     * Ticking sound: `--tick` or `-t`

 For example to do a pomodoro with ticking sound:
 ``` bash
 $ node blink.js -p -t
  ```
 Or to do solid style indicator for 45 minuets:
 ``` bash
 $ node blink.js --solid --length 45
 ```

### Common errors:
1. **USB permission (on linux)** : </br>
      If you get `cannot open device with path 0001:0004:00` error, you can either use your administrator rights (`sudo`) or set a udev rule (copy [51-blink1.rules](https://github.com/todbot/blink1/blob/master/linux/51-blink1.rules) to `/etc/udev/rules.d/`)
      * If you get error when trying to do `sudo node ...` run this command:
       ```
       n=$(which node);n=${n%/bin/node}; chmod -R 755 $n/bin/*; sudo cp -r $n/{bin,lib,share} /usr/local
       ```
       Click [here](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-with-nvm-node-version-manager-on-a-vps#-installing-nodejs-on-a-vps) for details of how this works.

<br/>
<br/>

**Want to know more about this research project?** see: [Summary of tasks](https://github.com/alt-code/TaskLights/blob/master/Summary.md)
