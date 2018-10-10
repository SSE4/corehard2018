---?color=black
@title[conan]

## packaging open-source libraries with conan.io

---?color=black
@title[install conan]

## install conan

```sh
pip install conan
```

---?color=black
@title[getting help]
### getting help

[https://cpplang-inviter.cppalliance.org/](https://cpplang-inviter.cppalliance.org/)

* #conan
* #bincrafters

---?color=black
@title[remotes-conan-center]
## remotes: conan-center

* currently ~120 packages available
* goal is to double amount by the end of year (2018)

---?color=black
@title[remotes-conan-community]

## remotes: conan-community

```sh
conan remote add conan-community 
"https://api.bintray.com/conan/conan-community/conan"
```

---?color=black
@title[remotes-bincrafters]

## remotes: bincrafters

```sh
conan remote add bincrafters 
"https://api.bintray.com/conan/bincrafters/public-conan"
```

---?color=black
@title[new packages]

## new packages

* Qt
* OpenCV
* ffmpeg
* SDL2
* wxWidgets
* wt
* protobuf

---?color=black
@title[wishlist]

## wishlist

### please vote!

[https://croydon.github.io/conan_inquiry/#!wishlist](https://croydon.github.io/conan_inquiry/#!wishlist)

---?color=black
@title[plug-ins]

## plug-ins

* binary linters
* signing
* license check
* update bintray metadata
* update GitHub metadata

---?color=black
@title[SCM]

## SCM

* Git
* SVN

---?color=black
@title[workspaces]

### workspaces

---?color=black
@title[profiles]

## profiles

---?color=black
@title[build_requires]

## build requires

* ninja_installer
* nasm_installer
* yasm_installer
* cygwin_installer
* msys2_installer
* mingw_installer
* premake_installer

---?color=black
@title[conan templates]

### conan templates

* conanfile + test package

* appveyor & travis manifests

[https://github.com/bincrafters/conan-templates](https://github.com/bincrafters/conan-templates)

---?color=black
@title[conan package tools]

### conan package tools

```sh
pip install conan-package-tools
```

[https://github.com/conan-io/conan-package-tools](https://github.com/conan-io/conan-package-tools)

---?color=black
@title[conan docker tools]

### conan docker tools

[https://github.com/conan-io/conan-docker-tools](https://github.com/conan-io/conan-docker-tools)

[https://github.com/dockcross/dockcross](https://github.com/dockcross/dockcross)

---?color=black
@title[conan readme generator]

### conan readme generator

```sh
pip install conan-readme-generator
```

---?color=black
@title[build helpers]

### build helpers

* CMake
* AutoToolsBuildEnvironment
* MSBuild

---?color=black
@title[CMake]

### CMake build helper

```python

    def configure_cmake(self):
        cmake = CMake(self)
        cmake.definition['ENABLE_LIBASTRAL'] = \
            self.options.libastral
        cmake.configure(build_dir=self.build_subfolder)
        return cmake

    def build_cmake(self):
        cmake = self.configure_cmake()
        cmake.build()

    def package(self):
        cmake = self.configure_cmake()
        cmake.install()
```

---?color=black
@title[MSBuild]

### MSBuild build helper

```python
    sln = 'libtheora_dynamic.sln' if \
       self.options.shared else 'libtheora_static.sln'
    msbuild = MSBuild(self)
    msbuild.build(sln, upgrade_project=True,
                  platforms={'x86': 'Win32',
                             'x86_64': 'x64'})
```

---?color=black
@title[AutoToolsBuildEnvironment]

### AutoToolsBuildEnvironment build helper

```python

    configure_args = []
    if self.options.shared:
        configure_args.extend(['--disable-static',
                               '--enable-shared'])
    else:
        configure_args.extend(['--disable-shared',
                               '--enable-static'])
    env_build = AutoToolsBuildEnvironment(self)
    env_build.configure(args=configure_args)
    env_build.make()
    env_build.install()
```
