---
layout: default
title: YoWASP
---

<style type="text/css">
blockquote {
  position: relative;
  padding: 0.35em 0px 0.35em 40px;
  line-height: 1.45;
  font-family: Georgia, serif;
  font-size: 18px;
  font-style: italic;
  color: #444;
  border: none;
}

blockquote:before {
  display: block;
  position: absolute;
  left: -20px;
  top: -20px;
  padding-left: 10px;
  content: "\201C";
  font-size: 80px;
  color: #888;
}

blockquote cite {
  display: block;
  margin-top: 5px;
  font-size: 14px;
}

blockquote cite:before {
  content: "\2014 \2009";
}

img.badge {
  padding: 0;
  margin: 0;
  border: none;
  top: 4px;
}

img.fossi-logo {
  padding: 0;
  margin: 0;
  border: none;
  top: 9px;
  margin-right: 10px;
  box-shadow: none;
}
</style>
<blockquote>
This is the most galaxy brained solution to windows package distribution I've seen yet, I'm impressed and horrified
<cite><a href="https://twitter.com/Amyayash">@Amyayash</a><!-- https://twitter.com/Amyayash/status/1320142568433340417 --></cite>
</blockquote>

## What is YoWASP?

YoWASP (**Yo**sys **W**eb**A**ssembly **S**ynthesis & **P**nR) is a project that aims to distribute up-to-date [FOSS FPGA tools][yosyshq] compiled to [WebAssembly][] via language package managers like [Python][]'s [PyPI][] and [JavaScript][]'s [NPM][].

[yosyshq]: https://github.com/YosysHQ/
[webassembly]: https://webassembly.org/
[python]: https://python.org/
[pypi]: https://pypi.org/
[javascript]: https://developer.mozilla.org/en-US/docs/Web/javascript
[npm]: https://npmjs.org/

### Why use WebAssembly?

A batch compiler, such as an FPGA toolchain, transforms input files to output files without using any OS services beyond basic bookkeeping. Is it really necessary to build something so fundamentally simple for a large matrix of *every OS* × *every CPU*? With [WebAssembly][] and [WASI][], it is now possible to build a single [universal binary][universal] that runs on many OSes and CPUs.

[wasi]: https://wasi.dev/
[universal]: https://kripken.github.io/talks/2020/universal.html

### Do I need a browser?

Despite the name, [WebAssembly][] is not tied to browsers; it is a kind of machine code that can be easily translated into x86, ARM, or other machine code that your CPU runs directly. The tools provided by the YoWASP project can run directly on top of an operating system as well as within a browser environment. The project also provides an [extension][vscode-ext] for Visual Studio Code, an editor built on top of browser technology.

[vscode-ext]: https://marketplace.visualstudio.com/items?itemName=yowasp.toolchain

### Why use language package managers?

Many new hardware definition languages are *[embedded][edsl]* in another *host* language, which comes with its own package manager and repository. For example, [Amaranth HDL][] is embedded in [Python][], which uses [pip][] and [PyPI][]. There are several benefits in distributing FPGA tools via language package managers:
  * Designers working in such HDLs are already familiar with the package manager of the host language, making it is a convenient distribution mechanism;
  * Synthesis and PnR tools can be added as ordinary dependencies to the project, and their versions can be frozen for reproducibility;
  * "Turnkey" toolchain installation enables new applications that generate FPGA bitstreams just-in-time, or use synthesis tools to transform netlists.

[edsl]: https://en.wikipedia.org/wiki/eDSL
[amaranth hdl]: https://github.com/amaranth-lang/amaranth
[pip]: https://pip.pypa.io/

## Which tools are provided?

