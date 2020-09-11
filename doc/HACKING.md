# Development

If you want to contribute, you are encouraged to do so. I'd totally like to see the tool growing. 
The whole application is built on an Electron base and written in plain Javascript and HTML.
Even though technically `node.js` modules for functionality like Webdav this was discarded since node modules will not run out of the box when migrating the code to phonegap for IOS and Android.
The good news is that it's really fast to set up your development environment. I personally use elementary Code with `node` installed in my system but it should work with pretty much any IDE.

# 1 Set up your build environment

As pointed out in the description, Boreal Incident Handling Tool is built in top of Electron which allows for multi platform compatibility.
You can easily install your tool chain the following way.

Start by installing node.js. Follow the links to their [download page](https://nodejs.org/en/download/).

With `nodejs` installed, checkout the Boreal Github repo (or fork first if you want to contribute) and checkout to `dev`, which is the branch in which I keep track of Boreal changes.

```
git clone https://github.com/febrezo/Aurora-Incident-Response
cd Aurora-Incident-Response/src
git checkout dev
```

Now you need to install Electron using node. Currently Aurora is configured to run with `electron` 4.0.6. 

```
npm install electron@4.0.6
```

You can now run the code by invoking:

```
node_modules/.bin/electron .
```

That's fast, isn't it?


# 2 Roadmap

The following points are already on the roadmap. Please just post a new issue or send a message on [Twitter](https://twitter.com/cyberfox) if you got any suggestions for new improvements.

* Add Webdav capability for easier sharing (Currently multiuser mode uses shares) &#128679;
* Add csv import and export functionality with custom field mapping
* Create a tablet version (only makes sense once Webdav works)
* Reporting System to export prefilled report templates (requires adding killchain stage to timeline elements)

# 3 Build executables for distribution

To build and cross build you can use the `electron-packager` tool which can be installed using `npm`. 

```
npm install electron-packager
```

To build it for Windows, once in the `src` folder:

```
./node_modules/.bin/electron-packager . Boreal --asar --prune --platform=win32 --electron-version=4.0.6 --arch=x64 --icon=icon/aurora.ico --out=release-builds --ignore "node_modules/\.bin"
```

To build it for MacOS, from the same `src` folder:

```
./node_modules/.bin/electron-packager ./src Boreal --overwrite --platform=darwin --arch=x64 --icon=icon/aurora.icns --prune=true --out=release-builds
```

And finally, to build it for GNU/Linux, in the same `src` folder type:

```
./node_modules/.bin/electron-packager . Boreal --asar --prune --platform=linux --electron-version=4.0.6 --arch=x64 --icon=icon/aurora.ico --out=release-builds --ignore "node_modules/\.bin"
```

# 4 Sourcecode Navigator

This section describes the various sourcecode files. For now I need to keep this section small. I tried to comment in the code as good as I can. If you got any questions, just ping me. If you want to join me developing the tool, there's a slack channel to communicate. Drop me a note and I will invite you.

### 4.1 `main.js`
Electron apps differentiates between a main (background) and a render process(chromium browser window). This file controls the main process.
 
For Aurora, you usually only need to go there if you want to turn on the Javascript console in the Aurora window. Just unquote the following line:

```
win.webContents.openDevTools()
``` 

The second thing that's handled there is autosaving and unlocking when you exit the program. For that the main and the render process share a global variable called <code>global.Dirty.is_dirty</code> that is used to signal to the main process if it can quit right away or if the file needs to be sanitized before exiting.
It's actually a very similar concept to the NTFS dirty bit.
 
### 4.2 `index.html`

This is the main Boreal file that strings together all scripts and stylesheets. It also initiates the GUI. Other than that it has no functionality.
 
### 4.3 `gui_definitions.js`

I tried as good as I can to separate code an design. This file holds all the definition json for the `w2ui` GUI. There is some code left in there
for the renderers that format certain columns. It didn't make sense to place them anywhere else.
 
### 4.4 `controller.js`

The controller injects the handling functions for gui events. So whenever a button is pressed, or any other event needed happens, controller.js handles what happens.
 
### 4.5 `gui_functions.js `

Every now and then operations happen that change something in the gui. That could e. g. be making all the datafields readonly when you don't have the lock or simply opening a popup.
All these functions are located in this file.
  
### 4.6 `data.js`

While the actual data is stored in the `w2ui` datasctructures, for saving and some other operations we need to bring it into out format. 
Transformations like this and all logic regarding saving and opening files is located here.
 
### 4.7 `data_template.js`
  
This holds templates for the internal data format of that version. Current format version is 3. 
 
### 4.8 `misp.js`
 
Code for MISP integration.
 
### 4.9 `virustotal.js`
  
Code for VT integration.
 
### 4.10 `settings.js`
 
Settings for different libraries. Currently only defines the time field format for `w2ui`.
 
### 4.11 `helper_functions.js`

Small helper functions that do not fit anywhere else.
