# There are two tests here, because the 2nd one depends on a version of
# GLib (2.48.2) that is very recent at the time of writing.

simple_resources = gnome.compile_resources('simple-resources',
  'simple.gresource.xml',
  install_header : true,
  export : true,
  source_dir : '../resources-data',
  c_name : 'simple_resources')

simple_res_exe = executable('simple-resources-test',
  'simple-main.c', simple_resources,
  dependencies: gio)
test('simple resource test', simple_res_exe)

gnome.compile_resources('simple-resources',
  'simple.gresource.xml',
  gresource_bundle: true,
  install: true,
  install_dir: get_option('datadir'),
  source_dir : '../resources-data',
)
test('simple resource test (gresource)', find_program('resources.py'))

if glib.version() >= '2.52.0'
  # This test cannot pass if GLib version is older than 9.99.9.
  # Meson will raise an error if the user tries to use the 'dependencies'
  # argument and the version of GLib is too old for generated resource
  # dependencies to work correctly.
  generated_resources = gnome.compile_resources('generated-resources',
    'generated.gresource.xml',
    source_dir : '../resources-data',
    c_name : 'generated_resources',
    dependencies : [res3_txt, res4_txt])

  generated_res_exe = executable('generated-resources-test',
    'generated-main.c', generated_resources,
    dependencies: gio)
  test('generated resource test', generated_res_exe)
endif
