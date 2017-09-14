cmake_minimum_required (VERSION 3.0)

project( mulle-objc-templates)

execute_process( COMMAND cat VERSION
                 WORKING_DIRECTORY "${PROJECT_SOURCE_DIR}"
                 OUTPUT_VARIABLE MULLE_OBJC_TEMPLATES_VERSION
                 OUTPUT_STRIP_TRAILING_WHITESPACE)
message( STATUS "MULLE_OBJC_TEMPLATES_VERSION is ${MULLE_OBJC_TEMPLATES_VERSION} according to VERSION")

set( PROJECT_VERSION "${MULLE_OBJC_TEMPLATES_VERSION}")
set( PUBLISHER "mulle-nat")

set( SCRIPTS
mulle-get-publisher
mulle-change-publisher
mulle-change-tap
mulle-templates-create
mulle-templates-print
)


INSTALL( FILES ${SCRIPTS}
PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ
            GROUP_EXECUTE GROUP_READ
            WORLD_EXECUTE WORLD_READ
DESTINATION "bin")

#
# Primarily used for packaging on Linux
#
# Debian:
#
# ```
# mkdir package
# cd package
# cmake ..
# cpack -G DEB
# ```
#


#
# CPack and project specific stuff
#
######

set( CPACK_PACKAGE_NAME "${PROJECT_NAME}")
set( CPACK_PACKAGE_VERSION "${PROJECT_VERSION}")
set( CPACK_PACKAGE_CONTACT "Nat! <nat@mulle-kybernetik.de>")
set( CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_SOURCE_DIR}/README.md")
set( CPACK_PACKAGE_DESCRIPTION_SUMMARY "🎁 Template management tools for mulle-objc")
set( CPACK_RESOURCE_FILE_LICENSE "${CMAKE_SOURCE_DIR}/LICENSE")
set( CPACK_STRIP_FILES false)

# stuff needed for Debian
# memo: its impossible to check for chosen generator here
#
# CPackDeb doesn't produce 100% proper debian file unfortunately
#
set( CPACK_DEBIAN_PACKAGE_HOMEPAGE "https://github.com/${PUBLISHER}/${PROJECT_NAME}")

# not strictly required
set( CPACK_DEBIAN_PACKAGE_DEPENDS "mulle-scion (>= 1858.0)")

# stuff needed for RPM

set( CPACK_RPM_PACKAGE_VENDOR "Mulle kybernetiK")

######
#
# must be after CPACK_PACKAGE_VERSION
include( CPack)
