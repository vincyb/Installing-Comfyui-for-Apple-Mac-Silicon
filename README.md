<head></head><h1 id="# Installing ComfyUI on Apple Silicon (M1–M4 and beyond) – 2025 Update" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">Installing ComfyUI on Apple Silicon (M1/M2/M3) – 2025 Update</h1><blockquote style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><p>A clean guide for setting up ComfyUI with MPS (Metal) support using Python 3.11 and <code>pyenv</code>.</p></blockquote><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="requirements" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">Requirements</h2><ul style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><li><p>macOS 12.3+ (macOS Sonoma or later recommended)</p></li><li><p>Xcode Command Line Tools:</p><pre><code class="fenced-code-block language-bash">xcode-select --install</code></pre></li><li><p>Homebrew installed (<a href="https://brew.sh/">https://brew.sh</a>)</p></li></ul><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="1-install-pyenv-and-python-311" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">1. Install <code>pyenv</code> and Python 3.11</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">brew install pyenv
pyenv install 3.11.8
pyenv global 3.11.8</code></pre><p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">Ensure shell integration:</p><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">echo 'eval "$(pyenv init --path)"' &gt;&gt; ~/.zprofile
echo 'eval "$(pyenv init -)"' &gt;&gt; ~/.zshrc
exec "$SHELL"</code></pre><p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">Check Python version:</p><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">python --version  # Should show 3.11.8</code></pre><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="2-clone-comfyui" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">2. Clone ComfyUI</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">git clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI</code></pre><p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">(Optional: Clone Manager)</p><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">cd custom_nodes
git clone https://github.com/ltdrdata/ComfyUI-Manager
cd ..</code></pre><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="3-create-virtual-environment" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">3. Create Virtual Environment</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">python -m venv comfyui-env
source comfyui-env/bin/activate</code></pre><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="4-install-pytorch-with-mps-support" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">4. Install PyTorch with MPS Support</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">pip install --upgrade pip
pip install torch torchvision torchaudio</code></pre><blockquote style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><p>This installs the stable PyTorch version with MPS support.</p></blockquote><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="5-install-comfyui-requirements" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">5. Install ComfyUI Requirements</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">pip install -r requirements.txt
pip install -r custom_nodes/ComfyUI-Manager/requirements.txt</code></pre><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="6-verify-mps-is-working" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">6. Verify MPS is Working</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">python
&gt;&gt;&gt; import torch
&gt;&gt;&gt; torch.ones(3, device="mps")
tensor([1., 1., 1.], device='mps:0')
&gt;&gt;&gt; exit()</code></pre><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="7-run-comfyui-with-mps" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">7. Run ComfyUI with MPS</h2><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0
python main.py --use-mps</code></pre>

<p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">You can also create a launcher script:</p>

<p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">``</p><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">#!/bin/bash
source comfyui-env/bin/activate
export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0
python main.py --use-mps</code></pre><p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">Make it executable:</p><pre style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><code class="fenced-code-block language-bash">chmod +x run.sh</code></pre><hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="removed-or-deprecated-steps" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">Removed or Deprecated Steps</h2>
Old Step | Updated Recommendation
-- | --
Python via .pkg installer | Use pyenv for version control
Anaconda install | Use lightweight venv
Nightly PyTorch CPU wheels | Use stable PyTorch (supports MPS)
TensorFlow install | Not needed for ComfyUI

<hr style="font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;"><h2 id="✅-summary" class="atx" style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">✅ Summary</h2><p style="caret-color: rgb(0, 0, 0); color: rgb(0, 0, 0); font-style: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration: none;">This updated guide simplifies your ComfyUI installation for Apple Silicon and ensures best compatibility with MPS and PyTorch 2025 improvements.</p># Installing ComfyUI on Apple Silicon (M1/M2/M3) – 2025 Update

> A clean guide for setting up ComfyUI with MPS (Metal) support using Python 3.11 and `pyenv`.

---

## Requirements

- macOS 12.3+ (macOS Sonoma or later recommended)
  
- Xcode Command Line Tools:
  
  ```bash
  xcode-select --install
  ```
  
- Homebrew installed ([https://brew.sh/](https://brew.sh/))
  

---

## 1. Install `pyenv` and Python 3.11

```bash
brew install pyenv
pyenv install 3.11.8
pyenv global 3.11.8
```

Ensure shell integration:

```bash
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
exec "$SHELL"
```

Check Python version:

```bash
python --version  # Should show 3.11.8
```

---

## 2. Clone ComfyUI

```bash
git clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI
```

(Optional: Clone Manager)

```bash
cd custom_nodes
git clone https://github.com/ltdrdata/ComfyUI-Manager
cd ..
```

---

## 3. Create Virtual Environment

```bash
python -m venv comfyui-env
source comfyui-env/bin/activate
```

---

## 4. Install PyTorch with MPS Support

```bash
pip install --upgrade pip
pip install torch torchvision torchaudio
```

> This installs the stable PyTorch version with MPS support.

---

## 5. Install ComfyUI Requirements

```bash
pip install -r requirements.txt
pip install -r custom_nodes/ComfyUI-Manager/requirements.txt
```

---

## 6. Verify MPS is Working

```bash
python
>>> import torch
>>> torch.ones(3, device="mps")
tensor([1., 1., 1.], device='mps:0')
>>> exit()
```

---

## 7. Run ComfyUI with MPS

```bash
export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0
python main.py
```

## 8: Running ComfyUI Automatically on macOS with Automator & AppleScript:

Step 1: Create the `run.sh` script Create a shell script named `run.sh` in your ComfyUI folder with the following content: 

```bash 
#!/bin/zsh

# Kill any process using port 8188 (ComfyUI default)
lsof -ti:8188 | xargs kill -9

# Navigate to ComfyUI directory
cd ~/ComfyUI || exit 1

# Activate virtual environment
source comfyui-env/bin/activate

# Set MPS-specific environment variable
export PYTORCH_ENABLE_MPS_FALLBACK=1 PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0

# Run ComfyUI
python main.py --force-fp16 --use-split-cross-attention &  # run in background
while ! curl -s http://127.0.0.1:8188 > /dev/null; do
  sleep 1
done
open -a "Google Chrome" http://127.0.0.1:8188
```

- Replace `/Users/yourusername/ComfyUI` with your actual ComfyUI path.
  
- Make the script executable by running:
  
  ```bash
  chmod +x /Users/yourusername/ComfyUI/run.sh
  ```
  

---

## 9: Create an Automator app using AppleScript

1. Open **Automator** and create a new **Application**.
  
2. Add the action **Run AppleScript**.
  
3. Paste this AppleScript code, updating the path if needed:
  

```applescript
tell application "Terminal"
    activate
    do script "cd ~/ComfyUI; ./run.sh"
end tell
```

4. Save the Automator application anywhere you like (e.g., Desktop).
  
5. Double-click the app to launch ComfyUI with your environment activated and MPS enabled.

---

## Removed or Deprecated Steps

| Old Step | Updated Recommendation |
| --- | --- |
| Python via .pkg installer | Use `pyenv` for version control |
| Anaconda install | Use lightweight `venv` |
| Nightly PyTorch CPU wheels | Use stable PyTorch (supports MPS) |
| TensorFlow install | Not needed for ComfyUI |

---

## ✅ Summary 

This updated guide simplifies your ComfyUI installation for Apple Silicon and ensures best compatibility with MPS and PyTorch 2025 improvements.

**Full Changelog**: https://github.com/vincyb/Installing-Comfyui-for-Apple-Mac-Silicon/commits/v2.0
