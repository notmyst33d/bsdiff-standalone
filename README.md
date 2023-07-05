# bsdiff-standalone
Standalone version of Android bsdiff

## Building
Building with GCC will fail because Android dropped GCC support a long time ago, so you need to install Clang to build Android bsdiff
```
$ CC=clang CXX=clang++ meson setup build
$ meson compile -C build
```

