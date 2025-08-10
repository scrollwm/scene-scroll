project('scene-scroll', 'c',
  version: '0.0.1',
  license: 'MIT',
  meson_version: '>=1.3',
  default_options: [
    'c_std=c11',
    'warning_level=2',
    'werror=false',
  ],
)

add_project_arguments(
  [
    '-DWLR_USE_UNSTABLE',
    '-D_POSIX_C_SOURCE=200809L',
  ],
  language: 'c',
)

# Compiler
cc = meson.get_compiler('c')

# Dependencies
wlroots = dependency('wlroots-0.20', version: ['>=0.20.0', '<0.21.0'])
wayland_server = dependency('wayland-server', version: '>=1.21.0')
wayland_protos = dependency('wayland-protocols', version: '>=1.41')
pixman = dependency('pixman-1')
math = cc.find_library('m')

scene_scroll_deps = [
  wlroots,
  wayland_server,
  wayland_protos,
  pixman,
  math,
]

# Source files
scene_scroll_sources = files(
  'src/debug.c',
  'src/drag_icon.c',
  'src/layer_shell_v1.c',
  'src/output_layout.c',
  'src/scene.c',
  'src/subsurface_tree.c',
  'src/surface.c',
  'src/xdg_shell.c',
)

# Include directories
scene_scroll_inc = include_directories('include')

# Build library
scene_scroll_lib = library(
  'scene-scroll',
  scene_scroll_sources,
  include_directories: scene_scroll_inc,
  dependencies: scene_scroll_deps,
  install: true,
)

# Generate pkg-config file
pkg = import('pkgconfig')
pkg.generate(
  scene_scroll_lib,
  description: 'Scene graph library extracted from Scroll window manager',
  subdirs: ['scene-scroll'],
)

# Declare dependency
scene_scroll_dep = declare_dependency(
  link_with: scene_scroll_lib,
  include_directories: scene_scroll_inc,
  dependencies: scene_scroll_deps,
)

# Install headers
install_headers(
  'include/scene-scroll/scene.h',
  subdir: 'scene-scroll',
)

# Install additional headers if they exist
fs = import('fs')
scene_headers = []
foreach h : ['color.h', 'output.h']
  header_path = join_paths('include/scene-scroll', h)
  if fs.exists(header_path)
    scene_headers += header_path
  endif
endforeach

if scene_headers.length() > 0
  install_headers(scene_headers, subdir: 'scene-scroll')
endif
