# Setup Stable Diffusion XL(SDXL) + WebUI(StableSwarmUI) for_vast.ai
* 2023/07/29 ver : StableSwarmUI 0.5-Alpha & SDXL 1.0
   * Ref. https://github.com/Stability-AI/StableSwarmUI
   * Ref. https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0
   * Ref. https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0
   * Ref. https://huggingface.co/stabilityai/sdxl-vae
* GPU sharing cloud service `Vast.ai` : https://cloud.vast.ai/
* * You need NOT install an expensive GPU into your local PC. 

# Preparation
1) Setup your local PC(Windows, macOS, Linux,...)'s SSH client setting. Generate a `SSH keypair(private key & public key)` for remote access.
2) Create a new account for vast.ai `Client Account Type`.
3) Regist your SSH public key into vast.ai `Account` menu.
4) Add credit 10 USD with your credit card on `Billing` menu. I DON'T recommend `Auto charge` setting.

# GPU Instance configuration
* Base docker image : `nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu22.04`
* Launch Type: `ssh`
* On-start script: `Not set`
* Disk Space To Allocate: `over ~60GB` (recommend)
* Launch mode : 
   * `Run interactive shell server, SSH`. This will allow you to connect and run commands using an SSH client.
   * `Checked` : Use direct SSH connection - faster than proxy, but limited to machines with open ports. Proxy ssh still available as backup.
* GPU Type :
   *  `Interruptible` and `On-Demand` : both OK
   *  Recommend GPU : 4090, 4080, 3090 (24GB GPU Mem) for SDXL ver 1.0 

# Setup procedures
1. Start a instance based on the above `Instance configuration`.
2. Wait until the instance loads the docker image and starts up. (5 minutes at the fastest, 20 minutes at the longest)
3. Push the `>_ CONNECT` button and copy the `Direct ssh connect` command.
* ex) 
```sh
ssh -p XXXXX root@AAA.BBB.CCC.DDD -L 8080:localhost:8080
```
4. Paste the command into your terminal/command prompt and add `-L 7801:localhost:7801 -L 7820:localhost:7820` for browser access (SSH local port fowarding)
* ex)
```sh
ssh -p XXXXX root@AAA.BBB.CCC.DDD -L 7801:localhost:7801 -L 7820:localhost:7820
```
5. Connect the instance via SSH with the above `4.` ssh command.
6. Install the Stable Diffusion WebUI(StableSwarmUI)
```sh
apt-get install vim unzip libgl1-mesa-dev libcairo2-dev wget git -y
apt-get install python3 python3-venv python3-dev python3-pip build-essential -y
apt-get install dotnet-sdk-7.0 -y

cd ~
mkdir SwarmUI
cd SwarmUI
git clone https://github.com/Stability-AI/StableSwarmUI
cd StableSwarmUI
./launch-linux.sh --launch_mode	none
```

7 Proceed `StableSwarmUI Installer` by your web browser
* access the installer page with your local PC's web browser
   * http://localhost:7801
* 1) Agree the licenses `Stable Diffusion Model License`
* 2) Select your favorite UI theme `Choose a theme:`
* 3) Select a checkbox of `Just Yourself On This PC` for the question `Who is this StableSwarmUI installation going to be used by?`
* 4) Select a checkbox of `ComfyUI (Local)` for the question `What backend would you like to use?`
* 5) Select your favorite checkpoints. e.g. `Stable Diffusion XL 1.0 (Base)` & `Stable Diffusion XL 1.0 (Refiner)`
* 6) start install with `Yes, I'm sure (Install Now)` button.

8. Have fun!
* access Stable Diffusion WebUI(SwarmUI) with your local PC's web browser
   * http://localhost:7801

9. Access ComfyUI (backend)
* access ComfyUI backend with your local PC's web browser
   * http://localhost:7820




# Ref. ( &Special thanks)
* https://cloud.vast.ai
* https://github.com/Stability-AI/StableSwarmUI
* https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0
* https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0
* https://huggingface.co/stabilityai/sdxl-vae
* https://hub.docker.com/r/nvidia/cuda/tags
* https://pytorch.org/get-started/pytorch-2.0/
* https://github.com/CompVis/stable-diffusion

