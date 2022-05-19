
cmake_minimum_required(VERSION 3.0.2)

project(LLVMDebugInfoCodeView)


set( SOURCE 
AppendingTypeTableBuilder.cpp
  CodeViewError.cpp
  CodeViewRecordIO.cpp
  ContinuationRecordBuilder.cpp
  CVSymbolVisitor.cpp
  CVTypeVisitor.cpp
  DebugChecksumsSubsection.cpp
  DebugCrossExSubsection.cpp
  DebugCrossImpSubsection.cpp
  DebugFrameDataSubsection.cpp
  DebugInlineeLinesSubsection.cpp
  DebugLinesSubsection.cpp
  DebugStringTableSubsection.cpp
  DebugSubsection.cpp
  DebugSubsectionRecord.cpp
  DebugSubsectionVisitor.cpp
  DebugSymbolRVASubsection.cpp
  DebugSymbolsSubsection.cpp
  EnumTables.cpp
  Formatters.cpp
  GlobalTypeTableBuilder.cpp
  LazyRandomTypeCollection.cpp
  Line.cpp
  MergingTypeTableBuilder.cpp
  RecordName.cpp
  RecordSerialization.cpp
  SimpleTypeSerializer.cpp
  StringsAndChecksums.cpp
  SymbolDumper.cpp
  SymbolRecordHelpers.cpp
  SymbolRecordMapping.cpp
  SymbolSerializer.cpp
  TypeDumpVisitor.cpp
  TypeIndex.cpp
  TypeIndexDiscovery.cpp
  TypeHashing.cpp
  TypeRecordHelpers.cpp
  TypeRecordMapping.cpp
  TypeStreamMerger.cpp
  TypeTableCollection.cpp

  

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
include_directories(${CMAKE_SOURCE_DIR}/include/DebugInfo/CodeView)

#静态库
add_library(${PROJECT_NAME} STATIC ${SOURCE} )
