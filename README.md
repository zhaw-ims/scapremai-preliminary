ScaPreMAI - Preliminary
=======================
This repo contains preliminary code for the ScaPreMAI project.

Structure
=========
The code goes into `src/`. We split the code by the language: 
C++ code goes into `src/cpp/`, Python code into `src/py/` *etc.*


C++
---
C++ code goes into `src/cpp/`. Namespaces follow the directories.

To build, first create a Python virtual environment where development
tools will be installed (such as conan):

```bash
cd {repository root}
python3 -m venv venv-dev-cpp
```

Activate the virtual environment (on Linux):
```
source venv-dev-cpp/bin/activate
```

Install development tools:
```bash
pip3 install -r src/cpp/python-dev-requirements.txt
```

Since we are using conan to install the dependencies, we need
to prepare it to use a more modern ABI (*e.g.*, if gcc > 5.1):
```bash
conan profile new default --detect
conan profile update settings.compiler.libcxx=libstdc++11 default
```

Now build everything in the `build/` directory:
```bash
mkdir build && cd build
```

We install the dependencies:
```bash
conan install ../src/cpp
```

Run CMake (Linux):
```bash
cmake ../src/cpp -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release
cmake --build .
```

or CMake in Windows:
```bash
cmake ../src/cpp -G "Visual Studio 16"
cmake --build . --config Release
```

We check the formatting with clang-format. Please install clang-format separately.
The following build target fails if the formatting is incorrect. Always run it before
committing:
```bash
make format
```

Please see https://docs.conan.io/en/latest/getting_started.html for more information on Conan.

Mapry
-----
Mapry schemas go into `src/mapry/`.

The generated code is checked into the repository. These steps are only necessary
if you want to re-generate the code (*e.g.*, if a schema needs to change).

To generate the code, first create a Python virtual environment where development
tools will be installed:

```bash
cd {repository root}
python3 -m venv venv-dev-mapry
```

Activate the virtual environment (on Linux):
```
source venv-dev-mapry/bin/activate
```

Install all the development tools:
```bash
pip3 install -r src/mapry/python-dev-requirements.txt
```

Generate the code for all the languages:
```bash
src/mapry/generate.py
```
