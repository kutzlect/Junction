pkgdatadir = join_paths(get_option('datadir'), meson.project_name())

gjspack = find_program('../troll/gjspack/bin/gjspack')
gresource = custom_target(meson.project_name() + '.gresource',
  input: ['main.js', '../po/POTFILES'],
  output: meson.project_name() + '.gresource',
  command: [
    gjspack,
    '--appid=' + meson.project_name(),
    '--resource-root', meson.project_source_root(),
    '--no-executable',
    '@INPUT0@',
    '--potfiles', '@INPUT1@',
    '@OUTDIR@',
  ],
  install: true,
  install_dir: pkgdatadir,
)

bin_conf = configuration_data()
bin_conf.set('GJS', find_program('gjs').full_path())
bin_conf.set('PACKAGE_VERSION', meson.project_version())
bin_conf.set('PACKAGE_NAME', meson.project_name())
bin_conf.set('prefix', prefix)
bin_conf.set('libdir', join_paths(get_option('prefix'), get_option('libdir')))
bin_conf.set('datadir', datadir)
bin_conf.set('pkgdatadir', pkgdatadir)

configure_file(
  input: 're.sonny.Junction',
  output: 're.sonny.Junction',
  configuration: bin_conf,
  install: true,
  install_dir: get_option('bindir')
)
