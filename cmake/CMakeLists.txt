# -----------------------------------------------------------------------------
# CannonBall CMake setup
#
# For ports, please try not to edit this file directly.
# Everything should go into a win64.cmake equivalent.
# -----------------------------------------------------------------------------

cmake_minimum_required (VERSION 3.18) # Might compile lower, but untested
project (cannonball)

# -----------------------------------------------------------------------------
# Directory Setup
# -----------------------------------------------------------------------------

# CMake files 
set(DCMAKE win64-opengl.cmake)
set(CMDIR ../cmake)

# Source location
set(main_cpp_base ../src/main)

# -----------------------------------------------------------------------------
# Platform Specific Setup
# -----------------------------------------------------------------------------

# Include relevant CMAKE file (default, mingw, pandora etc.)
if(TARGET)
    set(TCMAKE ${TARGET}.cmake)
    if(EXISTS ${CMDIR}/${TCMAKE})
        message("CMake files for ${TARGET} found, using ${TCMAKE}")
        include(${TCMAKE})
    else()
        message("CMake files for ${TARGET} not found, using ${DCMAKE}")
        include(${DCMAKE})
    endif()
else()
    message("TARGET not passed, using ${DCMAKE}")
    include(${DCMAKE})
endif(TARGET)

# -----------------------------------------------------------------------------
# Project Source Files
# -----------------------------------------------------------------------------
    
set(src_main
    "${main_cpp_base}/globals.hpp"
    "${main_cpp_base}/romloader.hpp"
    "${main_cpp_base}/roms.hpp"
    "${main_cpp_base}/trackloader.hpp"
    "${main_cpp_base}/setup.hpp"
    "${main_cpp_base}/stdint.hpp"
    "${main_cpp_base}/main.hpp"
    "${main_cpp_base}/video.hpp"
    "${main_cpp_base}/utils.hpp"

    "${main_cpp_base}/main.cpp"
    "${main_cpp_base}/romloader.cpp"
    "${main_cpp_base}/trackloader.cpp"
    "${main_cpp_base}/roms.cpp"
    "${main_cpp_base}/video.cpp"
    "${main_cpp_base}/utils.cpp"
    )

set(src_frontend
    "${main_cpp_base}/frontend/cabdiag.hpp"
    "${main_cpp_base}/frontend/config.hpp"
    "${main_cpp_base}/frontend/menu.hpp"
    "${main_cpp_base}/frontend/ttrial.hpp"

    "${main_cpp_base}/frontend/cabdiag.cpp"
    "${main_cpp_base}/frontend/config.cpp"
    "${main_cpp_base}/frontend/menu.cpp"
    "${main_cpp_base}/frontend/ttrial.cpp"
    )

set(src_hwvideo
    "${main_cpp_base}/hwvideo/hwroad.hpp"
    "${main_cpp_base}/hwvideo/hwsprites.hpp"
    "${main_cpp_base}/hwvideo/hwtiles.hpp"

    "${main_cpp_base}/hwvideo/hwroad.cpp"
    "${main_cpp_base}/hwvideo/hwsprites.cpp"
    "${main_cpp_base}/hwvideo/hwtiles.cpp"
    )
    
set(src_hwaudio
    "${main_cpp_base}/hwaudio/segapcm.hpp"
    "${main_cpp_base}/hwaudio/soundchip.hpp"
    "${main_cpp_base}/hwaudio/ym2151.hpp"
    
    "${main_cpp_base}/hwaudio/segapcm.cpp"
    "${main_cpp_base}/hwaudio/soundchip.cpp"
    "${main_cpp_base}/hwaudio/ym2151.cpp"
    )

