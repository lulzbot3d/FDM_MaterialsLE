# FDM_MaterialsLE

[![Profile Validation](https://github.com/lulzbot3d/FDM_MaterialsLE/actions/workflows/check-validate-profiles.yml/badge.svg)](https://github.com/lulzbot3d/FDM_MaterialsLE/actions/workflows/check-validate-profiles.yml)
[![Conan Package](https://github.com/lulzbot3d/FDM_MaterialsLE/actions/workflows/conan-package.yml/badge.svg)](https://github.com/lulzbot3d/FDM_MaterialsLE/actions/workflows/conan-package.yml)
[![Repo Size](https://img.shields.io/github/repo-size/lulzbot3d/FDM_MaterialsLE?style=flat)](https://github.com/lulzbot3d/FDM_MaterialsLE)
[![License](https://img.shields.io/github/license/lulzbot3d/FDM_MaterialsLE?style=flat)](https://github.com/lulzbot3d/FDM_MaterialsLE/blob/main/LICENSE)

FDM Materials LE database, used in Cura LulzBot Edition

## License

FDM_MaterialsLE is released under terms of the CC0-1.0 License. Terms of the license can be found in the LICENSE file or [on the creative commons website.](https://creativecommons.org/publicdomain/zero/1.0/)

> In general it boils down to:  
> **We waive all rights to the extend of the law. You can copy, modify, distribute as you like, even for commercial purposes.**

## System Requirements

### All Environments

- Python 3.6 or higher

## How To Build

> **Note:**  
> We are currently in the process of switch our builds and pipelines to an approach which uses [Conan](https://conan.io/) and pip to manage our dependencies, which are stored on our JFrog Artifactory server and in the pypi.org. At the moment not everything is fully ported yet, so bare with us.

If you have never used [Conan](https://conan.io/), read their [documentation](https://docs.conan.io/en/latest/index.html) which is quite extensive and well maintained. Conan is a Python program and can be installed using pip

### 1. Configure Conan

```bash
pip install conan --upgrade
conan config install https://github.com/lulzbot3d/conan-config-le.git
conan profile new default --detect --force
```

Community developers would have to remove the Conan cura-le repository because it requires credentials.

LulzBot developers need to request an account for our JFrog Artifactory server with IT

```bash
conan remote remove cura-le
```

### 2. Clone FDM_MaterialsLE

```bash
git clone https://github.com/lulzbot3d/FDM_MaterialsLE.git
cd FDM_MaterialsLE
```

## Creating a new FDM_MaterialsLE Conan package

To create a new FDM_Materials Conan package such that it can be used in CuraLE and UraniumLE, run the following command:

```shell
conan create . fdm_materialsle/<version>@<username>/<channel> --build=missing --update
```

This package will be stored in the local Conan cache (`~/.conan/data` or `C:\Users\username\.conan\data` ) and can be used in downstream projects, such as CuraLE and UraniumLE by adding it as a requirement in the `conanfile.py` or in `conandata.yml`.

Note: Make sure that the used `<version>` is present in the conandata.yml in the fdm_materials root

You can also specify the override at the commandline, to use the newly created package, when you execute the `conan install`
command in the root of the consuming project, with:

```shell
conan install . -build=missing --update --require-override=fdm_materialsle/<version>@<username>/<channel>
```

## Developing FDM_MaterialsLE In Editable Mode

You can use your local development repository downsteam by adding it as an editable mode package.
This means you can test this in a consuming project without creating a new package for this project every time.

```bash
    conan editable add . fdm_materialsle/<version>@<username>/<channel>
```

Then in your downsteam projects (CuraLE) root directory override the package with your editable mode package.

```shell
conan install . -build=missing --update --require-override=fdm_materialsle/<version>@<username>/<channel>
```
