sources = [
  'check.c',
  'check_error.c',
  'check_list.c',
  'check_log.c',
  'check_msg.c',
  'check_pack.c',
  'check_print.c',
  'check_run.c',
  'check_str.c',
]

if get_option('shared_lib')
  libtype = 'shared_library'
else
  libtype = 'static_library'
endif

checklib = build_target('check',
  sources,
  c_args: '-DHAVE_CONFIG_H=1',
  include_directories : [confinc],
  dependencies : libm,
  target_type : libtype,
)
