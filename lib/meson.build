sources = ['libcompat.c']

if not librt.found()
  sources = sources + ['clock_gettime.c',
    'timer_create.c', 'timer_delete.c',
    'timer_settime.c']
endif

if get_option('shared_lib')
  libtype = 'shared_library'
else
  libtype = 'static_library'
endif

compatlib = build_target('compat',
  sources,
  c_args: [cstd, '-DHAVE_CONFIG_H=1'],
  include_directories : [confinc],
  target_type : libtype,
)
