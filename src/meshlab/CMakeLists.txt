set(JHEAD_INCLUDE_DIR ${MESHLAB_SOURCE_DIR}/src/external/jhead)

include_directories(
  ${CMAKE_CURRENT_BINARY_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/..
  ${JHEAD_INCLUDE_DIR}
  )

add_definitions(-fPIC)
add_definitions(${Qt5Widgets_DEFINITIONS})

set(meshlab_basic_SRCS
  additionalgui.cpp
  changetexturename.cpp
  customDialog.cpp
  filterScriptDialog.cpp
  filterthread.cpp
  glarea.cpp
  glarea_setting.cpp
  layerDialog.cpp
  main.cpp
  mainwindow_Init.cpp
  mainwindow_RunTime.cpp
  ml_default_decorators.cpp
  ml_render_gui.cpp
  ml_rendering_actions.cpp
  ml_selection_buffers.cpp
  ml_std_par_dialog.cpp
  multiViewer_Container.cpp
  plugindialog.cpp
  savemaskexporter.cpp
  saveSnapshotDialog.cpp
  stdpardialog.cpp
  xmlgeneratorgui.cpp
  xmlstdpardialog.cpp
  ../external/vcglib/wrap/gui/trackball.cpp
  ../external/vcglib/wrap/gui/trackmode.cpp
  )

set(moc_files
  ../common/interfaces.h
  additionalgui.h
  alnParser.h
  changetexturename.h
  customDialog.h
  filterScriptDialog.h
  filterthread.h
  glarea.h
  glarea_setting.h
  layerDialog.h
  mainwindow.h
  meshlabeditdockwidget.h
  ml_default_decorators.h
  ml_render_gui.h
  ml_rendering_actions.h
  ml_selection_buffers.h
  ml_std_par_dialog.h
  multiViewer_Container.h
  plugindialog.h
  savemaskexporter.h
  saveSnapshotDialog.h
  snapshotsetting.h
  stdpardialog.h
  xmlgeneratorgui.h
  xmlstdpardialog.h
  )
QT5_WRAP_CPP(moc_SRCS ${moc_files})

set(uic_files
  ui/layerDialog.ui
  ui/filterScriptDialog.ui
  ui/customDialog.ui
  ui/savesnapshotDialog.ui
  ui/aboutDialog.ui
  ui/renametexture.ui
  ui/savemaskexporter.ui
  ui/congratsDialog.ui 
  ui/filtergui.ui
  ui/filtercreatortab.ui
  )
QT5_WRAP_UI(uic_SRCS ${uic_files})

QT5_ADD_RESOURCES(rcc_SRCS meshlab.qrc)

set(meshlab_SRCS
  ${meshlab_basic_SRCS}
  ${uic_SRCS}
  ${moc_SRCS}
  ${rcc_SRCS}
  )

add_executable(meshlab ${meshlab_SRCS})
target_link_libraries(meshlab common jhead ${OPENGL_LIBRARIES} ${QT_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
install(TARGETS meshlab
  RUNTIME DESTINATION ${BIN_DIR}
  LIBRARY DESTINATION ${LIB_DIR}
  ARCHIVE DESTINATION ${LIB_DIR})

# Local Variables:
# tab-width: 8
# mode: cmake
# indent-tabs-mode: t
# End:
# ex: shiftwidth=2 tabstop=8
