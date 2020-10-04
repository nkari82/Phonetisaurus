cmake_minimum_required(VERSION 3.10.2)

project(phonetisaurus)

cmake_host_system_information(RESULT _os QUERY OS_NAME)
cmake_host_system_information(RESULT _platform QUERY OS_PLATFORM)

message(STATUS "OS: " ${_os})
message(STATUS "Platform: " ${_platform})

find_path(OPENFST_INCLUDE_DIRS NAMES fst/fstlib.h paths {proper-location})

add_library(phonetisaurus STATIC
			src/lib/LatticePruner.cc
			src/lib/M2MFstAligner.cc
			src/lib/util.cc)
		
target_include_directories(phonetisaurus PUBLIC src
	PRIVATE src/3rdparty/utfcpp
	PRIVATE ${OPENFST_INCLUDE_DIRS})