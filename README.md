# Parallel-Sort
Sample sort is a parallel version of quicksort.

Result:

    An array of N items, sorted.

    Setup

    Read input file into a "floats" in memory.
    Allocate an array, sizes, of P longs.
    Use open / ftruncate to create the output file, same size as the input file.

    Sample

    Select 3*(P-1) items from the array.
    Sort those items.
    Take the median of each group of three in the sorted array, producing an array (samples) of (P-1) items.
    Add 0 at the start and +inf at the end (or the min and max values of the type being sorted) of the samples array so it has (P+1) items numbered (0 to P).

    Partition

    Spawn P threads, numbered p in (0 to P-1).
    Each thread builds a local array of items to be sorted by scanning the full input and taking items between samples[p] and samples[p+1].
    Write the local size to sizes[p].

    Sort locally

    Each thread uses quicksort to sort the local array.

    Write the data out to the file.

    Open a separate file descriptor to the output file in each thread.
    Use lseek to move to the correct location to write in the file.

    Cleanup

    Terminate the P subthreads.
