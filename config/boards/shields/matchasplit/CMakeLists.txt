# Unified CMakeLists.txt for MatchaSplit Shields (Left & Right)

message("Building MatchaSplit Shield")

# Include the necessary ZMK modules for keymap and matrix transformation
target_sources(app PRIVATE
    src/keymap.c
    src/matrix_transform.c
)

# Set the board name and shield type based on the selected SHIELD variable
if(NOT DEFINED SHIELD)
    message(FATAL_ERROR "SHIELD must be defined (either 'matchasplit_left' or 'matchasplit_right')")
endif()

# Set shield-specific variables based on the selected shield
if(SHIELD STREQUAL "matchasplit_left")
    set(SHIELD_NAME "matchasplit_left")
    set(DTC_OVERLAY_FILE "${CMAKE_CURRENT_LIST_DIR}/matchasplit_left.overlay")
elseif(SHIELD STREQUAL "matchasplit_right")
    set(SHIELD_NAME "matchasplit_right")
    set(DTC_OVERLAY_FILE "${CMAKE_CURRENT_LIST_DIR}/matchasplit_right.overlay")
else()
    message(FATAL_ERROR "Unknown shield specified: ${SHIELD}")
endif()

# Ensure Zephyr is included
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# Add the current shield directory to the include path
zephyr_include_directories(${CMAKE_CURRENT_LIST_DIR})

# Print confirmation
message("${SHIELD_NAME} shield configured successfully")
