bsp_src = [
  'bsp.c'
]

lib_inc = [
  include_directories('inc'),
]

bsp = static_library(
  'bsp',
  bsp_src,
  build_by_default: false,
  native: true,
)

bsp_dep = declare_dependency(
  include_directories: lib_inc,
  link_with: bsp,
)
