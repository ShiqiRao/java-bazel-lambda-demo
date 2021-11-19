load("@rules_java//java:defs.bzl", "java_binary", "java_library")

java_library(
    name="java-maven-lib",
    srcs = glob(["src/main/java/com/example/demo/*.java"]),
    deps = [
        "@maven//:com_amazonaws_aws_lambda_java_core",
        "@maven//:com_google_code_gson_gson",
        ],
)

java_binary(
    name = "lambda_binary",
    main_class = "com.example.demo.Handler",
    runtime_deps=[":java-maven-lib"],
)

genrule(
    name = "lambda_deploy",
    srcs = [":lambda_binary_deploy.jar"],
    outs = ["lambda_deploy.zip"],
    cmd = "$(location @bazel_tools//tools/zip:zipper) c $@ lib/lambda.jar=$(SRCS)",
    tools = ["@bazel_tools//tools/zip:zipper"],
    visibility = ["//visibility:public"],
)

