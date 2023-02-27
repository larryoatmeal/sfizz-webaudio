## sfizz WebAudio/WebMidi demo

Live demo (requires Chrome or one of its derivatives): https://sfz.tools/sfizz-webaudio/

This repository contains a HTML/Javascript/WebAssembly front-end for [sfizz](https://sfz.tools/sfizz), which allows prototyping of virtual instruments in the SFZ format.
Right now only generators and embedded sample files are supported. This uses the `emscripten` branch off my sfizz's fork, available [here](https://github.com/paulfd/sfizz/tree/emscripten).
Compared the main sfizz branch, the background loader is deactivated and all files are loaded in memory (since WebAssembly through browsers only allows access to a virtual file system).

### Building

Fetch submodules
```
git submodule update --init --recursive
```

This assumes you have the [emsdk](https://github.com/emscripten-core/emsdk) installed and activated.
```sh
mkdir build
cd build
emcmake cmake -DCMAKE_BUILD_TYPE=Release ..
make -j
echo "export default Module;" >> sfizz.wasm.js
```

From the `build` directory, you may then host the result on `localhost:8000` using python as
```sh
python3 -m http.server --directory ..
```

### Usage
Samples can only be embedded directly in SFZ as such:
```
<region> sample=kick_embedded.wav
<sample> name=kick_embedded.wav
    base64data=yA8QD1gPtAwgEFQQzBD4EZw....
```

Should build a helper script for doing this
