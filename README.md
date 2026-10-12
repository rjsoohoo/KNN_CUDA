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

This is the knn_cuda branch compatible for Windows OS. The original code is from [unlimblue/KNN_CUDA](https://github.com/unlimblue/KNN_CUDA)

#### Prerequisites
+ Cuda versions of PyTorch and Nvidia match
+ Installed Visual Studtio with c++ compiler

#### Install

+ add msvc to the Path environment variable (System variable) by:
    1. go to *Control Panel → System and Security → System → Advanced System Settings → New...* (under System variables):
    2. add to Path: *C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.26.28801\bin\Hostx64\x64*
    → this will get you rid of the following error: Error checking compiler version for cl: [WinError 2] The system cannot find the file specified
+ uninstall original knn_cuda if you have installed it before

+ git clone *windows* branch
```bash
git clone --branch windows https://github.com/blukaz/KNN_CUDA
```

+ install from source
++ in order to use *make* you can install [chocolatey](https://chocolatey.org/install). For more info you can check [here](https://stackoverflow.com/questions/32127524/how-to-install-and-use-make-in-windows)

++ run cmd (not PowerShell!) as admin

```bash
cd C:\\PATH_TO_KNN_CUDA
make
make install
```

#### Issues with original code
 Files which are not compatible with Windows platforms:

 + knn.cpp & knn.cu:
 ++ data type *long* on Linux 64-bit systems is 8 Bytes (64 bits), while on Windows 4 Bytes (32 bits): change *long* → *long long* 

 + makefile is suitable for Linux based shell commands and not Windows cmd commands
