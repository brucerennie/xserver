project('xserver', 'c',
        default_options: [
            'buildtype=debugoptimized',
            'c_std=gnu99',
        ],
        version: '25.0.0.5',
        meson_version: '>= 0.58.0',
)
release_date = '2025-07-11'

add_project_arguments('-DHAVE_DIX_CONFIG_H', language: ['c', 'objc'])
cc = meson.get_compiler('c')

add_project_arguments('-fno-strict-aliasing', language : 'c')
add_project_arguments('-fvisibility=hidden', language : 'c')
add_project_arguments('-Wvla', language: 'c')

add_project_link_arguments('-fvisibility=hidden', language : 'c')

if cc.get_id() == 'gcc' or cc.get_id() == 'clang'
    test_wflags = [
        '-Wall',
        '-Wpointer-arith',
        '-Wmissing-declarations',
        '-Wformat=2',
        '-Wstrict-prototypes',
        '-Wmissing-prototypes',
        '-Wnested-externs',
        '-Wbad-function-cast',
        '-Wold-style-definition',
        '-Wunused',
        '-Wuninitialized',
        '-Wshadow',
        '-Wmissing-noreturn',
        '-Wmissing-format-attribute',
        '-Wredundant-decls',
        '-Werror=implicit',
        '-Werror=nonnull',
        '-Werror=init-self',
        '-Werror=main',
        '-Werror=missing-braces',
        '-Werror=sequence-point',
        '-Werror=return-type',
        '-Werror=trigraphs',
        '-Werror=array-bounds',
        '-Werror=write-strings',
        '-Werror=address',
        '-Werror=int-to-pointer-cast',
        '-Werror=pointer-to-int-cast',
        '-Woverride-init',
        '-Wvla',
    ]
else
    test_wflags = []
endif

common_wflags = []
foreach wflag: test_wflags
    if cc.has_argument(wflag)
        common_wflags += [ wflag ]
    endif
endforeach

add_project_arguments(common_wflags, language : ['c', 'objc'])

libdrm_req = '>= 2.4.116'
libselinux_req = '>= 2.0.86'
xext_req = '>= 1.0.99.4'
xproto_req = '>= 7.0.31'
gbm_req = '>= 10.2'
xf86dgaproto_req = '>= 2.0.99.1'
xshmfence_req = '>= 1.1'

x11_dep = dependency('x11')
xproto_dep = dependency('xproto', version: xproto_req, fallback: ['xorgproto', 'ext_xorgproto'])
randrproto_dep = dependency('randrproto', version: '>= 1.6.0', fallback: ['xorgproto', 'ext_xorgproto'])
renderproto_dep = dependency('renderproto', version: '>= 0.11', fallback: ['xorgproto', 'ext_xorgproto'])
xextproto_dep = dependency('xextproto', version: '>= 7.2.99.901', fallback: ['xorgproto', 'ext_xorgproto'])
inputproto_dep = dependency('inputproto', version: '>= 2.3.99.1', fallback: ['xorgproto', 'ext_xorgproto'])
kbproto_dep = dependency('kbproto', version: '>= 1.0.3', fallback: ['xorgproto', 'ext_xorgproto'])
fontsproto_dep = dependency('fontsproto', version: '>= 2.1.3', fallback: ['xorgproto', 'ext_xorgproto'])
fixesproto_dep = dependency('fixesproto', version: '>= 6.0', fallback: ['xorgproto', 'ext_xorgproto'])
damageproto_dep = dependency('damageproto', version: '>= 1.1', fallback: ['xorgproto', 'ext_xorgproto'])
xcmiscproto_dep = dependency('xcmiscproto', version: '>= 1.2.0', fallback: ['xorgproto', 'ext_xorgproto'])
bigreqsproto_dep = dependency('bigreqsproto', version: '>= 1.1.0', fallback: ['xorgproto', 'ext_xorgproto'])
presentproto_dep = dependency('presentproto', version: '>= 1.4', fallback: ['xorgproto', 'ext_xorgproto'])

