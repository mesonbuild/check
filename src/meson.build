configure_file(
  input : 'check.h.in',
  output : 'check.h',
  configuration : cdata,
)

configure_file(
  input : '../meson/check_stdint.h.in',
  output : 'check_stdint.h',
  configuration : cdata,
)

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

checklib = build_target('check',
  sources,
  c_args: ['-DHAVE_CONFIG_H=1', ck_dll_exp_private],
  include_directories : [confinc],
  dependencies : [libm, compatlib_dep],
  target_type : libtype,
)
