licenses(["notice"])  # Apache 2

load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "dispatcher_lib",
    srcs = [
        "dispatcher_impl.cc",
        "file_event_impl.cc",
        "signal_impl.cc",
    ],
    hdrs = [
        "signal_impl.h",
    ],
    deps = [
        ":dispatcher_includes",
        ":real_time_system_lib",
        "//include/envoy/common:time_interface",
        "//include/envoy/event:signal_interface",
        "//include/envoy/network:listen_socket_interface",
        "//include/envoy/network:listener_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:thread_lib",
        "//source/common/filesystem:watcher_lib",
        "//source/common/network:connection_lib",
        "//source/common/network:dns_lib",
        "//source/common/network:listener_lib",
    ],
)

envoy_cc_library(
    name = "real_time_system_lib",
    srcs = [
        "event_impl_base.cc",
        "real_time_system.cc",
        "timer_impl.cc",
    ],
    hdrs = [
        "event_impl_base.h",
        "real_time_system.h",
        "timer_impl.h",
    ],
    deps = [
        ":libevent_lib",
        "//include/envoy/event:timer_interface",
        "//source/common/common:utility_lib",
        "//source/common/event:dispatcher_includes",
    ],
)

envoy_cc_library(
    name = "dispatcher_includes",
    hdrs = [
        "dispatcher_impl.h",
        "event_impl_base.h",
        "file_event_impl.h",
    ],
    deps = [
        ":libevent_lib",
        "//include/envoy/event:deferred_deletable",
        "//include/envoy/event:dispatcher_interface",
        "//include/envoy/event:file_event_interface",
        "//include/envoy/network:connection_handler_interface",
        "//source/common/common:minimal_logger_lib",
        "//source/common/common:thread_lib",
    ],
)

envoy_cc_library(
    name = "libevent_lib",
    srcs = ["libevent.cc"],
    hdrs = ["libevent.h"],
    external_deps = [
        "event",
    ],
    deps = [
        "//source/common/common:assert_lib",
        "//source/common/common:c_smart_ptr_lib",
    ],
)

envoy_cc_library(
    name = "dispatched_thread_lib",
    srcs = ["dispatched_thread.cc"],
    hdrs = ["dispatched_thread.h"],
    external_deps = [
        "event",
    ],
    deps = [
        ":dispatcher_lib",
        "//include/envoy/api:api_interface",
        "//include/envoy/event:dispatcher_interface",
        "//source/common/common:minimal_logger_lib",
        "//source/common/common:thread_lib",
        "//source/server:guarddog_lib",
    ],
)
