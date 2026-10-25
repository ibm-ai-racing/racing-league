# Windows Installation Guide

Everything you need to set up the IBM AI Racing League environment natively on Windows (no containers required).

📄 **[Open the full setup guide (PDF)](IBM_AI_Racing_League_Windows_Setup_Guide.pdf)**. Follow it step by step. This page is a short overview and a list of everything you will download.

## Steps covered in the guide

1. **Prerequisites**: hardware requirements, disk space, Python 3, Git, and C++ Build Tools
2. **TORCS + SCR**: download and unzip (no installer required, just extract and run)
3. **Python Packages**: create a virtual environment and install the necessary libraries
4. **`gym_torcs`**: the AI starter kit provided by the organizers (included in the same zip as TORCS)
5. **IBM Bob**: install the IBM fork of the VS Code editor with the IBM AI assistant and set up the Python extension

## Downloads

| # | What | Where | Notes |
|---|------|-------|-------|
| 1 | Python 3 | [python.org/downloads](https://www.python.org/downloads/) | Tick **Add Python to PATH** in the installer |
| 2 | Git for Windows | [git-scm.com/download/win](https://git-scm.com/download/win) | Default settings |
| 3 | Visual C++ Build Tools | [visualstudio.microsoft.com/visual-cpp-build-tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) | Select the **Desktop development with C++** workload (about 4 GB) |
| 4 | **Windows Installation Files** (TORCS + SCR + `gym_torcs`) | [Download zip](https://ibm.box.com/s/adts01qbpa6kj9g7oao1bb87pg9lfns4) | A single zip file. Extract it to `C:\RaceYourCode\` |
| 5 | **IBM Bob** | [Register and download](https://ibm.biz/university-bob) | Register first, then follow the instructions to install |
| 6 | PyTorch with CUDA (optional) | [pytorch.org/get-started/locally](https://pytorch.org/get-started/locally/) | Only if you have an NVIDIA GPU and want faster training |

Python packages (numpy, torch, tensorflow and others) are installed with `pip` inside your virtual environment. The guide has the exact command.

## Quick overview

- **Free disk space:** about 12 GB
- **OS:** Windows 10 or 11 (64-bit)
- **No dedicated GPU needed.** TORCS runs on integrated graphics.
- **Install location:** extract the zip to `C:\RaceYourCode\`, which gives you:

```
C:\RaceYourCode\
├── torcs\        <- the simulator (wtorcs.exe)
└── gym_torcs\    <- the AI starter kit (torcs_jm_par.py)
```

## Need help?

Join our [Discord community](https://discord.gg/KXhqwKqnB2) for announcements, Q&A, and collaboration. The last chapter of the PDF guide also has a troubleshooting section.
