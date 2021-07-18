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
</style>
<blockquote>
This is the most galaxy brained solution to windows package distribution I've seen yet, I'm impressed and horrified
<cite><a href="https://twitter.com/Amyayash">@Amyayash</a><!-- https://twitter.com/Amyayash/status/1320142568433340417 --></cite>
</blockquote>

## What is YoWASP?

YoWASP (**Yo**sys **W**eb**A**ssembly **S**ynthesis & **P**nR) is a project that aims to distribute up-to-date [FOSS FPGA tools][yosyshq] compiled to [WebAssembly][] via language package managers like [Python][]'s [PyPI][].

[yosyshq]: https://github.com/YosysHQ/
[webassembly]: https://webassembly.org/
[python]: https://python.org/
[pypi]: https://pypi.org/

### Why use WebAssembly?

A batch compiler, such as an FPGA toolchain, transforms input files to output files without using any OS services beyond basic bookkeeping. Is it really necessary to build something so fundamentally simple for a large matrix of *every OS* × *every CPU*? With [WebAssembly][] and [WASI][], it is now possible to build a single [universal binary][universal] that runs on many OSes and CPUs.

[wasi]: https://wasi.dev/
[universal]: https://kripken.github.io/talks/2020/universal.html

### Do I need a browser?

Despite the name, [WebAssembly][] is not tied to browsers; it is a kind of machine code that can be easily translated into x86, ARM, or other machine code that your CPU runs directly. The YoWASP project currently does **not** provide tools that can run in a browser.

### Why use language package managers?

Many new hardware definition languages are *[embedded][edsl]* in another *host* language, which comes with its own package manager and repository. For example, [nMigen][] is embedded in [Python][], which uses [pip][] and [PyPI][]. There are several benefits in distributing FPGA tools via language package managers:
  * Designers working in such HDLs are already familiar with the package manager of the host language, making it is a convenient distribution mechanism;
  * Synthesis and PnR tools can be added as ordinary dependencies to the project, and their versions can be frozen for reproducibility;
  * "Turnkey" toolchain installation enables new applications that generate FPGA bitstreams just-in-time, or use synthesis tools to transform netlists.

[edsl]: https://en.wikipedia.org/wiki/eDSL
[nmigen]: https://github.com/nmigen/nmigen
[pip]: https://pip.pypa.io/

## Which tools are provided?

This project provides packages for:

  * Yosys:
    * [upstream repository][yosys];
    * [package repository][yosys-pkg];
    * PyPI packages: [yowasp-yosys][].
  * nextpnr:
    * [nextpnr upstream repository][nextpnr];
    * [Project IceStorm upstream repository][icestorm];
    * [Project Trellis upstream repository][trellis];
    * [Project Oxide upstream repository][oxide];
    * [package repository][nextpnr-pkg];
    * PyPI packages: [yowasp-nextpnr-ice40][], [yowasp-nextpnr-ecp5][], [yowasp-nextpnr-nexus][].

[yosys]: http://www.clifford.at/yosys
[nextpnr]: https://github.com/YosysHQ/nextpnr/
[icestorm]: https://github.com/YosysHQ/icestorm/
[trellis]: https://github.com/YosysHQ/prjtrellis/
[oxide]: https://github.com/gatecat/prjoxide

[yosys-pkg]: https://github.com/YoWASP/yosys
[nextpnr-pkg]: https://github.com/YoWASP/nextpnr

[yowasp-yosys]: https://pypi.org/project/yowasp-yosys/
[yowasp-nextpnr-ice40]: https://pypi.org/project/yowasp-nextpnr-ice40/
[yowasp-nextpnr-ecp5]: https://pypi.org/project/yowasp-nextpnr-ecp5/
[yowasp-nextpnr-nexus]: https://pypi.org/project/yowasp-nextpnr-nexus/

## Which platforms are supported?

YoWASP relies on a [WebAssembly][] engine to run the WASM code, and inherits both its advantages and its limitations.

YoWASP is an early technology preview. At the moment, it uses the [Wasmtime][] engine, which supports the following platforms:

  * Linux (x86_64 and AArch64),
  * macOS (x86_64),
  * Windows (x86_64).

This list is unfortunately short. The maintainer of YoWASP is working together with the maintainers of several WebAssembly engines to expand it.

[wasmtime]: http://wasmtime.dev/
[wasmer]: https://wasmer.io/

## Are there other packages?

YoWASP isn't the only project that packages the open-source FPGA toolchain, and it has some limitations. One of the following projects may suit your workflow better:

  * [YosysHQ FPGA toolchain][hqtools] is a native build (x86_64 Linux and macOS only) that includes GHDL and programming tools (`iceprog`, `ecpprog`, `dfu-util`, etc).

[hqtools]: https://github.com/YosysHQ/fpga-toolchain

## How do I use the tools...

### ... with Python?

To use Yosys, install the `yowasp-yosys` package using [pip][] or add it as a dependency.

To use nextpnr-ice40, install the `yowasp-nextpnr-ice40-all` package using [pip][] or add it as a dependency. It is also possible to install individual `yowasp-nextpnr-ice40-<chip>` packages (where `<chip>` is `384` for iCE40LP384, `1k` for iCE40LP1K and iCE40HX1K, `5k` for iCE40UP5K, `8k` for iCE40LP8K and iCE40HX8K, and `u4k` for iCE5LP4K) if only a subset of all supported devices is wanted.

To use nextpnr-ecp5, install the `yowasp-nextpnr-ecp5-all` package using [pip][] or add it as a dependency. It is also possible to install individual `yowasp-nextpnr-ecp5-<chip>` packages (where `<chip>` is `25k` for LFE5U-12F and LFE5U/UM/UM5G-25F, `45k` for LFE5U/UM/UM5G-45F, and `85k` for LFE5U/UM/UM5G-85F) if only a subset of all supported devices is wanted.
  
To use nextpnr-nexus, install the `yowasp-nextpnr-nexus` package using [pip] or add it as a dependency. This package provides all of the supported devices.

The installed binaries are prefixed with `yowasp-`. Try running e.g. `yowasp-yosys --version` to see if everything works! When the tools are run for the first time, it will take a few seconds for them to be compiled to machine code.

If the packages are installed in a [virtualenv][], they will only be available in that virtual environment. Otherwise, they will be available system-wide or user-wide, similar to any other Python scripts installed via [pip][].

[virtualenv]: https://virtualenv.pypa.io/

### ... with other languages?

At the moment, only PyPI packages are provided. [Open an issue][issue] if you'd like YoWASP packages to be built for another ecosystem.

[issue]: https://github.com/YoWASP/yowasp.github.io/issues

## Are the tools slower?

Yosys built for WebAssembly is about half the speed of a native build. Nextpnr built for WebAssembly runs about as fast as a native build.

## How are the packages released?

Packages are [automatically](/maintaining) built and uploaded to the repository using [GitHub Actions][actions] after every push to one of the [package repositories][pkgrepos].

Every day, latest upstream changes are automatically pulled in, packaged, and uploaded to [Test PyPI][]. Every week, after manual review, latest upstream changes are packaged, uploaded to [PyPI][], and become available to downstream users.

[actions]: https://github.com/features/actions
[pkgrepos]: https://github.com/YoWASP
[test pypi]: https://test.pypi.org/
