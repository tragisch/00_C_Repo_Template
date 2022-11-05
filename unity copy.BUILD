filegroup(
    name = "TestRunnerGenerator",
    srcs = ["auto/generate_test_runner.rb"],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "HelperScripts",
    srcs = glob(["auto/*.rb"]),
    visibility = ["//visibility:public"],
)

filegroup(
    name = "TypeSanitizer",
    srcs = ["auto/type_sanitizer.rb"],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "UnityDir",
    srcs = ["."],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "UnitySrcs",
    srcs = ["src/unity.c"],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "UnityHdrs",
    srcs = [
        "src/unity.h",
        "src/unity_internals.h",
    ],
    visibility = ["//visibility:public"],
)

genrule(
    name = "UnityConfigForEmbeddedHdr",
    outs = ["unity_config.h"],
    cmd = """cat <<EOF > $@
#ifndef UNITY_CONFIG_H
#define UNITY_CONFIG_H

void printChar(char a);

void setUpPrint(void);

#define UNITY_OUTPUT_CHAR(a) printChar(a)
#define UNITY_OUTPUT_START() setUpPrint()

#endif
EOF""",
)

cc_library(
    name = "DefaultUnityConfigForEmbedded",
    hdrs = [":UnityConfigForEmbeddedHdr"],
)

cc_library(
    name = "Unity",
    srcs = [":UnitySrcs"],
    hdrs = [":UnityHdrs"],
    copts = ["-DUNITY_INCLUDE_DOUBLE"],
    strip_include_prefix = "src",
    visibility = ["//visibility:public"],
)

cc_library(
    name = "UnityForEmbedded",
    srcs = [":UnitySrcs"],
    hdrs = [":UnityHdrs"],
    copts = ["-DUNITY_INCLUDE_CONFIG_H"],
    strip_include_prefix = "src",
    visibility = ["//visibility:public"],
    deps = [":DefaultUnityConfigForEmbedded"],
)

cc_library(
    name = "UnityFixtures",
    srcs = glob(["extras/fixture/src/*.c"]),
    hdrs = glob(["extras/fixture/src/*.h"]),
    strip_include_prefix = "extras/fixture/src",
    visibility = ["//visibility:public"],
    deps = ["Unity"],
)
