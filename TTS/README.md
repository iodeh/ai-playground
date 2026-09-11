# DEPRECATED

These are the old scripts that were used with [TalkWithMe](https://github.com/scorbo2/TalkWithMe) up to and
including version 6. Starting in TalkWithMe v7, these scripts are now deprecated in favor of the much
better [tts-serve](https://github.com/scorbo2/tts-serve) project.

These scripts are kept here for historical reasons only. All new development should use `tts-serve`,
as it's just so much better.

## Historical stuff follows

These are support scripts for use with [dots.tts](https://github.com/rednote-hilab/dots.tts),
Qwen3-TTS, or OmniVoice in a local environment.

- `server_dotsTTS.py` - a simple REST API around `dots.tts`
- `server_qwen3TTS.py` - a simple REST API around `Qwen3-TTS`
- `server_omnivoice.py` - a simple REST API around `OmniVoice`
- All server scripts expose the following endpoints:
  - `POST /synthesize` clones a voice given reference audio, returns the requested text in that cloned voice.
  - `GET /health` simple health check to confirm server is up

Additionally, some useful helper sripts are also provided:

- `speak.sh` - A simple bash script to hit the REST API (quick and dirty version).
- `speak.py` - A newer and much-improved version of speak.sh... use this one, it's highly configurable.
- `parse.py` - A simple Python script to transcribe audio from an OpenAI-compatible transcription server.

## Using the `server*.py` scripts

These custom Python script can stand up a nice REST API in front of a locally-running TTS server,
and allow you to make TTS requests from shell scripts or code (example scripts provided above).

To set this up, copy the server script to your TTS project directory. For example:

```
cp server_dotsTTS.py /some/path/to/dots.tts/
cp server_qwen3TTS.py /some/path/to/Qwen3-TTS/
cp server_omnivoice.py /some/path/to/OmniVoice/
```

Then you can start it with uvicorn:

```
cd /some/path/to/dots.TTS
uvicorn server_dotsTTS:app --host 0.0.0.0 --port 8181

cd /some/path/to/Qwen3-TTS
uvicorn server_qwen3TTS:app --host 0.0.0.0 --port 8181

cd /some/path/to/OmniVoice
uvicorn server_omnivoice:app --host 0.0.0.0 --port 8181
```

Now you should be able to make REST requests against the `/synthesize` endpoint.
Refer to `speak.sh` or `speak.py` above for simple bash and Python examples.

The [TalkWithMe](https://github.com/scorbo2/TalkWithMe) application makes heavy
use of these server scripts for speech synthesis, if you want a more detailed usage example.

