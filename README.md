## GNNtest

To verify our performance in the inference part, we selected two specific GNN applications, gcn and graphsage. The profiling code is modified from [dgl/examples](https://github.com/dmlc/dgl/tree/master/examples).

We use [dgSPARSE-Wrapper](https://github.com/dgSPARSE/dgSPARSE-Wrapper) to complete our end2end experiment.

To run our test, first clone our project by

```
git clone git@github.com:fishmingyu/GNN-dgsparse-accleration.git
```

### spmmul

To test with spmmul, you could use the dgsparse.so in the spmmul directory. Then you could follow the README written in dgSPARSE-Wrapper.

```bash
mkdir -p dgSPARSE-Wrapper/lib/
mv spmmul/dgsparse.so dgSPARSE-Wrapper/lib/
```

We implement four algorithms named spmm_cuda_alg0, spmm_cuda_alg1, spmm_cuda_alg2 and spmm_cuda_alg3 respectively.
Thus, you have to change the name of the function in the following code, which is located in [here](https://github.com/dgSPARSE/dgSPARSE-Wrapper/blob/d1aa92db1598487a13099388251f522b51cee0f0/src/cuda-11.1/sparse_main.cc#L12079) for CUDA 11.1 version.

```
e.g.
LOAD_SPARSE_SYMBOL_FOR_ONCE(DGSPARSE_LIB, spmm_cuda);
-->
LOAD_SPARSE_SYMBOL_FOR_ONCE(DGSPARSE_LIB, spmm_cuda_algx);
```

In our paper, we select the algorithm with best performance.
