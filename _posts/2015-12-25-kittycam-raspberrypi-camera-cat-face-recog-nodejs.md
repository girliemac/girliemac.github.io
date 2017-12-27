---
title: KittyCam - Building a Raspberry Pi Camera with Cat Face Detection in Node.js
author: Tomomi Imura
layout: post
images:
  - /assets/images/articles/2015/12/jamie-detected.png
categories:
  - dev
  - raspberrypi
  - pubnub
  - javascript
  - node.js  
  - cats
---

![RPi KittyCam](https://lh3.googleusercontent.com/UuKlrNQWs5wFciRqI8qiZKTVoh4XrTBa40LD5mUa5MIn=w1346-h757-no "Rapsberry Pi KittyCam")

Ho, ho, ho! This is an overdue blog post for [the project](https://github.com/girliemac/RPi-KittyCam) I've worked on during summer!

Last August, I created this Raspberry Pi app using a camera and PIR motion sensor, written in Node.js with helps with **Johnny-Five** and **KittyDar**. As I promised on the README file of the GitHub repo, I am finally writing the detailed instruction of how I built hardware and wrote the app.

![KittyCam on YouTube](/assets/images/articles/2015/12/youtube-kittycam-thumb.jpg "YouTube")
[Watch the demo on YouTube :-)](https://www.youtube.com/watch?v=wqewhjhjaHY)


## How KittyCam Works

The software is written in Node.js, simply because JavaScript is the language I am most comfortable with, also it is fun!

This is the basic flow:

1. Detect motion (Use Johnny-Five IR.Motion obj)
2. Take photos (Raspistill, command line tool)
3. Cat facial detection (KittyDar)
4. Store the photos in cloud storage (Cloudinary)
5. Publish the data (URL) to PubNub for realtime streaming
6. Stream on web (subscribe the data from PubNub)

![KittyCam flow](/assets/images/articles/2015/12/kittyCam-app.png "KittyCam flow")

The hardware-software communication is done with [Johnny-Five](http://johnny-five.io/), open-source JavaScript robotics programming framework. I am using it to talk with a PIR sensor. When the sensor detect my cat (or any moving objects) nearby Raspberry Pi, it triggers the camera.

Photos are taken using `raspistill` command line. One cool thing about Node.js is that you can execute commands by spawning child processes.

Once a photo is taken, I am using another child process to detect if any cats are on the photo, using [KittyDar](https://github.com/harthur/kittydar), an open source face detection for cats, written by Heather Arthur.

Additionally, I am sending the photos (only photos with cats) to a cloud storage, and at the same time, I stream the photo to web browser using [PubNub](http://pubnub.com), because I work for the company!

Now, let's build your own!


## Building the Circuit with Raspberry Pi 2

### What you need

First, you need to get some hardware along with Raspberry Pi 2. I don't recommend any older Raspberry Pi, as their memory is too low to run some code.

The Pi needs to be pre-installed with **Raspbian OS**. And if you are starting from a scratch, with Raspberry Pi fresh out of box, you can take a look at [**Setting up Raspberry Pi** section of the instruction I wrote for my workshop](https://github.com/pubnub/workshop-raspberrypi) I give at conferences sometimes.

But if you are a newbie, I recommend to buy your first Pi from [CanaKit](http://www.amazon.com/gp/product/B008XVAVAW/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B008XVAVAW&linkCode=as2&tag=girliemac-20&linkId=DU2AO5J5GTPAQMPO), so you don't need to set it up all by yourself.


![What you need and how to assemble](/assets/images/articles/2015/12/what-you-need-raspberry-pi.jpg "The stuff you need and how to assemble")


1. Raspberry Pi 2 (with WiFi adapter) ([buy](http://amzn.to/1rk3VZY))
2. 5MP Camera Board Module ([buy](http://amzn.to/1UKaEXl))
3. Pyroelectric Infrared (PIR) motion sensor ([buy](http://amzn.to/1ZJ3Nir))
4. 3 Female/Female wires ([buy](http://amzn.to/1U8ajAZ))
5. Optional: LEGO compatible SmartiPi w/ camera case ([buy](http://amzn.to/28vkhAR))


### Assembling Hardware

This doesn't require much of wiring. You can connect a camera and a PIR sensor directory to a Pi without any breadboards or soldering, as you see in the photo above at the previous section, or this Fritzing diagram below.

![RPi KittyCam](/assets/images/articles/2015/12/pi-pir-camera_bb.png "Assemble PIR and camera")


#### Camera to Pi
- Connect the camera module to the CSI port. See [the video instruction of how to set up th camera module on RaspberryPi.org](https://www.raspberrypi.org/help/camera-module-setup/).

#### PIR Sensor to Pi
- 1 red wire: PIR-VCC to Pi's **5V** pin
- 1 black wire: PIR-GND to Pi's ground (**GND** pin)
- 1 whatever color wire (brown in the photo): PIR-OUT to Pi's Pin **7** (GPIO 4)



The photo below is my Pi enclosed in SmartiPi case:
![RPi KittyCam](https://lh3.googleusercontent.com/o-XG7ZijXM_UXQHuYrDxC6mlTofyUzUCmHqNmr6oRYZk=w1346-h757-no "Rapsberry Pi KittyCam")


## Working Remotely from Mac

You can plug in a monitor, keyboard, mouse, etc to your Pi and work directly on Raspbian GUI, or work from you Mac, like I usually do. This is how I work remotely on Mac:

### SSH-ing into Raspberry Pi

First, make sure your Pi and computer are on the same WiFi network.

If you are directly connecting your Pi to a monitor and a keyboard, open a terminal, and find the IP address:

```bash
pi@raspberrypi ~$ hostname -I
```

Or use some IP scanner app on Mac, like [Angry IP Scanner](http://angryip.org/download/#mac) to scan all connected devices.

Once you find the IP address, open a terminal app on Mac, and ssh into the address. I am using the default username for Pi, "pi".

```bash
tomomi@Mac ~$ ssh pi@10.0.1.13
```

Then type the password. Default is "raspberry".

Once connected to your Pi, you can create files, code, and execute from the terminal. Raspbian is a Debian based, so you can use usual linux commands.

### Coding on Your Fave IDE on Mac

I usually use **Sublime Text** to code, so I prefer doing so for coding on Pi as well.
Here's what I do:

First, download and install [Cyberduck](https://cyberduck.io) on Mac.

Then connect your Pi via SSH, using its IP address (See the screenshot below)
![Cyberduck to RPi](/assets/images/articles/2015/12/cyberduck-connect-rpi.png "Connect Rapsberry Pi via Cyberduck")

When you edit a file, open the file with "Edit".
![Cyberduck to RPi](/assets/images/articles/2015/12/cyberduck-connect-rpi-edit.png "Connect Rapsberry Pi via Cyberduck")

In my case, it automatically select Sublime to edit JavaScript files.



## Software Setup

### 1. Install node.js in your Raspberry Pi

Make sure your Pi is up-to-date!

```bash
$ sudo apt-get update
```

then

```bash
$ sudo apt-get upgrade
```

#### Download and Install

Let's download node from [node-arm](http://node-arm.herokuapp.com/), which is probably the easiest way:

```bash
$ wget http://node-arm.herokuapp.com/node_archive_armhf.deb
```

and install the package:

```bash
$ sudo dpkg -i node_archive_armhf.deb
```

Check if node is successfully installed.

```bash
$ node -v
```
As of Dec. 2015, the archive should install Node v0.12.6. This is the version I used and works fine for sure.


### 2. Enable Camera Access

To be able to use a hardware camera module with your Pi, you need to enable the software first.

Go to **Pi Software Config Tool** menu from a terminal:

```bash
$ sudo raspi-config
```

You should see the menu like this. Use arrow keys to select **Enable Camera**.

![Pi Software Config Tool](/assets/images/articles/2015/12/config-enable-pi-camera.png "Pi Software Config Tool")

Hit Return, then at the next screen, select **Enable**.

Test if your camera is working by try typing this command on terminal:

```bash
$ raspistill -o photo.jpg
```



## Installing Dependencies

If you wish to run the code from my GitHub repo, clone [RPi-KittyCam repo on GitHub](https://github.com/girliemac/RPi-KittyCam), and copy them over on Raspberry Pi.

It would be really nice if `$ npm install` successfully install all the dependencies, and voilà, but it does **not** work in that way, unfortunately. You still need to set up and install dependencies manually.


### 1. Prerequisite: Install Cairo to the System

for cat facial detection, I am using **kittydar**, which dependencies including **node-canvas**, which requires **Cairo**.

So let's get Cairo on your Raspbian first.

```bash
$ sudo apt-get install libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev build-essential g++
```

See more info on how to install Cairo for Node [Canvas](https://github.com/Automattic/node-canvas), see this [*Installation Ubuntu and other Debian based systems*](https://github.com/Automattic/node-canvas/wiki/Installation---Ubuntu-and-other-Debian-based-systems)

If you download the `node_modules` contents of my GitHub repo, skip the step 2, and proceed to step 3.
Otherwise, go to the next step to manually fresh-install the next several modules. Just running `npm install` to fetch all dependencies may fail because there is some incompatibilities. (I explain it later).

### 2. Install Dependency Modules

Now, `cd` to your working directry, and install dependencies.

#### Install Canvas

You need canvas (**node-canvas**) to be able to analyze images with KittyDar.

```bash
$ sudo npm install canvas
```

#### Install KittyDar

**Kittydar** is an open-source cat face detection. It takes an image (canvas) and tells you the if cats are in the image.

![Jamie detected](http://res.cloudinary.com/girliemac/image/upload/v1440530252/jrfqcdul46c84qlqlks9.png "Jamie detected by KittyDar")

*This is an actual photo taken by my Raspberry Pi, while Jamie was eating, and detected by KittyDar cat facial detection!*

Once your environment is set up, in this RPi-KittyCam dir, install node dependency modules.

Ideally install from `npm install kittydar —save`

However, node-canvas 1.0.1 (the version specified in package.json for KittyDar) failed to build with the current Node.js (v0.12.6).

So what I did was download the zip from github repo into *node_modules*, alter the `package.json`, where canvas: ~1.0.1 to ^1.0.1 so that the latest canvas is installed as I `npm install` from the kittydar directory.

Get the zip from [my forked repo](https://github.com/girliemac/kittydar).

*Note: Although, the repo is no longer maintained by the author, I am sending [a pull request](https://github.com/harthur/kittydar/pull/27]) for the fix.*

#### Install Johnny-Five

**Johnny-Five** is a JavaScript Robotics programming framework. It makes communicating with hardware so much easier.

```bash
$ npm install johnny-five
```

#### Install Raspi-io

**Raspi-io** is a library to be used as an I/O plugin with Johnny-Five. You need to install this to use Johnny-Five on Raspbian.

```bash
$ npm install raspi-io
```

### 3. Install 3rd Party Service Modules

This step is optional, if you don't want to create a web interface to stream the photos, or you would rather create your own web server without depending on the 3rd party services.

#### Install PubNub

For realtime live-updating the web interface, I am using PubNub.
To use the service, you need to [sign up](http://pubnub.com) to obtain your API keys.

```bash
$ npm install pubnub
```


#### Install Cloudinary

For storing photos, use Cloudinary.
To use the service, you need to [sign up](http://cloudinary.com/) to obtain your API keys.


```bash
$ npm install cloudinary
```


#### Set up your config.js with Credentials

Create a `config.js` in the root dir of the app.
The file should include your API keys:

```javascript
module.exports = {

  cloudinary: {
    cloud_name: 'your_name',
    api_key: 'your_API_key',
    api_secret: 'your_API_secret',
  },

  pubnub: {
    subscribe_key: 'your_sub_key',
    publish_key: 'your_pub_key'
  }

};
```

### 4. Run the Code

Once you have configured everything and have all source files from my GitHub repo, try running kittyCam.js.

You must run with sudo:

```bash
$ sudo node kittyCam.js
```

The camera will take a photo when a motion is detected by the PIR sensor.
Then the `child_process` runs to detect if there is any cats in the photo.
When there are any cat, it sends the photo to Cloudinary.

Analyzed photos are deleted from the filesystem to clear up Pi.

### 5. View the Live Photo Update on Web

- Get the web interface source code from `gh-pages` branch.
- Run the `index.html` on browser


![Jamie detected](https://raw.githubusercontent.com/girliemac/RPi-KittyCam/gh-pages/images/screenshot.png "KittyCam Web")

## Walking Through the Code

Although I am not writing a full tutorial how to write this Node app from scratch, I can explain some of the key features.

### Detecting Motion from a PIR Sensor

I am using Johnny-Five's `IR.Motion` object to detect the motion.

First, include the dependencies.

Then, create a new `motion` hardware instance at pin 7, and when a motion is detected, take a photo:

```javascript
var raspi = require('raspi-io');
var five = require('johnny-five');
var board = new five.Board({io: new raspi()});

board.on('ready', function() {

  var motion = new five.Motion('P1-7');

  motion.on('motionstart', function() {
    // Run raspistill command to take a photo with the camera module  
	// then detect cats from the photo
  })
});
```

### Execute Command with Child Process

In the code snippet above, where the first comment is, run `raspistill` command using `child_process.spawn()` to take a photo with the camera module:

```javascript
var filename = 'photo/image_'+i+'.jpg';
var args = ['-w', '320', '-h', '240', '-o', filename, '-t', '1'];
var spawn = child_process.spawn('raspistill', args);

spawn.on('exit', function(code) {
  console.log('A photo is saved as '+filename+ ' with exit code, ' + code);
  i++;

  // Detect cats from photos - see the next section
  ...
```

Here, I am saving photos in sequential orders.

### Detect Cat with KittyDar

To be able to keep taking photos without interruptions, as each photo is being processed, I am using another `child_process`, this time with `fork()`, an instance of spawn thats runs a new instance of the V8 engine to create multiple wrokers.

After the comment in the code snippet above, read another JS file:

```javascript
var imgPath = __dirname + '/' + filename;

var args = [imgPath];
var fork = child_process.fork(__dirname + '/detectCatsFromPhoto.js');
fork.send(args);

// the child process is completed
fork.on('message', function(base64) {
  if(base64) {
    // send the image to the cloud storage
  }
  deletePhoto(imgPath);
});
```

In **detectCatsFromPhoto.js**, start the child process and use canvas and kittydar to detect cats. Once the process is done, the image is returned in Base64:

```javascript
var fs = require('fs');
var kittydar = require('kittydar');
var Canvas = require('kittydar/node_modules/canvas');

process.on('message', function(m) {
  var imgPath = m[0];

  fs.readFile(imgPath, function(err, data) {
    var img = new Canvas.Image;
    img.src = data;

    //... snip snip, some canvas setup code here...

    var cats = kittydar.detectCats(canvas);
    var base64Img;

    if(cats.length > 0) {
      base64Img = canvas.toDataURL();
    }
    process.send(base64Img);
    process.exit(0);
  });
}
```

To see the entire source code, please take a look at [my GitHub repo](https://github.com/girliemac/RPi-KittyCam)!

Also to see how I used PubNub to stream the live photos on web browser, look at the source code on the [gh-pages branch](https://github.com/girliemac/RPi-KittyCam/tree/gh-pages).


## Known Issues

### Raspistill (Camera Software)

- Raspistill continuously takes a bunch of photos when I set `t = 0` (and crashes Pi while so many child process is running) so I have set `t = 1`, which causes delay. It seems to take only integer. Cats are too fast to wait for a second.
- The camera can't capture recognizable pics after the sun is set. The room light is too dark.

### KittyDar (Cat Facial Recognition)

- During his meal time, when Jamie (my cat) is eating food in his head-down position, the facial detection fails to recognize the cat face shape.
- When my cat moves, eats from the side of the dish, or put his butt on the camera, it fails to tell me my cat was eating.

#### The cat photos failed to be recognized

![Jamie undetected](https://raw.githubusercontent.com/girliemac/RPi-KittyCam/master/photo/image_14.jpg "Jamie undetected")
![Jamie undetected](https://raw.githubusercontent.com/girliemac/RPi-KittyCam/master/photo/image_150.jpg "Jamie undetected")
![Jamie undetected](https://raw.githubusercontent.com/girliemac/RPi-KittyCam/master/photo/image_166.jpg "Jamie undetected")
![Upside-down Jamie undetected](https://raw.githubusercontent.com/girliemac/RPi-KittyCam/master/photo/image_311.jpg "Jamie undetected")

## OMG, I demo'd KittyCam on Live TV Show!

See my [last blog post](http://www.girliemac.com/blog/2015/09/14/the-screen-savers-show/) about my experience being on Twit TV! You can watch the segment on the [recorded show](https://twit.tv/shows/new-screen-savers/episodes/19?autostart=false) too.


OK, I hope you enjoyed my lengthy blog post!


## References
- [Raspberry Pi](https://www.raspberrypi.org/): Teach, Learn, and Make with Raspberry Pi
- [Node ARM](https://github.com/nathanjohnson320/node_arm): Install node.js on a raspberry pi in two easy steps
- [Johnny-Five](http://johnny-five.io/): The original JavaScript Robotics programming framework
- [Raspi-IO](https://github.com/nebrius/raspi-io): An IO plugin for Johnny-Five that provides support for the Raspberry Pi
- [KittyDar](https://github.com/harthur/kittydar): Face detection for cats in JavaScript
- [Node Canvas](https://github.com/Automattic/node-canvas): A Cairo backed Canvas implementation for NodeJS
- [PubNub](https://www.pubnub.com/): The global realtime Data Stream Network for IoT, mobile, and web applications
