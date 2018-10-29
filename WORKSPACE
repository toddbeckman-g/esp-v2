workspace(name = "esf")

bind(
    name = "boringssl_crypto",
    actual = "//external:ssl",
)

# When updating envoy sha manually please update the sha in istio.deps file also
ENVOY_SHA = "15cfc5ad1a4d622126f642fa70699af753a2d310"

http_archive(
    name = "envoy",
    strip_prefix = "envoy-" + ENVOY_SHA,
    url = "https://github.com/envoyproxy/envoy/archive/" + ENVOY_SHA + ".zip",
)

load("@envoy//bazel:repositories.bzl", "envoy_dependencies")
envoy_dependencies()

load("@envoy//bazel:cc_configure.bzl", "cc_configure")
cc_configure()

load("@envoy_api//bazel:repositories.bzl", "api_dependencies")
api_dependencies()

load("@io_bazel_rules_go//go:def.bzl", "go_rules_dependencies", "go_register_toolchains")
load("@com_lyft_protoc_gen_validate//bazel:go_proto_library.bzl", "go_proto_repositories")
go_proto_repositories(shared=0)
go_rules_dependencies()
go_register_toolchains()

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
git_repository(
    name = "org_pubref_rules_protobuf",
    commit = "563b674a2ce6650d459732932ea2bc98c9c9a9bf",  # Nov 28, 2017 (bazel 0.8.0 support)
    remote = "https://github.com/pubref/rules_protobuf",
)