set(SRC_FILES
        src/main.cpp
        src/mainwindow.cpp
        src/mainwindow.ui
        src/offboard_thread.cpp
)

set(HEADER_FILES
        include/mainwindow.h
        include/offboard_thread.h
)


add_executable(mavsdk_gui_interface
${HEADER_FILES}
${SRC_FILES}
)

target_include_directories(mavsdk_gui_interface PUBLIC include)

# QT depenencies
target_link_libraries(mavsdk_gui_interface PRIVATE 
Qt${QT_VERSION_MAJOR}::Widgets 
)

# mavsdk dependencies
target_link_libraries(mavsdk_gui_interface PRIVATE 
    MAVSDK::mavsdk_telemetry
    MAVSDK::mavsdk_action
    MAVSDK::mavsdk_offboard
    MAVSDK::mavsdk
)


# Other dependencies
target_link_libraries(mavsdk_gui_interface PRIVATE 
comm_lib
)


set_target_properties(mavsdk_gui_interface PROPERTIES
    MACOSX_BUNDLE_GUI_IDENTIFIER my.example.com
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
)
