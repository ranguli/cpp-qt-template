find_package(Qt6 REQUIRED COMPONENTS Quick)

qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable(my_app_template
    main.cpp
)

qt_add_qml_module(MyAppTemplateControls
    URI MyAppTemplate.Controls
    VERSION 1.0
    QML_FILES
        ui/qml/MyAppTemplate/Controls/TextButton.qml
    OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/MyAppTemplate/Controls
)

qt_add_qml_module(MyAppTemplateLauncher
    URI MyAppTemplate.Launcher
    VERSION 1.0
    QML_FILES
        ui/qml/MyAppTemplate/Launcher/Launcher.qml
    OUTPUT_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/MyAppTemplate/Launcher
)


# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(my_app_template PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.MyAppTemplate
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(my_app_template
    PRIVATE Qt6::Quick
            MyAppTemplateControls
            MyAppTemplateLauncher
)

include(GNUInstallDirs)
install(TARGETS my_app_template
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

