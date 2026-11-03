load("@rules_pkg//pkg:install.bzl", "pkg_install")
load("@rules_pkg//pkg:mappings.bzl", "pkg_attributes", "pkg_filegroup", "pkg_files", "strip_prefix")

package(default_visibility = ["//visibility:public"])

pkg_files(
    name = "package_files_libraries",
    srcs = ["//modules/world_model/local_map:local_scene_builder"],
    attributes = pkg_attributes(mode = "0644"),
    prefix = "world_model/lib",
    strip_prefix = strip_prefix.from_root("modules/world_model"),
)

pkg_filegroup(
    name = "package_files",
    srcs = [":package_files_libraries"],
)

pkg_install(
    name = "install_dir",
    srcs = [":package_files"],
    tags = ["manual"],
)
