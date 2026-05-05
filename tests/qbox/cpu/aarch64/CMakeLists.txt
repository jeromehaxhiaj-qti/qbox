# All AArch64 CPU tests assemble their firmware with llvm-mc + ld.lld and load
# the resulting .bin at runtime (see load_firmware_binary in test/cpu.h).

qbox_build_firmware_bin(simple-write-test       aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(dmi-test                aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(dmi-test-async-inval    aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(dmi-test-concurrent-inval aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(dmi-test-reset          aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(ld-st-excl-fail         aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(halt-tests              aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(write_read              aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(reset-test              aarch64 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(smmu_router_stress_test_v2 aarch64 ${CMAKE_CURRENT_SOURCE_DIR})

qbox_add_cpu_test(aarch64-simple-write-test      100 simple-write-test.cc)
qbox_attach_firmware(aarch64-simple-write-test      simple-write-test)

qbox_add_cpu_test(aarch64-dmi-test               100 dmi-test.cc)
qbox_attach_firmware(aarch64-dmi-test               dmi-test)

qbox_add_cpu_test(aarch64-dmi-test-concurrent-inval 100 dmi-test-concurrent-inval.cc)
qbox_attach_firmware(aarch64-dmi-test-concurrent-inval dmi-test-concurrent-inval)

qbox_add_cpu_test(aarch64-dmi-test-reset         100 dmi-test-reset.cc)
qbox_attach_firmware(aarch64-dmi-test-reset         dmi-test-reset)

qbox_add_cpu_test(aarch64-ld-st-excl-fail-test   100 ld-st-excl-fail.cc)
qbox_attach_firmware(aarch64-ld-st-excl-fail-test   ld-st-excl-fail)

qbox_add_cpu_test(aarch64-write_read             100 write_read.cc)
qbox_attach_firmware(aarch64-write_read             write_read)

qbox_add_cpu_test(aarch64-dmi-test-async-inval   100 dmi-test-async-inval.cc)
qbox_attach_firmware(aarch64-dmi-test-async-inval   dmi-test-async-inval)

qbox_add_cpu_test(halt-tests                     100 halt-tests.cc)
qbox_attach_firmware(halt-tests                     halt-tests)

qbox_add_cpu_test(reset-test-system              100 reset-test-system.cc)
qbox_attach_firmware(reset-test-system              reset-test)

qbox_add_cpu_test(reset-test-cpu                 100 reset-test-cpu.cc)
qbox_attach_firmware(reset-test-cpu                 reset-test)

qbox_add_cpu_test(aarch64-smmu-router-stress-test-v2 100 smmu_router_stress_test_v2.cc)
qbox_attach_firmware(aarch64-smmu-router-stress-test-v2 smmu_router_stress_test_v2)
