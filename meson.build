project('check', 'c')

cc = meson.get_compiler('c')
cdata = configuration_data()
check_headers = [
  ['HAVE_DLFCN_H', 'dlfcn.h'],
  ['HAVE_FCNTL_H', 'fcntl.h'],
  ['HAVE_INTTYPES_H', 'inttypes.h'],
  ['HAVE_LOCALE_H', 'locale.h'],
  ['HAVE_MEMORY_H', 'memory.h'],
  ['HAVE_STDARG_H', 'stdarg.h'],
  ['HAVE_STDDEF_H', 'stddef.h'],
  ['HAVE_STDINT_H', 'stdint.h'],
  ['HAVE_STDLIB_H', 'stdlib.h'],
  ['HAVE_STRINGS_H', 'strings.h'],
  ['HAVE_STRING_H', 'string.h'],
  ['HAVE_SYS_STAT_H', 'sys/stat.h'],
  ['HAVE_SYS_TIME_H', 'sys/time.h'],
  ['HAVE_SYS_TYPES_H', 'sys/types.h'],
  ['HAVE_SYS_WAIT_H', 'sys/wait.h'],
  ['HAVE_TIME_H', 'time.h'],
  ['HAVE_UNISTD_H', 'unistd.h'],
  ['HAVE_VARARGS_H', 'varargs.h'],
]

foreach h : check_headers
  if cc.has_header(h.get(1))
    cdata.set(h.get(0), 1)
  endif
endforeach

check_functions = [
  ['HAVE_ALARM', 'alarm', '#include<unistd.h>'],
# check token HAVE_ASPRINTF
  ['HAVE_CLOCK_GETTIME', 'clock_gettime', '#include<time.h>'],
# check token HAVE_DECL_ALARM
# check token HAVE_DECL_CLOCK_GETTIME
# check token HAVE_DECL_GETLINE_GETTIMEOFDAY
# check token HAVE_DECL_LOCALTIME_R
# check token HAVE_DECL_SETENV
# check token HAVE_DECL_STRDUP
# check token HAVE_DECL_STRSIGNAL
# check token HAVE_DECL_TIMER_CREATE
# check token HAVE_DECL_TIMER_DELETE
# check token HAVE_DECL_TIMER_SETTIME
  ['HAVE_FORK', 'fork', '#include<unistd.h>'],
  ['HAVE_GETLINE', 'getline', '#include<stdio.h>'],
  ['HAVE_GETTIMEOFDAY', 'gettimeofday', '#include<sys/time.h>'],
# check token HAVE_INTMAX_T
# check token HAVE_LIBM
# check token HAVE_LIBRT
# check token HAVE_LOCALECONV
  ['HAVE_LOCALTIME_R', 'localtime_r', '#include<time.h>'],
# check token HAVE_LONG_DOUBLE
# check token HAVE_LONG_LONG_INT
# check token HAVE_MALLOC
# check token HAVE_MKSTEMP
# check token HAVE_PTHREAD
# check token HAVE_PTRDIFF_T
# check token HAVE_REALLOC
# check token HAVE_SETITIMER
  ['HAVE_SIGACTION', 'sigaction', '#include<signal.h>'],
  ['HAVE_SNPRINTF', 'snprintf', '#include<stdio.h>'],
# check token HAVE_STRDUP
  ['HAVE_STRSIGNAL', 'strsignal', '#include<signal.h>'],
# check token HAVE_STRUCT_ITIMERSPEC_IT_INTERVAL
# check token HAVE_STRUCT_ITIMERSPEC_IT_VALUE
# check token HAVE_STRUCT_LCONV_DECIMAL_POINT
# check token HAVE_STRUCT_LCONV_THOUSANDS_SEP
# check token HAVE_TIMER_CREATE
# check token HAVE_TIMER_DELETE
# check token HAVE_TIMER_SETTIME
# check token HAVE_UINTMAX_T
# check token HAVE_UINTPTR_T
# check token HAVE_UNSIGNED_LONG_LONG_INT
  ['HAVE_VASPRINTF', 'vasprintf', '#include<stdio.h>'],
  ['HAVE_VA_COPY', 'va-copy', '#include<stdarg.h>'],
  ['HAVE_VSNPRINTF', 'vsnprintf', '#include<stdio.h>'],
# check token HAVE___VA_COPY
]

foreach f : check_functions
  if cc.has_function(f.get(1), prefix : f.get(2))
    cdata.set(f.get(0), 1)
  endif
endforeach


b1 = cc.has_member('struct timespec', 'tv_nsec', prefix : '#include<time.h>')
b2 = cc.has_member('struct timespec', 'tv_sec', prefix : '#include<time.h>')
if not b1 or not b2
  cdata.set('STRUCT_TIMESPEC_DEFINITION_MISSING', 1)
endif

b1 = cc.has_member('struct itimerspec', 'it_interval', prefix : '#include<time.h>')
b2 = cc.has_member('struct itimerspec', 'it_value', prefix : '#include<time.h>')
if not b1 or not b2
  cdata.set('STRUCT_ITIMERSPEC_DEFINITION_MISSING', 1)
endif

# check token HAVE_STRUCT_TIMESPEC_TV_SEC

cdata.set('SIZEOF_CHAR', cc.sizeof('char'))
cdata.set('SIZEOF_INT', cc.sizeof('int'))
cdata.set('SIZEOF_LONG', cc.sizeof('long'))
cdata.set('SIZEOF_SHORT', cc.sizeof('short'))
cdata.set('SIZEOF_VOIDP', cc.sizeof('void*'))

cdata.set('HAVE_DECL_STRSIGNAL', 1)

if not cc.has_type('clockid_t')
  cdata.set('clockid_t', 'int')
endif

if not cc.has_type('timer_t')
  cdata.set('timer_t', 'int')
endif

librt = dependency('rt', required : false)
if librt.found()
   cdata.set('HAVE_LIBRT', 1)
endif

configure_file(input : 'config.h.meson',
  output : 'config.h',
  configuration : cdata)

confinc = include_directories('.')

cstd = ['-std=c99']


subdir('src')
subdir('lib')

check_dep = declare_dependency(include_directories : include_directories('src'),
  link_with : [checklib, compatlib])
subdir('tests')
