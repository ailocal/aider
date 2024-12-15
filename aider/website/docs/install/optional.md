---
parent: Installation
nav_order: 20
---

# Optional steps
{: .no_toc }

The steps below are completely optional.

- TOC
{:toc}


## Store your api keys 

You can [store your api keys in a .env file](/docs/config/dotenv.html)
and they will be loaded automatically whenever you run aider.

## Enable Playwright 

Aider supports adding web pages to the chat with the `/web <url>` command.
When you add a url to the chat, aider fetches the page and scrapes its
content.

By default, aider uses the `httpx` library to scrape web pages, but this only
works on a subset of web pages.
Some sites explicitly block requests from tools like httpx.
Others rely heavily on javascript to render the page content,
which isn't possible using only httpx.

Aider works best with all web pages if you install
Playwright's chromium browser and its dependencies:

```
playwright install --with-deps chromium
```

See the
[Playwright for Python documentation](https://playwright.dev/python/docs/browsers#install-system-dependencies)
for additional information.


## Enable voice coding 

Aider supports 
[coding with your voice](https://aider.chat/docs/usage/voice.html)
using the in-chat `/voice` command.

### Audio capture setup

Aider uses the [PortAudio](http://www.portaudio.com) library to
capture audio.
Installing PortAudio is completely optional, but can usually be accomplished like this:

- For Windows, there is no need to install PortAudio.
- For Mac, do `brew install portaudio`
- For Linux, do `sudo apt-get install libportaudio2`
  - Some linux environments may also need `sudo apt install libasound2-plugins`

### Whisper API configuration

By default, aider uses OpenAI's Whisper API for voice transcription. You can configure an alternate Whisper API provider:

```bash
# Via command line arguments
aider --set-env WHISPER_API_BASE=https://api.example.com --api-key whisper=your-api-key

# Via environment variables or .env file
WHISPER_API_BASE=https://api.example.com
WHISPER_API_KEY=your-api-key

# Via config file (.aider.conf.yml)
api-base:
  - whisper=https://api.example.com
api-key:
  - whisper=your-api-key
```

When using an alternate Whisper API endpoint:
- You must provide both the API base URL and API key
- Your OpenAI API key will not be sent to the alternate endpoint
- This is useful for:
  - Using a different Whisper API provider
  - Running Whisper locally or on your own infrastructure
  - Controlling costs or data privacy

API key behavior:
- If using a custom WHISPER_API_BASE, you must provide a WHISPER_API_KEY
- If using the default OpenAI endpoint (or no endpoint specified):
  - Will use WHISPER_API_KEY if provided
  - Will fall back to OPENAI_API_KEY if no WHISPER_API_KEY is set
- If neither key is available, an error will be raised

## Add aider to your editor 

Other projects have integrated aider into some IDE/editors.
It's not clear if they are tracking the latest
versions of aider,
so it may be best to just run the latest
aider in a terminal alongside your editor.

### NeoVim

[joshuavial](https://github.com/joshuavial) provided a NeoVim plugin for aider:

[https://github.com/joshuavial/aider.nvim](https://github.com/joshuavial/aider.nvim)

### VS Code

joshuavial also confirmed that aider works inside a VS Code terminal window.
Aider detects if it is running inside VSCode and turns off pretty/color output,
since the VSCode terminal doesn't seem to support it well.

### Other editors

If you are interested in creating an aider plugin for your favorite editor,
please let me know by opening a
[GitHub issue](https://github.com/Aider-AI/aider/issues).


## Install the development version of aider 

If you want the very latest development version of aider
you can install directly from GitHub:

```
python -m pip install --upgrade git+https://github.com/Aider-AI/aider.git
```

If you've git cloned the aider repository already, you can install "live" from your local copy. This is mostly useful if you are developing aider and want your current modifications to take effect immediately.

```
python -m pip install -e .
```

