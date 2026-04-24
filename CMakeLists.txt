cmake_minimum_required(VERSION 3.19)
project(QT_SmartHomeControlCenter LANGUAGES CXX)

find_package(Qt6 6.5 REQUIRED COMPONENTS Core Widgets)

qt_standard_project_setup()

set(CMAKE_AUTOUIC_SEARCH_PATHS
    ${CMAKE_CURRENT_SOURCE_DIR}/forms
)

qt_add_executable(QT_SmartHomeControlCenter
    WIN32 MACOSX_BUNDLE
    src/main.cpp
    src/mainwindow.cpp
    headers/mainwindow.h
    forms/mainwindow.ui
)

target_include_directories(QT_SmartHomeControlCenter
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/headers
        ${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(QT_SmartHomeControlCenter
    PRIVATE
        Qt::Core
        Qt::Widgets
)

install(TARGETS QT_SmartHomeControlCenter
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET QT_SmartHomeControlCenter
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
