add_library(
  sqlpp11-connector-sqlite3
  connection.cpp
  bind_result.cpp
  prepared_statement.cpp
  detail/connection_handle.cpp
  )

find_package(Threads)

target_link_libraries(
  sqlpp11-connector-sqlite3
  PUBLIC
  sqlpp11
  sqlite3
  Threads::Threads
  $<$<PLATFORM_ID:Linux>:dl>
  )
target_include_directories(
  sqlpp11-connector-sqlite3
  PRIVATE
  ${PROJECT_SOURCE_DIR}/include
  )
target_compile_options(
  sqlpp11-connector-sqlite3
  PRIVATE
  $<$<PLATFORM_ID:Windows>:$<$<CONFIG:Debug>:/MTd>>
  $<$<PLATFORM_ID:Windows>:$<$<CONFIG:Release>:/MT>>
  )

install(TARGETS sqlpp11-connector-sqlite3 DESTINATION lib)
