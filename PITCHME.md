---?color=gainsboro
@title[conan]

## packaging open-source libraries with conan.io

---?color=gainsboro
@title[install conan]

## INSTALL CONAN

```sh
$ pip install conan
```

---?color=gainsboro
@title[getting help]
### GETTING HELP

[https://cpplang-inviter.cppalliance.org/](https://cpplang-inviter.cppalliance.org/)

@div[right-50]
![invite](assets/img/qr_invite.png)
@divend

* #conan
* #bincrafters

---?color=gainsboro
@title[remotes-conan-center]
## REMOTES: CONAN-CENTER

* default remote
* official carefully-moderated repository
* currently ~120 packages available
* goal is to double amount by the end of year (2018)

---?color=gainsboro
@title[remotes-conan-community]

## REMOTES: CONAN-COMMUNITY

* supported by conan developers
* incubator for later conan-center inclusion
* +30 various packages
* foundational packages: zlib, bzip2, OpenSSL, etc.

```sh
$ conan remote add conan-community 
"https://api.bintray.com/conan/conan-community/conan"
```

---?color=gainsboro
@title[remotes-bincrafters]

## REMOTES: BINCRAFTERS

* supported by community
* incubator for later conan-center inclusion
* +200 various packages

```sh
$ conan remote add bincrafters 
"https://api.bintray.com/conan/bincrafters/public-conan"
```

---?color=gainsboro
@title[artifactory]

## Artifactory Community Edition

[https://jfrog.com/open-source/](https://jfrog.com/open-source/)

@div[right-50]
![artifactory](assets/img/qr_artifactory.png)
@divend

---?color=gainsboro
@title[nexus]

## Sonatype Nexus added conan support

---?color=gainsboro
@title[new packages]

## NEW PACKAGES

* Qt
* OpenCV
* ffmpeg
* SDL2
* wxWidgets
* wt
* ImageMagick
* protobuf

---?color=gainsboro
@title[wishlist]

## WISHLIST

### please vote!
### please add packages you want!

[https://croydon.github.io/conan_inquiry/#!wishlist](https://croydon.github.io/conan_inquiry/#!wishlist)

---?color=gainsboro
@title[python_requires]

## PYTHON_REQUIRES

---?color=gainsboro
@title[plug-ins]

## PLUG-INS

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

## WORKSPACES

---?color=gainsboro
@title[non-intrusive]

## non-intrusive CMake integration

---?color=gainsboro
@title[profiles]

## PROFILES

---?color=gainsboro
@title[build_requires]

## BUILD_REQUIRES

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

@div[right-50]
![artifactory](assets/img/qr_templates.png)
@divend

---?color=gainsboro
@title[conan package tools]

## CONAN PACKAGE TOOLS

```sh
$ pip install conan-package-tools
```
 ```sh
$ pip install bincrafters-package-tools
```

[https://github.com/conan-io/conan-package-tools](https://github.com/conan-io/conan-package-tools)

---?color=gainsboro
@title[conan docker tools]

## CONAN DOCKER TOOLS

[https://github.com/conan-io/conan-docker-tools](https://github.com/conan-io/conan-docker-tools)

[https://github.com/dockcross/dockcross](https://github.com/dockcross/dockcross)

---?color=gainsboro
@title[conan readme generator]

## CONAN README GENERATOR

* generates README
* adds badges for bintray/appveyor/travis
* adds list of options

```sh
$ pip install conan-readme-generator
```

---?color=gainsboro
@title[envy]

## ENVY

* updates travis & appveyor environment variables

```sh
$ pip install bincrafters-envy
```

---?color=gainsboro
@title[build helpers]

## BUILD HELPERS

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
