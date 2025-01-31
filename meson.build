project('xvnkb','c', default_options: 'c_std=gnu17',version: '0.2.11', meson_version: '>=1.4.0')

add_project_arguments('-DVK_NEED_UCHAR', language: 'c')

conf_data = configuration_data()
conf_data.set('version', meson.project_version())
conf_data.set('VK_USE_ABCSTROKE',get_option('abcstroke'))
conf_data.set('VK_USE_EXTSTROKE',get_option('extstroke'))
conf_data.set('VK_USE_PROSTROKE',get_option('prostroke'))

configure_file(output: 'config.h', input: 'config.h.in', configuration: conf_data)

dl_dep = dependency('dl')
xlib_dep = dependency('X11')
if get_option('xft').enabled()
    xft_dep = dependency('xft')
    add_project_arguments('-DUSE_XFT', language: 'c')
endif

deps = [dl_dep, xlib_dep, xft_dep]

core_src = ['xvnkb.c','visckey.c']
core = library('xvnkb', core_src, name_prefix: '', soversion: meson.project_version(), dependencies: deps)

src = ['data.c','flash.c','main.c','event.c','mainwin.c','menu.c','hotkey.c','systray.c','mode.c','property.c','session.c','xconfig.c','xresource.c','label.c','button.c','msgbox.c']
xvnkb = executable('xvnkb', src, dependencies: deps, link_with: core)

ctrl_src = ['tools/xvnkb_ctrl.c', 'tools/data.c','tools/mode.c','tools/property.c','tools/xconfig.c']
xvnkb_ctrl = executable('xvnkb_ctlr', ctrl_src, dependencies: deps, link_with: core)

