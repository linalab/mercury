# 🌕 Mercury Live Coding Environment 

**A minimal and human-readable language for the live coding of algorithmic electronic audiovisual performances.**

Mercury currently has 2 versions:

* Original version running in Max8 (Windows/Mac only) (you're in the right place)
* Web version running in the browser (Windows/Mac/Linux) [go to this repo](https://github.com/tmhglnd/mercury-playground)

**🚀 Start coding with the latest full version:** 

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/tmhglnd/mercury)](https://github.com/tmhglnd/mercury/releases)

[**👾 Or sketch in the browser playground!** (recommended for beginners)](https://mercury.timohoogland.com/)

[**🙏 Support Mercury by becoming a Patron**](https://www.patreon.com/bePatron?u=9649817) 

[**💬 Join the Discord Community!**](https://discord.gg/vt59NYU)

![Livecoding Performance with Mercury (photo: Zuzanna Zgierska)](media/mercury-live.png)

## 📋 Table of Contents

<!-- - [Newest Features](#-newest-features) -->
- 📟 [Mercury?](#-about)
- 🎮 [What can I do with Mercury?](#-features-overview)
- 🔭 [Who is it for?](#-vision--goals)
- 👩‍💻 [Code together with others!](#-collaborative-coding)
- 🚀 [Let's get started!](#-install)
	- [Quick Start](/docs/quick-start.md)
	- [Tutorial](/docs/tutorial.md)
	- [Documentation](/docs/table-of-content.md)
	- [Troubleshooting](/docs/08-troubleshooting.md)
	- [System Requirements](#-system-requirements)
	- [Sounds in Mercury](https://github.com/tmhglnd/mercury/blob/master/mercury_ide/media/README.md)
	<!-- - [Build Application](#-build-application) -->
- 🔎 [Read more](#-further-reading-and-listening)
- 👾 [Hear what others made](#-made-with-mercury)
- 🤓 [I like to help](#-contribute)
- 🔋 [Powered By](#-powered-by)
- 🙏 [Thanks](#-thanks)
- ✨ [Inspiration](#-inspiration)
- 📄 [Licenses](#-licenses)

<!-- ##  Newest Features

**Control external midi devices or send midi to other Applications with the new `midi` instrument**

```java
set midi getPorts
//=> prints the available devices to the console

new midi "Your Awesome Midi Device" time(1/4) note(7 1) length(100) gain(0.8)
```

**Input OSC addresses as arguments or output osc-messages in a similar way as using instruments**

```java
set osc default

new synth sine name(sn)
    set sn note(/sine/pitch 0) shape(5 /sine/release)
    set sn fx(reverb 1 /sine/verb)

new emitter osc name(myOSC) someParam(3.14)
    // result => /myOsc/someParam 3.14
``` -->

## 📟 About 

**Mercury is a minimal and human-readable language for the live coding of algorithmic electronic music.** 

All elements of the language are designed around making code more accessible and less obfuscating for the audience. This motivation stretches down to the coding style itself which uses clear descriptive names for functions and a clear syntax. Furthermore the editor is restricted to 30 lines of code, keeping all code always visible. Mercury provides the performer with an extensive library of algorithms to generate or transform numbersequences that can modulate parameters, such as melody and rhythm, over time. The environment produces sound in conjunction with visuals. Besides looking at the code, the audience is also looking at the visuals that are reactive to the sound or generated by the sound.

It is named after te planet Mercury. Mercury rules the creation and expression of our mental processes. The planet implores us to express ourselves. Mercury is about a quick wit, quick thinking. It lets us move from one thing to the next.

Mercury is programmed in the Cycling'74 Max8 node-based creative coding environment, as an abstracted layer on the Max/MSP audio engine and with the use of Node4Max for parsing, lexing and generative algorithms and Jitter/OpenGL for the visuals and the responsive texteditor.

Mercury uses the [Total Serialism NodeJS](https://github.com/tmhglnd/total-serialism#total-serialism) package available on npmjs.com. This package contains an extensive library of algorithmic composition methods.

![Screenshot of the Mercury environment](media/mercury-screenshot2.png)

## 🎮 Features Overview

Quick access to playback of samples and change timing and tempo of samples or synthesizers

```java
set tempo 89

new sample kick_909 time(1/4)
new sample hat_909 time(3/16)
```

Make rhythmic patterns with sequences of numbers and probabilities

```java
ring loBeat [1 0 0 1 0.5]
ring hiBeat [0 1 0.2 0]

new sample tabla_lo time(1/8) play(loBeat)
new sample tabla_hi time(1/8) play(hiBeat)
```

Generate psuedorandom melodic content for a synthesizer in a range and set a scale

```java
set scale minor d
set randomSeed 31415

ring melody random(16 0 24)

new synth saw note(melody) time(1/16) shape(4 100)
```

Design sounds with various effects

```java
new sample chimes time(2) speed(-0.25) fx(reverb 0.3 15) fx(drive 10) fx(lfo 1/8 sine)
```

Easily give multiple instruments the same effects

```java
new sample chimes time(2)
new sample harp_down time(3)
new sample gong_lo time(5)

set all fx(lfo 1/16) fx(delay) fx(reverb 0.5 11)
```

Generate sequences algorithmically to compose complex structures and choose from an extensive library of algorithms to work with

```java
set scale minor a 

ring rhythm euclidean(32 13)

ring melody spread(5 0 24)
ring melody palinedrome(melody)
ring melody clone(melody 0 5 7 3)
ring melody lace(melody melody)

new synth triangle note(melody 1) shape(1 80) play(rhythm)
```

Control external midi devices or send midi to other applications and use clock sync

```java
set midi getPorts
//=> prints the available devices to the console
new midi "Your Awesome Midi Device" time(1/4) note(7 1) length(100) sync(on)
```

Control other environments via OSC-messages

```java
ring params [0.25 0.5 0.75]

new emitter osc address(yourDevice) theParam(params) time(1/4)

// emits => /yourDevice/theParam 0.25
//          /yourDevice/theParam 0.5
//          /yourDevice/theParam 0.75
//          /yourDevice/theParam 0.25
//          etc...
```

Easily control parameters in Mercury via external OSC-messages

```java
new synth triangle fx(reverb /extOSC/verbAmount) fx(filter low /extOSC/cutoff 0.4) time(1) shape(1 1000)
```

**AND MANY MORE (TO COME...)**

## 🔭 Vision / Goals

- Provide creatives with a quick and hands-on coding environment/language to expres, communicate and improvise livecoded works.
- Use the environment as a teaching tool for:
	- introduction to (electronic) music
	- algorithmic composition
	- sequencing and pattern generating
	- sound design
	- creative coding and live coding
- Provide creatives with an hands-on language to create realtime processes
	- code sound and music
	- code visuals and let them react to sound
- Provide creatives with an extensive library of algorithmic composition techniques
	- released as a seperate Node Package titled [Total-Serialism](https://www.npmjs.com/package/total-serialism)
	- included in the Mercury environment through Node4Max
- Provide creatives with a multi-purpose non-linear-sequencer 
	- use OSC to communicate with other platforms
	- use MIDI to communicate with other platforms and devices
- Provide creatives with an easy sampler/synthesizer for sounddesign and composition
	- use external OSC to control parameters in the sampler/synthesis
	- use external MIDI devices and messages to play the sampler/synthesizers (coming soon...)
- Release a browser version and standalone Electron app, making getting started easier
- Collaborate in Mercury via the browser with Flok and code music together
- Extending the Mercury users-community and including extensions on the environment in the master-branch

⭐️ *watch and star this repo to keep up-to-date with the latest changes whenever they're made*

## 👩‍💻👨‍💻 Collaborative Coding

You can code together in Mercury using the amazing [**Flok**](https://flok.cc/) live coding environment in the browser. The easiest way to get started is by combining **Flok** with the **Mercury Playground**, but you can also combine Flok with the Mercury Max8 version.

- [Start coding together here](./docs/collaborate.md)

<!-- 
There are 3 options for how you can use Flok with Mercury:
1. Use Flok to combine Mercury with Hydra visuals (or other languages like Tidal, Foxdot and SuperCollider) on a localhost
2. Collaborate together in the same room (only requires 1 computer to run Mercury)
3. Collaborate remotely over a network (all computers need to run Mercury)

Install NodeJS v.12 [for Mac](https://nodejs.org/dist/latest-v12.x/node-v12.20.0.pkg) or [for Windows](https://nodejs.org/dist/latest-v12.x/node-v12.20.0-x64.msi).

Install the latest version of Mercury via the [quick start quide](https://github.com/tmhglnd/mercury/blob/master/docs/quick-start.md).

Install Flok via the Terminal with `npm install -g flok-web flok-repl`

**Localhost**

1. Run `flok-web` in the terminal
2. Open Google Chrome and go to `localhost:3000`
3. Setup Flok with target `mercury` (and optionally other targets like `hydra`) and click **Create session**.
4. Copy the `flok-repl -H xxx -s xxx -t mercury` command and run in the terminal.
5. **Join** the Flok with your nickname.

**Collaborate**

Now follow these steps for a succesful setup.
1. Open Google Chrome and go to [https://flok.clic.cf/](https://flok.clic.cf/)
1. Setup Flok with target `mercury` and click **Create session**.
2. Copy the `flok-repl -H xxx -s xxx -t mercury` command and run in the terminal.
4. **Join** the Flok with your nickname.

Now start typing some code! 🎵

- `Ctrl/Alt + Return` to evaluate
- `Ctrl/Alt + .` to silence

Flok will send the entire code via OSC messaging to port 4880. Mercury should be listening to this port automatically. Bug reports are very much welcome in the issues! -->

## 💻 Install

- 📖 [I need some help installing](./docs/tutorial.md)
- 🚀 [I'm an experienced computer user](./docs/quick-start.md)
- 💻 [Is my computer powerful enough?](#-system-requirements)

OR

- 🤓 I'll just [download](https://github.com/tmhglnd/mercury/releases) and figure it out myself

```
$ cd ~/Documents/Max\ 8/Projects
$ git clone http://github.com/tmhglnd/mercury
$ cd mercury
$ open mercury_ide/mercury_ide.maxproj
```

<!-- ### 🚀 Quick Start -->

<!-- [Open the Quick Start Guide](./docs/quick-start.md) -->

<!-- ### 📖 Tutorial -->

<!-- 🚧 (work in progress) 🚧 -->

<!-- If this is your first time with either the usage of creative coding software (like Max8), music theory, electronic music making and programming in general I highly recommend following the tutorial. -->

<!-- [Open the Tutorial](./docs/tutorial.md) -->

### ⚠ Troubleshooting

It could be that you are having issues with Mercury. Please follow the steps below:

- [Open the Troubleshooting](./docs/08-troubleshooting.md)

### 📖 Documentation

Full explanation of all the possibilities in Mercury:

- [Open the documentation](./docs/table-of-content.md)

### 💻 System Requirements

These system requirements are recommended to install and run Max and Mercury on your computer. Lower specs may work but it's not guaranteed. A dedicated Graphics Card (GPU) is also recommended to run the visual side of Mercury smoothly (the text-editor runs on the graphics card as well).

| OS | CPU | RAM |
| -- | --- | --- |
| Mac OSX 10.13 (at least 10.11.6+) | Intel i5 processor | 8 GB | 
| Windows 10 (7 or 8 may work) | Intel i5 or AMD mult-core processor | 8 GB |

<!-- ### 🛠 Build Application

`Optional`

**Why?** - Building the Application is recommended when using Mercury with other MaxMSP projects. This will allow Mercury to have a seperate thread from the other Max processes, giving it enough RAM and CPU space. Also the application will probably run more stable because the project can not be editted anymore. This, of course, also dependents on your system specifications.

**How?** - The Cycling'74 Max8 coding environment is needed to build the application from the `mercury_ide_x.x.x.maxproj` file. Open the `.maxproj` file and select `Build Collective/Application` from the `Settings` menu on the bottom of the project window. *Building the Application is not necessary in order to run the environment!* -->

### 🎵 Sounds

Most sounds in Mercury are downloaded from [freesound.org](http://www.freesound.org) and are licensed with Creative Commons Attribution or Creative Commons 0 licenses. If not downloaded from freesound it is made sure that the license allows to redistribute the sounds via the Mercury environment and that you can use them in your projects. A list of all the available sounds and the original sample can be found here:

- [List of sounds and credits](././mercury_ide/media/README.md)

## 🔍 Further reading

- [Mercury homepage](http://www.timohoogland.com/mercury-livecoding)
- [Paper in ICLC 2019](http://iclc.livecodenetwork.org/2019/papers/paper67.pdf)
- [Total Serialism Library](https://github.com/tmhglnd/total-serialism#total-serialism)

## 👾 Made with Mercury

- *Made something with Mercury? Please add a URL here and send a pull request!* 😎
- [T.mo - Liber Abaci (Mercury Coding Sessions)](https://youtu.be/syUL76qCV6w)
- [Roald van Dillewijn - Smashing Temparateness (Mercury Coding Sessions)](https://youtu.be/KJ4OpJ3-Ik0)
- [Rafa & Timo - "Hello, off-world!" (Mercury Coding Sessions)](https://youtu.be/BbOz1XBu8f8)
- [Guillem Góngora Moral - Transcription #1 (Mercury Coding Sessions)](https://youtu.be/wRVQHlghitM)
- [Anne Veinberg - CodeKlavier meets Mercury (Mercury Coding Sessions)](https://youtu.be/e4sPKOlaYS8)
- [Nick Levantis - Wake Up](https://youtu.be/UsfKF0ggn7k)
- [Rafa & Timo - "Hello, off-world!" (Live at NMF)](https://www.youtube.com/watch?v=7UWywv_DPHI&t=4s)
- [Roald van Dillewijn - Mercury & DigiLog](https://www.youtube.com/watch?v=1v7xicXuSbo&t=346s)
- [Sasj & Timo - Amalgam (Live at Github Sattelite 2020)](https://www.youtube.com/watch?v=zzmgX4QSBMM)
- [Anne Veinberg - CodeKlaver & Mercury Extension Tryout](https://www.youtube.com/watch?v=VSoibHwQJ98&t=175s)
- [Timo - Live at NerdLab VR 2020](https://www.youtube.com/watch?v=EW9x68sxhvM)
- [T.mo - Live at Eulerroom Equinox 2020](https://www.youtube.com/watch?v=X0FFcdd1QEE)
- [T.mo - Live at Algo:Ritmi 2020](https://www.facebook.com/timohoogland/videos/3654187371320680/)
- [T.mo - Live at NLCL Meetup STEIM](https://www.youtube.com/watch?v=leckC_yUMss)

## 📝 Contribute

Contributions to the Mercury environment are much appreciated in whatever form they come! You can contribute in any of the following ways:

- Add suggestions, bugs or feature-requests to the [issues](https://github.com/tmhglnd/mercury/issues)
- Make additions or changes to the Documentation, Tutorials, Examples and any other text in this repository
- Adjust the source code or make bugfixes and add features by forking and sending a pull request (see the [Guidelines](#guidelines))

In order to make changes to various types of source code files you will need the following:

- `patchers` - Requires Max8 environment and license to edit/modify/save the patchers of this project.
- `JS code` - Requires a standard code-editor (eg. VSCode or Atom) to edit/modify/save the JS code.
- `GenExpr Code` - Requires a standard code-editor (eg. VSCode or Atom) to edit/modify/save the GenExpr code.

### Guidelines

In order to receive your contribution please follow these steps:

1. Fork this repository (click `fork` in the top right)
2. Clone the repository to your computer `git clone https://github.com/<this-is-you>/<forked-repo>.git`
3. Branch the Fork `git checkout -b <name-your-branch>`
4. Make any changes/additions to the code or docs
5. Add, commit and push your changes `git add .` `git commit -a` `git push origin <your-branch-name>`
6. Go to your forked repo in the browser and click `compare & pull request`, then `create pull request`
7. Please add a comment to clarify what you did and why

[All steps with examples and images](https://github.com/firstcontributions/first-contributions/blob/master/README.md)

## 🔋 Powered By

- Mercury has been granted funding from [**Creative Industries Fund NL**](https://stimuleringsfonds.nl/en/)
- Mercury has been granted in-kind funding from [**Creative Coding Utrecht**](https://creativecodingutrecht.nl/)

## 🙏 Thanks

- Roald van Dillewijn for working together on osc and midi functionalities combined with his [Digilog modified guitar-pedals](https://roaldvandillewijn.nl/projects/digilog)
- Guillem Gongora Moral for using Mercury as a composition tool and sharing valuable feedback in the process
- Anne Veinberg for working with Mercury and a Mercury extensions for the [CodeKlavier](https://codeklavier.space/) project
- Rafaele Maria Andrade for collaboration on [networked performance](https://www.youtube.com/watch?v=7UWywv_DPHI&t=4s) between Mercury and Knurl
- Repo banner image by Annebel Bunt
- Live performance image by Zuzanna Zgierska

## ✨ Inspiration

During the development of Mercury (both the playground and the full version) I've found inspiration in many other live coding environments, practices and other platforms. Some of these are:

- [Hydra](https://hydra.ojack.xyz/) - Live coding visual synthesizer by Olivia Jack
- [Sema](https://sema.codes/about) - Live coding language design platform combined with Machine Learning
- [MIMIC Project](https://mimicproject.com/about) - a web platform for the artistic exploration of musical machine learning and machine listening.
- [Tidal](https://tidalcycles.org/index.php/Welcome) - Live coding of patterns
- [Sonic Pi](https://sonic-pi.net/) - The live coding synth for everyone
- [Tone.js](https://tonejs.github.io/) - Webaudio framework for programming synths and sequencers
- [Nearley](https://nearley.js.org/) - Parsing toolkit

## 📄 Licenses

- Main Source - [The GNU GPL v.3 License](https://choosealicense.com/licenses/gpl-3.0/) (c) Timo Hoogland 2019-2023
- Sound Files - Individually licensed, listed under [media/README.md](/mercury_ide_0.9.9/media/README.md)
- Documentation - [The CC BY-SA 4.0 License](https://creativecommons.org/licenses/by-sa/4.0/) (c) Timo Hoogland 2019-2023
- Examples - [The CC BY-SA 4.0 License](https://creativecommons.org/licenses/by-sa/4.0/) (c) Timo Hoogland 2019-2023
- Max8 - Proprietary Software, Max (c) 1990-2019 Cycling'74 / IRCAM All rights reserved

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
