# bazel
C++ bazel

# 引用外部库
```
package(default_visibility = ["//visibility:public"])

cc_import(
    name = "xxx",
    static_library = "xxx.a", // 引用静态库
)

cc_import(
    name = "xxx",
    shared_library = "xxx.so", // 引用动态库
)
```
```
load("@rules_cc//cc:defs.bzl", "cc_library")

package(default_visibility = ["//visibility:public"])

cc_library(
    name = "xxx",
    srcs = glob(
        [
            "**/*.cpp",
        ],
        exclude = ["xxx/*.cpp"], // 排除文件
        exclude_directories = 1, // 排除目录
    ),
    hdrs = glob(
        [
            "**/*.h",
        ],
        exclude = ["xxx/*.h"],
        exclude_directories = 1,
    ),
    copts = [
        "-Ilibs/", // 相对于工程
    ],
    includes = [
        "xxx",
    ],
    linkstatic = 1,
    deps = [
        "//xxx:xxx",
    ],
)
```
```
load("@rules_cc//cc:defs.bzl", "cc_binary")

package(default_visibility = ["//visibility:public"])

cc_binary(
    name = "xxx",
    srcs = glob([
        "*.cpp",
        "*.h",
    ]),
    linkstatic = 1,
    deps = [
        "//xxx:xxx",
    ],
)

```
```
build --spawn_strategy=standalone
build --repo_env=CC=clang
build --repo_env=CXX=clang++
build --cxxopt="-std=c++11"
build --copt="-DTHREADED"
build --copt="-DDEBUG"
build --copt="-D_DEBUG_"
build --copt="-D_MEMORY_TRACE_"
build --copt="-Werror"
build --copt="-Wall"
build --copt="-Wno-reserved-user-defined-literal"
build --copt="-Wno-unused-command-line-argument"
build --copt="-Wno-invalid-offsetof"
build --copt="-Wno-deprecated-register"
build --copt="-Wno-self-assign"
build --copt="-m64" 
build --copt="-g"
build --copt="-fPIC"
build --copt="-DJAEGERTRACING_WITH_YAML_CPP"
build --linkopt="-Wl,--allow-multiple-definition"
build --linkopt="-rdynamic"
build --linkopt="-lpthread"
build --linkopt="-ldl"
build --linkopt="-lanl"
build --linkopt="-lreadline"
build --linkopt="-lrt"
build --linkopt="-lm"
build --linkopt="-fuse-ld=gold"
```
