CXX=`root-config --cxx`
CXXFLAGS=`root-config --cflags` -Wall -Werror -O3 -Wextra -Wno-unused-local-typedefs -Wno-deprecated-declarations -std=c++11 -g

ifeq "$(GCCVERSION)" "1"
	CXXFLAGS += -Wno-error=misleading-indentation
endif

#INCLUDE=-I$(PWD) -I/sphenix/u/cmcginn/testinstall/CleanSPHENIXMacros
INCLUDE=-I$(PWD) -I/sphenix/u/cmcginn/testinstall/CleanPRMacros -I/sphenix/u/cmcginn/testinstall
ROOTLIBS=`root-config --glibs`

MKDIR_LIB=mkdir -p $(PWD)/lib
MKDIR_OUTPUT=mkdir -p $(PWD)/output

all: mkdirLib mkdirOutput treeMakerDict.C lib/libTreeMaker.so

mkdirLib:
	$(MKDIR_LIB)

mkdirOutput:
	$(MKDIR_OUTPUT)

treeMakerDict.C: TreeMaker.h Linkdef.h
	@rootcint -f $@ -c $(INCLUDE) -p $^

lib/libTreeMaker.so: treeMakerDict.C TreeMaker.C
	@$(CXX) $(CXXFLAGS) -shared  $(INCLUDE) -o lib/libTreeMaker.so $(ROOTLIBS)


clean:
	rm -f *.so
	rm -f lib/*.so
	rm -rf lib
	rm -f *.o
	rm -f *~
	rm -f *#
	rm -f treeMakerDict.C
	rm -f *.pcm