videoproto_dep = dependency('videoproto', fallback: ['xorgproto', 'ext_xorgproto'])
compositeproto_dep = dependency('compositeproto', version: '>= 0.4', fallback: ['xorgproto', 'ext_xorgproto'])
recordproto_dep = dependency('recordproto', version: '>= 1.13.99.1', fallback: ['xorgproto', 'ext_xorgproto'])
scrnsaverproto_dep = dependency('scrnsaverproto', version: '>= 1.1', fallback: ['xorgproto', 'ext_xorgproto'])
resourceproto_dep = dependency('resourceproto', version: '>= 1.2.0', fallback: ['xorgproto', 'ext_xorgproto'])
xf86driproto_dep = dependency('xf86driproto', version: '>= 2.1.0', fallback: ['xorgproto', 'ext_xorgproto'], required: get_option('dri1') == 'true')
dri2proto_dep = dependency('dri2proto', version: '>= 2.8', fallback: ['xorgproto', 'ext_xorgproto'], required: get_option('dri2') == 'true')
dri3proto_dep = dependency('dri3proto', version: '>= 1.4', fallback: ['xorgproto', 'ext_xorgproto'], required: get_option('dri3') == 'true')
xineramaproto_dep = dependency('xineramaproto', fallback: ['xorgproto', 'ext_xorgproto'])
xf86bigfontproto_dep = dependency('xf86bigfontproto', version: '>= 1.2.0', fallback: ['xorgproto', 'ext_xorgproto'], required: get_option('xf86bigfont'))
xf86vidmodeproto_dep = dependency('xf86vidmodeproto', version: '>= 2.2.99.1', fallback: ['xorgproto', 'ext_xorgproto'])
applewmproto_dep = dependency('applewmproto', version: '>= 1.4', fallback: ['xorgproto', 'ext_xorgproto'], required: false)
xshmfence_dep = dependency('xshmfence', version: xshmfence_req, required: false)
dpmsproto_dep = dependency('dpmsproto', version: '>= 1.2', required: get_option('dpms'))

pixman_dep = dependency('pixman-1')
libbsd_dep = dependency('libbsd-overlay', required: false)
xkbcomp_dep = dependency('xkbcomp', required: false)
xkbfile_dep = dependency('xkbfile')
xfont2_dep = dependency('xfont2', version: '>= 2.0')

dbus_required = get_option('systemd_logind') == 'true'
dbus_dep = dependency('dbus-1', version: '>= 1.0', required: dbus_required)

build_systemd = get_option('systemd_notify') == 'true'
# libsystemd-daemon was moved into libsystemd in version 209
libsystemd_daemon_dep = dependency('libsystemd', version: '>= 209', required: false)
if not libsystemd_daemon_dep.found()
    libsystemd_daemon_dep = dependency('libsystemd-daemon', required: false)
endif

build_hashtable = false

# Resolve default values of some options
xkb_dir = get_option('xkb_dir')
if xkb_dir == ''
    if xkbcomp_dep.found() and xkbcomp_dep.type_name() == 'pkgconfig'
        xkb_dir = xkbcomp_dep.get_variable(pkgconfig : 'xkbconfigdir')
    endif
    if xkb_dir == ''
        xkb_dir = join_paths(get_option('prefix'), 'share/X11/xkb')
    endif
endif

xkb_output_dir = get_option('xkb_output_dir')
if xkb_output_dir == ''
    xkb_output_dir = join_paths(xkb_dir, 'compiled')
endif

xkb_bin_dir = get_option('xkb_bin_dir')
if xkb_bin_dir == ''
    if xkbcomp_dep.found() and xkbcomp_dep.type_name() == 'pkgconfig'
        xkb_bin_dir = xkbcomp_dep.get_variable(pkgconfig : 'bindir')
    endif
    if xkb_bin_dir == ''
        xkb_bin_dir = join_paths(get_option('prefix'), get_option('bindir'))
    endif
endif

dfp = get_option('default_font_path')
if dfp == ''
    fontrootdir = get_option('fontrootdir')
    if fontrootdir == ''
        fontutil_dep = dependency('fontutil', required: false)
        if fontutil_dep.found()
            fontrootdir = fontutil_dep.get_variable(pkgconfig : 'fontrootdir')
        else
            fontrootdir = join_paths(get_option('prefix'), get_option('datadir'), 'fonts', 'X11')
        endif
    endif
    dfp_elements = [
        join_paths(fontrootdir, 'misc'),
        join_paths(fontrootdir, 'TTF'),
        join_paths(fontrootdir, 'OTF'),
        join_paths(fontrootdir, 'Type1'),
        join_paths(fontrootdir, '100dpi'),
        join_paths(fontrootdir, '75dpi'),
    ]
    if host_machine.system() == 'darwin'
       dfp_elements += [
       '/Library/Fonts',
       '/System/Library/Fonts',
    ]
    endif
    default_font_path = ','.join(dfp_elements)
