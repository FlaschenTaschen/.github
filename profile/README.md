<h1 align="center">🍾 FlaschenTaschen</h1>

<p align="center"><em>A wall of light made from milk crates and bottles.</em></p>

<p align="center">
  <img src="https://img.shields.io/badge/display-45×35%20(1,575%20px)-brightgreen" alt="Display size" />
  <img src="https://img.shields.io/badge/protocol-UDP%20:1337-blue" alt="Protocol" />
  <img src="https://img.shields.io/badge/origin-Noisebridge%20SF%202016-orange" alt="Origin" />
  <img src="https://img.shields.io/badge/Maker%20Faire%202016-Editor's%20Choice-yellow" alt="Award" />
</p>

---

**FlaschenTaschen** ("bottle bags") is a networked LED art installation born at
[Noisebridge](https://noisebridge.net/wiki/Flaschen_Taschen) in San Francisco in 2016. It is built
from a 9×7 grid of milk crates filled with aluminum-wrapped bottles — **45×35 pixels, 1,575 LEDs in
all** — and it won the **Editor's Choice Award at Maker Faire 2016**.

Any program can paint the wall by sending it pixels: a tiny image (PPM/P6) wrapped in a UDP packet on
port **1337**, with optional metadata for placement and multi-layer compositing. That simple protocol
is what ties this organization's projects together — one display, many ways to drive it.

This org gathers a family of clients, libraries, demos, and utilities built around that protocol,
descended from the original [hzeller/flaschen-taschen](https://github.com/hzeller/flaschen-taschen)
server and Carl Gorringe's [cgorringe/ft-demos](https://github.com/cgorringe/ft-demos) collection.

## Projects

| Project | Language | What it is |
| --- | --- | --- |
| **[ft-cpp](https://github.com/FlaschenTaschen/ft-cpp)** | C++ | The unified C++ codebase — server (terminal / RGB-matrix / spixels backends), the `libftclient` library, content clients (send-text/image/video), and demos, all under one make-based build. The reference implementation. |
| **[ft-py](https://github.com/FlaschenTaschen/ft-py)** | Python | `flaschen-taschen-py` — a pip-installable client with a drawing canvas, text/image/video generators, CLI tools, and 9+ interactive demos (Game of Life, plasma, fractals, Matrix rain…). |
| **[ft-swift](https://github.com/FlaschenTaschen/ft-swift)** | Swift | A Swift package: the `FlaschenTaschenClientKit` library, content clients, 15+ generative demos ported from ft-demos, a debugger, and a native macOS display server. |
| **[ft-scripts](https://github.com/FlaschenTaschen/ft-scripts)** | Python | Real-world displays for a wall in the wild — now-playing track info from Volumio and live SF MUNI transit arrivals, ready to run on a Raspberry Pi via cron or systemd. |

## How it works

```
P6
45 35
255
#FT: <x> <y> <z>          ← optional placement + layer
[ binary RGB pixel data ] ← one UDP packet → the wall
```

Pick the language you like, point a client at the display's host on port 1337, and start drawing.

## Getting started

The quickest taste is the Python client:

```bash
pip install flaschen-taschen-py
send-text -g 45x35 -h display.local "Hello, wall"
```

Or build the C++ reference server and run a demo locally:

```bash
git clone https://github.com/FlaschenTaschen/ft-cpp && cd ft-cpp
make server          # terminal backend by default
make client          # client tools + games
```

Each repository has its own README with full install, build, and usage details.

## Get involved

- **Build something** — any language that can send a UDP packet can drive the wall. Pick a client library above and start drawing.
- **Add a demo** — the Python and Swift repos make it easy to drop in a new animation; open a PR.
- **Learn the backstory** — see the [Flaschen Taschen wiki](https://noisebridge.net/wiki/Flaschen_Taschen) and the [protocol docs](https://github.com/hzeller/flaschen-taschen/blob/master/doc/protocols.md).
- **Ask questions** — open an issue on the relevant repository.

## License

`ft-cpp` is **GPLv3** (following the upstream server). `ft-py`, `ft-swift`, and `ft-scripts` are **MIT**.
See each repository's `LICENSE` for details.

## Credits

Built on the original FlaschenTaschen by the **Noisebridge** community (San Francisco, 2016) —
[hzeller/flaschen-taschen](https://github.com/hzeller/flaschen-taschen), with demos from
[cgorringe/ft-demos](https://github.com/cgorringe/ft-demos).
