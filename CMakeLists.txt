cmake_minimum_required(VERSION 3.28...3.30)
if(OS_WINDOWS AND DROIDCAM_OVERRIDE)
  add_library(droidcam-obs-virtual-output MODULE)
  add_library(OBS::droidcam-obs-virtual-output ALIAS droidcam-obs-virtual-output)

  find_package(Qt6 REQUIRED Widgets)

  target_sources(
    droidcam-obs-virtual-output
    PRIVATE
      src/droidcam.rc
      src/plugin.cc
      src/plugin.h
      src/queue.h
      src/structs.h
      src/sys-win.cc
      src/yuv420_yuyv.c
  )

  target_link_libraries(droidcam-obs-virtual-output PRIVATE OBS::libobs OBS::frontend-api OBS::w32-pthreads Qt::Widgets)

  set_target_properties_obs(droidcam-obs-virtual-output PROPERTIES FOLDER plugins PREFIX "")
endif()
