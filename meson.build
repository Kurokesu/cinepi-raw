project('cinepi-raw', 'c', 'cpp',
        meson_version : '>= 0.64.0',
        version : '2.0.0',
        default_options : [
            'werror=false',
            'warning_level=3',
            'cpp_std=c++17',
            'c_std=c11',
            'buildtype=release',
        ],
        license : 'BSD-2-Clause')

cpp_arguments = ['-pedantic', '-Wno-unused-parameter', '-faligned-new']
cpp_arguments += '-D_FILE_OFFSET_BITS=64'

cxx = meson.get_compiler('cpp')
cpu = host_machine.cpu()

if cxx.get_id() == 'gcc'
    cpp_arguments += '-Wno-psabi'
endif

if cpu == 'aarch64'
    cpp_arguments += '-ftree-vectorize'
endif

add_project_arguments(cpp_arguments, language : 'cpp')

libcamera_dep = dependency('libcamera', required : true)
rpicam_app_dep = dependency('rpicam_app', required : true)

# The rpicam_app pkg-config doesn't include its own header base dir,
# but system headers use relative includes like "core/metadata.hpp"
rpicam_app_inc = include_directories('/usr/include/rpicam-apps')

summary({
            'libcamera version' : libcamera_dep.version(),
            'rpicam_app' : rpicam_app_dep.found(),
        },
        section : 'Dependencies')

subdir('cinepi')
