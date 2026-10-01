# 🦙 Ollama Beginner's Guide
### Run AI Models on Your Own Computer, Free, Offline, and Private
**For Windows and Linux Users | Student-Friendly | Step-by-Step**

---

## 📑 Table of Contents

1. [What is Ollama?](#1-what-is-ollama)
2. [What You Need Before Starting](#2-what-you-need-before-starting)
3. [Installing Ollama on Windows](#3-installing-ollama-on-windows)
4. [Installing Ollama on Linux](#4-installing-ollama-on-linux)
5. [Running Your First AI Model](#5-running-your-first-ai-model)
6. [Chatting with the Model](#6-chatting-with-the-model)
7. [Essential Ollama Commands (Cheat Sheet)](#7-essential-ollama-commands-cheat-sheet)
8. [Which Model Should I Choose?](#8-which-model-should-i-choose)
9. [Where Are Models Stored? Managing Disk Space](#9-where-are-models-stored-managing-disk-space)
10. [Using Ollama with a Chat Window (Optional)](#10-using-ollama-with-a-chat-window-optional)
11. [Using Ollama from Python (Optional)](#11-using-ollama-from-python-optional)
12. [Troubleshooting Common Problems](#12-troubleshooting-common-problems)
13. [Updating and Uninstalling Ollama](#13-updating-and-uninstalling-ollama)
14. [Quick Summary](#14-quick-summary)

---

## 1. What is Ollama?

**Ollama** is a free tool that lets you download and run AI language models (similar to ChatGPT) **directly on your own computer**.

**Why use it?**

| Benefit | Meaning |
|---|---|
| 💸 **Free** | No subscription needed |
| 🔒 **Private** | Your chats stay on your computer |
| 📴 **Offline** | Works without internet (after the model is downloaded) |
| 🎓 **Great for learning** | Perfect for students, coding practice, and projects |

> 💡 **Simple idea:** Think of Ollama as an "app store + player" for AI models. You download a model once, then chat with it anytime.

---

## 2. What You Need Before Starting

### ✅ Minimum Requirements

| Item | Recommended |
|---|---|
| **RAM (memory)** | At least **8 GB** (16 GB is better) |
| **Free disk space** | At least **10 GB** (models are big) |
| **Internet** | Needed to download Ollama and models |
| **Windows version** | Windows 10 (version 22H2 or newer) or Windows 11 |
| **Linux** | Most modern distributions (Ubuntu, Debian, Fedora, Arch, etc.) |
| **GPU** | **Optional.** Ollama works on CPU only; a GPU just makes it faster |

> 📝 **No GPU? No problem!** Small models run fine on a normal laptop CPU, just a bit slower.

### 🔍 How to check your RAM

**Windows:** Press `Ctrl + Shift + Esc` → click **Performance** → click **Memory**.

**Linux:** Open a terminal and type:
```bash
free -h
```

### 🔍 How to check free disk space

**Windows:** Open **File Explorer** → **This PC** → look under your C: drive.

**Linux:**
```bash
df -h
```

---

## 3. Installing Ollama on Windows

### Step 1: Download the installer
1. Open your web browser.
2. Go to: **https://ollama.com/download**
3. Click **Download for Windows**.
4. A file named `OllamaSetup.exe` will download.

### Step 2: Run the installer
1. Double-click `OllamaSetup.exe`.
2. If Windows asks *"Do you want to allow this app to make changes?"*, click **Yes**.
3. Click **Install** and wait for it to finish.

> ✅ Ollama installs **without needing Administrator rights** in most cases, and it starts running quietly in the background (you'll see a 🦙 llama icon in the system tray near the clock).

### Step 3: Open a terminal
You can use either:
- **Command Prompt:** Press the `Windows` key → type `cmd` → press `Enter`
- **PowerShell:** Press the `Windows` key → type `powershell` → press `Enter`

### Step 4: Check that Ollama is installed
Type this and press `Enter`:
```bash
ollama --version
```

You should see something like:
```
ollama version is 0.x.x
```

🎉 **If you see a version number, Ollama is installed!** Skip to [Section 5](#5-running-your-first-ai-model).

> ❌ **If you see "ollama is not recognized":** Close the terminal completely, open a **new** one, and try again. If it still fails, restart your computer.

---

## 4. Installing Ollama on Linux

### Step 1: Open the terminal
- On most systems press `Ctrl + Alt + T`.

### Step 2: Make sure `curl` is installed
```bash
curl --version
```
If you get an error, install it:

**Ubuntu / Debian / Linux Mint:**
```bash
sudo apt update
sudo apt install curl -y
```

**Fedora:**
```bash
sudo dnf install curl -y
```

**Arch Linux:**
```bash
sudo pacman -S curl
```

### Step 3: Run the official install command
Copy and paste this single line:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

- Enter your password if asked (nothing shows while typing, that's normal).
- Wait until the installation finishes.

### Step 4: Check that Ollama is installed
```bash
ollama --version
```

### Step 5: Check that the Ollama service is running
```bash
systemctl status ollama
```
You should see **`active (running)`** in green. Press `q` to exit.

If it is **not** running, start it:
```bash
sudo systemctl start ollama
```

To make it start automatically every time you turn on the computer:
```bash
sudo systemctl enable ollama
```

> 💡 **No systemd?** (some minimal systems or WSL setups) You can start the server manually by running `ollama serve` in one terminal window and using a second terminal for everything else.

🎉 **Ollama is installed!**

---

## 5. Running Your First AI Model

Now the fun part! The steps are the **same** for Windows and Linux.

### Step 1: Pick a small model first
For beginners, we recommend **Llama 3.2 (3B)**. It's small (about 2 GB), fast, and smart enough for learning.

### Step 2: Run this command
```bash
ollama run llama3.2
```

### What happens next?
1. Ollama sees you don't have the model yet and **downloads it automatically**.
2. You'll see a progress bar like this:
   ```
   pulling manifest
   pulling dde5aa3fc5ff... 45% ▕██████        ▏ 900 MB/2.0 GB
   ```
3. When it finishes, you'll see a prompt like:
   ```
   >>> Send a message (/? for help)
   ```

🎉 **The model is ready. You can now chat!**

> ⏳ **Be patient:** The first download may take 5 to 30 minutes depending on your internet speed. This only happens **once**. Next time it starts instantly.

> 💻 **Low on RAM (4 to 8 GB)?** Use a tiny model instead:
> ```bash
> ollama run llama3.2:1b
> ```

---

## 6. Chatting with the Model

At the `>>>` prompt, just type a question and press `Enter`.

**Example conversation:**
```
>>> Explain what a variable is in programming, like I'm 12.

A variable is like a labeled box where you store something...

>>> Write a Python program to add two numbers.

(the model writes the code)
```

### 💬 Useful commands inside the chat

| Type this | What it does |
|---|---|
| `/?` | Show help |
| `/clear` | Clear the conversation memory |
| `/set verbose` | Show speed statistics |
| `/bye` | **Exit the chat** |

You can also press `Ctrl + D` to exit.

### ✍️ Writing multi-line messages
Start with three quotes `"""`, write as many lines as you want, then end with `"""`:
```
>>> """
Summarize this text:
Line 1...
Line 2...
"""
```

### 🔁 Starting again later
Next time, just open the terminal and run the same command:
```bash
ollama run llama3.2
```
It starts immediately because the model is already downloaded.

---

## 7. Essential Ollama Commands (Cheat Sheet)

Keep this table handy! Run these in your **terminal** (not inside the chat).

| Command | What it does |
|---|---|
| `ollama --version` | Show installed version |
| `ollama run <model>` | Download (if needed) and chat with a model |
| `ollama pull <model>` | Only download a model (no chat) |
| `ollama list` | Show all models you've downloaded |
| `ollama ps` | Show which models are currently loaded in memory |
| `ollama stop <model>` | Unload a model from memory |
| `ollama rm <model>` | **Delete** a model to free disk space |
| `ollama show <model>` | Show details about a model |
| `ollama serve` | Start the Ollama server manually |
| `ollama help` | Show all available commands |

### 📌 Examples
```bash
ollama pull gemma3:1b      # download only
ollama list                # see what you have
ollama run gemma3:1b       # chat with it
ollama rm gemma3:1b        # delete it
```

> 💡 **Tip:** Model names look like `name:size`. For example, `llama3.2:1b` means the "1 billion parameter" version. If you skip the `:size`, Ollama downloads the default version.

---

## 8. Which Model Should I Choose?

Bigger models are smarter but need more RAM and are slower. Pick based on **your computer's RAM**.

| Your RAM | Recommended models | Example command |
|---|---|---|
| **4 GB** | Tiny models | `ollama run llama3.2:1b` |
| **8 GB** | Small models | `ollama run llama3.2` or `ollama run gemma3:4b` |
| **16 GB** | Medium models | `ollama run qwen2.5:7b` or `ollama run mistral` |
| **32 GB+** | Larger models | `ollama run gemma3:27b` |

### 🎯 Models by purpose

| Goal | Try this |
|---|---|
| General chat and homework help | `llama3.2`, `gemma3` |
| Coding help | `qwen2.5-coder`, `codellama` |
| Step-by-step reasoning | `deepseek-r1:1.5b` (small) |
| Very low-end computer | `tinyllama`, `llama3.2:1b` |

> 🔎 **See all available models:** Visit **https://ollama.com/library**. Each model page shows the exact command to run it and the available sizes.

> ⚠️ **Rule of thumb:** A model's download size is roughly the RAM it needs, plus some extra. A 4 GB model needs about 6 to 8 GB of free RAM.

---

## 9. Where Are Models Stored? Managing Disk Space

Models are large files (1 to 20+ GB each). Delete the ones you don't use.

### See what you have
```bash
ollama list
```
Example output:
```
NAME               ID            SIZE      MODIFIED
llama3.2:latest    a80c4f17acd5  2.0 GB    2 hours ago
gemma3:1b          8648f39daa8f  815 MB    1 day ago
```

### Delete a model
```bash
ollama rm gemma3:1b
```

### Default storage locations

| System | Folder |
|---|---|
| **Windows** | `C:\Users\<YourName>\.ollama\models` |
| **Linux** (service install) | `/usr/share/ollama/.ollama/models` |
| **Linux** (manual `ollama serve` as your user) | `~/.ollama/models` |

---

## 10. Using Ollama with a Chat Window (Optional)

If you prefer a nice window instead of the black terminal:

- **Windows:** Recent versions of Ollama include a simple desktop app. Click the 🦙 icon in the system tray or search for **Ollama** in the Start menu to open it, then pick a model and start chatting.
- **Any system:** Install a free web interface such as **Open WebUI**. It gives you a ChatGPT-style page in your browser and connects to Ollama automatically. (It needs Docker or Python, so it's best tried after you're comfortable with the basics.)

> The terminal method in this guide always works, no matter which version you have.

---

## 11. Using Ollama from Python (Optional)

Great for student projects! Ollama runs a local server at `http://localhost:11434`.

### Step 1: Install the Python library
```bash
pip install ollama
```
> On Linux, if `pip` isn't found, try `pip3 install ollama`. If you get an "externally managed environment" error, create a virtual environment first:
> ```bash
> python3 -m venv myenv
> source myenv/bin/activate
> pip install ollama
> ```

### Step 2: Make sure the model is downloaded
```bash
ollama pull llama3.2
```

### Step 3: Create a file called `chat.py`
```python
import ollama

response = ollama.chat(
    model="llama3.2",
    messages=[
        {"role": "user", "content": "Give me 3 tips to study better."}
    ],
)

print(response["message"]["content"])
```

### Step 4: Run it
```bash
python chat.py
```
(Use `python3 chat.py` on Linux if needed.)

🎉 You just built your first AI program!

---

## 12. Troubleshooting Common Problems

### ❌ Problem 1: `ollama` is not recognized (Windows)
**Fix:**
1. Close all terminal windows and open a **new** one.
2. Restart your computer.
3. Re-run `OllamaSetup.exe` to reinstall.

---

### ❌ Problem 2: `command not found: ollama` (Linux)
**Fix:** The install may have failed. Run the install command again:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

---

### ❌ Problem 3: "Error: could not connect to ollama server"
The Ollama background service isn't running.

**Windows:** Open the **Ollama** app from the Start menu, or run:
```bash
ollama serve
```

**Linux:**
```bash
sudo systemctl start ollama
```
or run `ollama serve` in a separate terminal.

---

### ❌ Problem 4: Model download is very slow or stuck
**Fix:**
- Check your internet connection.
- Press `Ctrl + C` and run the same command again. **Downloads resume** from where they stopped.

---

### ❌ Problem 5: "Error: model requires more system memory"
Your computer doesn't have enough RAM for that model.

**Fix:** Choose a smaller model:
```bash
ollama run llama3.2:1b
```

---

### ❌ Problem 6: The model is very slow
**Fixes:**
- Close other heavy programs (browser tabs, games).
- Use a smaller model (such as a `1b` or `3b` version).
- This is normal on CPU-only computers. Replies come word by word.

---

### ❌ Problem 7: "No space left on device" / disk full
**Fix:** Delete unused models:
```bash
ollama list
ollama rm <model-name>
```

---

### ❌ Problem 8: Port already in use (`11434`)
Ollama is probably already running. You don't need to start it again. Just run `ollama run <model>`.

---

### ❌ Problem 9: Linux, I want to see error logs
```bash
journalctl -u ollama -e
```

---

## 13. Updating and Uninstalling Ollama

### 🔄 Updating

**Windows:** Ollama usually updates itself. When an update is ready, click the 🦙 tray icon and choose the update option. Or download the newest installer from https://ollama.com/download and run it.

**Linux:** Run the install command again:
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### 🗑️ Uninstalling

**Windows:**
1. Open **Settings → Apps → Installed apps**.
2. Find **Ollama** → click the three dots → **Uninstall**.
3. (Optional) Delete leftover models: remove the folder `C:\Users\<YourName>\.ollama`.

**Linux:**
```bash
sudo systemctl stop ollama
sudo systemctl disable ollama
sudo rm /etc/systemd/system/ollama.service
sudo rm $(which ollama)
sudo rm -r /usr/share/ollama
sudo userdel ollama
sudo groupdel ollama
```
> ⚠️ The line with `/usr/share/ollama` **deletes all your downloaded models.**

---

## 14. Quick Summary

### ⚡ The whole guide in 5 steps

| Step | Windows | Linux |
|---|---|---|
| **1. Download/Install** | Download `OllamaSetup.exe` from ollama.com/download and run it | `curl -fsSL https://ollama.com/install.sh \| sh` |
| **2. Open terminal** | `cmd` or PowerShell | `Ctrl + Alt + T` |
| **3. Verify** | `ollama --version` | `ollama --version` |
| **4. Run a model** | `ollama run llama3.2` | `ollama run llama3.2` |
| **5. Exit chat** | `/bye` | `/bye` |

### ✅ Beginner Checklist
- [ ] I checked I have at least 8 GB RAM and 10 GB free disk space
- [ ] I installed Ollama
- [ ] `ollama --version` shows a version number
- [ ] I ran `ollama run llama3.2` and the model downloaded
- [ ] I asked the model a question and got an answer
- [ ] I know how to list (`ollama list`) and delete (`ollama rm`) models

---

## 🎉 Congratulations!

You now have your own AI running on your own computer. Experiment with different models, ask questions, practice coding, and build projects.

**Helpful links**
- 🌐 Official website: https://ollama.com
- 📚 Model library: https://ollama.com/library
- 💻 Official GitHub: https://github.com/ollama/ollama

> 📝 *Note: Ollama is updated often. If a screen or command looks slightly different from this guide, check the official website for the latest instructions.*

**Happy learning! 🚀**
