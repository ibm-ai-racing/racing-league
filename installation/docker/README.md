# TORCS AI Racing – Container Setup

This folder contains what you need to run the TORCS simulator in a container and test it with a sample AI agent.

| File | Purpose |
|------|---------|
| `torcs_jm_par.py` | Sample agent. Use it to test that the container works and as a starting point for your own controller. |

## How it works

You write and run your Python code **on your own computer** (VS Code + IBM Bob). A **Podman container** runs the TORCS simulator headlessly and shows the race in your **web browser**.

- Python agent (your computer) ⇄ UDP port `3001` ⇄ TORCS (container)
- Live view: <http://localhost:8080>

## Requirements

- Windows 10/11, macOS 12+, or Linux (Ubuntu 20.04+)
- Intel/AMD (amd64) or Apple Silicon (arm64)
- 8 GB RAM (16 GB recommended), 5 GB free disk space
- Python 3.9+, VS Code, IBM Bob extension, [Podman](https://podman.io/docs/installation)

## 1. Install Podman

**macOS**

```bash
brew install podman
podman machine init
podman machine start
```

**Windows** – install from <https://podman.io/docs/installation> (enable WSL2 when prompted, restart if asked), then in PowerShell:

```powershell
podman machine init
podman machine start
```

**Linux (Ubuntu/Debian)**

```bash
sudo apt-get update && sudo apt-get install -y podman
```

Check with `podman --version`.

## 2. Start the TORCS container

```bash
podman run -d --rm \
  -p 8080:8080 \
  -p 3001:3001/udp \
  --name torcs-server \
  quay.io/john_sloe/torcs-env:latest
```

- `-d` runs in the background
- `--rm` removes the container when stopped
- `-p 8080:8080` browser view
- `-p 3001:3001/udp` connection for your Python agent

The image is multi-arch; Podman picks arm64 or amd64 automatically.

## 3. Check the simulation

Open <http://localhost:8080>. A blue screen saying
`SCR server waiting for connection on port 3001...` means the server is ready.

## 4. Run the sample agent

In a terminal, from the folder containing `torcs_jm_par.py`:

```bash
python3 torcs_jm_par.py
```

Switch back to the browser – the car should connect and start driving.

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Connection refused on port 3001 | Check the container is running (`podman ps`) and restart it with the command in step 2. Make sure UDP 3001 is not blocked. |
| Browser: unable to connect at port 8080 | Container is stopped or the port was not mapped. Use `-p 8080:8080` when starting. |
| Car drives off the track immediately | Lower `TARGET_SPEED` to 60–80 km/h and increase `CENTERING_GAIN` in `torcs_jm_par.py`. |
| Podman architecture error on startup | `podman pull quay.io/john_sloe/torcs-env:latest` |

## Daily loop

1. Start the container (step 2)
2. Open <http://localhost:8080>
3. Edit your code in VS Code with IBM Bob
4. Run `python3 torcs_jm_par.py`
5. Stop the agent (`Ctrl+C`), tweak parameters, rerun
