
cmake_minimum_required(VERSION 3.0.2)

project(LLVMTransformsUtils)


set( SOURCE 

ASanStackFrameLayout.cpp
AddDiscriminators.cpp
BasicBlockUtils.cpp
BreakCriticalEdges.cpp
BuildLibCalls.cpp
BypassSlowDivision.cpp
CallPromotionUtils.cpp
CanonicalizeAliases.cpp
CloneFunction.cpp
CloneModule.cpp
CodeExtractor.cpp
CtorUtils.cpp
DemoteRegToStack.cpp
EntryExitInstrumenter.cpp
EscapeEnumerator.cpp
Evaluator.cpp
FlattenCFG.cpp
FunctionComparator.cpp
FunctionImportUtils.cpp
GlobalStatus.cpp
GuardUtils.cpp
InlineFunction.cpp
ImportedFunctionsInliningStatistics.cpp
InstructionNamer.cpp
IntegerDivision.cpp
LCSSA.cpp
LibCallsShrinkWrap.cpp
Local.cpp
LoopRotationUtils.cpp
LoopSimplify.cpp
LoopUnroll.cpp
LoopUnrollAndJam.cpp
LoopUnrollPeel.cpp
LoopUnrollRuntime.cpp
LoopUtils.cpp
LoopVersioning.cpp
LowerInvoke.cpp
LowerMemIntrinsics.cpp
LowerSwitch.cpp
Mem2Reg.cpp
MetaRenamer.cpp
ModuleUtils.cpp
NameAnonGlobals.cpp
PredicateInfo.cpp
PromoteMemoryToRegister.cpp
StripGCRelocates.cpp
SSAUpdater.cpp
SSAUpdaterBulk.cpp
SanitizerStats.cpp
SimplifyCFG.cpp
SimplifyIndVar.cpp
SimplifyLibCalls.cpp
SplitModule.cpp
StripNonLineTableDebugInfo.cpp
SymbolRewriter.cpp
UnifyFunctionExitNodes.cpp
Utils.cpp
ValueMapper.cpp
VNCoercion.cpp
  

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