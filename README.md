# 🚀 ConvoDynamics

Welcome to **ConvoDynamics**, your portal to unraveling human interaction like never before. Delve into conversations and unveil the concealed emotional depths that steer each interaction. Acquire insights to enrich communication and cultivate deeper connections in every dialogue.

---
## ✨ Project Showcase

Here are a few snapshots of ConvoDynamics in action.

*(To add your images, upload them to your GitHub repository and replace the placeholder `#` links below with the direct URLs to your images.)*

| | | |
|:----------------------------------------------------------:|:----------------------------------------------------------:|:----------------------------------------------------------:|
| **Description for Image 1** | **Description for Image 2** | **Description for Image 3** |
| ![Showcase Image 1](https://via.placeholder.com/400x300.png?text=Your+Image+Here) | ![Showcase Image 2](https://via.placeholder.com/400x300.png?text=Your+Image+Here) | ![Showcase Image 3](https://via.placeholder.com/400x300.png?text=Your+Image+Here) |

---
## 📋 Prerequisites (NVIDIA GPU Setup)

These steps are required for GPU acceleration. Your system must have **Python 3.10** installed.

1.  **FFmpeg**:
    * Download the latest release from an official source (e.g., [gyan.dev](https://www.gyan.dev/ffmpeg/builds/) or [BtbN's GitHub](https://github.com/BtbN/FFmpeg-Builds/releases)).
    * Extract the archive, move the folder to your `C:` drive, and add its `bin` folder to your system's **Path** environment variable.

2.  **cuDNN for CUDA 11.x**:
    * Download the cuDNN TAR file from the [NVIDIA Developer site](https://developer.nvidia.com/cudnn-downloads?target_os=Windows&target_arch=x86_64&target_version=Agnostic&cuda_version=11).
    * Extract the archive and add its `bin` folder to your system's **Path**.

3.  **CUDA Toolkit 11.8**:
    * Download and install the CUDA Toolkit 11.8 from the [NVIDIA archive](https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Windows&target_arch=x86_64&target_version=11).
    * Verify that the installer has added the following two paths to your system's **Path** environment variable:
        * `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\bin`
        * `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\libnvvp`

---
## 🛠️ Installation

Follow these steps carefully to set up your environment.

1.  **Clone the Repository**:
    ```bash
    # Replace with your actual repository URL
    git clone [https://github.com/your-username/ConvoDynamics.git](https://github.com/your-username/ConvoDynamics.git)
    cd ConvoDynamics
    ```

2.  **Create and Activate Virtual Environment**:
    ```bash
    # Create the virtual environment
    python -m venv myenv

    # Activate it
    .\myenv\Scripts\activate
    ```

3.  **Install Core Libraries (WhisperX & PyTorch)**:
    ```bash
    # Install whisperx from GitHub
    pip install git+[https://github.com/m-bain/whisperx.git](https://github.com/m-bain/whisperx.git)

    # Install PyTorch for CUDA 11.8
    pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url [https://download.pytorch.org/whl/cu118](https://download.pytorch.org/whl/cu118)
    ```

4.  **Install Project Requirements**:
    ```bash
    # Install all packages from the requirements.txt file
    pip install -r requirements.txt --no-deps
    ```
    > **Note**: The `--no-deps` flag helps mitigate dependency conflicts. If a library fails, try installing it individually with `pip install library-name==version.number`.

5.  **Install Additional Libraries**:
    ```bash
    # This specific version of tensorflow-intel should resolve potential NumPy version issues
    pip install tensorflow-intel==2.13.0

    # Install a specific version of PyTorch Lightning for compatibility
    pip install pytorch-lightning==2.0.2
    ```

6.  **Re-run Installation (If Needed)**: If you encounter library issues, re-running the commands from **Step 3** can sometimes resolve them.

---
## 🐛 Troubleshooting

Here are solutions for common errors you might encounter.

* **Error: `cublas64_*.dll not found`**
    1.  Navigate to your CUDA bin directory: `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.8\bin`.
    2.  Find the existing `cublas` DLL file (e.g., `cublas64_11.dll`).
    3.  Make a copy of it and rename the copy to the exact DLL filename mentioned in the error message.

* **Error: `TypeError: ... hotwords ...`**
    1.  Navigate to the `whisperx` library in your virtual environment: `.\myenv\Lib\site-packages\whisperx\asr.py`.
    2.  Find the `default_asr_options` dictionary.
    3.  Modify the line to add an empty `hotwords` list to the transcription options.
        ```python
        # Find the line that defines TranscriptionOptions and add the hotwords argument
        default_asr_options=faster_whisper.transcribe.TranscriptionOptions(**default_asr_options, hotwords=[])
        ```

* **Error: Live Recording Fails**
    1.  Open the `main.py` file in the project.
    2.  Find the `get_speakers_0` function (or a similar function responsible for handling live audio input).
    3.  Inside this function, you should find two blocks of code—one active and one commented out. Swap them by commenting out the currently active block and uncommenting the other one.
