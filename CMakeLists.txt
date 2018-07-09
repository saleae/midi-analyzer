cmake_minimum_required (VERSION 3.11)
project(midi_analyzer)

# custom CMake Modules are located in the cmake directory.
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

include(ExternalAnalyzerSDK)

set(SOURCES 
src/MidiAnalyzer.cpp
src/MidiAnalyzer.h
src/MidiAnalyzerResults.cpp
src/MidiAnalyzerResults.h
src/MidiAnalyzerSettings.cpp
src/MidiAnalyzerSettings.h
src/MidiSimulationDataGenerator.cpp
src/MidiSimulationDataGenerator.h
)

add_library(midi_analyzer SHARED ${SOURCES})
target_link_libraries(midi_analyzer PRIVATE Saleae::AnalyzerSDK)

if(MSVC)
    install(TARGETS midi_analyzer RUNTIME DESTINATION "Analyzers")
else()
    install(TARGETS midi_analyzer LIBRARY DESTINATION "Analyzers")
endif()

set_post_build_destination(midi_analyzer)
