AUTOMAKE_OPTIONS = subdir-objects

AM_LDFLAGS =
AM_CFLAGS = $(fftw_CFLAGS) $(cfitsio_CFLAGS)
AM_CXXFLAGS = $(fftw_CXXFLAGS) $(cfitsio_CXXFLAGS)
AM_CPPFLAGS = -I${top_srcdir}/src

if USE_OPENMP
AM_CPPFLAGS += -DUSE_OPENMP
AM_CXXFLAGS += $(OPENMP_CXXFLAGS)
AM_LDFLAGS += $(OPENMP_LDFLAGS)
endif

if USE_FFTW_THREADS
AM_CPPFLAGS += -DFFTW_THREADING
endif

if USE_GSL
AM_CXXFLAGS += $(gsl_CXXFLAGS)
else
AM_CPPFLAGS += -DNO_GSL
endif

if USE_NLOPT
AM_CXXFLAGS += $(nlopt_CXXFLAGS)
else
AM_CPPFLAGS += -DNO_NLOPT
endif

################################################################################
# Source files
################################################################################

C_SRC = mp_enorm.c \
        statistics.c \
        mersenne_twister.c

FIT_SRC = levmar_fit.cpp \
          mpfit.cpp \
          diff_evoln_fit.cpp \
          DESolver.cpp \
          utilities.cpp \
          print_results.cpp \
          config_file_parser.cpp
if USE_NLOPT
FIT_SRC += nmsimplex_fit.cpp
endif

MODEL_SRC = model_object.cpp \
            convolver.cpp

FUNCTION_SRC = function_object.cpp \
               func_gaussian.cpp \
               func_exp.cpp \
               func_gen-exp.cpp \
               func_sersic.cpp \
               func_gen-sersic.cpp \
               func_core-sersic.cpp \
               func_broken-exp.cpp \
               func_broken-exp2d.cpp \
               func_moffat.cpp \
               func_flatsky.cpp \
               func_gaussian-ring.cpp \
               func_gaussian-ring2side.cpp \
               func_edge-on-disk_n4762.cpp \
               func_edge-on-disk_n4762v2.cpp \
               func_edge-on-ring.cpp \
               func_edge-on-ring2side.cpp \
               add_functions.cpp
if USE_GSL
FUNCTION_SRC += func_edge-on-disk.cpp \
                integrator.cpp \
                func_expdisk3d.cpp \
                func_brokenexpdisk3d.cpp \
                func_gaussianring3d.cpp
endif

COMMON_SRC = commandline_parser.cpp \
             image_io.cpp

################################################################################
# Header files
################################################################################

C_HDR = definitions.h \
        mersenne_twister.h \
        statistics.h \
        mp_enorm.h

FIT_HDR = diff_evoln_fit.h \
          DESolver.h \
          levmar_fit.h \
          mpfit_cpp.h \
          param_struct.h \
          utilities_pub.h \
          print_results.h \
          config_file_parser.h
if USE_NLOPT
FIT_HDR += nmsimplex_fit.h
endif
                    
MODEL_HDR = model_object.h \
            convolver.h

FUNCTION_HDR = function_object.h \
               func_gaussian.h \
               func_exp.h \
               func_gen-exp.h \
               func_sersic.h \
               func_gen-sersic.h \
               func_core-sersic.h \
               func_broken-exp.h \
               func_broken-exp2d.h \
               func_moffat.h \
               func_flatsky.h \
               func_gaussian-ring.h \
               func_gaussian-ring2side.h \
               func_edge-on-disk_n4762.h \
               func_edge-on-disk_n4762v2.h \
               func_edge-on-ring.h \
               func_edge-on-ring2side.h \
               add_functions.h
if USE_GSL
FUNCTION_HDR += func_edge-on-disk.h \
                integrator.h \
                func_expdisk3d.h \
                func_brokenexpdisk3d.h \
                func_gaussianring3d.h
endif

COMMON_HDR = commandline_parser.h \
             image_io.h

LIB_HDR = definitions.h \
          model_object.h \
          add_functions.h \
          param_struct.h \
          levmar_fit.h \
          diff_evoln_fit.h \
          function_object.h \
          convolver.h \
          config_file_parser.h \
          print_results.h \
          mpfit_cpp.h
if USE_NLOPT
LIB_HDR += nmsimplex_fit.h
endif
          

################################################################################
# Main programs
################################################################################

bin_PROGRAMS = imfit makeimage
lib_LTLIBRARIES = libimfit.la

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = ${top_srcdir}/imfit.pc

################################################################################

libimfit_la_SOURCES = $(C_SRC) $(FIT_SRC) $(MODEL_SRC) $(FUNCTION_SRC) \
                      $(C_HDR) $(FIT_HDR) $(MODEL_HDR) $(FUNCTION_HDR)

libimfit_la_LDFLAGS = $(fftw_LIBS) $(gsl_LIBS) $(nlopt_LIBS)

pkginclude_HEADERS = $(LIB_HDR)
                     
################################################################################

makeimagedir = ${includedir}

makeimage_LDADD = $(fftw_LIBS) $(gsl_LIBS) $(nlopt_LIBS) $(cfitsio_LIBS) libimfit.la

makeimage_SOURCES = makeimage_main.cpp \
                    $(COMMON_HDR) $(COMMON_SRC)
                    

################################################################################

imfitdir = ${includedir}

imfit_LDADD = $(fftw_LIBS) $(gsl_LIBS) $(nlopt_LIBS) $(cfitsio_LIBS) libimfit.la

imfit_SOURCES = bootstrap_errors.h \
                bootstrap_errors.cpp \
                imfit_main.cpp \
                $(COMMON_HDR) $(COMMON_SRC)
                