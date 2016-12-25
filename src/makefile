CC = g++
CFLAGS = -O4 -Wall
INCS = -I../bliss-0.73

all: tmf

tmf: main.o events.o edges.o tsubgraph.o subnets.o binner.h motif.o progress_counter.o bin_limits.o
	mkdir -p ../bin
	${CC} ${CFLAGS} -o  ../bin/tmf main.o tsubgraph.o subnets.o events.o edges.o motif.o progress_counter.o bin_limits.o -lstdc++ -L ../bliss-0.73 -lbliss

main.o: events.o tsubgraph.o main.cc subnets.o
	${CC} ${CFLAGS} -c ${INCS} main.cc 

tsubgraph.o: tsubgraph.h tsubgraph.cc 
	${CC} ${CFLAGS} -c ${INCS} tsubgraph.cc

events.o: events.h events.cc
	${CC} ${CFLAGS} -c ${INCS} events.cc  

edges.o: edges.h edges.cc
	${CC} ${CFLAGS} -c ${INCS} edges.cc 

subnets.o: subnets.h subnets.cc
	${CC} ${CFLAGS} -c ${INCS} subnets.cc

bin_limits.o: bin_limits.h bin_limits.cc
	${CC} ${CFLAGS} -c ${INCS} bin_limits.cc

motif.o: motif.h motif.cc
	${CC} ${CFLAGS} -c ${INCS} motif.cc

progress_counter.o: progress_counter.h progress_counter.cc
	${CC} ${CFLAGS} -c ${INCS} progress_counter.cc

clean:
	rm -f ../bin/tmf main.o events.o edges.o tsubgraph.o subnets.o motif.o progress_counter.o bin_limits.o
