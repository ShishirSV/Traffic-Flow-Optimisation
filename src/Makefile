CC = g++
NVCC = nvcc

# run make all to create ./maxflow executable
all : maxflow

# run make debug to create ./maxflowdbg executable, which is the debug build to use in cuda-gdb and cuda-memcheck
debug : maxflowdbg

maxflow : obj/graph_s.o obj/io_par.o obj/main.o obj/preflow.o obj/push_relabel_kernel.o obj/push_relabel.o obj/global_relabel.o
	$(NVCC) obj/graph_s.o obj/io_par.o obj/main.o obj/preflow.o obj/push_relabel_kernel.o obj/push_relabel.o obj/global_relabel.o -o maxflow

maxflowdbg : obj/graph_s.o obj/io_par.o obj/main.o obj/preflow.o obj/push_relabel_kernel.o obj/push_relabel.o obj/global_relabel.o
	$(NVCC) obj/graph_s.o obj/io_par.o obj/main.o obj/preflow.o obj/push_relabel_kernel.o obj/push_relabel.o obj/global_relabel.o -g -G -o maxflowdbg

obj/main.o : main.cu obj
	$(NVCC) -c main.cu -o obj/main.o

obj/graph_s.o : graph_s.cpp obj
	$(CC) -c graph_s.cpp -o obj/graph_s.o

obj/io_par.o : io_par.cu obj
	$(NVCC) -c io_par.cu -o obj/io_par.o

obj/preflow.o : preflow.cu obj
	$(NVCC) -c preflow.cu -o obj/preflow.o 

obj/push_relabel.o : push_relabel.cu obj
	$(NVCC) -c push_relabel.cu -o obj/push_relabel.o 

obj/push_relabel_kernel.o : push_relabel_kernel.cu obj
	$(NVCC) -c push_relabel_kernel.cu -o obj/push_relabel_kernel.o 

obj/global_relabel.o : global_relabel.cu obj
	$(NVCC) -c global_relabel.cu -o obj/global_relabel.o

obj :
	mkdir obj

# run make clean to clean obj files and the executable(s)
clean :

	if [ obj ] ; \
	then \
		rm obj/*.o ; \
		rmdir obj ; \
	fi ; \
	if [ maxflow ] ; \
	then \
		rm ./maxflow ; \
	fi ;
	if [ maxflowdbg ] ; \
	then \
		rm ./maxflowdbg ; \
	fi ;