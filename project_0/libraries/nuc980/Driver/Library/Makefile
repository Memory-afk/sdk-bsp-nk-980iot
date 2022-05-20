TARGET	?= libstddriver_gcc

#################################
# GNU ARM Embedded Toolchain
#################################
CC=arm-none-eabi-gcc
CXX=arm-none-eabi-g++
LD=arm-none-eabi-ld
AR=arm-none-eabi-ar
AS=arm-none-eabi-as
CP=arm-none-eabi-objcopy
OD=arm-none-eabi-objdump
NM=arm-none-eabi-nm
SIZE=arm-none-eabi-size
A2L=arm-none-eabi-addr2line

#################################
# Working directories
#################################
STDDRIVER_DIR = ../
ROOT		 = ../Library
OBJECT_DIR	 = $(ROOT)/build/gcc
BIN_DIR		 = $(ROOT)/build/gcc

#################################
# Source Files
#################################

# Search path and source files for the ST stdperiph library

CSOURCES =  $(notdir $(wildcard $(STDDRIVER_DIR)/Source/*.c))

INCLUDE_DIRS  =	-I$(ROOT)
INCLUDE_DIRS += -I$(STDDRIVER_DIR)/Include 
INCLUDE_DIRS +=	-I$(DEVICE_DIR)

#################################
# Object List
#################################
OBJECTS=

#################################
# Target Output Files
#################################
TARGET_A=$(TARGET).a

#################################
# Flags
#################################
MCFLAGS= -mcpu=arm926ej-s
OPTIMIZE = -O0 -gdwarf-2
DEFS=
CFLAGS=-c $(MCFLAGS) $(DEFS) $(OPTIMIZE) $(addprefix -I,$(INCLUDE_DIRS)) -std=c99
CXXFLAGS=-c $(MCFLAGS) $(DEFS) $(OPTIMIZE) $(addprefix -I,$(INCLUDE_DIRS)) -std=c++11
LDSCRIPT=
LDFLAGS =

#################################
# Build
#################################
all: clean $(TARGET_A)

$(TARGET_A):
	@echo -n "Build $@ ..."
	@cd $(STDDRIVER_DIR)/Source && \
		$(CC) -c $(INCLUDE_DIRS) $(CFLAGS) $(CSOURCES)
	$(AR) cr -o $@ \
		$(STDDRIVER_DIR)/Source/*.o
	$(SIZE) $(TARGET_A)

#################################
# Recipes
#################################
.PHONY: all clean

clean:
	rm -f $(STDDRIVER_DIR)/Source/*.o $(TARGET_A)