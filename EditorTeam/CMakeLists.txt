cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

project(THare VERSION 0.2 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_custom_target(copy_arch_debug ALL
    COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/arch ${CMAKE_CURRENT_BINARY_DIR}/arch
)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Widgets PrintSupport)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Widgets PrintSupport)
find_package(Qt6 REQUIRED COMPONENTS LinguistTools)

set(PROJECT_SOURCES
        main.cpp
        mainwindow.cpp
        mainwindow.h
        mainwindow.ui
        helpbrowser.cpp
        helpbrowser.h
        const_strings.h
        idevhandler.h
        filehandler.h
        filehandler.cpp
        settingskeeper.cpp
        settingskeeper.h
        searchform.h
        searchform.cpp
        searchhighlight.h
        searchhighlight.cpp
)

set(TS_SRC_FILES
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/l10n_en.ts
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/l10n_ru.ts
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/qtmultimedia_ru.ts
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/qtbase_ru.ts
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/qt_ru.ts)

set(QM_FILES
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/l10n_en.qm
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/l10n_ru.qm
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/qtmultimedia_ru.qm
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/qtbase_ru.qm
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation/qt_ru.qm)

set(RESOURCES 
	${CMAKE_CURRENT_SOURCE_DIR}/resources/resources.qrc)

set_source_files_properties(${TS_SRC_FILES}
    PROPERTIES OUTPUT_LOCATION
        ${CMAKE_CURRENT_SOURCE_DIR}/resources/translation)

set(APP_NAME THare)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)

    if(UNIX)
            qt_add_executable(
                ${APP_NAME}
                MANUAL_FINALIZATION
                ${PROJECT_SOURCES}
                ${RESOURCES}
            )
    else()
            qt_add_executable(
                ${APP_NAME}
                WIN32
                MANUAL_FINALIZATION
                ${PROJECT_SOURCES}
                ${RESOURCES}
            )
    endif(UNIX)

else()
    message(FATAL_ERROR "THare supports QT6 only.")
endif()

qt_add_lrelease(${APP_NAME}
    TS_FILES ${TS_SRC_FILES} )

add_custom_command(
        TARGET ${APP_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E remove -f
        ${QM_FILES}
    )

target_link_libraries(${APP_NAME} PRIVATE Qt${QT_VERSION_MAJOR}::Widgets Qt${QT_VERSION_MAJOR}::PrintSupport)

install(TARGETS ${EXE_NAME}
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_executable(${APP_NAME})
endif()