set(src_sdl
	"${main_cpp_base}/sdl2/audio.hpp"
	"${main_cpp_base}/sdl2/timer.hpp"
	"${main_cpp_base}/sdl2/input.hpp"
	"${main_cpp_base}/sdl2/renderbase.hpp"

    "${main_cpp_base}/sdl2/audio.cpp"
	"${main_cpp_base}/sdl2/timer.cpp"
	"${main_cpp_base}/sdl2/input.cpp"
	"${main_cpp_base}/sdl2/renderbase.cpp"
    )
   
if(OPENGL)
	set(src_render
	    "${main_cpp_base}/sdl2/rendergl.hpp"
	    "${main_cpp_base}/sdl2/rendergl.cpp"
	)
elseif(OPENGLES)
	set(src_render
	    "${main_cpp_base}/sdl2/rendergles.hpp"
	    "${main_cpp_base}/sdl2/rendergles.cpp"
	)   
else()
	set(src_render
	    "${main_cpp_base}/sdl2/rendersurface.hpp"
	    "${main_cpp_base}/sdl2/rendersurface.cpp"
	)
endif()

set(src_directx
    "${main_cpp_base}/directx/ffeedback.hpp"
    "${main_cpp_base}/directx/ffeedback.cpp"
)

set(src_cannonboard
    "${main_cpp_base}/cannonboard/asyncserial.hpp"
    "${main_cpp_base}/cannonboard/interface.hpp"
    "${main_cpp_base}/cannonboard/asyncserial.cpp"
    "${main_cpp_base}/cannonboard/interface.cpp"
)

set(src_engine
    "${main_cpp_base}/engine/oaddresses.hpp"
    "${main_cpp_base}/engine/oanimseq.hpp"
    "${main_cpp_base}/engine/oanimsprite.hpp"
    "${main_cpp_base}/engine/oattractai.hpp"
    "${main_cpp_base}/engine/obonus.hpp"
    "${main_cpp_base}/engine/ocrash.hpp"
    "${main_cpp_base}/engine/oentry.hpp"
    "${main_cpp_base}/engine/oferrari.hpp"
    "${main_cpp_base}/engine/ohiscore.hpp"
    "${main_cpp_base}/engine/ohud.hpp"
    "${main_cpp_base}/engine/oinitengine.hpp"
    "${main_cpp_base}/engine/oinputs.hpp"
    "${main_cpp_base}/engine/olevelobjs.hpp"
    "${main_cpp_base}/engine/ologo.hpp"
    "${main_cpp_base}/engine/omap.hpp"
    "${main_cpp_base}/engine/omusic.hpp"
    "${main_cpp_base}/engine/ooutputs.hpp"
    "${main_cpp_base}/engine/opalette.hpp"
    "${main_cpp_base}/engine/oroad.hpp"
    "${main_cpp_base}/engine/osmoke.hpp"
    "${main_cpp_base}/engine/osprite.hpp"
    "${main_cpp_base}/engine/osprites.hpp"
    "${main_cpp_base}/engine/ostats.hpp"
    "${main_cpp_base}/engine/otiles.hpp"
    "${main_cpp_base}/engine/otraffic.hpp"
    "${main_cpp_base}/engine/outils.hpp"
    "${main_cpp_base}/engine/outrun.hpp"
    "${main_cpp_base}/engine/ozoom_lookup.hpp"

    "${main_cpp_base}/engine/oanimseq.cpp"
    "${main_cpp_base}/engine/oattractai.cpp"
    "${main_cpp_base}/engine/obonus.cpp"
    "${main_cpp_base}/engine/ocrash.cpp"
    "${main_cpp_base}/engine/oferrari.cpp"
    "${main_cpp_base}/engine/ohiscore.cpp"
    "${main_cpp_base}/engine/ohud.cpp"
    "${main_cpp_base}/engine/oinitengine.cpp"
    "${main_cpp_base}/engine/oinputs.cpp"
    "${main_cpp_base}/engine/olevelobjs.cpp"
    "${main_cpp_base}/engine/ologo.cpp"
    "${main_cpp_base}/engine/omap.cpp"
    "${main_cpp_base}/engine/omusic.cpp"
    "${main_cpp_base}/engine/ooutputs.cpp"
    "${main_cpp_base}/engine/opalette.cpp"
    "${main_cpp_base}/engine/oroad.cpp"
    "${main_cpp_base}/engine/osmoke.cpp"
    "${main_cpp_base}/engine/osprite.cpp"
    "${main_cpp_base}/engine/osprites.cpp"
    "${main_cpp_base}/engine/ostats.cpp"
    "${main_cpp_base}/engine/otiles.cpp"
    "${main_cpp_base}/engine/otraffic.cpp"
    "${main_cpp_base}/engine/outils.cpp"
    "${main_cpp_base}/engine/outrun.cpp"
    )

