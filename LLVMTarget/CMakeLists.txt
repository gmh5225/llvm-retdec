
cmake_minimum_required(VERSION 3.0.2)

project(LLVMTarget)


set( SOURCE 
Target.cpp
TargetIntrinsicInfo.cpp
TargetLoweringObjectFile.cpp
TargetMachine.cpp
TargetMachineC.cpp

)

set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -D_RELEASE=1") 
set(CMAKE_CXX_FLAGS_MINSIZEREL "${CMAKE_CXX_FLAGS_MINSIZEREL} -D_MINSIZEREL=1") 
set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "${CMAKE_CXX_FLAGS_RELWITHDEBINFO} -D_RELWITHDEBINFO=1" ) 

set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -D_RELEASE=1") 
set(CMAKE_C_FLAGS_MINSIZEREL "${CMAKE_C_FLAGS_MINSIZEREL} -D_MINSIZEREL=1") 
set(CMAKE_C_FLAGS_RELWITHDEBINFO "${CMAKE_C_FLAGS_RELWITHDEBINFO} -D_RELWITHDEBINFO=1" )


#Tools Exe类的Release模式禁用优化，方便调试
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /Od") 
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /ZI") 

#Tools Exe类的Release模式禁用优化，方便调试
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /Od") 
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} /ZI") 


#set win32/win64
if(MSVC)
if(CMAKE_CL_64)
add_definitions(-DWIN64)
else()
add_definitions(-DWIN32)
endif()
endif()

#include
include_directories(${CMAKE_SOURCE_DIR}/include)

#静态库
add_library(${PROJECT_NAME} STATIC ${SOURCE} )

#X86架构后端
add_subdirectory(X86)
set_target_properties(LLVMX86CodeGen PROPERTIES FOLDER "X86")

#链接静态库
target_link_libraries(${PROJECT_NAME} LLVMCodeGen)
target_link_libraries(${PROJECT_NAME} LLVMProfileData)
target_link_libraries(${PROJECT_NAME} LLVMX86CodeGen)
