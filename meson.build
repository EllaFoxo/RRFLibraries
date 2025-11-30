project(
    'librrflibraries',
    'c',
    'cpp',
    version : '3.6.1',
    default_options : [
        'c_std=gnu99',
        'cpp_std=gnu++17',
        'board=TOOL1RR'
    ]
)

includes = [
    'src/'
]

sources = [
    'src/General/IP4String.cpp',
    'src/General/IPAddress.cpp',
    'src/General/NamedEnum.cpp',
    'src/General/NumericConverter.cpp',
    'src/General/SafeStrtod.cpp',
    'src/General/SafeVsnprintf.cpp',
    'src/General/SimpleMath.cpp',
    'src/General/StringBuffer.cpp',
    'src/General/StringFunctions.cpp',
    'src/General/StringRef.cpp',
    'src/General/Strnlen.cpp',
    'src/Math/Deviation.cpp',
    'src/Math/DeviationAccumulator.cpp',
    'src/Math/Isqrt.cpp',
    'src/RTOSIface/RTOSIface.cpp',
]

if get_option('board') == 'TOOL1RR'
    includes += []
    sources += []

    add_project_arguments(
        '-D__SAME51N19A__',
        '-DRTOS',
        '-c',
        '-mcpu=cortex-m4',
        '-mthumb',
        '-fno-math-errno',
        '-mfpu=fpv4-sp-d16',
        '-mfloat-abi=hard',
        '-mfp16-format=ieee',
        '-ffunction-sections',
        '-fdata-sections',
        '-nostdlib',
        '-Wdouble-promotion',
        '-fsingle-precision-constant',
        '-Wa,-ahl=$*.s',
        '-fstack-usage',
        '-fdump-rtl-expand',
        language : 'c'
    )

    add_project_arguments(
        '-D__SAME51N19A__',
        '-DRTOS',
        '-c',
        '-mcpu=cortex-m4',
        '-mthumb',
        '-fno-math-errno',
        '-mfpu=fpv4-sp-d16',
        '-mfloat-abi=hard',
        '-mfp16-format=ieee',
        '-ffunction-sections',
        '-fno-threadsafe-statics',
        '-fdata-sections',
        '-fno-rtti',
        '-fno-exceptions',
        '-nostdlib',
        '-Wundef',
        '-Wdouble-promotion',
        '-fsingle-precision-constant',
        '-Wa,-ahl=$*.s',
        '-fstack-usage',
        '-fdump-rtl-expand',
        language : 'cpp'
    )
endif

libfreertos = subproject('libfreertos')
libfreertos_dep = libfreertos.get_variable('libfreertos_dep')

librrflibraries = static_library(
    'rrflibraries',
    sources,
    include_directories : include_directories(includes),
    dependencies : libfreertos_dep
)

librrflibraries_dep = declare_dependency(
    include_directories : include_directories(includes),
    link_with : librrflibraries
)
