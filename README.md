# Boreal: Incident Handling Tool

Boreal is a fork of [Aurora](https://github.com/cyb3rfox/Aurora-Incident-Response), an amazing original idea by Mathias Fulchs to document cases in incident response scenarios. As he says in the original repository it is "Developed by Incident Responders for Incident Responders".
Aurora (and Boreal) brings "Spreadsheet of Doom" used in the SANS FOR508 class to the next level. 

It's intended to be used in small and big incident response investigations to track findings, tasks, making reporting easy and generally stay on top pf the game.


## 1. But why a fork?

This fork is intended to deploy my own testing builds of Aurora prior to merge them. 
The changes I will submit here will be GPLv3-licensed, that is to say, any user receiving or forking this repo should take into account that the source code SHOULD be provided to the users to which the app is conveyed. This is something that is relevant for me from an ethical point of view: keeping code (and derivate code) as opened to the public as possible.  

This is fully compatible with Mathias Fulchs original licensing proposal (Apache License) since GPLv3 software can include Apache-licensed code providing that the code is appropiately quoted and mentioned.  

This fork does not mean that I'm not contributing to Aurora. Any relevant changes I'll do, I'll share them upstream with the original repository as I have already been doing lately. But while the the changes are merged upstream, having the chance of testing the builds separetely is also a good point.

And yes. Boreal comes from [Aurora Boreal](https://en.wikipedia.org/wiki/Aurora). 

## 2. Download & Installation

You can download the current release of Boreal: Incident Handling Tool from the [Release Page](https://github.com/febrezo/Aurora-Incident-Response/releases). Boreal Incident Handling Tool is available for MacOS, Windows and Linux. We are working on making it available for iPads and Android Tablets as well.

## 3. Development

If you want to contribute, you are encouraged to do so. I'd totally like to see the tool growing. 
The whole application is built on an Electron base and written in plain Javascript and HTML.
Even though technically `node.js` modules for functionality like Webdav this was discarded since node modules will not run out of the box when migrating the code to phonegap for IOS and Android.
The good news is that it's really fast to set up your development environment. I personally use elementary Code with `node` installed in my system but it should work with pretty much any IDE.

### 3.1 Set up your build environment

As pointed out in the description, Boreal Incident Handling Tool is built in top of Electron which allows for multi platform compatibility.
You can easily install your tool chain the following way.

Start by installing node.js. Follow the links to their [download page](https://nodejs.org/en/download/).

With `nodejs` installed, checkout the Boreal Github repo (or fork first if you want to contribute) and checkout to `dev`, which is the branch in which I keep track of Boreal changes.

```
git clone https://github.com/febrezo/Aurora-Incident-Response
cd Aurora-Incident-Response/src
```


Now you need to install Electron using node. Currently Boreal is configured to run with Electron 4.0.6. 

```
npm install electron@4.0.6
```

You can now run the code by invoking

```
node_modules/.bin/electron .
```

That's fast, isn't it?

### 3.2 Roadmap

The following points are already on the roadmap. Please just post a new issue or send a message on twitter if you got any suggestions for new improvements.

* Add Webdav capability for easier sharing (Currently multiuser mode uses shares) &#128679;
* Add csv import and export functionality with custom field mapping
* Create a tablet version (only makes sense once Webdav works)
* Reporting System to export prefilled report templates (requires adding killchain stage to timeline elements)

### 3.3 Build executables for distribution

To build and cross build you can use `c`. 

```
npm install electron-packager
```

To build it for Windows, once in the `src` folder:

```
./node_modules/.bin/electron-packager . Aurora --asar --prune --platform=win32 --electron-version=4.0.6 --arch=x64 --icon=icon/aurora.ico --out=release-builds --ignore "node_modules/\.bin"
```

To build it for MacOS, from the same `src` folder:

```
./node_modules/.bin/electron-packager ./src Aurora --overwrite --platform=darwin --arch=x64 --icon=icon/aurora.icns --prune=true --out=release-builds
```

And finally, to build it for GNU/Linux, in the same `src` folder type:


```
./node_modules/.bin/electron-packager . Aurora --asar --prune --platform=linux --electron-version=4.0.6 --arch=x64 --icon=icon/aurora.ico --out=release-builds --ignore "node_modules/\.bin"
```

### 3.4 Sourcecode Navigator

This section describes the various sourcecode files. For now I need to keep this section small. I tried to comment in the code as good as I can. If you got any questions, just ping me. If you want to join me developing the tool, there's a slack channel to communicate. Drop me a note and I will invite you.

#### 3.4.1 `main.js`
Electron apps differentiates between a main (background) and a render process(chromium browser window). This file controls the main process.
 
For Aurora, you usually only need to go there if you want to turn on the Javascript console in the Aurora window. Just unquote the following line:

```
win.webContents.openDevTools()
``` 

The second thing that's handled there is autosaving and unlocking when you exit the program. For that the main and the render process share a global variable called <code>global.Dirty.is_dirty</code> that is used to signal to the main process if it can quit right away or if the file needs to be sanitized before exiting.
It's actually a very similar concept to the NTFS dirty bit.
 
#### 3.4.2 `index.html`
This is the main Boreal file that strings together all scripts and stylesheets. It also initiates the GUI. Other than that it has no functionality.
 
#### 3.4.3 `gui_definitions.js`
I tried as good as I can to separate code an design. This file holds all the definition json for the w2ui gui. There is some code left in there
for the renderers that format certain columns. It didn't make sense to place them anywhere else.
 
#### 3.4.4 `controller.js`
The controller injects the handling functions for gui events. So whenever a button is pressed, or any other event needed happens, controller.js handles what happens.
 
#### 3.4.5 `gui_functions.js `
Every now and then operations happen that change something in the gui. That could e.g. be making all the datafields readonly when you don't have the lock or simply opening a popup.
All these functions are located in this file.
  
#### 3.4.6 `data.js`
While the actual data is stored in the w2ui datasctructures, for saving and some other operations we need to bring it into out format. 
Transformations like this and all logic regarding saving and opening files is located here.
 
#### 3.4.7 `data_template.js`
  
This holds templates for the internal data format of that version. Current format version is 3. 
 
#### 3.4.8 `misp.js`
 
Code for MISP integration.
 
#### 3.4.9 `virustotal.js`
  
Code for VT integration.
 
#### 3.4.10 `settings.js`
 
Settings for different libraries. Currently only defines the time field format for w2ui.
 
#### 3.4.11 `helper_functions.js`
Small helper functions that do not fit anywhere else.


## 4 Credits

Thanks to [Mathias Fuchs](https://twitter.com/mathias_fuchs) for the idea. It's obvious the amount of time spent in developing Aurora and his knowledge in the field. Incident responders like me myself are in debt with his job.

Projects like this can only be realized because many people invested thousands of hours into writing cool libraries and other software. Others contribute professional UI items. Thank you for all your great work.

Aurora is concretely build on the following dependencies: 

* Electron https://www.electronjs.org
* jquery https://jquery.com
* w2ui http://w2ui.com/web/
* vis.js https://visjs.org
* icons8 https://icons8.com
* Fontawesome https://fontawesome.com

Besides the incredible amount of work that people invested into these projects, you need other support as well. Writing the code is easy, but making it a tool the works in reality depends on a vast amount of experience from many incident responders. 
Here Mathias particularly wanted to mention the members of his IR team who contributed their knowledge and helped testing the tool in real world cases:

* Rothi
* Bruno
* Sandro

Even though this is a side and weekend project it's still good to know, that his employer Infoguard AG supports me in any way they can. So thanks to them too:

* Ernesto
* Thomas



