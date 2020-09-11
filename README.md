# Boreal: Incident Handling Tool

Boreal is a fork of [Aurora](https://github.com/cyb3rfox/Aurora-Incident-Response), an amazing original idea by Mathias Fulchs to document cases in incident response scenarios. As he says in the original repository it is "Developed by Incident Responders for Incident Responders".
Aurora (and Boreal) brings "Spreadsheet of Doom" used in the SANS FOR508 class to the next level. 

It's intended to be used in small and big incident response investigations to track findings, tasks, making reporting easy and generally stay on top of the game.

## 1. Download & Installation

You can download the current release of **Boreal: Incident Handling Tool** from the [Release Page](https://github.com/febrezo/Aurora-Incident-Response/releases). Boreal Incident Handling Tool is available for MacOS, Windows and Linux. We are working on making it available for iPads and Android Tablets as well.

## 2. But why a fork?

This fork is intended to deploy my own testing builds of Aurora prior to merge them. 
The changes I will submit here will be GPLv3-licensed, that is to say, any user receiving or forking this repo should take into account that the source code SHOULD be provided to the users to which the app is conveyed. This is something that is relevant for me from an ethical point of view: keeping code (and derivate code) as opened to the public as possible.  

This is fully compatible with Mathias Fulchs original licensing proposal (Apache License) since GPLv3 software can include Apache-licensed code providing that the code is appropiately quoted and mentioned.  

This fork does not mean that I'm not contributing to Aurora. Any relevant changes I'll do, I'll share them upstream with the original repository as I have already been doing lately. But while the the changes are merged upstream, having the chance of testing the builds separetely is also a good point.

And yes. Boreal comes from [Aurora Boreal](https://en.wikipedia.org/wiki/Aurora). 

## 3. Development

If you want to contribute, you are encouraged to do so. You will find all the information required in the [`HACKING.md`](doc/HACKING.md) file. Give it a try.

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



