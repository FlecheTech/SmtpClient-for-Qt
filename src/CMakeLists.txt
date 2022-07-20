cmake_minimum_required(VERSION 3.14)

project(SmtpMime2 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core Network CoreTools)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core Network CoreTools)

set(PROJECT_SOURCES
    emailaddress.cpp
    mimeattachment.cpp
    mimefile.cpp
    mimehtml.cpp
    mimeinlinefile.cpp
    mimemessage.cpp
    mimepart.cpp
    mimetext.cpp
    smtpclient.cpp
    quotedprintable.cpp
    mimemultipart.cpp
    mimecontentencoder.cpp
    mimebase64encoder.cpp
    mimeqpencoder.cpp
    mimeqpformatter.cpp
    mimebase64formatter.cpp
    mimecontentformatter.cpp
    emailaddress.h
    mimeattachment.h
    mimefile.h
    mimehtml.h
    mimeinlinefile.h
    mimemessage.h
    mimepart.h
    mimetext.h
    smtpclient.h
    SmtpMime
    quotedprintable.h
    mimemultipart.h
    smtpmime_global.h
    mimecontentencoder.h
    mimebase64encoder.h
    mimeqpencoder.h
    mimeqpformatter.h
    mimebase64formatter.h
    mimecontentformatter.h
    ../LICENSE
    ../README.md
)

add_definitions(
    -DSMTP_MIME_LIBRARY
)

if(${QT_VERSION_MAJOR} GREATER_EQUAL 6)
    qt_add_library(SmtpMime2
        MANUAL_FINALIZATION
        ${PROJECT_SOURCES}
    )
# Define target properties for Android with Qt 6 as:
#    set_property(TARGET SmtpMime2 APPEND PROPERTY QT_ANDROID_PACKAGE_SOURCE_DIR
#                 ${CMAKE_CURRENT_SOURCE_DIR}/android)
# For more information, see https://doc.qt.io/qt-6/qt-add-library.html#target-creation
else()
    if(ANDROID)
        add_library(SmtpMime2 SHARED
            ${PROJECT_SOURCES}
        )
# Define properties for Android with Qt 5 after find_package() calls as:
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
    else()
        add_library(SmtpMime2
            ${PROJECT_SOURCES}
        )
    endif()
endif()

target_link_libraries(SmtpMime2 PRIVATE Qt${QT_VERSION_MAJOR}::Core Qt${QT_VERSION_MAJOR}::Network)

if(QT_VERSION_MAJOR EQUAL 6)
    qt_finalize_target(SmtpMime2)
endif()
