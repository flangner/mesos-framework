HEADERS = config.hpp
SOURCES := quobyte-mesos-executor.cpp executor.cpp
BINARY = quobyte-mesos-executor
MESOS_SRC = ../thirdparty/mesos
INCLUDE_DIRS = -I../common -I$(MESOS_SRC)/src -I$(MESOS_SRC)/build/include -I$(MESOS_SRC)/include -I$(MESOS_SRC)/build/src -I$(MESOS_SRC)/build/3rdparty/zookeeper-3.4.5/src/c/include/ -I$(MESOS_SRC)/build/3rdparty/zookeeper-3.4.5/src/c/generated/ -I$(MESOS_SRC)/build/3rdparty/libprocess/3rdparty/picojson-4f93734/

CXX = g++
CXXFLAGS = -g -O2 -pthread -std=c++11
LDFLAGS += -L$(MESOS_LIB_DIR) -lmesos-$(MESOS_VERSION) -lprotobuf
CXXCOMPILE = $(CXX) $(INCLUDE_DIRS) $(INCLUDES) $(CXXFLAGS) -c $< 
CXXLINK = $(CXX) $(LDFLAGS) -o $(BINARY)

OBJS := $(SOURCES:.cpp=.o)
default: all
all: $(BINARY)

executor.tar.gz: $(BINARY)
	./gather_libs.sh
	tar cvf executor.tar.gz $(BINARY) .libs

$(BINARY): $(OBJS)
	$(CXXLINK) $(OBJS) ../common/libquobyteproto.a
	
.cpp.o: $(HEADERS)
	$(CXXCOMPILE)
	
.cc.o: $(HEADERS)
	$(CXXCOMPILE)
	
clean:
	(rm -f quobyte-mesos $(OBJS))
