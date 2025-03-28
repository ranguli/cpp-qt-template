find_package(Qt6 REQUIRED COMPONENTS Quick)

qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable(shalrath
    main.cpp
)

qt_add_qml_module(ShalrathControls
    URI Shalrath.Controls
    VERSION 1.0
    QML_FILES
        ui/qml/Shalrath/Controls/TextButton.qml
    OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/Shalrath/Controls
)

qt_add_qml_module(ShalrathLauncher
    URI Shalrath.Launcher
    VERSION 1.0
    QML_FILES
        ui/qml/Shalrath/Launcher/Launcher.qml
    OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/Shalrath/Launcher
)


# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(shalrath PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.Shalrath
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(shalrath
    PRIVATE Qt6::Quick
            ShalrathControls
            ShalrathLauncher
)

include(GNUInstallDirs)
install(TARGETS shalrath
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

