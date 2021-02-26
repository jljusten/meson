project('rust linking to libm', 'c', 'rust')

if host_machine.system() == 'darwin'
  error('MESON_SKIP_TEST: doesnt work right on macos, please fix!')
endif

cc = meson.get_compiler('c')
dep_m = cc.find_library('m', required : false, static : false)
if not dep_m.found()
  error('MESON_SKIP_TEST: Could not find a @0@ libm'.format(get_option('static') ? 'static' : 'shared'))
endif

# Change to false to use the hack/dylib path for librs_math which passes
# the test
if true

librs_math = static_library(
  'rs_math',
  'rs_math.rs',
  dependencies : [dep_m],

  # HACK: Should dep_m not bring this flag along?
  rust_args : ['-L', '/usr/lib/x86_64-linux-gnu'],
)

else

# This hack makes the test pass
librs_math = static_library(
  'rs_math',
  'rs_math.rs',
  rust_args : ['-L', '/usr/lib/x86_64-linux-gnu', '-l', 'dylib=m'],
)

endif

e = executable(
  'prog', 'prog.rs',
  link_with : [librs_math],
)

test('cdepstest', e)
