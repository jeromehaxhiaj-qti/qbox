# Hexagon firmwares: assembled with llvm-mc -arch=hexagon, linked with ld.lld,
# objcopied to a raw .bin that the test loads via load_firmware_binary.

qbox_build_firmware_bin(ld-st-mmio             hexagon ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(hex-reset              hexagon ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(load-store-test        hexagon ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(hexagon_smmu_firmware  hexagon ${CMAKE_CURRENT_SOURCE_DIR}
    EXTRA_LD_ARGS --defsym TESTER_ADDR=0x40000 --defsym REG_DEBUG=0x28 --defsym PAGE_SIZE=0x1000)

qbox_add_cpu_test(hexagon-ld-st-mmio-test 100 ld-st-mmio.cc)
qbox_attach_firmware(hexagon-ld-st-mmio-test ld-st-mmio)

qbox_add_cpu_test(hexagon-reset-test 100 hex-reset.cc)
qbox_attach_firmware(hexagon-reset-test hex-reset)

set(HEXAGON_STANDALONE_TEST_NAME "load-store-test")

add_executable(
    ${HEXAGON_STANDALONE_TEST_NAME}
    ${HEXAGON_STANDALONE_TEST_NAME}.cc
)

target_link_libraries(
    ${HEXAGON_STANDALONE_TEST_NAME}
    PRIVATE
    ${TARGET_LIBS}
    gs_memory
    router
    qemu_cpu_hexagon
    hexagon_globalreg
)

add_dependencies(${HEXAGON_STANDALONE_TEST_NAME} load-store-test-firmware)
target_compile_definitions(${HEXAGON_STANDALONE_TEST_NAME} PRIVATE
    FIRMWARE_BIN_PATH="${CMAKE_CURRENT_BINARY_DIR}/load-store-test.bin")

add_test(NAME hexagon-${HEXAGON_STANDALONE_TEST_NAME} COMMAND ${HEXAGON_STANDALONE_TEST_NAME})

qbox_add_cpu_test(hexagon-smmu-stress-test-v2 100 hexagon_smmu_stress_test_v2.cc)
qbox_attach_firmware(hexagon-smmu-stress-test-v2 hexagon_smmu_firmware)
