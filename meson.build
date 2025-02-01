project(
    'aimeio-multi',
    'c',
    version: '0.0.1',
    default_options: [
        'warning_level=3',
    ],
)

add_project_arguments(
    '-DCOBJMACROS',
    '-DDIRECTINPUT_VERSION=0x0800',
    '-DWIN32_LEAN_AND_MEAN',
    '-D_WIN32_WINNT=_WIN32_WINNT_WIN7',
    '-DMINGW_HAS_SECURE_API=1',
    '-Wno-unused',
    language: 'c',
)

cc = meson.get_compiler('c')

if cc.get_id() != 'msvc'
    add_project_arguments(
        '-ffunction-sections',
        '-fdata-sections',
        '-flto',  # Enable Link-Time Optimization
        language: 'c',
    )

    add_project_link_arguments(
        '-Wl,--enable-stdcall-fixup',
        '-Wl,--exclude-all-symbols',
        '-Wl,--gc-sections',
        '-static-libgcc',
        '-flto',  # Enable Link-Time Optimization
        '-Wl,-s',  # Strip debug symbols
        language: 'c',
    )
endif

# 找到并包含 cJSON 库
cjson_dep = dependency('cjson', required: true)

inc = include_directories('.')

# 添加 aimeio 子目录
subdir('aimeio')

# 编译 aimeio 目录下的文件并链接 cJSON 库
aimeio_sources = files(
    'aimeio/aimeio.c',
    # 添加其他源文件
)

executable(
    'aimeio',
    aimeio_sources,
    include_directories: inc,
    dependencies: cjson_dep,
)
