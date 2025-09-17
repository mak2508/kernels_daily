This problem took me a little longer to figure out.

First, we need to be careful about our indexing. Since we are working with row major indexing, we find an index into a matrix by doing:
```
idx = row_idx * num_cols + col_idx
```

I had an incorrect indexing pattern that worked on the test input but was failing upon submission, so it was a little difficult to debug. I would recommend [this guide](https://www.youtube.com/watch?v=nOxKexn3iBo) by Jeremy Howard on how to run CUDA kernels in Jupyter Notebooks. I will possibly add a guide within this repo too eventually.

The next thing to be careful of is how we are doing our accumulation for each element in C. Initially, I was doing accumulation directly into an index in C as follows:
```
for (int i = 0; i < N; ++i) {
            C[row * K + col] += A[row * N + i] * B[i * K + col];
        }
```
This is problematic for 2 reasons. One is that it could actually be wrong, since we don't know if C is initialized to zeros. Second, this times out because we have xN extra memory accesses in each iteration. This is inefficient, and instead having an accumulator is much more efficient.