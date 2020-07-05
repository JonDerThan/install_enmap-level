# Introduction

`enmap-level@2.1.0` depends on `level@^3.0.0` which then depends on `leveldown@^3.0.0`.
The latter fails to install. However, later versions (for example`leveldown@5.6.0`) seem to work just fine.

To install this new version you have to change either the dependencies of `level@^3.0.0` or the dependencies of `enmap-level@2.1.0`.
For me the first worked fine.


# Installation

1. Remove the `enmap-level` dependency out of your `package.json` file.

2. (_Recommended_) Remove all currently installed modules:
    ```bash
    rm -r ./node_modules/ ./package-lock.json
    ```

3. Install all of your dependencies (except `enmap-level`):
    ```bash
    npm install
    ```

4. Download `enmap-level@2.1.0` and `level@3.0.2` from here:

    * [enmap-level@2.1.0](https://github.com/eslachance/enmap-level/tree/a8ad6270e5784f2465d209f1710e856bda19b54e)
    * [level@3.0.2](https://github.com/Level/level/tree/v3.0.2)

5. Unpack both of these modules into your `./node-modules/` directory (important: the folders must be named `enmap-level` and `level` instead of for example `enmap-level-master`). Your directory should look like this after:
    ```bash
    ├── node_modules
    │   ├── enmap-level
    │   │   └── ...
    │   ├── level
    │   │   ├── package.json # <--- modify this in step 6
    │   │   └── ...
    │   └── ...
    ├── package.json # <--- modified in step 1
    ├── main.js
    └── ...
    ```

6. Modify the `package.json` file of `level@3.0.2`, which should be located here: `./node-modules/level/package.json`.
Search for the dependencies and change the `leveldown` version from `^3.0.0` to for example `5.6.0`. The dependencies should then look like this:
    ```json
    "dependencies": {
        "level-packager": "^2.0.2",
        "leveldown": "5.6.0",
        "opencollective-postinstall": "^2.0.0"
    }
    ```

7. Install these modified dependencies by running
    ```bash
    npm install
    ```
    in the `./node-modules/level/` directory.

**Steps 4-6 can be skipped by copying the already modified modules out of `./modified_node_modules/` to `./node_modules/`.**


## Side notes
Installing the other modules first is very important, since every time you run `npm install` all the modified packages will be removed.

Because of that I would also recommend to store the `enmap-level` module and the modified `level` module in a seperate folder to enable you to copy them each time you update your other packages (if you do not already use the modified packages out of `./modified_node_modules/`).
