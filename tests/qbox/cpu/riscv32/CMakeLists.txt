# Each RISC-V test ships a paired .S + .ld and gets its firmware built via the
# shared helper defined in tests/qbox/CMakeLists.txt.

qbox_build_firmware_bin(riscv32-reset       riscv32 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(riscv32-dmi-test    riscv32 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(riscv32-irq-test    riscv32 ${CMAKE_CURRENT_SOURCE_DIR})
qbox_build_firmware_bin(riscv32-qtimer-test riscv32 ${CMAKE_CURRENT_SOURCE_DIR})

qbox_add_cpu_test(riscv32-reset-test 100 riscv32-reset.cc)
qbox_attach_firmware(riscv32-reset-test riscv32-reset)

qbox_add_cpu_test(riscv32-dmi-test 100 riscv32-dmi-test.cc)
qbox_attach_firmware(riscv32-dmi-test riscv32-dmi-test)

qbox_add_cpu_test(riscv32-irq-test 100 riscv32-irq-test.cc)
qbox_attach_firmware(riscv32-irq-test riscv32-irq-test)
target_include_directories(riscv32-irq-test PRIVATE
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/qemu-components/timer/riscv_aclint_mtimer/include>)

qbox_add_cpu_test(riscv32-qtimer-test 100 riscv32-qtimer-test.cc)
qbox_attach_firmware(riscv32-qtimer-test riscv32-qtimer-test)
target_include_directories(riscv32-qtimer-test PRIVATE
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/qemu-components/timer/riscv_aclint_mtimer/include>)
