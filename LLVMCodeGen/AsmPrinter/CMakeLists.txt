
  cmake_minimum_required(VERSION 3.0.2)
  
  project(LLVMAsmPrinter)

  set( SOURCE 
    AccelTable.cpp
  AddressPool.cpp
  ARMException.cpp
  AsmPrinter.cpp
  AsmPrinterDwarf.cpp
  AsmPrinterInlineAsm.cpp
  DbgEntityHistoryCalculator.cpp
  DebugHandlerBase.cpp
  DebugLocStream.cpp
  DIE.cpp
  DIEHash.cpp
  DwarfCFIException.cpp
  DwarfCompileUnit.cpp
  DwarfDebug.cpp
  DwarfExpression.cpp
  DwarfFile.cpp
  DwarfStringPool.cpp
  DwarfUnit.cpp
  EHStreamer.cpp
  ErlangGCPrinter.cpp
  OcamlGCPrinter.cpp
  WinCFGuard.cpp
  WinException.cpp
  CodeViewDebug.cpp
  WasmException.cpp
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
  include_directories(${CMAKE_SOURCE_DIR}/LLVMTarget/X86)

  #静态库
  add_library(${PROJECT_NAME} STATIC ${SOURCE} )

  #链接静态库
target_link_libraries(${PROJECT_NAME} LLVMDebugInfoCodeView)