else
    default_font_path = dfp
endif

glamor_option = get_option('glamor')

hal_option = get_option('hal')
if ['windows', 'darwin', 'cygwin'].contains(host_machine.system())
    hal_option = 'false'
endif

udev_option = get_option('udev')
udev_kms_option = get_option('udev_kms')
if not dependency('libudev', required: (udev_option == 'true' or udev_kms_option == 'true')).found()
    udev_option = 'false'
    udev_kms_option = 'false'
endif

build_udev = (udev_option != 'false')
build_udev_kms = (udev_kms_option != 'false')

if get_option('systemd_logind') == 'auto'
    build_systemd_logind = build_udev_kms and dbus_dep.found()
else
    build_systemd_logind = get_option('systemd_logind') == 'true'
endif

with_dtrace = get_option('dtrace')
if with_dtrace
    dtrace = find_program('dtrace', required: true)
endif

build_xorg = false
if (host_machine.system() != 'windows')
    if get_option('xorg') == 'auto'
        build_xorg = (host_machine.system() != 'darwin' and
                      host_machine.system() != 'windows')
    else
        build_xorg = get_option('xorg') == 'true'
    endif
endif
xorgsdkdir = join_paths(get_option('prefix'), get_option('includedir'), 'xorg')
libxcvt_dep = dependency('libxcvt', fallback: ['libxcvt', 'libxcvt_dep'], required: build_xorg)

## configure Xnest - nesting X server
build_xnest = get_option('xnest') != 'false'

build_xwin = false
if get_option('xwin') == 'auto'
    if host_machine.system() == 'windows'
            build_xwin = true
    endif
else
    build_xwin = get_option('xwin') == 'true'
endif

build_xquartz = false
if get_option('xquartz') == 'auto'
    if host_machine.system() == 'darwin'
            build_xquartz = true
    endif
else
    build_xquartz = get_option('xquartz') == 'true'
endif

build_rootless = false
if build_xquartz
    build_rootless = true
endif

build_xephyr = get_option('xephyr')
build_xvfb = get_option('xvfb')

summary({
        'Xorg': build_xorg,
        'Xnest': build_xnest,
        'Xvfb': build_xvfb,
        'Xwin': build_xwin,
        'Xquartz': build_xquartz,
    },
    section: 'DDX',
    bool_yn: true,
)

# IPv6 support
have_AF_INET6 = cc.compiles('''
#ifdef WIN32
#include <winsock2.h>
#else
#include <sys/socket.h>
#endif
int main(void) { int foo = AF_INET6; return foo; }''')
if get_option('ipv6') == 'auto'
    build_ipv6 = cc.has_function('getaddrinfo') and have_AF_INET6
else
    build_ipv6 = get_option('ipv6') == 'true'
endif
if build_ipv6 and not have_AF_INET6
    error('ipv6 support needs AF_INET6')
endif
message('IPv6 support: ' + (build_ipv6 ? 'YES' : 'NO'))

int10 = get_option('int10')
if int10 == 'auto'
    int10 = 'x86emu'
    if host_machine.cpu() == 'ppc' and host_machine.system() == 'freebsd'
        int10 = 'stub'
    endif
    if host_machine.cpu() == 'arm'
        int10 = 'stub'
    endif
endif

hal_dep = []
if hal_option == 'auto'
    if not build_udev
        hal_dep = dependency('hal', required: false)
        build_hal = hal_dep.found()
    else
        build_hal = false
    endif
else
    build_hal = hal_option == 'true'
    if build_hal
        hal_dep = dependency('hal')
    endif
endif

if build_hal
    message('WARNING: HAL is deprecated and might be removed in near future')
    message('If you really need it, please file a feature request on keeping it')
    message('and explain why you need it, what your use case is.')
endif

if build_udev and build_hal
    error('Hotplugging through both libudev and hal not allowed')
