
cmake_minimum_required(VERSION 3.0.2)

project(LLVMIPO)


set( SOURCE 
AlwaysInliner.cpp
ArgumentPromotion.cpp
BarrierNoopPass.cpp
BlockExtractor.cpp
CalledValuePropagation.cpp
ConstantMerge.cpp
CrossDSOCFI.cpp
DeadArgumentElimination.cpp
ElimAvailExtern.cpp
ExtractGV.cpp
ForceFunctionAttrs.cpp
FunctionAttrs.cpp
FunctionImport.cpp
GlobalDCE.cpp
GlobalOpt.cpp
GlobalSplit.cpp
HotColdSplitting.cpp
IPConstantPropagation.cpp
IPO.cpp
InferFunctionAttrs.cpp
InlineSimple.cpp
Inliner.cpp
Internalize.cpp
LoopExtractor.cpp
LowerTypeTests.cpp
MergeFunctions.cpp
PartialInlining.cpp
PassManagerBuilder.cpp
PruneEH.cpp
#  SampleProfile.cpp
SCCP.cpp
StripDeadPrototypes.cpp
StripSymbols.cpp
SyntheticCountsPropagation.cpp
ThinLTOBitcodeWriter.cpp
WholeProgramDevirt.cpp

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

#链接静态库
target_link_libraries(${PROJECT_NAME} LLVMAnalysis)
target_link_libraries(${PROJECT_NAME} LLVMIRReader)