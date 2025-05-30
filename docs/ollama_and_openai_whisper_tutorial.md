# Deploy Language Process Applications Using Ollama

## Installation

### Step 1: Download and Install Ollama Framework
  ```bash
  $ curl -fsSL https://ollama.com/install.sh | sh

  # After running the above command, verify the installation by checking the version:
  $ ollama --version
  ```

### Step 2: Find and Download a Suitable Model
Visit the [Models](https://ollama.com/search) page to find a suitable model and size. Use the `ollama pull` command to download a pre-built model (here we use **llama3.2 1B** as an example):
  ```bash
  $ ollama pull llama3.2:1b

  # Ensure the model is downloaded successfully by listing available models:
  $ ollama models
  ```

### Step 3: Install Python Library
  ```bash
  $ pip install ollama

  # Verify the installation by checking the installed packages:
  $ pip list | grep ollama
  ```

## Usage
### Command-Line Response
  Activate the Q&A environment using the `ollama run` command and input your query:
  ```bash
  $ ollama run llama3.2:1b
  ```
  To exit the Q&A environment, press Ctrl+C.

### Python Streaming Responses
  Create a `streaming.py` file using a text editor like `vim` and add the following content:
  ```python
  from ollama import chat
  
  stream = chat(
      model='llama3.2',
      messages=[{'role': 'user', 'content': 'Why is the sky blue?'}],
      stream=True,
  )
  
  for chunk in stream:
    print(chunk['message']['content'], end='', flush=True)
 ```
 Run the `streaming.py` file
 ```bash
 $ python streaming.py
 ```

# Deploy Whisper Applications Using OpenAI Library

## Installation
  To use the Whisper library, you need to install it along with some dependencies. Follow these steps:

  ```bash
  $ pip install -U openai-whisper
  $ sudo apt update && sudo apt install ffmpeg
  $ pip install setuptools-rust
  ```

## Python Usage
From the [Whisper GitHub repository](https://github.com/openai/whisper), select the desired model and test it using the example audio files provided in the repository.
```python
import whisper, time

model_name = "tiny"
model = whisper.load_model(model_name)

t = time.time()
result = model.transcribe("./data/time.mp3")
print(result["text"], f", Real-Time Factor: {(time.time() - t)/3}")
```
