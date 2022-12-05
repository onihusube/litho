project('chttpp', 'cpp', default_options : ['warning_level=3', 'cpp_std=c++20'], meson_version : '>=0.58.0')

#インクルードディレクトリ
include_dir = include_directories('include')

#コンパイルオプション調整
cppcompiler = meson.get_compiler('cpp').get_argument_syntax()

if cppcompiler == 'msvc'
    # VSプロジェクトに編集しうるファイルを追加する
    vs_files = ['include/litho.hpp', 'test/litho_test.c pp']
elif cppcompiler == 'gcc'
    vs_files = []
endif

if not meson.is_subproject()

# デバッグ用設定
env = environment()
env.set('cpp_debugstl', 'true')
meson.add_devenv(env)

# テストプロジェクト用の設定追加
if cppcompiler == 'msvc'
    options = ['/source-charset:utf-8', '/Zc:__cplusplus']
elif cppcompiler == 'gcc'
    options = []
endif

# 依存プロジェクト
boostut_dep = dependency('boost.ut')

exe = executable('litho_test', 'test/litho_test.cpp', include_directories : include_dir, extra_files : vs_files, cpp_args : options, dependencies : boostut_dep)
test('litho test', exe)

else

# ライブラリ利用時の設定追加
if cppcompiler == 'msvc'
    options = ['/source-charset:utf-8']
elif cppcompiler == 'gcc'
    options = []
endif

# subprojectとして構築時は依存オブジェクトの宣言だけしとく
litho_dep = declare_dependency(include_directories : include_directories('include'), cpp_args : options)

endif