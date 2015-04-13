add_definitions(${COLLADA_CFLAGS_OTHER})
add_definitions(-DNO_BOOST)
include_directories(${COLLADA_INCLUDE_DIRS})
link_directories(${COLLADA_LIBRARY_DIRS})
set(OSG_PLUGINS osgPlugins-${OSG_VERSION})
set(TARGET_DEFAULT_PREFIX osgdb_)
set(COLLADA_USE_STATIC OFF)
set(DYNAMIC_OPENSCENEGRAPH TRUE)

SET(TARGET_SRC
    daeReader.cpp
    daeRAnimations.cpp
    daeRGeometry.cpp
    daeRMaterials.cpp
    daeRSceneObjects.cpp
    daeRSkinning.cpp
    daeRTransforms.cpp
    daeWAnimations.cpp
    daeWGeometry.cpp
    daeWMaterials.cpp
    daeWriter.cpp
    daeWSceneObjects.cpp
    daeWTransforms.cpp
    domSourceReader.cpp
    ReaderWriterDAE.cpp
)

SET(TARGET_H 
    daeReader.h
    daeWriter.h
    domSourceReader.h
    ReaderWriterDAE.h
)


IF(COLLADA_USE_STATIC)
    IF(WIN32)
        ADD_DEFINITIONS(-DBOOST_ALL_NO_LIB)
        SET(TARGET_LIBRARIES_VARS
            COLLADA_STATIC_LIBRARY
            COLLADA_LIBXML_LIBRARY
            COLLADA_ZLIB_LIBRARY
            COLLADA_PCRECPP_LIBRARY
            COLLADA_PCRE_LIBRARY
            COLLADA_MINIZIP_LIBRARY
            COLLADA_BOOST_FILESYSTEM_LIBRARY
            COLLADA_BOOST_SYSTEM_LIBRARY)
    ELSE()
        SET(TARGET_LIBRARIES_VARS
            COLLADA_STATIC_LIBRARY
            COLLADA_LIBXML_LIBRARY
            COLLADA_PCRECPP_LIBRARY
            COLLADA_PCRE_LIBRARY
            COLLADA_BOOST_FILESYSTEM_LIBRARY
            COLLADA_BOOST_SYSTEM_LIBRARY)
    ENDIF()
ELSE()
    IF(WIN32)
        ADD_DEFINITIONS(-DDOM_DYNAMIC)
        SET(TARGET_LIBRARIES_VARS COLLADA_DYNAMIC_LIBRARY)
    ELSE()
        SET(TARGET_LIBRARIES_VARS
                    COLLADA_DYNAMIC_LIBRARY
                    COLLADA_BOOST_FILESYSTEM_LIBRARY)
    ENDIF()

ENDIF()
 
SET(TARGET_ADDED_LIBRARIES osgSim osgAnimation) 

#### end var setup  ###
SETUP_PLUGIN(dae dae)
SET_TARGET_PROPERTIES(${TARGET_TARGETNAME} PROPERTIES PREFIX "")


