# Copyright (C) 2008-2016 TrinityCore <http://www.trinitycore.org/>
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

# Enable precompiled headers when using the GCC compiler.

message(STATUS "SCRIPT PREPARATIONS")

macro(PrepareScripts name out)
  file(GLOB_RECURSE found
    ${name}/*.h
    ${name}/*.cpp
  )
  list(APPEND ${out} ${found})
  message(STATUS "  -> Prepared: ${name}")
endmacro(PrepareScripts)

PrepareScripts(Spells PRIVATE_SOURCES)
PrepareScripts(Commands PRIVATE_SOURCES)

if(SCRIPTS)
<<<<<<< HEAD
  PrepareScripts(Custom scripts_STAT_SRCS)
  PrepareScripts(World scripts_STAT_SRCS)
  PrepareScripts(OutdoorPvP scripts_STAT_SRCS)
  PrepareScripts(EasternKingdoms scripts_STAT_SRCS)
  PrepareScripts(Kalimdor scripts_STAT_SRCS)
  PrepareScripts(Outland scripts_STAT_SRCS)
  PrepareScripts(Northrend scripts_STAT_SRCS)
  PrepareScripts(Maelstrom scripts_STAT_SRCS)
  PrepareScripts(Pandaria scripts_STAT_SRCS)
  PrepareScripts(Draenor scripts_STAT_SRCS)
  PrepareScripts(Events scripts_STAT_SRCS)
  PrepareScripts(Pet scripts_STAT_SRCS)
=======
  PrepareScripts(Custom PRIVATE_SOURCES)
  PrepareScripts(World PRIVATE_SOURCES)
  PrepareScripts(OutdoorPvP PRIVATE_SOURCES)
  PrepareScripts(EasternKingdoms PRIVATE_SOURCES)
  PrepareScripts(Kalimdor PRIVATE_SOURCES)
  PrepareScripts(Outland PRIVATE_SOURCES)
  PrepareScripts(Northrend PRIVATE_SOURCES)
  PrepareScripts(Maelstrom PRIVATE_SOURCES)
  PrepareScripts(Events PRIVATE_SOURCES)
  PrepareScripts(Pet PRIVATE_SOURCES)
>>>>>>> upstream/6.x
endif()

message(STATUS "SCRIPT PREPARATION COMPLETE")
message("")

list(APPEND PRIVATE_SOURCES
  ${CMAKE_CURRENT_SOURCE_DIR}/ScriptLoader.h
  ${CMAKE_CURRENT_SOURCE_DIR}/ScriptLoader.cpp)

if (USE_SCRIPTPCH)
  set(PRIVATE_PCH_HEADER PrecompiledHeaders/ScriptPCH.h)
  set(PRIVATE_PCH_SOURCE PrecompiledHeaders/ScriptPCH.cpp)
endif ()

GroupSources(${CMAKE_CURRENT_SOURCE_DIR})

add_library(scripts
  ${PRIVATE_SOURCES}
  ${PRIVATE_PCH_SOURCE}
)

target_include_directories(scripts
  PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
  PRIVATE
    ${CMAKE_CURRENT_BINARY_DIR})

target_link_libraries(scripts
  PUBLIC
    game)

set_target_properties(scripts
    PROPERTIES
      FOLDER
        "server")

# Generate precompiled header
if (USE_SCRIPTPCH)
  add_cxx_pch(scripts ${PRIVATE_PCH_HEADER} ${PRIVATE_PCH_SOURCE})
endif()
