#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#

package(default_visibility = ["//test/behaviour:__subpackages__"])
load("@graknlabs_dependencies//tool/checkstyle:rules.bzl", "checkstyle_test")

java_library(
    name = "steps",
    srcs = [
        "KeyspaceSteps.java"
    ],
    deps = [
        # Internal Package Dependencies
        "//test/behaviour/connection:steps",

        # Internal Repository Dependencies
        "@graknlabs_common//:common",

        # External Maven Dependencies
        "@maven//:junit_junit",
        "@maven//:io_cucumber_cucumber_java",
    ]
)

java_test(
    name = "test-core",
    srcs = [
        "KeyspaceTest.java"
    ],
    test_class = "grakn.client.test.behaviour.connection.keyspace.KeyspaceTest",
    deps = [
        # Package dependencies
        "//test/setup:grakn-setup",

        # External dependencies from Maven
        "@maven//:io_cucumber_cucumber_junit",
    ],
    runtime_deps = [
        ":steps"
    ],
    data = [
        "@graknlabs_verification//behaviour/connection:keyspace.feature",
        "@graknlabs_grakn_core_artifact//file", # Make sure to pass the path in args below
    ],
    args = [ # The order of the arguments matter
        "grakn-core", # Keep at index 0, will be accessible at args[1]
        "$(location @graknlabs_grakn_core_artifact//file)", # Keep at index 1, will be accessible at args[2]
    ],
    classpath_resources = ["//test/setup:logback"],
    size = "large",
)

# To run this test, you need to provide environment variables:
# --test_env GRAKN_KGMS_ADDRESS=***
# --test_env GRAKN_KGMS_USERNAME=****
# --test_env GRAKN_KGMS_PASSWORD=****
java_test(
    name = "test-kgms",
    srcs = [
        "KeyspaceTest.java"
    ],
    test_class = "grakn.client.test.behaviour.connection.keyspace.KeyspaceTest",
    deps = [
        # Package dependencies
        "//test/setup:grakn-setup",

        # External dependencies from Maven
        "@maven//:io_cucumber_cucumber_junit",
    ],
    runtime_deps = [
        ":steps"
    ],
    data = [
        "@graknlabs_verification//behaviour/connection:keyspace.feature",
    ],
    args = [ # The order of the arguments matter
        "grakn-kgms", # Keep at index 0, will be accessible at args[1]
    ],
    classpath_resources = ["//test/setup:logback"],
    size = "large",
)

checkstyle_test(
    name = "checkstyle",
    targets = [
        ":steps",
        ":test-core",
        ":test-kgms",
    ],
    license_type = "apache"
)
