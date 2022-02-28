# dmx-flok

This is a clone of [dmx-web](https://github.com/node-dmx/dmx-web) edited for live-coding on [flok](https://github.com/munshkr/flok).

## setup

On the computer that has DMX:

    git clone https://github.com/micuat/dmx-flok.git # Clone the repository
	  cd dmx-flok
	  npm install
	  node dmx-web.js -c dmx-web.json

`public.js` has to be hosted online. For example, you can use https://light-academy.glitch.me/script.js

open a flok session on https://flok.clic.cf/. The session must be opened on the computer that has the DMX interface plugged in.

load the script

    loadScript("https://light-academy.glitch.me/script.js")
    lights(1,1,1,1)
    light0([0,1],()=>Math.sin(time*3),1)

## API

`lights(r,g,b,a)` overwrites all light colors

`light0(r,g,b,a)` sets light colors on the 0th light

currently index is hardcoded (5 lights) and only RGB lights are supported. They have to be configured on `dmx-web.json` and `dmx-web.js` according to your setup.

---

# original document: node-dmx

Webinterface and HTTP API using [node-dmx](https://github.com/node-dmx/dmx)

## Install

`npm install -g dmx-web`

## Webinterface

### Configuration

The Daemon `dmx-web` looks for a configuration file in `/etc/dmx-web.json`. An alternate location can be passed as a command line argument.

This configuration file consists of three sections:

- Server
- Universes
- Presets

In the Server section you can set the listen port and host.
Under Universes you describe the DMX Universes with details like which output driver to use and which devices are at which address.
The presets section allows you to specify a state some channels should be set when the preset is called.

A example configuration is in the repository by the name `dmx-web-example.conf`

### Run

`dmx-web [-c <full-path to config file>]`

### Run as a service

On MacOS you can run dmx-web as a service by adding a launch script to `/Library/LaunchDaemons`. See the example file.

### Animation HTTP API

A List of Channel Transistions can be POSTed to `/animation/<universe>`. Each transistion is a JSON Object with at least the `to` property present. The Value of which also has to be an Object describing the channel end-states.

A duration for this transistion can be given in the `duration` property.
If not specified 0ms is assumed.

Example:

	[
		{"to": {"10": 0, "20": 0}},
		{"to": {"10": 255}, "duration": 2000},
		{"to": {"20": 255}, "duration": 1000}
	]

This sets channels 10 and 20 to zero. Then transistions channel 10 to 255 in 2 seconds. After that channel 20 is faded to 255 in 1 second.


## Community

We're happy to help. Chat with us on IRC in #dmx on libera.chat.
