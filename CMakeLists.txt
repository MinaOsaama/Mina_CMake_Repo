cmake_minimum_required(VERSION 3.0)
project(Snake_effect)

#find toolchain program
find_program(AVR-GCC avr-gcc)
set(CMAKE_C_COMPILER ${AVR-GCC})
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mmcu=atmega32")
set(cc-flag  -mmcu=atmega32)

set(main_source ./src/main.c)
set(lib_source ./lib/libMDIO.a)
set(elf_file Snake_effect.elf)
set(input_falg -lm)
set(output_flag -o)
set(elf_to_hex avr-objcopy)
set(hex_flag -O ihex)
set(hex_file snake_effect.hex)
set(bin_rep binaryReport.txt)
set(build_dir build)

execute_process(COMMAND ${AVR-GCC} ${cc-flag} ${main_source} ${lib_source} ${input_falg} ${output_flag} ${elf_file})
execute_process(COMMAND ${elf_to_hex} ${hex_flag} ${elf_file} ${hex_file})

file(TOUCH ${bin_rep})
execute_process(COMMAND bash bin_redir.sh)
file(MAKE_DIRECTORY build)
file(COPY ${bin_rep} ${elf_file} ${hex_file}  DESTINATION ${build_dir})
file(REMOVE ${bin_rep} ${elf_file} ${hex_file} )
