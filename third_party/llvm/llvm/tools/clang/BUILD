package(default_visibility = ["//visibility:public"])

licenses(["notice"])

genrule(
    name = "clang_format_extract",
    srcs = ["@clang//file"],
    outs = ["clang-format"],
    cmd = " && ".join([
        "IN=$$(pwd)/$(SRCS)",
        "OUT=$$(pwd)/$@",
        "TMP=$$(mktemp -d $${TMPDIR:-/tmp}/genrule.XXXXXXXXXX)",
        "cd $$TMP",
    ]) + " && " + select({
        ":darwin": "tar xf $$IN */bin/clang-format",
        "//conditions:default": "tar xf $$IN --wildcards */bin/clang-format",
    }) + " && " + " && ".join([
        "mv */bin/clang-format $$OUT",
        "rm -rf $$TMP",
    ]),
    executable = True,
)

config_setting(
    name = "darwin",
    values = {"cpu": "darwin"},
    visibility = ["//visibility:private"],
)
