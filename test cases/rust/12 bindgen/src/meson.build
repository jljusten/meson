gen = rust.bindgen(
  input : 'header.h',
  output : 'header.rs',
  include_directories : inc,
)

rust_rlib = static_library(
  'rust_lib',
  gen
)
