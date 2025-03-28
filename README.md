# cpp-qt-template

Modern project C++20 project template that uses CMake, Qt 6, QML, and vcpkg.

## About

The project template is developed with the premise that the UI will be written entirely in QML to promote sepration of concerns. The UI should be split into distinct QML modules to encourage scalability and re-usability.

### Why use this?

- There are much more thorough and more popular project templates out there. There's actually very little reason for _you_ to use this, unless your needs are similar to mine. This template doesn't really try to be everything to everyone, it fits my use case, and doesn't contain a lot of stuff I don't need.

### Why use vcpkg?

There are a number of pros to vcpkg:

- We get an actual package manager
    - We don't need to use git submodules, CMake FetchContent, copy code into our repo, use a system package manager (usually), etc.
- We get slightly more reproducible builds, which is great.

It isn't without downsides:

- I genuinely can't get Qt to work via `vcpkg` yet (at least on Linux) - even via a dependency manager building something like Qt from source is _not_ for the faint of heart apparently.
- **So vcpkg is really here for any non-Qt dependencies**

## Requirements

- CMake ≥ 3.21
- Ninja (at least by default, other build presets can be configured)
- C++20
- [vcpkg](https://github.com/microsoft/vcpkg)
- Qt (sourced by you, through your OS package manager or some other means)

## Usage

This project assumes you already have [vcpkg](https://github.com/microsoft/vcpkg) installed - by cloning it somewhere, running the bootstrap script, and set the `VCPKG_ROOT` envrionment variable.

### Building

Release builds (using Ninja) can be created using:

```bash
cmake --preset=release
cmake --build --preset=release
```

Debug builds (also with Ninja) can made with:

```bash
cmake --preset=default
cmake --build build
```

To do a fresh configure:

```bash
cmake --preset=release --fresh
```

Or to wipe away a build:

```bash
cmake --build --preset=release --target clean
```
