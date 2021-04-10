cmake_minimum_required(VERSION 3.16)

project(OctoPlayer8 
    VERSION 1.0.0)

add_subdirectory(Juce)

juce_add_gui_app(OctoPlayer8)

juce_generate_juce_header(OctoPlayer8)

target_sources(OctoPlayer8
    PRIVATE
        Source/Main.cpp
        Source/MainComponent.cpp)

target_compile_definitions(OctoPlayer8
    PRIVATE
        # JUCE_WEB_BROWSER and JUCE_USE_CURL would be on by default, but you might not need them.
        JUCE_WEB_BROWSER=0  # If you remove this, add `NEEDS_WEB_BROWSER TRUE` to the `juce_add_gui_app` call
        JUCE_USE_CURL=0     # If you remove this, add `NEEDS_CURL TRUE` to the `juce_add_gui_app` call
        JUCE_APPLICATION_NAME_STRING="$<TARGET_PROPERTY:OctoPlayer8,JUCE_PRODUCT_NAME>"
        JUCE_APPLICATION_VERSION_STRING="$<TARGET_PROPERTY:OctoPlayer8,JUCE_VERSION>")

# juce_add_binary_data(OctoPlayer8Data SOURCES ...)

target_link_libraries(OctoPlayer8
    PRIVATE
        # OctoPlayer8Data            # If we'd created a binary data target, we'd link to it here
        juce::juce_audio_basics
        juce::juce_audio_devices
        juce::juce_audio_formats
        juce::juce_audio_processors
        juce::juce_audio_utils
        juce::juce_core
        juce::juce_data_structures
        juce::juce_events
        juce::juce_graphics
        juce::juce_gui_basics
        juce::juce_gui_extra
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags)
