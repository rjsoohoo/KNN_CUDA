# KNN_CUDA (Archive)

> **Author's note:**
> 
> **Recreation of [`unlimblue/KNN_CUDA`](https://github.com/unlimblue/KNN_CUDA)**
>
> The original `unlimblue` account and its `KNN_CUDA` repo are no longer available on GitHub.
> After researching from multiple sources, this repository aims to accurately recreate the original to resemble its last known state.
> Resources used:
> - [`unlimblue/KNN_CUDA`](https://github.com/unlimblue/KNN_CUDA)
>    - Original repo that is no longer available
>    - Creator has also been referred to as `sli` and `Shuaipeng Li` according to commit history
>    - According to given email address `sli@mail.bnu.edu.cn` (probably now defunct), creator possibly had affiliation with Beijing Normal University
>
>  - [Wayback Machine archives of `unlimblue/KNN_CUDA` pages](https://web.archive.org/web/*/https://github.com/unlimblue/KNN_CUDA/*)
>    - Used to assess the last known appearance of the repo, its tags, and its releases before deletion
>    - Provided ability to download wheels `KNN_CUDA-0.1-py3-none-any.whl` and `KNN_CUDA-0.2-py3-none-any.whl` for recreating releases
>
>  - [`gt4o4/KNN_CUDA`](https://github.com/gt4o4/KNN_CUDA)
>    - Essential fork that has preserved both `master` and `windows` repo branches along with their last known commits from the original creator
>
>  - [`blukaz/KNN_CUDA/windows`](https://github.com/blukaz/KNN_CUDA/tree/windows)
>    - Fork that created the essential `windows` branch and that `unlimblue` merged into the original repo
>
>  - [`altaykacan/KNN_CUDA_reborn`](https://github.com/altaykacan/KNN_CUDA_reborn)
>    - Reupload of the 0.2 release files for the Linux version of `unlimblue/KNN_CUDA`
>    - Inspiration for this archival/recreation fork
>
> 
> The hashes for `unlimblue`'s last commits to `KNN_CUDA` are:
> - master branch: [`619617b51ce2df785e276164cd8cac0234eb8e8c`](https://github.com/rjsoohoo/KNN_CUDA/tree/619617b51ce2df785e276164cd8cac0234eb8e8c)
> - windows branch: [`08b8947b75f179efcbb61089ee3ae73d8644f8ea`](https://github.com/rjsoohoo/KNN_CUDA/tree/08b8947b75f179efcbb61089ee3ae73d8644f8ea)
>
> Other than adding author's note(s) to the top of `README.md` file, there have been no other changes to `unlimblue`'s repo or `blukaz`'s branch.
> There is no intention to change anything else in the future.
> In the installation instructions below, be aware that using `unlimblue`'s username won't work since the account no longer exists.
> 
>  **I claim no ownership of this code and all rights belong to the original authors.**
> 
> **End of author's note.**

# KNN_CUDA

+ ref: [kNN-CUDA](https://github.com/vincentfpgarcia/kNN-CUDA)
+ ref: [pytorch knn cuda](https://github.com/chrischoy/pytorch_knn_cuda)
+ author: [sli@mail.bnu.edu.cn](sli@mail.bnu.edu.cn)


#### Modifications 
+ Aten support
+ pytorch v1.0+ support
+ pytorch c++ extention 

#### Performance

+ dim   = 5
+ k     = 100
+ ref   = 224
+ query = 224
+ Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz
+ NVIDIA GeForce 940MX

| Loop   | sklearn | CUDA    | Memory   |
| :---:  | :---:   | :---:   | :---:    |
| 100    | 2.34 ms | 0.06 ms | 652/1024 |
| 1000   | 2.30 ms | 1.40 ms | 652/1024 |


#### Install


+ from source

```bash
git clone https://github.com/unlimblue/KNN_CUDA.git
cd KNN_CUDA
make && make install
```

+ from wheel

```bash
pip install --upgrade https://github.com/unlimblue/KNN_CUDA/releases/download/0.2/KNN_CUDA-0.2-py3-none-any.whl
```
And then, make sure [`ninja`](https://ninja-build.org/) has been installed:
  1. see [https://pytorch.org/tutorials/advanced/cpp_extension.html](https://pytorch.org/tutorials/advanced/cpp_extension.html)
  2. **or just**:
```bash
wget -P /usr/bin https://github.com/unlimblue/KNN_CUDA/raw/master/ninja
```

+ for windows

You should use branch `windows`:

```bash
git clone --branch windows https://github.com/unlimblue/KNN_CUDA.git
cd C:\\PATH_TO_KNN_CUDA
make
make install
```

#### Usage

```python
import torch

# Make sure your CUDA is available.
assert torch.cuda.is_available()

from knn_cuda import KNN
"""
if transpose_mode is True, 
    ref   is Tensor [bs x nr x dim]
    query is Tensor [bs x nq x dim]
    
    return 
        dist is Tensor [bs x nq x k]
        indx is Tensor [bs x nq x k]
else
    ref   is Tensor [bs x dim x nr]
    query is Tensor [bs x dim x nq]
    
    return 
        dist is Tensor [bs x k x nq]
        indx is Tensor [bs x k x nq]
"""

knn = KNN(k=10, transpose_mode=True)

ref = torch.rand(32, 1000, 5).cuda()
query = torch.rand(32, 50, 5).cuda()

dist, indx = knn(ref, query)  # 32 x 50 x 10
```
