# ============================================================================
#
# This file hosts all tests.
#
# If INCLUDE_PILE_SOURCES_DIRECTLY is ON then PROGRESS_SOURCES and
# PROGRESS_HEADERS are defined we add them to the executable. PROGRESS_LIBRARY
# is empty.
#
# On the other hand if INCLUDE_PILE_SOURCES_DIRECTLY is
# OFF then PROGRESS_SOURCES and PROGRESS_HEADERS are empty and we link
# against PROGRESS_LIBRARY that is now the name of the target that
# builds the library.
#
# ============================================================================

find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

if (NOT INCLUDE_PILE_SOURCES_DIRECTLY)
    set (PROGRESS_LIBRARY progress)
endif()

add_executable(test_basic
    ${PROGRESS_SOURCES}
    ${PROGRESS_HEADERS}
    basic.cc)

target_link_libraries(test_basic
    ${GTEST_BOTH_LIBRARIES}
    ${PROGRESS_LIBRARY})

add_test(
    NAME test_basic
    COMMAND $<TARGET_FILE:test_basic>)
