
FROM alpine:edge
RUN apk add openssh-client
RUN apk add openmpi --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing

RUN apk add build-base
RUN apk add openmpi-dev --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing

WORKDIR /local
RUN echo $' \n\
\t #include <mpi.h> \n\
\t #include <stdio.h> \n\
\t #include <stdlib.h> \n\
\n\
int main (int argc, char **argv) {\n\
        int rc, size, myrank; \n\
        rc = MPI_Init (&argc, &argv); \n\
        if (rc != MPI_SUCCESS) { fprintf (stderr, "MPI_Init() failed"); return EXIT_FAILURE; } \n\
        rc = MPI_Comm_size (MPI_COMM_WORLD, &size); \n\
        if (rc != MPI_SUCCESS) { fprintf (stderr, "MPI_Comm_size() failed"); goto exit_with_error; } \n\
        rc = MPI_Comm_rank (MPI_COMM_WORLD, &myrank); \n\
        if (rc != MPI_SUCCESS) { fprintf (stderr, "MPI_Comm_rank() failed"); goto exit_with_error; } \n\
        fprintf (stdout, "Hello, I am rank %d/%d", myrank, size); \n\
        MPI_Finalize(); \n\
        return EXIT_SUCCESS; \n\
 exit_with_error: \n\
        MPI_Finalize(); \n\
        return EXIT_FAILURE; \n\
} ' > mpitest.c
RUN cat mpitest.c

RUN mpicc mpitest.c -o mpitest