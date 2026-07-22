# Flaschen Taschen


The [Flaschen Taschen](https://www.noisebridge.net/wiki/Flaschen_Taschen) is a networked video display made out of 1,575 beer bottles, each containing an RGB LED, in a 9x7 grid of milk crates. It was built by [Noisebridge](https://www.noisebridge.net/wiki) for Maker Faire 2016, where it won the Editor's Choice Award.

## Protocol

The FT protocol is PPM-over-UDP to port 1337, with an optional annotation for image placement. For a description of PPM, see [here](https://netpbm.sourceforge.net/doc/ppm.html). The maxval must be 255.

The placement annotation is written as a comment in the PPM header starting with `#FT: `, then three ASCII decimal numbers for x, y, and z positions. The x and y positions count right and down from the top-left corner, and the z position indicates a layer (a number from 0 to 15). Higher layers are drawn above lower layers. The RGB value #000000 on layers above 0 is interpreted as transparent, and shows the contents of a lower layer. This can be useful for compositing. For opaque black, send #010101.

For example, the following message places a 6x6 image at x=5, y=0, z=15.
```
P6
6 6
#FT: 5 0 15
255
[36 3-byte RGB colors]
```

Since each milk crate is 5x5 pixels, the image will cover the second milk crate in the first row, and extend one pixel right and down. 

For more details, see the [original protocol documentation](https://github.com/hzeller/flaschen-taschen/blob/master/doc/protocols.md).

## This organization

This org contains clients, servers, libraries, demos, and utilities built around the FT protocol in various languages.

| Repo | Language | Notes |
| --- | --- | --- |
| [ft-cpp](https://github.com/FlaschenTaschen/ft-cpp) | C++ | Modernization of the [original codebase](https://github.com/hzeller/flaschen-taschen). |
| [ft-py](https://github.com/FlaschenTaschen/ft-py) | Python | Port of client library and demos. |
| [ft-swift](https://github.com/FlaschenTaschen/ft-swift) | Swift | Port of client library and demos. |
| [ft-darwin](https://github.com/FlaschenTaschen/ft-darwin) | Swift | Apple-native Flaschen Taschen display server. |
| [ft-scripts](https://github.com/FlaschenTaschen/ft-scripts) | Python | Client programs which display currently playing music and MUNI bus arrivals. |
| [ft-esp32](https://github.com/FlaschenTaschen/ft-esp32) | C++ | Standalone ESP32+WS2812B display server. |

## Get involved

Pick your favorite language and follow the README to get started. If you're at Noisebridge, the Flaschen Taschen is reachable at `ft.local`. If not, you can run a local display server in your terminal:

```bash
git clone https://github.com/FlaschenTaschen/ft-cpp
cd ft-cpp
make server
./build/server/ft-server
```

New demos, projects, client libraries, and questions are always welcome. You can open a github issue or pull request, or visit [#flaschen-taschen](https://discord.com/channels/720514857094348840/958465813478772757) in the Noisebridge discord.

## Credits

The Flaschen Taschen is the work of the Noisebridge community in 2016 and beyond. The projects in this org are descended from hzeller's [original flaschen-taschen repo](https://github.com/hzeller/flaschen-taschen) and Carl Gorringe's [ft-demos](https://github.com/cgorringe/ft-demos).

<p align="center">
  <img src="https://raw.githubusercontent.com/FlaschenTaschen/.github/main/profile/1000px-Flaschentable.jpg" alt="The FlaschenTaschen LED wall glowing in rainbow colors above a workbench at Noisebridge" width="460" />
  <br />
  <sub>The Flaschen Taschen in Noisebridge · <a href="https://www.noisebridge.net/wiki/File:Flaschentable.jpg">Photo source</a></sub>
</p>
