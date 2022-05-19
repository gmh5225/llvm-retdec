
cmake_minimum_required(VERSION 3.0.2)

project(LLVMScalarOpts)


set( SOURCE 
ADCE.cpp
  AlignmentFromAssumptions.cpp
  BDCE.cpp
  CallSiteSplitting.cpp
  ConstantHoisting.cpp
  ConstantProp.cpp
  CorrelatedValuePropagation.cpp
  DCE.cpp
  DeadStoreElimination.cpp
  DivRemPairs.cpp
  EarlyCSE.cpp
  FlattenCFGPass.cpp
  Float2Int.cpp
  GuardWidening.cpp
  GVN.cpp
  GVNHoist.cpp
  GVNSink.cpp
  IVUsersPrinter.cpp
  InductiveRangeCheckElimination.cpp
  IndVarSimplify.cpp
  InferAddressSpaces.cpp
  InstSimplifyPass.cpp
  JumpThreading.cpp
  LICM.cpp
  LoopAccessAnalysisPrinter.cpp
  LoopSink.cpp
  LoopDeletion.cpp
  LoopDataPrefetch.cpp
  LoopDistribute.cpp
  LoopIdiomRecognize.cpp
  LoopInstSimplify.cpp
  LoopInterchange.cpp
  LoopLoadElimination.cpp
  LoopPassManager.cpp
  LoopPredication.cpp
  LoopRerollPass.cpp
  LoopRotation.cpp
  LoopSimplifyCFG.cpp
  LoopStrengthReduce.cpp
  LoopUnrollPass.cpp
  LoopUnrollAndJamPass.cpp
  LoopUnswitch.cpp
  LoopVersioningLICM.cpp
  LowerAtomic.cpp
  LowerExpectIntrinsic.cpp
  LowerGuardIntrinsic.cpp
  MakeGuardsExplicit.cpp
  MemCpyOptimizer.cpp
  MergeICmps.cpp
  MergedLoadStoreMotion.cpp
  NaryReassociate.cpp
  NewGVN.cpp
  PartiallyInlineLibCalls.cpp
  PlaceSafepoints.cpp
  Reassociate.cpp
  Reg2Mem.cpp
  RewriteStatepointsForGC.cpp
  SCCP.cpp
  SROA.cpp
  Scalar.cpp
  Scalarizer.cpp
  SeparateConstOffsetFromGEP.cpp
  SimpleLoopUnswitch.cpp
  SimplifyCFGPass.cpp
  Sink.cpp
  SpeculativeExecution.cpp
  SpeculateAroundPHIs.cpp
  StraightLineStrengthReduce.cpp
  StructurizeCFG.cpp
  TailRecursionElimination.cpp
  WarnMissedTransforms.cpp
  

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


