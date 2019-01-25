load('//:buckaroo_macros.bzl', 'buckaroo_deps')
load('//:subdir_glob.bzl', 'subdir_glob')

genrule(
  name = 'config-h',
  out = 'config.h',
  cmd = 'touch $OUT',
)

linux_headers = {
  'config.h': 'config-generic.h',
}

macos_headers = {
  'config.h': 'macos/src/config-mac.h',
}

cxx_library(
  name = 'xml2',
  header_namespace = '',
  exported_headers = dict(
    subdir_glob([
      ('include', '**/*.h'),
    ]).items() + [
      ('libxml/xmlversion.h', 'include/libxml/xmlversion-generic.h'),
    ]
  ),
  headers = subdir_glob([
    ('', '*.h'),
  ]),
  platform_headers = [
    ('macos.*', macos_headers),
    ('linux.*', linux_headers),
  ],
  # preprocessor_flags = [
  #   '-DLIBXML_LZMA_ENABLED=1',
  # ],
  srcs = glob([
    '*.c',
  ], exclude = glob([
    'run*.c',
    'test*.c',
    'trio.c',
  ])),
  deps = buckaroo_deps(),
  visibility = [
    'PUBLIC',
  ],
)
