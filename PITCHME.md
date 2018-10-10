---?color=gainsboro
@title[conan]

## packaging open-source libraries with conan.io

---?color=gainsboro
@title[install conan]

## install conan

```sh
$ pip install conan
```

---?color=gainsboro
@title[getting help]
### getting help

[https://cpplang-inviter.cppalliance.org/](https://cpplang-inviter.cppalliance.org/)

@div[right-50]
![invite](assets/img/qr_invite.png)
@divend

* #conan
* #bincrafters

---?color=gainsboro
@title[remotes-conan-center]
## remotes: conan-center

* currently ~120 packages available
* goal is to double amount by the end of year (2018)

---?color=gainsboro
@title[remotes-conan-community]

## remotes: conan-community

```sh
$ conan remote add conan-community 
"https://api.bintray.com/conan/conan-community/conan"
```

---?color=gainsboro
@title[remotes-bincrafters]

## remotes: bincrafters

```sh
$ conan remote add bincrafters 
"https://api.bintray.com/conan/bincrafters/public-conan"
```

---?color=gainsboro
@title[artifactory]

## Artifactory Community Edition

[https://jfrog.com/open-source/](https://jfrog.com/open-source/)

---?color=gainsboro
@title[nexus]

## Sonatype Nexus added conan support

---?color=gainsboro
@title[new packages]

## new packages

* Qt
* OpenCV
* ffmpeg
* SDL2
* wxWidgets
* wt
* protobuf

---?color=gainsboro
@title[wishlist]

## wishlist

### please vote!

[https://croydon.github.io/conan_inquiry/#!wishlist](https://croydon.github.io/conan_inquiry/#!wishlist)

---?color=gainsboro
@title[plug-ins]

## plug-ins

* conan center checker
* binary linters
* signing
* license check
* update bintray metadata
* update GitHub metadata

---?color=gainsboro
@title[SCM]

## SCM

* Git
* SVN

---?color=gainsboro
@title[workspaces]

## workspaces

---?color=gainsboro
@title[profiles]

## profiles

---?color=gainsboro
@title[build_requires]

## build requires

* ninja_installer
* nasm_installer
* yasm_installer
* cygwin_installer
* msys2_installer
* mingw_installer
* premake_installer
* cmake_installer

---?color=gainsboro
@title[conan templates]

## conan templates

* conanfile + test package
* appveyor & travis manifests
* regular template
* header-only
* installer (build tool)

[https://github.com/bincrafters/conan-templates](https://github.com/bincrafters/conan-templates)

---?color=gainsboro
@title[conan package tools]

## conan package tools

```sh
$ pip install conan-package-tools
```
 ```sh
$pip install bincrafters-package-tools
```

[https://github.com/conan-io/conan-package-tools](https://github.com/conan-io/conan-package-tools)

---?color=gainsboro
@title[conan docker tools]

## conan docker tools

[https://github.com/conan-io/conan-docker-tools](https://github.com/conan-io/conan-docker-tools)

[https://github.com/dockcross/dockcross](https://github.com/dockcross/dockcross)

---?color=gainsboro
@title[conan readme generator]

## conan readme generator

```sh
$ pip install conan-readme-generator
```

---?color=gainsboro
@title[envy]

## envy

```sh
$ pip install bincrafters-envy
```

---?color=gainsboro
@title[build helpers]

## build helpers

* CMake
* AutoToolsBuildEnvironment
* MSBuild

---?color=gainsboro
@title[CMake]

## CMake build helper

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

---?color=gainsboro
@title[MSBuild]

## MSBuild build helper

```python
    sln = 'libtheora_dynamic.sln' if \
       self.options.shared else 'libtheora_static.sln'
    msbuild = MSBuild(self)
    msbuild.build(sln, upgrade_project=True,
                  platforms={'x86': 'Win32',
                             'x86_64': 'x64'})
```

---?color=gainsboro
@title[AutoToolsBuildEnvironment]

## AutoToolsBuildEnvironment build helper

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
