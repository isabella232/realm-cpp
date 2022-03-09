set(SOURCES
    sdk.cpp
    object.cpp
) # REALM_SOURCES

set(HEADERS
    sdk.hpp
    app.hpp
    db.hpp
    notifications.hpp
    object.hpp
    persisted.hpp
    results.hpp
    schema.hpp
    task.hpp
    thread_safe_reference.hpp
    type_info.hpp
) # REALM_INSTALL_HEADERS

add_library(cpprealm STATIC ${SOURCES} ${HEADERS})
set_target_properties(cpprealm PROPERTIES
    PUBLIC_HEADER "${HEADERS}"
)

# Let consuming targets always have the realmcpp headers folder in their header search path
target_include_directories(cpprealm INTERFACE
    $<BUILD_INTERFACE:${cpprealm_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

target_link_libraries(cpprealm PUBLIC Realm::ObjectStore curl)

if(CMAKE_COMPILER_IS_GNUCXX AND CMAKE_CXX_COMPILER_VERSION VERSION_GREATER_EQUAL 10 AND CMAKE_CXX_COMPILER_VERSION VERSION_LESS 11)
    target_compile_options(cpprealm PUBLIC -fcoroutines)
endif()

install(TARGETS cpprealm
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/cpprealm
)