endif

build_dbus = build_hal or build_systemd_logind

udev_dep = dependency('', required:false)
if build_udev or build_udev_kms
    udev_dep = dependency('libudev', version: '>= 143')
endif

log_dir = get_option('log_dir')
if log_dir == ''
    log_dir = join_paths(get_option('prefix'), get_option('localstatedir'), 'log')
endif

module_dir = join_paths(get_option('libdir'), get_option('module_dir'))

if glamor_option == 'auto'
    build_glamor = build_xorg
else
    build_glamor = glamor_option == 'true'
endif

gbm_dep = dependency('', required: false)
epoxy_dep = dependency('', required: false)
if build_glamor
    gbm_dep = dependency('gbm', version: gbm_req, required: false)
    epoxy_dep = dependency('epoxy', required: false)
endif

# Lots of sha1 options, because Linux is about choice :)

# The idea behind the ordering here is that we should first prefer system
# builtin providers, and then smaller implementations of over larger ones.
test_sha1 = [
    'libc',          # libmd API is in libc on some BSDs
    'CommonCrypto',  # darwin API
    'CryptoAPI',     # windows API
    'libmd',         # other BSDs & Solaris
    'libsha1',       # "a tiny library providing a SHA1 implementation, created for facilitating X server compilation on embedded devices where larger libraries containing SHA1 implementations are not needed"
    'libnettle',
    'libgcrypt',     # in debian base system
    'libcrypto',
]

if get_option('sha1') != 'auto'
    test_sha1 = [get_option('sha1')]
endif

sha1_found = false
foreach t : test_sha1
    if t == 'libc'
        if cc.has_function('SHA1Init')
            sha1_found = true
            sha1_dep = dependency('', required: false)
        endif
    elif t == 'CommonCrypto'
        if cc.has_function('CC_SHA1_Init')
            sha1_found = true
            sha1_dep = dependency('', required: false)
        endif
    elif t == 'CryptoAPI'
        if cc.has_header('wincrypt.h')
            sha1_found = true
            sha1_dep = dependency('', required: false)
        endif
    elif t == 'libmd'
        md_dep = cc.find_library('md', required: false)
        if md_dep.found()
            sha1_found = true
            sha1_dep = md_dep
        endif
    elif t == 'libsha1'
        libsha1_dep = dependency('libsha1', required: false)
        if libsha1_dep.found()
            sha1_found = true
            sha1_dep = libsha1_dep
        endif
    elif t == 'libnettle'
        nettle_dep = dependency('nettle', required: false)
        if nettle_dep.found()
            sha1_found = true
            sha1_dep = nettle_dep
        endif
    elif t == 'libgcrypt'
        gcrypt_dep = dependency('libgcrypt', required: false)
        if gcrypt_dep.found()
            sha1_found = true
            sha1_dep = gcrypt_dep
        endif
    elif t == 'libcrypto'
        # we don't need all of OpenSSL, just libcrypto
        libcrypto_dep = cc.find_library('crypto', required: false)
        openssl_dep = dependency('openssl', required: false)
        if libcrypto_dep.found() or openssl_dep.found()
            sha1_found = true
            if libcrypto_dep.found()
               sha1_dep = libcrypto_dep
            else
               sha1_dep = openssl_dep
            endif
        endif
    endif

    if sha1_found
        sha1 = t
        break
    endif
endforeach

if sha1_found
    message('Using @0@ SHA1 functions'.format(sha1))
else
    if get_option('sha1') != 'auto'
        error('@0@ SHA1 requested, but not found'.format(get_option('sha1')))
    else
        error('No suitable SHA1 implementation found')
    endif
endif

xdmcp_dep = dependency('', required : false)
if get_option('xdmcp')
    xdmcp_dep = dependency('xdmcp')
endif

has_xdm_auth = get_option('xdm-auth-1')

if not xdmcp_dep.found()
  has_xdm_auth = false
endif

build_glx = get_option('glx')
if build_glx
    build_hashtable = true
endif

libdrm_dep = dependency('libdrm', version: libdrm_req, required: false)

if get_option('dri1') == 'auto'
    build_dri1 = xf86driproto_dep.found() and libdrm_dep.found()
else
    build_dri1 = get_option('dri1') == 'true'
