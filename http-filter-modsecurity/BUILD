package(default_visibility = ["//visibility:public"])

load(
    "@envoy//bazel:envoy_build_system.bzl",
    "envoy_cc_binary",
    "envoy_cc_library",
    "envoy_cc_test",
)

load("@envoy_api//bazel:api_build_system.bzl", "api_proto_library")

api_proto_library(
    name = "http_filter_proto",
    srcs = ["http_filter.proto"],
    deps = [
        # TODO - "@envoy_api//envoy/api/v2/core:http_uri" (bad visibility)
    ]
)

envoy_cc_library(
    name = "http_filter_lib",
    copts=["-Wno-unused-function", "-Wno-unused-parameter", "-Wno-reorder", "-Wno-unused-variable", "-Imodsecurity/include"],
    srcs = ["utility.cc", "http_filter.cc", "webhook_fetcher.cc"],
    hdrs = glob(["utility.h", "http_filter.h", "webhook_fetcher.h", "well_known_names.h"]),
    repository = "@envoy",
    deps = [
        ":http_filter_proto_cc",
        "//:libmodsecurity",
        "@envoy//source/exe:envoy_common_lib",
    ],
)

envoy_cc_library(
    name = "http_filter_config",
    srcs = ["http_filter_config.cc"],
    copts=["-Wno-unused-function", "-Wno-unused-parameter", "-Wno-reorder", "-Wno-unused-variable", "-Imodsecurity/include"],
    repository = "@envoy",
    deps = [
        ":http_filter_lib",
        "@envoy//include/envoy/server:filter_config_interface"
    ],
)

envoy_cc_test(
    name = "http_filter_integration_test",
    srcs = ["http_filter_integration_test.cc"],
    repository = "@envoy",
    deps = [
        ":http_filter_config",
        "@envoy//test/integration:http_integration_lib",
    ],
)
