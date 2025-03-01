# Android Kernel Builder

This repository provides an automated system for building, testing, and packaging custom Android kernels using GitHub Actions. It streamlines the workflow for developers who want to create, test, and deploy custom kernels without needing a local setup. This builder is inspired by work done in the [kernel_build](https://github.com/zclkkk/kernel_build) repository.

## Features

- **Automated Kernel Builds:** Utilizes GitHub Actions for a fully automated kernel build process.
- **Multiple Toolchain Support:** Supports both Clang and GCC toolchains.
- **KernelSU Integration:** Includes seamless integration with KernelSU for root functionality.
- **AnyKernel Packaging:** Automatically packages the built kernel using AnyKernel for easy flashing.
- **Customizable Build Options:** Offers extensive customization through environment variables and build flags.
- **Clear Build Logs:** Provides detailed logs and status reports for each build.
- **Easy Setup:** Simple configuration using environment variables.
- **Swap Management:** Automatically configures swap space for resource-intensive builds.
- **Dependency Management:** Automatically installs the necessary dependencies for building.

## Getting Started

### Prerequisites

- A GitHub account.
- A fork of this repository.
- Basic knowledge of kernel development.
- A working knowledge of GitHub Actions.

### Configuration

The build process is controlled through environment variables defined in the repository settings or directly in the `main.yml` file. The following table lists the available variables and their descriptions.

| Variable                | Description                                                                                                                                   | Example                                                                                                        |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `TOOLCHAIN_REPO`        | URL of the Android kernel toolchain repository.                                                                                               | `https://github.com/yourusername/yourtoolchainrepo.git`                                                      |
| `KERNEL_SOURCE_REPO`    | URL of your kernel source repository.                                                                                                        | `https://github.com/yourusername/yourkernelrepo.git`                                                          |
| `ANYKERNEL_REPO`        | URL of your AnyKernel3 repository.                                                                                                           | `https://github.com/yourusername/youranykernelrepo.git`                                                        |
| `KERNELSU_SETUP_SCRIPT` | URL of the KernelSU setup script.                                                                                                             | `https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh`                                      |
| `CLANG_PATH`            | Path to the Clang compiler binaries within the toolchain.                                                                                     | `$GITHUB_WORKSPACE/tools/path/to/clang/bin`                                                |
| `GCC_PATH`              | Path to the GCC (aarch64) compiler binaries within the toolchain.                                                                             | `$GITHUB_WORKSPACE/tools/path/to/gcc64/bin`                                   |
| `GCC32_PATH`            | Path to the GCC (arm) compiler binaries within the toolchain.                                                                                 | `$GITHUB_WORKSPACE/tools/path/to/gcc32/bin`                                       |
| `LD_LIBRARY_PATH`       | Path to the Clang library files within the toolchain.                                                                                         | `$GITHUB_WORKSPACE/tools/path/to/ld-library/lib64`                                               |
| `CROSS_COMPILE`         | Prefix for the aarch64 cross-compiler.                                                                                                       | `$GITHUB_WORKSPACE/tools/path/to/gcc64/bin/aarch64-linux-android-`          |
| `CROSS_COMPILE_ARM32`   | Prefix for the arm cross-compiler.                                                                                                           | `$GITHUB_WORKSPACE/tools/path/to/gcc32/bin/arm-linux-androideabi-`            |
| `USER`                  | Username for the build process.                                                                                                               | `yourusername`                                                                                                |
| `HOST`                  | Host information (codename from `lsb_release -cs`).                                                          | `focal`                                                                                                        |
| `DEFCONFIG`             | Default kernel configuration file.                                                                                                            | `examples_defconfig`                                                                                           |
| `KERNEL_BRANCH`         | Branch of the kernel source repository to use.                                                                                               | `main`                                                                                                         |
| `ANYKERNEL_BRANCH`      | Branch of the AnyKernel3 repository to use.                                                                                                   | `master`                                                                                                       |
| `BUILD_FLAGS`           | Build flags to be passed to the kernel build process                                                                                           | `CC=clang AR=llvm-ar NM=llvm-nm AS=llvm-as STRIP=llvm-strip READELF=llvm-readelf OBJDUMP=llvm-objdump OBJCOPY=llvm-objcopy CLANG_TRIPLE=aarch64-linux-gnu-` |
| `TOOLCHAIN_PATH`        | Directory where the toolchain will be located (relative to the repository root).                                                             | `tools`                                                                                                        |
| `KERNEL_SOURCE_PATH`    | Directory where the kernel source will be located (relative to the repository root).                                                         | `kernel-source`                                                                                                |
| `ANYKERNEL_PATH`        | Directory where AnyKernel3 will be located (relative to the repository root).                                                                  | `AnyKernel3`                                                                                                   |

### Steps

1. **Fork the Repository:** Click the "Fork" button at the top right of this page to create a copy of this repository in your GitHub account.
2. **Clone Your Fork:**

    ```bash
    git clone https://github.com/yourusername/android_kernel_builder.git
    cd android_kernel_builder
    ```

3. **Configure Environment Variables:** Define the following environment variables in your repository's settings (**Settings > Secrets and variables > Actions > New repository secret**) or directly in the `main.yml` workflow file if you prefer.

4. **Modify `main.yml` (Optional):** Customize the `.github/workflows/main.yml` file to adjust build steps, kernel configuration, or other aspects of the workflow if needed.

5. **Run the Workflow:**
    - Go to the "Actions" tab in your forked repository.
    - Select the "Build Kernel" workflow.
    - Click "Run workflow" and confirm.

6. **Monitor the Build:** Track the build process in the "Actions" tab.

7. **Download the Kernel:** Once the build is complete, you can download the packaged kernel from the "Artifacts" section of the build's summary. The artifact name will be : `KERNEL_NAME-KERNEL_VERSION-DATE`

## Credits

- This project was inspired by the work done in the [kernel_build](https://github.com/zclkkk/kernel_build) repository.
- Special thanks to [zclkkk](https://github.com/zclkkk) for the initial inspiration.
- Special thanks to [tiann](https://github.com/tiann) for KernelSU
