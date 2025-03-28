find_package(GTest REQUIRED)

add_executable(test_smoke
  test_smoke.cpp
)

target_link_libraries(test_smoke
  PRIVATE GTest::gtest_main
)

include(GoogleTest)
gtest_discover_tests(test_smoke)
