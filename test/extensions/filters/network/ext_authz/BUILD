load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_fuzz_test",
    "envoy_package",
    "envoy_proto_library",
)
load(
    "//test/extensions:extensions_build_system.bzl",
    "envoy_extension_cc_test",
)

licenses(["notice"])  # Apache 2

envoy_package()

envoy_extension_cc_test(
    name = "ext_authz_test",
    srcs = ["ext_authz_test.cc"],
    extension_names = ["envoy.filters.network.ext_authz"],
    rbe_pool = "6gig",
    deps = [
        "//source/common/buffer:buffer_lib",
        "//source/common/event:dispatcher_lib",
        "//source/common/json:json_loader_lib",
        "//source/common/network:address_lib",
        "//source/common/protobuf:utility_lib",
        "//source/common/stats:stats_lib",
        "//source/extensions/filters/network:well_known_names",
        "//source/extensions/filters/network/ext_authz",
        "//test/extensions/filters/common/ext_authz:ext_authz_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/server:server_factory_context_mocks",
        "//test/mocks/tracing:tracing_mocks",
        "@envoy_api//envoy/extensions/filters/network/ext_authz/v3:pkg_cc_proto",
    ],
)

envoy_extension_cc_test(
    name = "config_test",
    srcs = ["config_test.cc"],
    extension_names = ["envoy.filters.network.ext_authz"],
    rbe_pool = "6gig",
    deps = [
        "//source/extensions/filters/network/ext_authz:config",
        "//test/mocks/server:factory_context_mocks",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/filters/network/ext_authz/v3:pkg_cc_proto",
    ],
)

envoy_proto_library(
    name = "ext_authz_fuzz_proto",
    srcs = ["ext_authz_fuzz.proto"],
    deps = [
        "@envoy_api//envoy/extensions/filters/network/ext_authz/v3:pkg",
    ],
)

envoy_cc_fuzz_test(
    name = "ext_authz_fuzz_test",
    srcs = ["ext_authz_fuzz_test.cc"],
    corpus = "ext_authz_corpus",
    rbe_pool = "6gig",
    deps = [
        ":ext_authz_fuzz_proto_cc_proto",
        "//source/common/buffer:buffer_lib",
        "//source/extensions/filters/network/ext_authz",
        "//test/extensions/filters/common/ext_authz:ext_authz_mocks",
        "//test/mocks/network:network_mocks",
        "//test/mocks/runtime:runtime_mocks",
        "//test/mocks/server:server_factory_context_mocks",
        "@envoy_api//envoy/extensions/filters/network/ext_authz/v3:pkg_cc_proto",
    ],
)
