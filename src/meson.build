main_src = [
  'main.cpp',
]

main = executable(
  'main.elf',
  #[srcs, startupfile],
  main_src,
  link_args : [link_args, '-Wl,--gc-sections'],
  # dependencies : link_deps,
  # include_directories : [inc, target_includes],
)
