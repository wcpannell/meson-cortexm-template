cdata = configuration_data()

doxygen = find_program('doxygen', required : false)
sphinx = find_program('sphinx-build', required : false)
breath = find_program('breathe-apidoc', required : false)

if find_program('dot', required : false).found()
  cdata.set('HAVE_DOT', 'YES')
else
  cdata.set('HAVE_DOT', 'NO')
endif
cdata.set('PROJECT_NAME', meson.project_name())
cdata.set('VERSION', meson.project_version())
cdata.set('TOP_SRCDIR', meson.project_source_root())
cdata.set('TOP_BUILDDIR', meson.project_build_root())
cdata.set('DOXYGEN_OUTPUT', meson.project_build_root() + '/docs/doxygen')

doxyfile = configure_file(
	input: 'Doxyfile.in',
	output: 'Doxyfile',
	configuration: cdata,
	install: false
)

sphinxfile = configure_file(
  input: 'conf.py.in',
  output: 'conf.py',
  configuration: cdata,
  install: false
)

# Copy sphinx source files to builddir
sphinx_sources = [
  'index.rst'
]
foreach file : sphinx_sources
  configure_file(input: file, output: file, copy: true)
endforeach

# datadir = join_paths(get_option('datadir'), 'docs', 'myname')

doxy_target = custom_target(
	'myname-doxy-docs',
	input: doxyfile,
	output: 'doxygen',
	command: [doxygen, doxyfile],
#	install: true,
#	install_dir: datadir
)

html_target = custom_target(
  'myname-docs',
  input: doxy_target,
  output: 'docs',
  command: [
    sphinx,
    '-b',
    'html',
    '-E',
    meson.current_build_dir(),
    meson.current_build_dir() + '/docs/'
  ]
  #depends: doxy_target
)

