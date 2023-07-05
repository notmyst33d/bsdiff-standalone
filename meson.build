project('bsdiff-standalone', 'c', 'cpp')

libbrotli = library(
  'brotli',
  [
    'brotli/c/common/constants.c',
    'brotli/c/common/context.c',
    'brotli/c/common/dictionary.c',
    'brotli/c/common/platform.c',
    'brotli/c/common/transform.c',
    'brotli/c/dec/bit_reader.c',
    'brotli/c/dec/decode.c',
    'brotli/c/dec/huffman.c',
    'brotli/c/dec/state.c',
    'brotli/c/enc/backward_references.c',
    'brotli/c/enc/backward_references_hq.c',
    'brotli/c/enc/bit_cost.c',
    'brotli/c/enc/block_splitter.c',
    'brotli/c/enc/brotli_bit_stream.c',
    'brotli/c/enc/cluster.c',
    'brotli/c/enc/command.c',
    'brotli/c/enc/compress_fragment.c',
    'brotli/c/enc/compress_fragment_two_pass.c',
    'brotli/c/enc/dictionary_hash.c',
    'brotli/c/enc/encode.c',
    'brotli/c/enc/encoder_dict.c',
    'brotli/c/enc/entropy_encode.c',
    'brotli/c/enc/fast_log.c',
    'brotli/c/enc/histogram.c',
    'brotli/c/enc/literal_cost.c',
    'brotli/c/enc/memory.c',
    'brotli/c/enc/metablock.c',
    'brotli/c/enc/static_dict.c',
    'brotli/c/enc/utf8_util.c',
  ],
  link_args: ['-lm'],
)

libbz = library(
  'bz',
  [
    'bzip2/blocksort.c',
    'bzip2/bzlib.c',
    'bzip2/compress.c',
    'bzip2/crctable.c',
    'bzip2/decompress.c',
    'bzip2/huffman.c',
    'bzip2/randtable.c',
  ],
  c_args: ['-DUSE_MMAP'],
)

libdivsufsort = library(
  'divsufsort',
  [
    'libdivsufsort/lib/divsufsort.c',
    'libdivsufsort/lib/sssort.c',
    'libdivsufsort/lib/trsort.c',
    'libdivsufsort/lib/utils.c',
  ],
  include_directories: [
    'libdivsufsort/include',
    'libdivsufsort/android_include',
  ],
  c_args: ['-DHAVE_CONFIG_H=1'],
)

libdivsufsort64 = library(
  'divsufsort64',
  [
    'libdivsufsort/lib/divsufsort.c',
    'libdivsufsort/lib/sssort.c',
    'libdivsufsort/lib/trsort.c',
    'libdivsufsort/lib/utils.c',
  ],
  include_directories: [
    'libdivsufsort/include',
    'libdivsufsort/android_include',
  ],
  c_args: [
    '-DHAVE_CONFIG_H=1',
    '-DBUILD_DIVSUFSORT64',
  ],
)

libbsdiff = library(
  'bsdiff',
  [
    'bsdiff/brotli_compressor.cc',
    'bsdiff/bsdiff.cc',
    'bsdiff/bz2_compressor.cc',
    'bsdiff/compressor_buffer.cc',
    'bsdiff/diff_encoder.cc',
    'bsdiff/endsley_patch_writer.cc',
    'bsdiff/logging.cc',
    'bsdiff/patch_writer.cc',
    'bsdiff/patch_writer_factory.cc',
    'bsdiff/split_patch_writer.cc',
    'bsdiff/suffix_array_index.cc',
  ],
  include_directories: [
    'libdivsufsort/android_include',
    'bsdiff/include',
  ],
  c_args: ['-D_FILE_OFFSET_BITS=64'],
  link_with: [
    libbrotli,
    libbz,
    libdivsufsort,
    libdivsufsort64,
  ],
)

libbspatch = library(
  'bspatch',
  [
    'bsdiff/brotli_decompressor.cc',
    'bsdiff/bspatch.cc',
    'bsdiff/bz2_decompressor.cc',
    'bsdiff/buffer_file.cc',
    'bsdiff/decompressor_interface.cc',
    'bsdiff/extents.cc',
    'bsdiff/extents_file.cc',
    'bsdiff/file.cc',
    'bsdiff/logging.cc',
    'bsdiff/memory_file.cc',
    'bsdiff/patch_reader.cc',
    'bsdiff/sink_file.cc',
    'bsdiff/utils.cc',
  ],
  include_directories: ['bsdiff/include'],
  c_args: ['-D_FILE_OFFSET_BITS=64'],
  link_with: [
    libbrotli,
    libbz,
  ],
)

executable(
  'bsdiff',
  [
    'bsdiff/bsdiff_arguments.cc',
    'bsdiff/bsdiff_main.cc',
  ],
  include_directories: ['bsdiff/include'],
  link_with: [
    libbsdiff,
    libbrotli,
    libbz,
    libdivsufsort,
    libdivsufsort64,
  ],
)

executable(
  'bspatch',
  [
    'bsdiff/bspatch_main.cc',
  ],
  include_directories: ['bsdiff/include'],
  link_with: [
    libbspatch,
    libbrotli,
    libbz,
  ],
)
