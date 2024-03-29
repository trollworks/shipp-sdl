cmake_minimum_required(VERSION 3.22)
project(SDL2)

set(BUILD_SHARED_LIBS OFF)
set(BUILD_STATIC_LIBS ON)

set(CMAKE_POLICY_DEFAULT_CMP0077 "NEW")

function(assert VAR)
  if(NOT ${VAR})
    message(FATAL_ERROR "\nAssertion failed: ${VAR} (value is '${${VAR}})\n")
  endif()
endfunction()

find_package(OpenGL REQUIRED)

set(SDL_SHARED OFF)
set(SDL_STATIC ON)
set(SDL_TEST OFF)

set(SDL2_DISABLE_INSTALL OFF)
set(SDL2_DISABLE_UNINSTALL ON)

add_subdirectory(upstream)

get_directory_property(HAVE_SDL_AUDIO
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/upstream"
  DEFINITION HAVE_SDL_AUDIO
)
get_directory_property(HAVE_SDL_VIDEO
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/upstream"
  DEFINITION HAVE_SDL_VIDEO
)
get_directory_property(HAVE_SDL_TIMERS
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/upstream"
  DEFINITION HAVE_SDL_TIMERS
)
get_directory_property(HAVE_SDL_THREADS
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/upstream"
  DEFINITION HAVE_SDL_THREADS
)
get_directory_property(HAVE_SDL_FILESYSTEM
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/upstream"
  DEFINITION HAVE_SDL_FILESYSTEM
)

assert(HAVE_SDL_AUDIO)
assert(HAVE_SDL_VIDEO)
assert(HAVE_SDL_TIMERS)
assert(HAVE_SDL_THREADS)
assert(HAVE_SDL_FILESYSTEM)

