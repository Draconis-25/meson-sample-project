project('sample_cpp_project', 'cpp',
    version : '1.0',
    license : [ 'proprietary'],
    meson_version : '>= 0.50.0',
    default_options : [ 'warning_level=3', 'buildtype=debugoptimized', 'cpp_std=c++11' ]
)

# Variables tracking sources and libraries
library_path = []
project_sources = []
project_header_files = []
project_test_sources = []

inc = [include_directories('include')]

subdir('include')
subdir('third_party')
# This is where you should add in include directories

# This triggers the builds of sources
subdir('src')
# This links all the static libs into the main source file to form a binary

sample_cpp_project_bin_deps = [
  meson.get_compiler('cpp').find_library('fizz', required : true, dirs : library_path)
]

sample_cpp_project_bin_dep_libs = [
  foo_lib,
  bar_lib,
  baz_lib,
]

sample_cpp_project_bin = executable('sample_cpp_project_bin', 
  main_source, 
  include_directories : inc, 
  cpp_pch : 'pch/pch.h',
  dependencies : sample_cpp_project_bin_deps,
  link_with : sample_cpp_project_bin_dep_libs)

gtest = subproject('gtest')

if get_option('enable-tests')
  subdir('tests')
endif

subdir('docs')

# This regex excludes any sources from the third_party, tests, benchmarks 
# and gtest related files.
regex = '^((?!(third_party|tests|benchmarks|gtest)).)*$'

