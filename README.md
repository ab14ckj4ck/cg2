# cg2

---

## 📝 Automatic Testing Pipeline & Final Submission

**The assignments.icg.tugraz.at automatically runs your code in a testing pipeline as soon as you push to a `submission` branch. This branch is also the one that will be used for the final testing of your solution, so make sure that you do not forget to push to the `submission` branch!**

For `submission` you must create a `submission` branch and push your code into this branch. This will also trigger an automated test, for which you can view build logs, output logs and rendered images in the CI/CD section of the gitlab webinterface. We will only grade solutions that have been pushed to the `submission` branch of your repository! To build the framework, please follow the build instructions down below.

**To submit:**
```bash
git checkout -b submission
git push origin submission
```

You can view test results, logs, output images, and diffs in the GitLab **CI/CD** section after each push. 
> Make sure to push your final solution to the `submission` branch, or it will not be graded.

---

## 🛠️ Building and Running the Framework

The following tools are required:

- C++ toolchain with C++17 support (e.g. GCC 13.x)
- [CMake 3.10+](https://cmake.org/) [3]
- OpenGL 3 (typically installed with system graphics libraries)

This framework supports **cross-platform builds**, but we officially support **Docker-based Dev Containers** and **Ubuntu 22.04 native** installations. Windows is supported only via Docker/WSL2.

---

## 📂 Recommended: VS Code with Dev Container

If you're using [Visual Studio Code](https://code.visualstudio.com/) with the **Dev Containers extension**:

1. Install the extension: `ms-vscode-remote.remote-containers`
2. Open the repo in VS Code
3. Use "Open Folder in Container..."

![VSCode Devcontainer](descriptions/images/vscode_devcontainer.png)

That's it!
The container will auto-build and install all dependencies (GCC 13, CMake, etc.) based on our provided Dockerfile. You can then build and run with the regular `make` commands.

For Windows users: You must run VS Code **inside WSL2** (use this [guide](https://code.visualstudio.com/blogs/2020/07/01/containers-wsl)), and open the repo using `code .` from a WSL terminal. In theory, it should also work on a Mac with a few workarounds, but we can not guarantee anything and do not support it because our team does not possess the needed hardware.

---

### 🐛 Debugging with VS Code
We provide you with a launch.json file that contains some debug configurations for VS Code. Simply hit F5 in VS Code to start the debugger. In the Debugging Panel on the left you can select which configuration you want to debug. Feel free to add your own configurations!

## 🏠 Ubuntu 22.04 Native Installation

You can also compile and run the framework natively on Ubuntu (22.04 or later). First, install the necessary tools:

```bash
sudo apt update
sudo apt install -y software-properties-common
sudo add-apt-repository -y ppa:ubuntu-toolchain-r/test
sudo apt update
sudo apt install -y \
    gcc-13 g++-13 cmake build-essential \
    imagemagick git gdb \
    mesa-utils libglu1-mesa-dev freeglut3-dev mesa-common-dev \
    libgl1-mesa-dev libglx-mesa0 libgles2-mesa-dev xorg-dev \
    ffmpeg xvfb python3 python3-pip
```
```bash
# Python image diff support
pip install pillow numpy
```

To build:
```bash
make clean build
```
To run tests:
```bash
make test
```
Or use the scripts in the scripts folder:
```bash
cd scripts
./test_all.sh
```
---

## 💼 Git Workflow for Submission

```bash
git add <modified_files>
git commit -m "Must be very meaningful message, otherwise the pipeline is sad :("
git push origin submission
```

Create and push the submission branch:
```bash
git checkout -b submission
git push origin submission
```

**We only grade solutions that are in the `submission` branch!**

---

## 🐳 Docker Image (Optional for Manual CLI Builds)

You can manually build and run the framework using Docker:

```bash
docker build -t cg2-runner .
```

Then run:
```bash
docker run --init -v $PWD:/cg2 -it cg2-runner make test
```

On Windows:
```bash
docker run --init -v ${PWD}:/cg2 -it cg2-runner sh -c "make test"
```
---

## 🔁 GitLab CI/CD Pipeline

Every time you push to `submission`, the GitLab CI will:
- Compile your code
- Run automated tests (e.g. stereo rendering, distortion correction, timewarp)
- Save screenshots and image diffs as artifacts

You can inspect these results by clicking **CI/CD > Pipelines** in the left sidebar of GitLab.

Make sure your pipeline is **green** and look at the diffs the before deadline! ✅

---
