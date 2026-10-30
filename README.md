# Informant Toolchains

Informant uses self-contained toolchains rather than depending on an
Inform installation elsewhere on the computer. The VS Code extension and
compiler environment are distributed separately, allowing Informant to
install and manage the Inform environment used by a project without
changing another Inform installation on the system.

An Informant Toolchain contains the native compiler programs together
with the Inform resources, documentation, extensions, templates, and
player components needed for the normal development workflow. Toolchains
are available for each supported operating system and share the same
general package organization.

At a high level, a toolchain contains:

``` text
PACKAGE/
|
+-- Compilers/
+-- Documentation/
+-- Extensions/
+-- HTML/
+-- Imagery/
+-- Inter/
+-- Languages/
+-- Miscellany/
+-- Pipelines/
+-- Player/
+-- Redist/
+-- Templates/
```

The exact contents can vary between releases, but each directory has a
clear role in providing the complete Inform development environment used
by Informant.

## Toolchain Components

`Compilers/`

Contains the native `inform7`, `inform6`, and `inblorb` programs for the
target operating system. These programs provide the principal compile
and release pipeline used by Informant.

`Inter/` and `Pipelines/`

Contain Inform's kits and processing definitions used by the compiler.
These resources form part of the version-matched Inform environment.

`Extensions/` and `Languages/`

Provide the standard Inform extensions and language resources included
with the selected Inform release. Extensions installed separately by the
user remain distinct from those supplied by the toolchain.

`Documentation/` and `Imagery/`

Provide Inform documentation and supporting images used by the
documentation and generated Index.

`Templates/`, `HTML/`, and `Miscellany/`

Provide release templates, web presentation resources, Index resources,
and other supporting material used by Inform during compilation and
release.

`Player/`

Contains the Quixe/GlkOte browser-player resources used by Informant for
integrated Glulx playback.

`REDIST/`

Contains redistribution and licensing material for components included
in the packaged toolchain.

## Compilation

For Inform 10, the principal compiler pipeline can be summarized as:

``` text
Inform 7 source
      |
      v
   inform7
      |
      v
generated Inform 6 source
      |
      v
   inform6
      |
      v
  story file
      |
      +------> inblorb for packaged release output
```

The compiler programs work with the surrounding kits, extensions,
languages, pipelines, and release resources. Informant therefore manages
the toolchain as a complete package rather than as a collection of
independent executables.

## Platform Packages

Informant provides toolchain packages for Windows, macOS, and Linux. The
overall package organization is consistent across platforms, while the
native programs in `Compilers/` are built for the operating system and
architecture of each package.

The macOS toolchain is distributed as a universal package supporting
Intel and Apple silicon. Windows and Linux use their corresponding
native x86-64 packages.

Installing a toolchain does not replace or modify another Inform
installation. Informant stores its managed toolchains separately and
uses the toolchain selected for the current project.

## Versioned Environments

A toolchain represents a matched Inform environment. Its compiler
programs and supporting resources belong to the same toolchain release,
giving Informant a predictable set of files to use when compiling,
playing, documenting, and releasing a project.

Conceptually:

``` text
Informant
   |
   v
selected toolchain
   |
   v
PACKAGE/
   |
   +-- compiler programs
   +-- Inform kits and pipelines
   +-- standard extensions and languages
   +-- documentation and imagery
   +-- release resources
   +-- integrated player
```

This separation also allows more than one toolchain to be installed. A
project can select an appropriate installed toolchain without requiring
a system-wide change to Inform.

## Toolchain Sources and Releases

Informant toolchains are assembled from the Inform ecosystem and
packaged for use by Informant. Build automation, source information, and
downloadable releases are maintained in the Informant toolchain
repository:

-   [Informant Toolchain
    Actions](https://github.com/interactivefiction/informant-toolchains/actions)
-   [Informant Toolchain
    Releases](https://github.com/interactivefiction/informant-toolchains/releases)

The toolchain is distributed separately from the Informant VS Code
extension.

## Licensing

The GitHub Actions workflows used to build and package the Informant
toolchains, including their YAML workflow files, are provided under the
**Artistic License 2.0**.

The toolchains themselves contain components from the Inform ecosystem
with their respective licenses. Redistribution and licensing information
for components included in a packaged toolchain is provided in the
toolchain's `REDIST/` directory.

Licensing for the Informant VS Code extension is separate from the
toolchain build automation and packaged toolchain components. Informant
itself is licensed under the **GNU General Public License, version 3
only (GPL-3.0-only)**.
