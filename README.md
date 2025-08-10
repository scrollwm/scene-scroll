# scene-scroll

Scene graph library extracted from Scroll window manager.

This library contains Scroll's modified wlroots scene graph implementation with
custom modifications for content and workspace scaling.

## Building

```bash
meson setup build
ninja -C build
sudo ninja -C build install
```

## Usage

Include in your meson.build:
```meson
scene_scroll_dep = dependency('scene-scroll')
```

Use in your code:
```c
#include <scene-scroll/scene.h>
```

## Origin

Extracted from Scroll commit: 1.11.3
Generated on: 2025-08-10T11:44:54.081147