endif

if get_option('dri2') == 'auto'
    build_dri2 = dri2proto_dep.found() and libdrm_dep.found()
else
    build_dri2 = get_option('dri2') == 'true'
endif

if host_machine.system() in ['freebsd', 'openbsd']
   epoll_dep = dependency('epoll-shim')
else
   epoll_dep = []
endif

have_eventfd = cc.has_header('sys/eventfd.h', dependencies: epoll_dep)
if get_option('dri3') == 'auto'
    build_dri3 = dri3proto_dep.found() and xshmfence_dep.found() and libdrm_dep.found() and have_eventfd
else
    build_dri3 = get_option('dri3') == 'true'
    if build_dri3
       if not xshmfence_dep.found()
           error('DRI3 requested, but xshmfence not found')
       endif
       if not have_eventfd
           error('DRI3 requested, but sys/eventfd.h not found')
       endif
    endif
endif

libdrm_required = (build_dri1 or build_dri2 or build_dri3) and get_option('drm') == true
if not libdrm_dep.found() and libdrm_required
    error('DRI requested, but LIBDRM not found')
endif

build_modesetting = libdrm_dep.found() and dri2proto_dep.found()

build_vgahw = false
if get_option('vgahw') == 'auto'
    if (host_machine.system() != 'darwin' and
        host_machine.system() != 'windows')
        build_vgahw = true
    endif
else
    build_vgahw = get_option('vgahw') == 'true'
endif

build_dpms = get_option('dpms')
if build_xquartz
    build_dpms = false
endif

build_xf86bigfont = get_option('xf86bigfont')
build_screensaver = get_option('screensaver')
build_res = get_option('xres')
if build_res
    build_hashtable = true
endif

build_xinerama = get_option('xinerama')
build_xsecurity = get_option('xcsecurity')
build_namespace = get_option('namespace')

build_xv = get_option('xv')
build_xvmc = get_option('xvmc')
if not build_xv
    build_xvmc = false
endif

build_dga = false
xf86dgaproto_dep = dependency('', required: false)
if get_option('dga') == 'auto'
    xf86dgaproto_dep = dependency('xf86dgaproto', version: xf86dgaproto_req, required: false)
    if xf86dgaproto_dep.found()
        build_dga = true
    endif
elif get_option('dga') == 'true'
    xf86dgaproto_dep = dependency('xf86dgaproto', version: xf86dgaproto_req, required: true)
    build_dga = true
endif

build_apm = false
if (get_option('linux_apm') == true and
   host_machine.system() == 'linux')
    if cc.has_header('linux/apm_bios.h')
        build_apm = true
    endif
endif

build_acpi = false
if (get_option('linux_acpi') == true and
   host_machine.system() == 'linux')
    if (host_machine.cpu() == 'x86' or
       host_machine.cpu() == 'x86_64' or
       host_machine.cpu() == 'ia64')
        build_acpi = true
    endif
endif

build_mitshm = false
if get_option('mitshm') == 'auto'
    build_mitshm = cc.has_header('sys/shm.h')
elif get_option('mitshm') == 'true'
    build_mitshm = true
endif

m_dep = cc.find_library('m', required : false)
dl_dep = cc.find_library('dl', required : false)

common_dep = [
    xproto_dep,
    randrproto_dep,
    renderproto_dep,
    xextproto_dep,
    inputproto_dep,
    kbproto_dep,
    fontsproto_dep,
    fixesproto_dep,
    damageproto_dep,
    xcmiscproto_dep,
    bigreqsproto_dep,
    presentproto_dep,
    libsystemd_daemon_dep,

    videoproto_dep,
    compositeproto_dep,
    recordproto_dep,
    scrnsaverproto_dep,
    resourceproto_dep,
    xf86driproto_dep,
    dri2proto_dep,
    dri3proto_dep,
    xineramaproto_dep,
    xf86bigfontproto_dep,
    xf86dgaproto_dep,
    xf86vidmodeproto_dep,
    applewmproto_dep,
    dpmsproto_dep,

    pixman_dep,
    libbsd_dep,
    xkbfile_dep,
    xfont2_dep,
    xdmcp_dep,
]

