cmake_minimum_required(VERSION 3.22)
project(Snake_effect)


#find toolchain program
find_program(AVR-GCC avr-gcc)
set(CMAKE_C_COMPILER ${AVR-GCC})
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -mmcu=atmega32")

set(source MDIO_Prg.c )
set(lib_source MDIO_Prg.o )
set(out libMDIO.a)
set(lib_command  ar rcs)

execute_process(COMMAND ${lib_command} ${out} ${lib_source})
execute_process(COMMAND avr-gcc  ${source} -o ${lib_source} )
execute_process(COMMAND echo "static library  generated")

#set(out libMDIO)
#set(Lib_source MDIO_Prg.c )
#add_library(libMDIO STATIC ${Lib_source})
#target_include_directories(${out} PUBLIC ./ )
