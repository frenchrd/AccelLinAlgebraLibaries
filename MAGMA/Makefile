all: setEnv fortran_sgesv clean

.PHONY: setEnv fortran_sgesv clean

LIBS=-lcuda -lmagma -lmagmablas
MAGMAMODULE=./magma.f90
MAGMADEVMOD=./magma.cuf
SRC=sgesv.f90
DEVSRC=dgesv_gpu.cuf
OUTPUT=./magma_sgesv

setEnv:
ifdef CRAY_PRGENVINTEL
	$(error PrgEnv-gnu must be loaded!)
endif

ifdef CRAY_PRGENVPGI
	$(error PrgEnv-gnu must be loaded!)
endif

ifdef CRAY_PRGENVCRAY
	$(error PrgEnv-gnu must be loaded!)
endif
ifndef CRAY_LIBSCI
	$(error Must load the cray-libsci module!)
endif
#Check to see if the CUDA toolkit is loaded
ifndef CUDATOOLKIT_HOME
	$(error Must load the cudatoolkit module!)
endif

ifndef MAGMA_INC
	$(error Must load the MAGMA module!)
endif

setDev:
ifdef CRAY_PRGENVINTEL
	$(error PrgEnv-pgi must be loaded!)
endif

ifdef CRAY_PRGENVCRAY
	$(error PrgEnv-pgi must be loaded!)
endif
ifdef GCC_VERSION
	$(error PrgEnv-pgi must be loaded!)
endif
ifndef CRAY_LIBSCI
	$(error Must load the cray-libsci module!)
endif
#Check to see if the CUDA toolkit is loaded
ifndef CUDATOOLKIT_HOME
	$(error Must load the cudatoolkit module!)
endif

ifndef MAGMA_INC
	$(error Must load the MAGMA module!)
endif


fortran_sgesv: setEnv
	ftn $(MAGMAMODULE) $(LIBS) $(SRC) -o $(OUTPUT)

fortran_device: setDev
	ftn $(MAGMADEVMOD) $(LIBS) $(DEVSRC) -o $(OUTPUT)

C_sgesv: setEnv
	cc $(LIBS) sgesv.c -o $(OUTPUT)

clean: 
	rm -f *.o *.mod

