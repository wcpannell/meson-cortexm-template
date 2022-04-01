project(
  'PROJECT NAME',
  ['cpp', 'c'],
  default_options : [
    'c_std=c17', 'build.c_std=c17',
    'cpp_std=c++17', 'build.cpp_std=c++17',
  ],
  meson_version : '>=0.56.0',
  version : '0.1.0',
  license : 'Proprietary'
)

# initialize globals (filled in cross-file)
srcs = []
link_args = []
link_deps = []
startupfiles = []
c_args = ['-Wall', '-Wextra']
cpp_args = ['-Wall', '-Wextra']


# includes should be set in lower level files
# inc = include_directories('include', 'bsp')

if get_option('disable-rtti')
	cpp_args += '-fno-rtti'
endif

if get_option('disable-exceptions')
	cpp_args += ['-fno-exceptions', '-fno-unwind-tables']
endif

if get_option('enable-pedantic')
	c_args += '-pedantic'
	cpp_args += '-pedantic'
else
	c_args += '-Wno-pedantic'
	cpp_args += '-Wno-pedantic'
endif

# only needed if we have build files in these directories
# subdir('include')
subdir('src')
# subdir('test')


# Choose correct BSP for build environment
if meson.is_cross_build()
  subdir('bsp/host')
else
  subdir('bsp/native')
endif

# Include startup and linkfile paths if crossbuild
# This could be at a lower level, or as part of bsp
if meson.is_cross_build()
  linkfiles = files(['PATH/TO/LINKFILE.LD', ])
  foreach linkfile : linkfiles
          link_args += ['-Wl,-T,@0@/@1@'.format(meson.current_source_dir(), linkfile)]
  endforeach

  startupfiles += files([
  'PATH/TO/startup_asm.S',
  'PATH/TO/system_c.c'
  ])
endif

# Generate map file
link_args += '-Wl,-Map,mapfile.map'

# Generate assembly
c_args += ['-save-temps=obj', '-fverbose-asm', '-g3']

# Only rebuild docs for cross-compile
if meson.is_cross_build()
  subdir('docs')
endif
