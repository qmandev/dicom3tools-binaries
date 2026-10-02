# dicom3tools-binaries

Prebuilt `dciodvfy`, the DICOM IOD validator from David Clunie's
[dicom3tools](https://www.dclunie.com/dicom3tools.html), as a universal macOS
binary, for validating DICOM files in continuous integration.

**Unofficial build.** Not produced, endorsed, or supported by the dicom3tools
author or PixelMed Publishing. **Not tested or approved for clinical use**, as
dicom3tools' own licence states.

## Release `dicom3tools-20260927113651`

| | |
|---|---|
| Asset | `dciodvfy-20260927113651-macos-universal.tar.gz` — `dciodvfy` and dicom3tools' `COPYRIGHT` |
| SHA-256 (archive) | `dd80fdabacc7a67f56ddcd950a04e275fad2593f344d0e2679fa9221d1b63443` |
| SHA-256 (`dciodvfy`) | `a028ce6efe9ab7460b4761d139301c9f27ec1b4f171da2742901cdceb847d7ea` |
| Source | `dicom3tools_1.00.snapshot.20260927113651.tar.bz2`, SHA-256 `a78040922ed52008280fab06fcadcff03f40926784d8b129948d4ffac8c0b09e` |
| Architectures | arm64, x86_64 (universal); macOS 10.9 or later |
| Links | `libSystem` and `libc++` only |
| Signature | ad hoc, by the linker |

dciodvfy compiles the standard's IOD definitions in, so the snapshot also fixes
which edition of the rules it checks.

## Use

```bash
curl -sSLO https://github.com/qmandev/dicom3tools-binaries/releases/download/dicom3tools-20260927113651/dciodvfy-20260927113651-macos-universal.tar.gz
echo "dd80fdabacc7a67f56ddcd950a04e275fad2593f344d0e2679fa9221d1b63443  dciodvfy-20260927113651-macos-universal.tar.gz" | shasum -a 256 -c
tar xzf dciodvfy-20260927113651-macos-universal.tar.gz
./dciodvfy -new file.dcm
```

## How it was built

From a fresh download of the snapshot above, following dicom3tools' `INSTALL`,
with no changes to the source:

```bash
./Configure
imake -I./config -DInstallInTopDir
make World
make install
```

macOS 26.5.1 · Xcode 26.6 · Apple clang 21.0.0 (clang-2100.1.1.101) ·
imake 1.0.11 and makedepend 1.0.10 (Homebrew). No UID root was configured: the
build's default `0.0.0.0` affects only tools that create DICOM instances, never
`dciodvfy`, which only reads.

The build is not bit-for-bit reproducible — C++ toolchains embed paths and
timestamps — so the checksums above pin this particular binary rather than any
rebuild of it.

## Licence

dicom3tools is © David A. Clunie DBA PixelMed Publishing, under a BSD 3-Clause
licence. Its full text is in `NOTICE` and is included as `COPYRIGHT` in every
release archive; it must accompany any redistribution of the binary.
