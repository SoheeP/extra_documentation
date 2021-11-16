### Build 환경
* Windows 10
* VSCode IDE 사용
  - C/C++, C/C++ Themes, C/C++ Extension Pack, Cmake, CmakeTools Extension 설치

### VSCode `settings.json` 에 아래 내용 추가
```JSON
{
    "cmake.mingwSearchDirs": [
        "C:\\msys64\\mingw64\\bin",
        "C:\\mingw64\\bin"
    ],
    "cmake.generator": "MinGW Makefiles",
    "cmake.buildBeforeRun": false,
    "cmake.clearOutputBeforeBuild": false,
    "cmake.ctest.parallelJobs": 1,
}
```

### VSCode `cmake-tools-kits.json` 에 아래 내용 추가
```JSON
{
    "name": "GCC 11.2.0",
    "compilers": {
      "C": "C:\\mingw64\\bin\\x86_64-w64-mingw32-gcc.exe",
      "CXX": "C:\\mingw64\\bin\\x86_64-w64-mingw32-g++.exe"
    },
    "preferredGenerator": {
      "name": "MinGW Makefiles"
    },
    "environmentVariables": {
      "PATH": "C:\\mingw64\\bin"
    }
  },
```

### VSCode `c_cpp_properties.json`
```JSON
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "windowsSdkVersion": "10.0.22000.0",
            "compilerPath": "C:/mingw64/bin/g++.exe",
            "cStandard": "c11",
            "cppStandard": "c++11",
            "intelliSenseMode": "windows-gcc-x64",
            "configurationProvider": "ms-vscode.cmake-tools"
        }
    ],
    "version": 4
}
```
- 해당 파일은 VSCode 에서 사용하는 C/C++ 구성파일.

### Problem
파일 빌드 시, `cc1.exe: error: too many filenames given.  Type cc1.exe --help for usage` 라는 에러메세지가 출력되면서, 파일을 못찾는다는 메세지도 함께 출력

### Solve
`CMakeList.txt`내에 `CMAKE_C_FLAGS`, `CMAKE_CXX_FLAGS`작성으로 발생한 에러로 확인되어 해당 Command들을 모두 주석처리 후 빌드함.
```txt
cmake_minimum_required(VERSION 3.0.0)
project(ProjectName)

# set(CMAKE_CXX_STANDARD 11)
# set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -o2 -W -Wall")
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -o2 -W -Wall")

...
```