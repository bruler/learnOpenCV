# Copyright 2017 Kapil Gupta
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.2)
PROJECT(objecttracking)
find_package(OpenCV 3.2 REQUIRED )

set( NAME_SRC
    tracker.cpp
)

# settings
set(CMAKE_CXX_FLAGS "-std=c++11 -O3 -Wall -Wextra -Wuninitialized")
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)

INCLUDE_DIRECTORIES( ${CMAKE_CURRENT_SOURCE_DIR}/include )
link_directories( ${CMAKE_BINARY_DIR}/bin)
add_executable( ${CMAKE_PROJECT_NAME} ${NAME_SRC} ${NAME_HEADERS} )
target_link_libraries( ${CMAKE_PROJECT_NAME} ${OpenCV_LIBS} )