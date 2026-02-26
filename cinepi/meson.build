hiredis_dep = dependency('hiredis', required : false)
redis_plus_plus_dep = dependency('redis++', required : false)

if not hiredis_dep.found()
  hiredis_lib = meson.get_compiler('cpp').find_library('hiredis', required: true)
else
  hiredis_lib = hiredis_dep
endif

if not redis_plus_plus_dep.found()
  redis_plus_plus_lib = meson.get_compiler('cpp').find_library('redis++', required: true)
else
  redis_plus_plus_lib = redis_plus_plus_dep
endif

sources = [
  'cinepi_raw.cpp',
  'dng_encoder.cpp',
  'sharedContextStage.cpp',
  'mjpegPreviewStage.cpp',
  'cinepi_controller.cpp',
  'cinepi_sound.cpp',
  'cinepi_state.cpp',
  'utils.cpp'
]

spdlog_dep = dependency('spdlog')
json_dep = dependency('jsoncpp')
jpeg_dep = dependency('libjpeg', required : true)
tiff_dep = dependency('libtiff-4', required : true)
boost_dep = dependency('boost', modules : ['program_options'], required : true)
thread_dep = dependency('threads', required : true)
alsa_dep = dependency('alsa')
udev_dep = dependency('libudev')
mhd_dep = dependency('nadjieb_mjpeg_streamer', required : true)

cinepi_raw_deps = [
  libcamera_dep,
  rpicam_app_dep,
  hiredis_lib,
  redis_plus_plus_lib,
  spdlog_dep,
  json_dep,
  jpeg_dep,
  tiff_dep,
  boost_dep,
  thread_dep,
  alsa_dep,
  udev_dep,
  mhd_dep,
]

cinepi_raw = executable('cinepi-raw', sources,
             include_directories : rpicam_app_inc,
             dependencies: cinepi_raw_deps,
             install : true)
