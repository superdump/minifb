project('minifb', ['c', 'objc'])
objc_sources = [
    'src/macosx/MacMiniFB.m',
    'src/macosx/OSXWindow.h',
    'src/macosx/OSXWindow.m',
    'src/macosx/OSXWindowFrameView.h',
    'src/macosx/OSXWindowFrameView.m'
]
frameworks_dep = dependency('appleframeworks', modules: 'Cocoa')
i = include_directories('include')
l = static_library('minifb', objc_sources,
    dependencies: frameworks_dep,
    include_directories : i)
minifb_dep = declare_dependency(include_directories: i,
    link_with: l)