This project provides packages for:

  * Yosys:
    * [upstream repository][yosys];
    * [package repository][yosys-pkg];
    * PyPI packages: [<img src="https://img.shields.io/pypi/v/yowasp-yosys?label=yowasp-yosys&color=green" alt="yowasp-yosys" class="badge">](https://pypi.org/project/yowasp-yosys/).
    * NPM packages: [<img src="https://img.shields.io/npm/v/@yowasp/yosys?label=@yowasp/yosys&color=green" alt="@yowasp/yosys" class="badge">](https://npmjs.com/package/@yowasp/yosys).
  * nextpnr:
    * [nextpnr upstream repository][nextpnr];
    * [Project IceStorm upstream repository][icestorm];
    * [Project Trellis upstream repository][trellis];
    * [Project Oxide upstream repository][oxide];
    * [Project Apicula upstream repository][apicula];
    * [package repository][nextpnr-pkg];
    * PyPI packages: [<img src="https://img.shields.io/pypi/v/yowasp-nextpnr-ice40?label=yowasp-nextpnr-ice40&color=green" alt="yowasp-nextpnr-ice40" class="badge">](https://pypi.org/project/yowasp-nextpnr-ice40/), [<img src="https://img.shields.io/pypi/v/yowasp-nextpnr-ecp5?label=yowasp-nextpnr-ecp5&color=green" alt="yowasp-nextpnr-ecp5" class="badge">](https://pypi.org/project/yowasp-nextpnr-ecp5/), [<img src="https://img.shields.io/pypi/v/yowasp-nextpnr-machxo2?label=yowasp-nextpnr-machxo2&color=green" alt="yowasp-nextpnr-machxo2" class="badge">](https://pypi.org/project/yowasp-nextpnr-machxo2/), [<img src="https://img.shields.io/pypi/v/yowasp-nextpnr-nexus?label=yowasp-nextpnr-nexus&color=green" alt="yowasp-nextpnr-nexus" class="badge">](https://pypi.org/project/yowasp-nextpnr-nexus/), [<img src="https://img.shields.io/pypi/v/yowasp-nextpnr-gowin?label=yowasp-nextpnr-gowin&color=green" alt="yowasp-nextpnr-gowin" class="badge">](https://pypi.org/project/yowasp-nextpnr-gowin/).
    * NPM packages: [<img src="https://img.shields.io/npm/v/@yowasp/nextpnr-ice40?label=@yowasp/nextpnr-ice40&color=green" alt="@yowasp/nextpnr-ice40" class="badge">](https://npmjs.com/package/@yowasp/nextpnr-ice40), [<img src="https://img.shields.io/npm/v/@yowasp/nextpnr-ecp5?label=@yowasp/nextpnr-ecp5&color=green" alt="@yowasp/nextpnr-ecp5" class="badge">](https://npmjs.com/package/@yowasp/nextpnr-ecp5), [<img src="https://img.shields.io/npm/v/@yowasp/nextpnr-machxo2?label=@yowasp/nextpnr-machxo2&color=green" alt="@yowasp/nextpnr-machxo2" class="badge">](https://npmjs.com/package/@yowasp/nextpnr-machxo2), [<img src="https://img.shields.io/npm/v/@yowasp/nextpnr-nexus?label=@yowasp/nextpnr-nexus&color=green" alt="@yowasp/nextpnr-nexus" class="badge">](https://npmjs.com/package/@yowasp/nextpnr-nexus).
  * boolector:
    * [upstream repository][boolector];
    * [package repository][boolector-pkg];
    * PyPI packages: [<img src="https://img.shields.io/pypi/v/yowasp-boolector?label=yowasp-boolector&color=green" alt="yowasp-boolector" class="badge">](https://pypi.org/project/yowasp-boolector/).
  * openFPGALoader:
    * [upstream repository][openFPGALoader];
    * [package repository][openFPGALoader-pkg];
    * NPM packages: [<img src="https://img.shields.io/npm/v/@yowasp/openfpgaloader?label=@yowasp/openfpgaloader&color=green" alt="@yowasp/openfpgaloader" class="badge">](https://npmjs.com/package/@yowasp/openfpgaloader).

[yosys]: https://yosyshq.net/yosys/
[nextpnr]: https://github.com/YosysHQ/nextpnr/
[icestorm]: https://github.com/YosysHQ/icestorm/
[trellis]: https://github.com/YosysHQ/prjtrellis/
[oxide]: https://github.com/gatecat/prjoxide
[apicula]: https://github.com/YosysHQ/apicula
[boolector]: https://boolector.github.io/
[openFPGALoader]: https://github.com/trabucayre/openFPGALoader

[yosys-pkg]: https://github.com/YoWASP/yosys
[nextpnr-pkg]: https://github.com/YoWASP/nextpnr
[boolector-pkg]: https://github.com/YoWASP/boolector
[openFPGALoader-pkg]: https://github.com/YoWASP/openFPGALoader-web

## Which platforms are supported?

### Python embedding

YoWASP Python relies on a [WebAssembly][] engine to run the Wasm code, and inherits both its advantages and its limitations.

At the moment, YoWASP Python uses the [Wasmtime][] engine, which supports the following platforms:

  * Linux (x86_64 and AArch64),
  * macOS (x86_64 and AArch64),
  * Windows (x86_64).

[wasmtime]: http://wasmtime.dev/

### Browser/Node.js embedding

YoWASP JavaScript relies on the [WebAssembly][] engine in [the browser](https://caniuse.com/wasm) or [Node.js](https://nodejs.org/) to run the Wasm code. Any version of a major browser or Node.js released within the last several years offers full support for WebAssembly.

## Are there other packages?

YoWASP isn't the only project that packages the open-source FPGA toolchain, and it has some limitations. One of the following projects may suit your workflow better:

  * [YosysHQ OSS CAD suite][hqtools] is a native build that includes GHDL and programming tools (`iceprog`, `ecpprog`, `dfu-util`, etc).

[hqtools]: https://github.com/YosysHQ/oss-cad-suite-build

## How do I use the tools...

### ... with Python?

To use Yosys, install the `yowasp-yosys` package using [pip][] or add it as a dependency. It provides the `yowasp-yosys`, `yowasp-sby`, and `yowasp-yosys-smtbmc` executables.

To use Boolector, install the `yowasp-boolector` package using [pip][] or add it as a dependency. It provides the `yowasp-boolector` executable.

To use nextpnr-ice40, install the `yowasp-nextpnr-ice40` package using [pip][] or add it as a dependency. This package contains support for every device, and provides the `yowasp-nextpnr-ice40`, `yowasp-icepack`, `yowasp-iceunpack`, `yowasp-icebram`, `yowasp-icemulti`, and `yowasp-icepll` executables.

To use nextpnr-ecp5, install the `yowasp-nextpnr-ecp5` package using [pip][] or add it as a dependency. This package contains support for every device, and provides the `yowasp-nextpnr-ecp5`, `yowasp-ecppack`, `yowasp-ecpunpack`, `yowasp-ecpbram`, `yowasp-ecpmulti`, and `yowasp-ecppll` executables.

To use nextpnr-machxo2, install the `yowasp-nextpnr-machxo2` package using [pip][] or add it as a dependency. This package contains support for every device, and provides the `yowasp-nextpnr-machxo2`, `yowasp-xo2pack`, `yowasp-xo2unpack`, `yowasp-xo2bram`, `yowasp-xo2multi`, and `yowasp-xo2pll` executables. The `yowasp-xo2*` executables are bit-for-bit identical to the `yowasp-ecp*` executables above, but are renamed to avoid a conflict during installation.

To use nextpnr-nexus, install the `yowasp-nextpnr-nexus` package using [pip] or add it as a dependency. This package contains support for every device, and provides the `yowasp-nextpnr-nexus` and `yowasp-prjoxide` executables.

To use nextpnr-gowin, install the `yowasp-nextpnr-gowin` package using [pip] or add it as a dependency. This package contains support for every device, and provides the `yowasp-nextpnr-gowin` executable. It also depends on a compatible version of the `Apicula` package, which provides the `gowin_pack` and `gowin_unpack` executables.

Try running e.g. `yowasp-yosys --version` to see if everything works! When the tools are run for the first time, it will take a few seconds for them to be compiled to machine code.

If the packages are installed in a [virtualenv][], they will only be available in that virtual environment. Otherwise, they will be available system-wide or user-wide, similar to any other Python scripts installed via [pip][].

Consider also using [PDM](https://pdm.fming.dev/), which conveniently provides a way to set the required environment variables automatically in the `pyproject.toml` file...

```toml
[project]
...
dependencies = [
    "yowasp-yosys",
    "yowasp-nextpnr-ice40",
]

[tool.pdm.scripts]
_.env_file = ".env.toolchain"
...
```

... together with a `.env.toolchain` file...

```
YOSYS=yowasp-yosys
NEXTPNR_ICE40=yowasp-nextpnr-ice40
ICEPACK=yowasp-icepack
```

... such that they are set for any command run with `pdm run <command>`.

[virtualenv]: https://virtualenv.pypa.io/

### ... in a browser?

These instructions assume the use of [ES Modules][esm], and make use of the [jsDelivr][] content delivery network. It is also possible to distribute the YoWASP binaries by adding the relevant `@yowasp/*` NPM package as a dependency using a bundler such as [webpack](https://webpack.js.org/).

To use Yosys, import the [@yowasp/yosys][] NPM package from the CDN and call its `runYosys` entry point:

```js
import { runYosys } from 'https://cdn.jsdelivr.net/npm/@yowasp/yosys/gen/bundle.js';
await runYosys(["--version"]);
```

The [JavaScript runtime README][runtime-js-README] describes how to transfer files to and from the application.

[esm]: https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/
[jsDelivr]: https://www.jsdelivr.com/
[@yowasp/yosys]: https://www.npmjs.com/package/@yowasp/yosys
[runtime-js-README]: https://github.com/YoWASP/runtime-js#readme

### ... within Node.js?

These instructions assume the use of [ES Modules][esm].

To use Yosys, install the [@yowasp/yosys][] NPM package as a dependency, which can be done by running `npm install @yowasp/yosys`, import it and call its `runYosys` entry point:

```js
import { runYosys } from '@yowasp/yosys';
await runYosys(["--version"]);
```

The [JavaScript runtime README][runtime-js-README] describes how to transfer files to and from the application.

### ... with other languages?

At the moment, only PyPI and NPM packages are provided. [Open an issue][issue] if you'd like YoWASP packages to be built for another ecosystem.

[issue]: https://github.com/YoWASP/yowasp.github.io/issues

## Are the tools slower?

Yosys built for WebAssembly is about half the speed of a native build. Nextpnr built for WebAssembly runs about as fast as a native build.

## How are the packages released?

Routine YoWASP maintenance is [fully automated](/maintaining#maintenance-automation). Upstream changes and releases are tracked daily without manual intervention.
