workspace(
    name = "my_workspace",
    managed_directories = {"@npm": ["node_modules"]},
)

# Load the http_archive rule.
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Load the rules_nodejs repository
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "d63ecec7192394f5cc4ad95a115f8a6c9de55c60d56c1f08da79c306355e4654",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/4.6.1/rules_nodejs-4.6.1.tar.gz"],
)

# Load the node_repositories function
load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories")

# This rule installs nodejs, npm, and yarn, but does NOT install
# your npm dependencies into your node_modules folder.
# You must still run the package manager to do this.
node_repositories(
    package_json = ["//:package.json"],
    node_version = "16.13.2", # specific Node.js version
)

# The npm_install rule runs npm anytime the package.json or package-lock.json file changes.
# It also extracts any Bazel rules distributed in an npm package.
load("@build_bazel_rules_nodejs//:index.bzl", "npm_install")
npm_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "npm",
    # Paths to the package*.json files
    package_json = "//:package.json",
    package_lock_json = "//:package-lock.json",
)