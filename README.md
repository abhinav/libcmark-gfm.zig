# libcmark-gfm.zig

Zig build of the [cmark-gfm](https://github.com/github/cmark-gfm) library
with no bindings or modifications.

**Targeted cmark-gfm version**: 0.29.0.gfm.13

Implementation largely based on [kristoff-it/cmark-gfm](https://github.com/kristoff-it/cmark-gfm)
but without forking the cmark-gfm repository.

## Usage

1. Add the dependency to your `build.zig.zon` file.
   You can use the `fetch` command to do this.

    ```bash
    zig fetch --save=libcmark-gfm "https://github.com/abhinav/libcmark-gfm.zig/archive/0.2.0.tar.gz"
    ```

2. Import the dependency in your build.zig file.

    ```zig
    const libcmark_gfm = b.dependency("libcmark-gfm", .{
        .target = target,
        .optimize = optimize,
    });
    ```

3. Link against the 'cmark-gfm' artifact in your build.zig file.

    ```zig
    const lib = b.addModule(...);
    lib.linkLibrary(libcmark_gfm.artifact("cmark-gfm"));
    ```

    If you need GitHub extensions, also add 'cmark-gfm-extensions' artifact.

    ```zig
    lib.linkLibrary(libcmark_gfm.artifact("cmark-gfm-extensions"));
    ```

4. Use the library in your code.

    ```zig
    const c = @cImport({
        @cInclude("cmark-gfm.h");
    });

    // ...
    const doc = c.cmark_parse_document(ptr, len, opts);
    ```

## License

This software is made available under the BSD3 license.
See LICENSE for details.
