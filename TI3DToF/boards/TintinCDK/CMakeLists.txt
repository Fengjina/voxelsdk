add_library(tintincdk SHARED
  TintinCDKCamera.cpp
  TintinCDKCameraUVC.cpp
  TintinCDKCameraFactory.cpp
  TintinCDKDownloaderFactory.cpp
  TintinEEPROMDownloader.cpp
  ${COMMON_LIB_FILES}
)

set_voxel_library_output_directory(tintincdk)

generate_export_header(tintincdk
  EXPORT_FILE_NAME "SymbolExports.h"
  EXPORT_MACRO_NAME SYMBOL_EXPORT
)

target_link_libraries(tintincdk 
  ti3dtof voxel ${COMMON_LIBS}
)

install(TARGETS tintincdk
  LIBRARY DESTINATION lib/voxel COMPONENT ti3dtof
  ARCHIVE DESTINATION lib/voxel COMPONENT ti3dtof
  RUNTIME DESTINATION lib/voxel COMPONENT ti3dtof
)

list(APPEND CONF_FILES
  boards/TintinCDK/TintinCDKCamera.conf
  boards/TintinCDK/TintinCDKCameraLensOnly.conf
  boards/TintinCDK/TintinCDKCameraShortRange.conf
  boards/TintinCDK/TintinCDKCameraLongRange.conf
  boards/TintinCDK/TintinCDKCameraHighAmbient.conf
  boards/TintinCDK/TintinCDKCameraNoCalibration.conf
  boards/TintinCDK/TintinCDKCameraExtraLongRange.conf
  boards/TintinCDK/TintinCDKCameraPhaseOffset.bin
)

set(CONF_FILES "${CONF_FILES}" PARENT_SCOPE)

list(APPEND UDEV_FILES
  boards/TintinCDK/72-TintinCDK.rules
)

set(UDEV_FILES "${UDEV_FILES}" PARENT_SCOPE)

set_target_properties(tintincdk PROPERTIES 
                      VERSION ${VOXEL_VERSION} 
                      SOVERSION ${VOXEL_ABI_VERSION})

