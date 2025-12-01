project(
    'RRFLibraries',
    'c',
    'cpp',
    version : '3.6.1',
    default_options : [
        'c_std=gnu99',
        'cpp_std=gnu++17',
        'prefer_static=true'
    ]
)

mcu = get_option('mcu')
if mcu == ''
    error('Target MCU was not specified. Example: -Dmcu=ATSAME51G19A')
endif
freertos_mcu = get_option('freertos_mcu')

includes = [
    'src/'
]

if build_machine.system() == 'windows'
    g = run_command('scripts\glob.bat', check : false)
    source_globber = find_program('scripts\glob.bat')
else
    g = run_command('scripts/glob.sh', check : false)
    source_globber = find_program('scripts/glob.sh')
endif

newline = '''
'''

if mcu == 'ATSAME51G19A'
    if freertos_mcu == ''
        freertos_mcu = mcu
    endif

    add_project_arguments(
        '-D__SAME51G19A__',
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

sources = g.stdout().strip().split(newline)
message('=== Sources ===')
foreach s : sources
    message(s)
endforeach
message('===============')

freertos = subproject('FreeRTOS', default_options : { 'mcu' : freertos_mcu })
freertos_dep = freertos.get_variable('freertos_dep')

RRFLibraries = static_library(
    'RRFLibraries',
    sources,
    include_directories : include_directories(includes),
    dependencies : freertos_dep
)

RRFLibraries_dep = declare_dependency(
    include_directories : include_directories(includes),
    link_with : RRFLibraries
)
