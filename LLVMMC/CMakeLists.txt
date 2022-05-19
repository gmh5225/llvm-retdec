
cmake_minimum_required(VERSION 3.0.2)

project(LLVMMC)


set( SOURCE 
ConstantPools.cpp
  ELFObjectWriter.cpp
  MCAsmBackend.cpp
  MCAsmInfo.cpp
  MCAsmInfoCOFF.cpp
  MCAsmInfoDarwin.cpp
  MCAsmInfoELF.cpp
  MCAsmInfoWasm.cpp
  MCAsmMacro.cpp
  MCAsmStreamer.cpp
  MCAssembler.cpp
  MCCodeEmitter.cpp
  MCCodePadder.cpp
  MCCodeView.cpp
  MCContext.cpp
  MCDwarf.cpp
  MCELFObjectTargetWriter.cpp
  MCELFStreamer.cpp
  MCExpr.cpp
  MCFragment.cpp
  MCInst.cpp
  MCInstPrinter.cpp
  MCInstrAnalysis.cpp
  MCInstrDesc.cpp
  MCLabel.cpp
  MCLinkerOptimizationHint.cpp
  MCMachOStreamer.cpp
  MCMachObjectTargetWriter.cpp
  MCNullStreamer.cpp
  MCObjectFileInfo.cpp
  MCObjectStreamer.cpp
  MCObjectWriter.cpp
  MCRegisterInfo.cpp
  MCSchedule.cpp
  MCSection.cpp
  MCSectionCOFF.cpp
  MCSectionELF.cpp
  MCSectionMachO.cpp
  MCSectionWasm.cpp
  MCStreamer.cpp
  MCSubtargetInfo.cpp
  MCSymbol.cpp
  MCSymbolELF.cpp
  MCTargetOptions.cpp
  MCValue.cpp
  MCWasmObjectTargetWriter.cpp
  MCWasmStreamer.cpp
  MCWin64EH.cpp
  MCWinCOFFStreamer.cpp
  MCWinEH.cpp
  MachObjectWriter.cpp
  StringTableBuilder.cpp
  SubtargetFeature.cpp
  WasmObjectWriter.cpp
  WinCOFFObjectWriter.cpp

  

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


add_subdirectory(MCParser)
set_target_properties(LLVMMCParser PROPERTIES FOLDER "MC")

add_subdirectory(MCDisassembler)
set_target_properties(LLVMMCDisassembler PROPERTIES FOLDER "MC")


#链接静态库
target_link_libraries(${PROJECT_NAME} LLVMMCParser)
target_link_libraries(${PROJECT_NAME} LLVMMCDisassembler)