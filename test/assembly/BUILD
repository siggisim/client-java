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

load("@graknlabs_dependencies//tool/checkstyle:rules.bzl", "checkstyle_test")

java_test(
    name = "test-assembly-query",
    srcs = [
        "QueryTest.java",
    ],
    test_class = "grakn.client.test.assembly.QueryTest",
    deps = [
        # Internal dependencies
        "//:client-java",
        "//test/setup:grakn-setup",
        "//test/setup:grakn-properties",

        # External dependencies from @graknlabs
        "@graknlabs_graql//java:graql",

        # External dependencies from Maven
        "@maven//:commons_io_commons_io",
        "@maven//:org_hamcrest_hamcrest_library",
        "@maven//:org_zeroturnaround_zt_exec",
        "@maven//:org_slf4j_slf4j_api",
    ],
    data = ["@graknlabs_grakn_core_artifact//file"],
    args = [ # The order of the arguments matter
        "grakn-core", # Keep at index 0, will be accessible at args[1]
        "$(location @graknlabs_grakn_core_artifact//file)", # Keep at index 1, will be accessible at args[2]
    ],
    classpath_resources = ["//test/setup:logback"],
)

checkstyle_test(
    name = "checkstyle",
    targets = [
        ":test-assembly-query",
    ],
)
