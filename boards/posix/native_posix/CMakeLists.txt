zephyr_library()
zephyr_library_compile_definitions(_POSIX_CHEATS_H)
zephyr_library_sources(
	hw_models_top.c
	timer_model.c
	irq_handler.c
	irq_ctrl.c
	main.c
	tracing.c
	cmdline_common.c
	cmdline.c
	)

zephyr_ld_options(
  -lm
)

# Override the C standard used for compilation to C 2011
# This is due to some tests using _Static_assert which is a 2011 feature, but
# otherwise relying on compilers supporting it also when set to C99.
# This was in general ok, but with some host compilers and C library versions
# it led to problems. So we override it to 2011 for native_posix.
set_property(GLOBAL PROPERTY CSTD c11)
