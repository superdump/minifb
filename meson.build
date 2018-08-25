project('minifb', ['c'],
    default_options: ['warning_level=1',
        'buildtype=debugoptimized'])

sources = []
deps = []

host_system = host_machine.system()

if host_system == 'linux'
    wayland_opt_dep = dependency('wayland', required: false)
    x11_opt_dep = dependency('x11', required: false)
    if wayland_opt_dep.found()
        sources += ['src/wayland/WaylandMiniFB.c']
        deps += [wayland_opt_dep]
    else if x11_opt_dep.found()
        sources += ['src/x11/X11MiniFB.c']
        deps += [x11_opt_dep]
    else
        error('Linux builds require either Wayland or X11')
    endif
else if host_system == 'darwin'
    add_languages('objc')
    sources += [
        'src/macosx/MacMiniFB.m',
        'src/macosx/OSXWindow.h',
        'src/macosx/OSXWindow.m',
        'src/macosx/OSXWindowFrameView.h',
        'src/macosx/OSXWindowFrameView.m'
    ]
    deps += [dependency('appleframeworks', modules: 'Cocoa')]
else if host_system == 'windows'
    sources += ['src/windows/WinMiniFB.c']
else
    error('Unsupported platform: ' + host_system)
endif

if sources.length() == 0
    error('No sources to build. Something went wrong...')
endif

i = include_directories('include')
l = static_library('minifb', sources,
    dependencies: deps,
    include_directories : i)
minifb_dep = declare_dependency(include_directories: i,
    link_with: l)
