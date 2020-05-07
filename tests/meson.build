tests = [
  ['check_check_export', ['check_check_sub.c', 'check_check_master.c',
    'check_check_log.c', 'check_check_fork.c', 'check_check_export_main.c']],
  ['check_check', ['check_list.c', 'check_check_sub.c', 'check_check_master.c',
    'check_check_msg.c', 'check_check_log.c', 'check_check_log_internal.c',
    'check_check_limit.c', 'check_check_fork.c', 'check_check_fixture.c',
    'check_check_pack.c', 'check_check_exit.c', 'check_check_selective.c',
    'check_check_main.c']],
  ['check_mem_leaks', ['check_mem_leaks.c', 'check_check_log.c', 'check_check_fork.c',
    'check_check_exit.c', 'check_check_selective.c', 'check_check_sub.c',
    'check_check_master.c']],
#  ['stress', ['check_stress.c']],
  ['nofork', ['check_nofork.c']],
#  ['nofork_teardown', ['check_nofork_teardown.c']],
#  ['ex_output', ['ex_output.c']],
]

foreach t : tests
  exe = executable(t.get(0), t.get(1),
    c_args: ['-DHAVE_CONFIG_H=1', '-DTIMEOUT_TESTS_ENABLED=0'],
    include_directories: confinc,
    dependencies : check_dep,
    )
  test(t.get(0), exe)
endforeach