inc = include_directories(
    '.',
    'Xext',
    'Xi',
    'composite',
    'damageext',
    'exa',
    'fb',
    'glamor',
    'mi',
    'miext/damage',
    'miext/shadow',
    'miext/sync',
    'dbe',
    'dix',
    'dri3',
    'include',
    'present',
    'randr',
    'render',
    'xfixes',
)

build_xselinux = false
if get_option('xselinux') != 'false'
    dep_selinux = dependency('libselinux', version: libselinux_req,
			     required: get_option('xselinux') == 'true')
    dep_audit = dependency('audit', required: get_option('xselinux') == 'true')
    if get_option('xselinux') == 'true'
        build_xselinux = true
    else
        build_xselinux = dep_selinux.found() and dep_audit.found()
    endif

    if build_xselinux
        common_dep += dep_selinux
        common_dep += dep_audit
    endif
endif

socket_dep = []
if host_machine.system() == 'windows'
    socket_dep = meson.get_compiler('c').find_library('ws2_32')
    common_dep += socket_dep
endif

if get_option('libunwind')
    common_dep += dependency('libunwind', required: true)
endif

glx_inc = include_directories('glx')

top_dir_inc = include_directories('.')

serverconfigdir = get_option('serverconfigdir')
if serverconfigdir == ''
    serverconfigdir = join_paths(get_option('prefix'), get_option('libdir'), 'xorg')
endif

subdir('man')

require_docs = get_option('docs') == 'true'
require_devel_docs = get_option('devel-docs') == 'true'
require_docs_pdf = (require_docs or require_devel_docs) and get_option('docs-pdf') == 'true'

sgml_doctools_dep = dependency('xorg-sgml-doctools',
                               required: require_docs or require_devel_docs)
xmlto = find_program('xmlto', required: require_docs or require_devel_docs)
xsltproc = find_program('xsltproc', required: require_docs or require_devel_docs)
fop = find_program('fop', required: require_docs_pdf)

build_docs = (get_option('docs') != 'false' and
    sgml_doctools_dep.found() and
    xmlto.found())

build_docs_devel = (get_option('devel-docs') != 'false' and
    sgml_doctools_dep.found() and
    xmlto.found())

build_docs_pdf = (get_option('docs-pdf') != 'false' and
    (build_docs or build_docs_devel) and
    fop.found())

if build_docs or build_docs_devel
    doc_sgml_path = sgml_doctools_dep.get_variable(pkgconfig : 'sgmlrootdir')
    doc_stylesheet_srcdir = join_paths(doc_sgml_path, 'X11')

    # Meson does not and will not support functions so we are copy-pasting
    # documentation build code around which is unfortunate
    # See https://mesonbuild.com/FAQ.html#why-doesnt-meson-have-user-defined-functionsmacros

    docs_xmlto_search_flags = [
        '--searchpath', doc_stylesheet_srcdir,
        '--searchpath', meson.project_build_root(),
    ]

    docs_xslt_search_flags = [
        '--path', doc_stylesheet_srcdir,
        '--path', meson.project_build_root(),
    ]
endif

# Include must come first, as it sets up dix-config.h
subdir('include')

# X server core
subdir('config')
subdir('dix')
subdir('dri3')
subdir('glx')
subdir('fb')
subdir('mi')
subdir('os')
# X extensions
subdir('composite')
subdir('damageext')
subdir('dbe')
subdir('miext/damage')
subdir('miext/shadow')
subdir('miext/sync')
if build_rootless
    subdir('miext/rootless')
endif
subdir('present')
if build_xwin or build_xquartz
    subdir('pseudoramiX')
endif
subdir('randr')
subdir('record')
subdir('render')
subdir('xfixes')
subdir('xkb')
subdir('Xext')
subdir('Xi')
# other
if build_glamor
    subdir('glamor')
endif
if build_xorg or get_option('xephyr')
    subdir('exa')
endif
subdir('doc')

# Common static libraries of all X servers
libxserver = [
    libxserver_mi,
    libxserver_dix,

    libxserver_composite,
    libxserver_damageext,
    libxserver_dbe,
    libxserver_randr,
    libxserver_miext_damage,
    libxserver_render,
    libxserver_present,
    libxserver_xext,
    libxserver_miext_sync,
    libxserver_xfixes,
    libxserver_xi,
    libxserver_xkb,
    libxserver_record,

    libxserver_os,
]

