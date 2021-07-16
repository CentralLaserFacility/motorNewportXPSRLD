# Makefile
TOP = ../..
include $(TOP)/configure/CONFIG
#
# Both the following line, and a line in the *.dbd file,
# must be uncommented to use diagnostic debugging messages.
#!USR_CXXFLAGS += -DDEBUG

# The Newport XPS_RLD_driver.cpp file uses "char *" when they should use "const char *".
# Turn off warnings when we call this functions with string constants
USR_CPPFLAGS_Linux += -Wno-write-strings

ifeq ("$(HAVE_LIBCURL)", "YES")
  USR_CXXFLAGS += -DHAVE_LIBCURL
  PROD_SYS_LIBS += curl
endif

ifeq ("$(HAVE_LIBSSH2)", "YES")
  USR_CXXFLAGS += -DHAVE_LIBSSH2
  PROD_SYS_LIBS += ssh2
endif

# Install the XPS header file in case applications in another module need to use it
INC += XPS_RLD_drivers.h

DBD += devNewport.dbd
ifdef SNCSEQ
DBD += devNewportSeq.dbd
endif

LIBRARY_IOC = NewportXPSRLD

NewportXPSRLD_SRCS += NewportRegister.cc

# MM3000 (i.e., MM3000) device driver.
NewportXPSRLD_SRCS += devMM3000.cc drvMM3000.cc

# MM4000/5 (i.e., MM4000) device driver.
NewportXPSRLD_SRCS += devMM4000.cc drvMM4000.cc
NewportXPSRLD_SRCS += drvMM4000Asyn.c
ifdef SNCSEQ
NewportXPSRLD_SRCS += MM4005_trajectoryScan.st
endif

# PM500 device driver.
NewportXPSRLD_SRCS += devPM500.cc  drvPM500.cc

# ESP300 device driver.
NewportXPSRLD_SRCS += devESP300.cc drvESP300.cc

# SMC100 device driver
NewportXPSRLD_SRCS += SMC100Driver.cpp

# Agilis device drivers
NewportXPSRLD_SRCS += AG_UC.cpp
NewportXPSRLD_SRCS += AG_CONEX.cpp

# XPS C8 device driver
NewportXPSRLD_SRCS += asynOctetSocket.cpp 
NewportXPSRLD_SRCS += XPS_RLD_drivers.cpp 
NewportXPSRLD_SRCS += drvXPSAsynAux.c
NewportXPSRLD_SRCS += xps_ftp.c
NewportXPSRLD_SRCS += xpsSFTPUpload.c
# This is the model 2 asyn driver
NewportXPSRLD_SRCS += drvXPSAsyn.c XPSAsynInterpose.c
# This is the model 3 asyn driver
NewportXPSRLD_SRCS += XPSController.cpp
NewportXPSRLD_SRCS += XPSAxis.cpp
ifdef SNCSEQ
NewportXPSRLD_SRCS += XPS_trajectoryScan.st
NewportXPSRLD_SRCS += xpsSlave.st
endif
#
NewportXPSRLD_SRCS += hxp_drivers.cpp
NewportXPSRLD_SRCS += HXPDriver.cpp
 
# strtok_r needed on WIN32
NewportXPSRLD_SRCS_WIN32 += strtok_r.c

# XPS Gathering test function
NewportXPSRLD_SRCS += XPSGathering.c
NewportXPSRLD_SRCS += XPSGatheringRegister.c

# Function which will run a tcl script on an XPS
NewportXPSRLD_SRCS += tclCall.cc

NewportXPSRLD_LIBS += motor asyn
ifdef SNCSEQ
NewportXPSRLD_LIBS += seq pv
endif
NewportXPSRLD_LIBS += $(EPICS_BASE_IOC_LIBS)
NewportXPSRLD_SYS_LIBS_WIN32 += ws2_32

PROD_IOC += XPSGatheringMain
XPSGatheringMain_SRCS += XPSGatheringMain.c
XPSGatheringMain_LIBS += Newport motor asyn
ifdef SNCSEQ
XPSGatheringMain_LIBS += seq pv
endif
XPSGatheringMain_LIBS += $(EPICS_BASE_IOC_LIBS)

PROD_IOC += XPSGathering2
XPSGathering2_SRCS += XPSGathering2.c
XPSGathering2_LIBS += Newport motor asyn
XPSGathering2_LIBS += $(EPICS_BASE_IOC_LIBS)

PROD_IOC += testSFTPUpload
testSFTPUpload_SRCS += testSFTPUpload.cpp
testSFTPUpload_LIBS += Newport asyn $(EPICS_BASE_IOC_LIBS)

ifeq ("$(HAVE_LIBCURL)", "YES")
  PROD_IOC += curl_gen
endif

include $(TOP)/configure/RULES