set(src_engine_audio
    "${main_cpp_base}/engine/audio/commands.hpp"
    "${main_cpp_base}/engine/audio/osound.hpp"
    "${main_cpp_base}/engine/audio/osoundint.hpp"
    "${main_cpp_base}/engine/audio/osoundadr.hpp"

    "${main_cpp_base}/engine/audio/osound.cpp"
    "${main_cpp_base}/engine/audio/osoundint.cpp"
    )

set(SRCS
    ${src_main}
    ${src_frontend}
    ${src_hwvideo}
    ${src_hwaudio}
    ${src_sdl}
    ${src_render}
    ${src_directx}
    ${src_cannonboard}
    ${src_engine}
    ${src_engine_audio}
)

# Group files into relevant filters for Visual Studio build
SOURCE_GROUP(src FILES ${src_main})
SOURCE_GROUP(src\\frontend FILES ${src_frontend})
SOURCE_GROUP(src\\hwvideo FILES ${src_hwvideo})
SOURCE_GROUP(src\\hwaudio FILES ${src_hwaudio})
SOURCE_GROUP(src\\sdl FILES ${src_sdl})
SOURCE_GROUP(src\\sdl FILES ${src_render})
SOURCE_GROUP(src\\directx FILES ${src_directx})
SOURCE_GROUP(src\\cannonboard FILES ${src_cannonboard})
SOURCE_GROUP(src\\engine FILES ${src_engine})
SOURCE_GROUP(src\\engine\\audio FILES ${src_engine_audio})

# Add Icon For Windows Builds
if(WIN32)
  set(SRCS ${SRCS} ../res/cannonball.rc)
endif(WIN32)

add_executable(cannonball ${SRCS})

# -----------------------------------------------------------------------------
# Compiler Definitions
# -----------------------------------------------------------------------------

if(OPENGL)
    add_definitions(-DWITH_OPENGL)
endif()

if(OPENGLES)
    add_definitions(-DWITH_OPENGLES)
endif()

if(CANNONBOARD)
    add_definitions(-DCANNONBOARD)
endif()

# -----------------------------------------------------------------------------
# Library Setup
# -----------------------------------------------------------------------------

set(BOOST_INCLUDEDIR ${boost_dir})
find_package(Boost REQUIRED)

set(SDL2_DIR ${sdl2_dir})
find_package(SDL2 REQUIRED)
message("SDL2 Include  : ${SDL2_INCLUDE_DIRS}")
message("SDL2 Libraries: ${SDL2_LIBRARIES}")

# Include
include_directories(
    ${main_cpp_base}
    ${BOOST_INCLUDEDIR}
    ${SDL2_INCLUDE_DIRS}
)

link_directories(
    ${platform_link_dirs}
)

target_link_libraries(cannonball
    ${SDL2_LIBRARIES}
    ${platform_link_libs}
)

# -----------------------------------------------------------------------------
# Copy useful files to build destination
# -----------------------------------------------------------------------------

configure_file(../res/config.xml ./config.xml 
    COPYONLY
)

configure_file(../res/tilemap.bin ./res/tilemap.bin
    COPYONLY 
)
configure_file(../res/tilepatch.bin ./res/tilepatch.bin
    COPYONLY 
)