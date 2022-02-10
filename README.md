# Jupyter Desktop Server with UCSF Chimera installed
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/Jupyter-desktop_with_chimera/master?urlpath=desktop)

## How to use <=== CURRENTLY DOESN'T WORK DUE TO OPENGL ISSUE?!?!?

To get started, click on `launch binder` badge at the top of bottom of this page.

After launch, when the linux desktop comes up, choose 'Use default config' button on the left.

Use Firefox to download the linux installer for UCSF Chimera.

Opened a terminal using icon at the bottom.
Moved the installer from `Downloads` to home using:

```bash
mv Downloads/chimera-1.14-linux_x86_64.bin
```

Change permissions on installer following along with step number (2) under 'Downloading and Installation' at https://www.cgl.ucsf.edu/chimera/data/downloads/1.5.2/linux.html

```bash
chmod +x chimera-1.14-linux_x86_64.bin
```

Then run the installer by entering:

```bash
./chimera-1.14-linux_x86_64.bin
```

Accepting the defaults except use `4` when have a long list of where to put link.

Then ready to launch. (Option A: is to type `chimera` in terminal.)

When launch UCSF chimera by selecting `Applications` > `Run Program..` and then typing `chimera`, chimera tries to launch and I see a splach screen in chimera that says:

```bash
chimera startup error
Error initalizing OpenGL: X server is missing OpenGL GLX extension
Couldnt configure togl widget
```



Troubleshooting the current road-block
--------------------------------------

The issue seems to be summarized [here](https://virtualgl.org/vgldoc/2_2_1/):
>"Some remote display software, such as VNC, lacks the ability to run OpenGL applications at all. Other remote display software forces OpenGL applications to use a slow software-only OpenGL renderer, to the detriment of performance as well as compatibility. The traditional method of displaying OpenGL applications to a remote X server (indirect rendering) supports 3D hardware acceleration, but this approach causes all of the OpenGL commands and 3D data to be sent over the network to be rendered on the client machine. This is not a tenable proposition unless the data is relatively small and static, unless the network is very fast, and unless the OpenGL application is specifically tuned for a remote X-Windows environment."

Troubleshooting ideas:

https://www.cgl.ucsf.edu/chimera/data/downloads/1.5/linux.html

from http://www.cgl.ucsf.edu/chimera/graphics/updatelinux.html and , I see `glxinfo` is the way to explore further but When I run `glxinfo` on command line I get:

```bash
Error: couldnt find RGB GLX visual or fbconfig
```

glxgears gives a similar issue. Do I need `xvfb` started?

Yes. Running that  based on Halfgaar's comment [here](https://unix.stackexchange.com/questions/104914/why-does-xvfb-run-glxgears-fail-with-an-swrast-error)allows `glxgears` and `glxinfo` to run. First to show for `glxgears`.

```bash
xvfb-run --server-args "-screen 0 1920x1080x24" glxgears
```

Did CTRL-C to stop it after clear `glxgears` was running. I don't know if it stops itself.

So I ran the following to check the OpenGL info like I had seen advised at [here](http://ubuntuhandbook.org/index.php/2019/12/install-mesa-19-3-ubuntu-18-04-19-10/).


```bash
xvfb-run --server-args "-screen 0 1920x1080x24" glxinfo | grep "OpenGL"
```
Works and gives me information about OpenGL using `Mesa`.

Next problem to overcome is that want UCSF Chimera to run in the XFCE4 OS GUI. Will this help there? I suspect not since I tried with Firefox and it just waited in terminal as if running and when I tried to open application in OS GUI, it said it was running. So it works but I cannot access it in the GUI this way. How to get Firefox in the OS GUI to use the MESA? [This](https://bugzilla.mozilla.org/show_bug.cgi?id=731836) seemed most helpful I've found so far in regards to that, and then I also found [this](https://superuser.com/questions/930807/using-a-locally-built-libosmesa-to-enable-webgl-in-firefox) but even that person seemed to not be able to get it to work(??), but I haven't figured out how quite yet.


Troubleshooting further info

https://github.com/mne-tools/mne-binder/issues/2#issuecomment-479523225

https://discourse.slicer.org/t/3d-slicer-cloud-computing-again/5781/11


https://groups.google.com/a/lbl.gov/forum/?nomobile=true#!topic/singularity/F1mMAU2ex9M

https://askubuntu.com/questions/418532/whats-ubuntu-package-for-virtualgl-libs

https://forums.developer.nvidia.com/t/error-couldnt-get-an-rgb-double-buffered-visual/108823

`vglrun glxgears` <=== How do I get `vglrun`? I tried what was at https://askubuntu.com/questions/418532/whats-ubuntu-package-for-virtualgl-libs but still not running

http://www.cgl.ucsf.edu/chimera/graphics/updatelinux.html

http://ubuntuhandbook.org/index.php/2019/12/install-mesa-19-3-ubuntu-18-04-19-10/


https://www.wikihow.com/Install-Mesa-(OpenGL)-on-Linux-Mint

-----

## Technical details

[Original source repo](https://github.com/yuvipanda/jupyter-desktop-server) allows running Run XFCE (or other desktop environments) on a JupyterHub. Source based on https://github.com/ryanlovett/nbnovnc and a fork of https://github.com/manics/jupyter-omeroanalysis-desktop .

------

### Testing Pandasgui here

Since this had build essentials installed by apt, I thought it would work to get past the issue I was seeing about `evdev`` installing with pip, as pointe out [here](https://github.com/adamerose/PandasGUI/issues/81#issuecomment-808436130), and fortunately it did. So was wondering if I can use it now?
Seems I can use it in the desktop if I do a little more:

Opened JupyterLab in another tab and in terminal there ran the following following [Pandasgui documentation] to install the current pandasgui:
```shell
pip install git+https://github.com/adamerose/pandasgui.git
```

I know that seems redundant since conda supposedly installed pandasgui, but despite looking I couldn't find where to point at to use it on command line, and turns out this trick works to add `pandasgui` to path.

Now if I open a new terminal in the deksptop and type `pandasgui --help` it opens an empty pandasgui graphic program window! (Note I was expecting usage text because of `--help` but it opened the program. `pandasgui` alone did nothing.)

I suspect if I called it with a tab-separated file or a dataframe maybe, it would open it. It has an `import` in it that lists recognizing several file formats.  
I'll note when I try to use 'Browser Sample Datasets' inside the program's window, it chokes on it saying `os` has no attribute `startfile.`


----

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/Jupyter-desktop_with_chimera/master?urlpath=desktop)
