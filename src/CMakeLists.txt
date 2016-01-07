add_library(
  sqlpp11-connector-sqlite3
  connection.cpp
  bind_result.cpp
  prepared_statement.cpp
  detail/connection_handle.cpp
  )

if(NOT EXISTS ${SQLITE_INCLUDE_DIR}/sqlite3.h)
  message(SEND_ERROR "Can't find sqlite3.h. Set the variable SQLITE_INCLUDE_DIR to the absolute path to the directory containing sqlite3.h")
endif()

target_include_directories(
  sqlpp11-connector-sqlite3
  PUBLIC
  ${SQLITE_INCLUDE_DIR}
  )

find_library(
  SQLITE_LIBRARIES
  sqlite3
  HINTS "${SQLITE_INCLUDE_DIR}/../"
  PATH_SUFFIXES "lib" "lib/Debug" "lib/Release"
  )

target_link_libraries(
  sqlpp11-connector-sqlite3
  PUBLIC
  ${SQLITE_LIBRARIES}
  )

message(STATUS "SQLITE_LIBRARIES: ${SQLITE_LIBRARIES}")
install(TARGETS sqlpp11-connector-sqlite3 DESTINATION lib)