libxserver += libxserver_dri3

if build_namespace
    subdir('Xext/namespace')
    libxserver += libxserver_namespace
endif

subdir('hw')

build_tests = get_option('tests') and host_machine.system() != 'windows'
if build_tests
    subdir('test')
endif

if build_xorg
    sdkconfig = configuration_data()
    awk = find_program('awk')

    sdkconfig.set('prefix', get_option('prefix'))
    sdkconfig.set('exec_prefix', '${prefix}')
    sdkconfig.set('libdir', join_paths('${exec_prefix}', get_option('libdir')))
    sdkconfig.set('includedir', join_paths('${prefix}', get_option('includedir')))
    sdkconfig.set('datarootdir', join_paths('${prefix}', get_option('datadir')))
    sdkconfig.set('moduledir', join_paths(join_paths('${exec_prefix}', module_dir), module_abi_tag))
    sdkconfig.set('sdkdir', join_paths('${prefix}', get_option('includedir'), 'xorg'))
    sdkconfig.set('sysconfigdir', join_paths('${datarootdir}', 'X11/xorg.conf.d'))

    sdkconfig.set('abi_ansic',
        run_command(awk, '-F', '[(,)]',
                    '/^#define ABI_ANSIC.*SET/ { printf "%d.%d", $2, $3 }',
                    files('hw/xfree86/common/xf86Module.h'),
                    check: false
        ).stdout()
    )
    sdkconfig.set('abi_videodrv',
        run_command(awk, '-F', '[(,)]',
                    '/^#define ABI_VIDEODRV.*SET/ { printf "%d.%d", $2, $3 }',
                    files('hw/xfree86/common/xf86Module.h'),
                    check: false
        ).stdout()
    )
    sdkconfig.set('abi_xinput',
        run_command(awk, '-F', '[(,)]',
                    '/^#define ABI_XINPUT.*SET/ { printf "%d.%d", $2, $3 }',
                    files('hw/xfree86/common/xf86Module.h'),
                    check: false
        ).stdout()
    )
    sdkconfig.set('abi_extension',
        run_command(awk, '-F', '[(,)]',
                    '/^#define ABI_EXTENSION.*SET/ { printf "%d.%d", $2, $3 }',
                    files('hw/xfree86/common/xf86Module.h'),
                    check: false
        ).stdout()
    )

    sdk_required_modules = [
      'pixman-1 >= 0.27.2',
      f'xproto @xproto_req@',
      'xfont2 >= 2.0',
    ]

    # XXX this isn't trying very hard, but hard enough.
    sdkconfig.set('PACKAGE_VERSION', meson.project_version())
    sdkconfig.set('SDK_REQUIRED_MODULES', ' '.join(sdk_required_modules))
    sdkconfig.set('symbol_visibility', '-fvisibility=hidden')
    sdkconfig.set('XORG_DRIVER_LIBS', '')

    # On Windows, modules built with the SDK will need to link with server and
    # module implibs to resolve symbols
    if host_machine.system() == 'windows'
        sdkconfig.set('XORG_DRIVER_LIBS', '-lXorg.exe -L\${moduledir} -lshadow -no-undefined')
    endif

    configure_file(
        input: 'xorg-server.pc.in',
        output: 'xorg-server.pc',
        configuration: sdkconfig,
        install_dir: join_paths(get_option('prefix'),
                                get_option('libdir'),
                                'pkgconfig'),
    )

    install_data('xorg-server.m4',
                 install_dir: join_paths(get_option('datadir'), 'aclocal'))
endif

if build_docs or build_docs_devel
    docxmlconfig = configuration_data()
    docxmlconfig.set('PACKAGE_VERSION', meson.project_version())
    docxmlconfig.set('RELEASE_DATE', release_date)
    configure_file(
        input: 'xserver.ent.in',
        output: 'xserver.ent',
        configuration: docxmlconfig
    )
endif

# finally write config files. doing that very late, so other subdirs still
# have a change to add config items
configure_file(output : 'dix-config.h',
               configuration : conf_data)

configure_file(output : 'xorg-server.h',
               input : 'include/xorg-server.h.meson.in',
               configuration : conf_data,
               install: build_xorg,
               install_dir: xorgsdkdir)
