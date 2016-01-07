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

install(TARGETS sqlpp11-connector-sqlite3 DESTINATION lib)
