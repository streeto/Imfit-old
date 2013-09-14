AUTOMAKE_OPTIONS = subdir-objects

AM_LDFLAGS =
AM_CFLAGS = $(fftw_CFLAGS) $(cfitsio_CFLAGS)
AM_CXXFLAGS = $(fftw_CXXFLAGS) $(cfitsio_CXXFLAGS)
AM_CPPFLAGS = -I${top_srcdir}/src -I${top_srcdir}/src/function_objects
my_LIBS = $(fftw_LIBS) $(cfitsio_LIBS)

if USE_OPENMP
AM_CPPFLAGS += -DUSE_OPENMP
AM_CXXFLAGS += $(OPENMP_CXXFLAGS)
AM_LDFLAGS += $(OPENMP_LDFLAGS)
endif

if USE_FFTW_THREADS
# This is probably not the most portable way.
my_LIBS += -lfftw3_threads
AM_CPPFLAGS += -DFFTW_THREADING
endif

if USE_GSL
GSL_SRC = function_objects/func_edge-on-disk.cpp \
          function_objects/integrator.cpp \
          function_objects/func_expdisk3d.cpp \
          function_objects/func_brokenexpdisk3d.cpp \
          function_objects/func_gaussianring3d.cpp
GSL_HDR = function_objects/func_edge-on-disk.h \
          function_objects/integrator.h \
          function_objects/func_expdisk3d.h \
          function_objects/func_brokenexpdisk3d.h \
          function_objects/func_gaussianring3d.h
AM_CXXFLAGS += $(gsl_CXXFLAGS)
my_LIBS += $(gsl_LIBS)
else
GSL_SRC = 
GSL_HDR = 
AM_CPPFLAGS += -DNO_GSL
endif

if USE_NLOPT
NLOPT_SRC = nmsimplex_fit.cpp
NLOPT_HDR = nmsimplex_fit.h
AM_CXXFLAGS += $(nlopt_CXXFLAGS)
my_LIBS += $(nlopt_LIBS)
else
NLOPT_SRC = 
NLOPT_HDR = 
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
          print_results.cpp

MODEL_SRC = model_object.cpp \
            convolver.cpp

FUNCTION_SRC = function_objects/function_object.cpp \
               function_objects/func_gaussian.cpp \
               function_objects/func_exp.cpp \
               function_objects/func_gen-exp.cpp \
               function_objects/func_sersic.cpp \
               function_objects/func_gen-sersic.cpp \
               function_objects/func_core-sersic.cpp \
               function_objects/func_broken-exp.cpp \
               function_objects/func_broken-exp2d.cpp \
               function_objects/func_moffat.cpp \
               function_objects/func_flatsky.cpp \
               function_objects/func_gaussian-ring.cpp \
               function_objects/func_gaussian-ring2side.cpp \
               function_objects/func_edge-on-disk_n4762.cpp \
               function_objects/func_edge-on-disk_n4762v2.cpp \
               function_objects/func_edge-on-ring.cpp \
               function_objects/func_edge-on-ring2side.cpp

COMMON_SRC = commandline_parser.cpp \
             utilities.cpp \
             image_io.cpp \
             config_file_parser.cpp \
             add_functions.cpp

################################################################################
# Header files
################################################################################

C_HDR = mersenne_twister.h \
        statistics.h \
        mp_enorm.h

FIT_HDR = diff_evoln_fit.h \
          DESolver.h \
          levmar_fit.h \
          mpfit_cpp.h \
          param_struct.h \
          print_results.h
                    
MODEL_HDR = model_object.h \
            convolver.h

FUNCTION_HDR = function_objects/function_object.h \
               function_objects/func_gaussian.h \
               function_objects/func_exp.h \
               function_objects/func_gen-exp.h \
               function_objects/func_sersic.h \
               function_objects/func_gen-sersic.h \
               function_objects/func_core-sersic.h \
               function_objects/func_broken-exp.h \
               function_objects/func_broken-exp2d.h \
               function_objects/func_moffat.h \
               function_objects/func_flatsky.h \
               function_objects/func_gaussian-ring.h \
               function_objects/func_gaussian-ring2side.h \
               function_objects/func_edge-on-disk_n4762.h \
               function_objects/func_edge-on-disk_n4762v2.h \
               function_objects/func_edge-on-ring.h \
               function_objects/func_edge-on-ring2side.h

COMMON_HDR = commandline_parser.h \
             image_io.h \
             config_file_parser.h \
             add_functions.h \
             definitions.h \
             utilities_pub.h

################################################################################
# Main programs
################################################################################

bin_PROGRAMS = imfit makeimage
lib_LTLIBRARIES = libimfit.la

################################################################################

libimfit_la_SOURCES = $(C_SRC) $(FIT_SRC) $(MODEL_SRC) $(FUNCTION_SRC) \
                      $(GSL_SRC) $(NLOPT_SRC) \
                      $(C_HDR) $(FIT_HDR) $(MODEL_HDR) $(FUNCTION_HDR) \
                      $(GSL_HDR) $(NLOPT_HDR)

################################################################################

makeimagedir = ${includedir}

makeimage_LDADD = $(my_LIBS) libimfit.la

makeimage_SOURCES = makeimage_main.cpp \
                    $(COMMON_HDR) $(COMMON_SRC)
                    

################################################################################

imfitdir = ${includedir}

imfit_LDADD = $(my_LIBS) libimfit.la

imfit_SOURCES = bootstrap_errors.h \
                bootstrap_errors.cpp \
                imfit_main.cpp \
                $(COMMON_HDR) $(COMMON_SRC)
                