# SpotiByeAds (Homebrew Compatibility Fork)
 [![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/) 
 [![GitHub license](https://img.shields.io/github/license/daspartho/SpotiByeAds.svg)](https://github.com/daspartho/SpotiByeAds/blob/main/LICENSE)
 [![Documentation Status](https://readthedocs.org/projects/spotibyeads/badge/?version=latest)](https://spotibyeads.readthedocs.io/en/latest/?badge=latest)
 
[See the Original Project Here](https://github.com/daspartho/SpotiByeAds)

No one likes interruptions! Don't you hate it when you're listening to your favorite jazz track or your EDM playlist and an ad for Old Spice or Pepsi starting playing interrupting your mood? With SpotiByeAds, you can listen ad-free allowing you to concentrating less on those ads and more towards the task at hand!

# How it works?
SpotiByeAds or SBA for short utilizes Python with the SpotiPy API and Pynput Libraries as well as the `os` and `sys` modules in order to provide you with an ad-free experience.

First, it asks you for your Spotify Username, Client ID and Client Secret (which is done by running `python main.py`). Of course if you've used this program and have saved the credentials, it should load a json file with your credentials in it and if not, it will ask for your credentials.
Note that whenever you enter your credentials, you have the option of either saving your credentials for future use or keeping your credentials just for that session of using SBA.

After SBA has your credentials, it will establish a connection with Spotify by restarting it and setting it to your last known track/playlist.
When an ad enters your spotify queue, SBA will detect the current track as an ad and restart the app. After the restart, SBA will automatically queue up the next track!

# Requirements
- Python 3
- Pip (Python's Package Manager)

# Installation
> It should be noted that this is a quick way to get SBA (SpotiByeAds) up and running!
>
> For a detailed documentation, go [here](https://spotibyeads.readthedocs.io/en/latest/).

- First, clone the repository.
```
git clone https://github.com/ThaumielSparrow/spotibye-homebrew
```
- Then, change your current directory into the SpotiByeAds repository.
```
cd spotibye-homebrew
```
- Finally, install the requirements in the requirements file.
```
pip install -r requirements.txt
```
- From here, SpotiByeAds is installed. Continue to the Setting Up section in order to connect SpotiByeAds to Spotify itself.

# Setting up

You should need to do these only the first time.

1. Go to https://developer.spotify.com/dashboard and sign in with your Spotify account.
2. Click on the 'CREATE AN APP' option and provide an app name and app description as you'd like.
3. Go to 'EDIT SETTINGS' and fill in the Redirect URIs placeholder with http://localhost:8080/, click Add, then click on Save.
4. Copy down your **Client ID** and **Client Secret** (found by clicking Reveal Client Secret). You will need these when you run the script later on.
   - ⚠️ **Please remember to never share your Client Secret with anyone. This could lead to your account getting stolen or irregular Spotify user behavior that could lead to account termination.**
   - **Developers of SpotiByeAds will never ask for your Client Secret.**

⚠️⚠️⚠️

If you are on Linux and installed a **containerized** version of Spotify (e.g via Snap or Flatpack) or any unofficial forms of distribution (or have installed Spotify in a location other than the default location chosen by the installer and is not in $PATH), please paste the path to the Spotify executable on your computer (or a command that starts up the Spotify app) in the `main.py` script on the line described below:
```python
    PATH = (shutil.which("spotify")  # For any system with spotify on $PATH
            or ("{HOMEDRIVE}{HOMEPATH}\AppData\Roaming\Spotify\Spotify.exe"
                .format_map(os.environ) if os.name == "nt"  # Windows
                else "/Applications/Spotify.app" if sys.platform == "darwin"  # MacOS
                else ""  # Custom path if installation is different
               )
           )
```
Please find this part of the script and paste the path/command within the `""` (empty quotes) on the line with the comment `# Custom path ...`.

⚠️⚠️⚠️

# Usage
1. Open Spotify and start a track or playlist.
2. Run the script from a terminal using `python main.py` in the local repository's directory (or probably by double-clicking on the `main` python script from your file explorer on Windows).
   - If it's the first time running the script, enter your Spotify username and paste in the **Client ID** and **Client Secret** when prompted to enter them.
4. Script will start running and automatically start skipping ads.

## Pausing playback, Skipping tracks, Changing playlists.

Due to the way the script works, pausing and playing or manually changing tracks disrupts its work, such that the next ad that comes up might not be skipped.

When you want to perform any of the above actions:
1. Go to the terminal where in the script is running.
2. Press `Ctrl-C` **once**.
3. Follow the prompts to perform your desired action.

⚠️**Note**: If you're using **Command Prompt** on windows, please note that it might have some unwanted behaviour with keyboard input that affects this feature. **You are strongly advised to run the script in _Windows Powershell_**.

# Building

## MacOS / Linux 
If you'd like to build for Mac / Linux, do the following:
1. To build in a development environment (to make sure it works right), run `python setup.py py2app -A`. Please note: This builds the app in something called *alias mode*. This is NOT a proper build, and will only work on the machine it was run on.
2. To build a proper package, run `python setup.py py2app`. 

## Any major platform
You'll need Python 3 with the `PyInstaller` package installed. The run the following command in a terminal from the project directory.
```
pyinstaller --onefile --collect-submodules pynput -c -n SpotiByeAds main.py
```
If succesful, then check for the executable file in the `dist/` directory created.
