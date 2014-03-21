
cmake_minimum_required(VERSION 2.8.12)

project(CommeFont)

find_package(ECM 0.0.11 REQUIRED NO_MODULE)

set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})

include(KDEInstallDirs)
include(ECMPackageConfigHelpers)
include(ECMSetupVersion)
include(FeatureSummary)


# create a Config.cmake and a ConfigVersion.cmake file and install them
set(CMAKECONFIG_INSTALL_DIR "${CMAKECONFIG_INSTALL_PREFIX}/CommeFont")

include(ECMPackageConfigHelpers)


ecm_setup_version(1.0 VARIABLE_PREFIX COMMEFONT
                  PACKAGE_VERSION_FILE "${CMAKE_CURRENT_BINARY_DIR}/CommeFontConfigVersion.cmake"
)

ecm_configure_package_config_file("${CMAKE_CURRENT_SOURCE_DIR}/CommeFontConfig.cmake.in"
                                  "${CMAKE_CURRENT_BINARY_DIR}/CommeFontConfig.cmake"
                                  INSTALL_DESTINATION  ${CMAKECONFIG_INSTALL_DIR}
)

install(FILES
        "${CMAKE_CURRENT_BINARY_DIR}/CommeFontConfig.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/CommeFontConfigVersion.cmake"
        DESTINATION "${CMAKECONFIG_INSTALL_DIR}"
        COMPONENT Devel)

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)

set(COMME_FONT_INSTALL_DIR  ${CMAKE_INSTALL_PREFIX}/${SHARE_INSTALL_PREFIX}/fonts/comme)
set(VERSION_PATH "version-1.0")
FILE(GLOB fontFiles "${CMAKE_CURRENT_SOURCE_DIR}/${VERSION_PATH}/*.ttf")

install(FILES ${fontFiles} DESTINATION ${COMME_FONT_INSTALL_DIR})
