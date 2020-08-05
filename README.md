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
Couldn't configure togl widget
```

Troubleshooting the current road-block
--------------------------------------

The issue seems to be summarized [here](https://virtualgl.org/vgldoc/2_2_1/):
>"Some remote display software, such as VNC, lacks the ability to run OpenGL applications at all. Other remote display software forces OpenGL applications to use a slow software-only OpenGL renderer, to the detriment of performance as well as compatibility. The traditional method of displaying OpenGL applications to a remote X server (indirect rendering) supports 3D hardware acceleration, but this approach causes all of the OpenGL commands and 3D data to be sent over the network to be rendered on the client machine. This is not a tenable proposition unless the data is relatively small and static, unless the network is very fast, and unless the OpenGL application is specifically tuned for a remote X-Windows environment."

Troubleshooting ideas:

https://www.cgl.ucsf.edu/chimera/data/downloads/1.5/linux.html

from http://www.cgl.ucsf.edu/chimera/graphics/updatelinux.html and , I see `glxinfo` is the way to explore further but When I run `glxinfo` on command line I get:

```bash
Error: couldn't find RGB GLX visual or fbconfig
```

glxgears gives a similar issue. Do I need `xvfb` started?


https://github.com/mne-tools/mne-binder/issues/2#issuecomment-479523225

https://discourse.slicer.org/t/3d-slicer-cloud-computing-again/5781/11


https://groups.google.com/a/lbl.gov/forum/?nomobile=true#!topic/singularity/F1mMAU2ex9M

https://askubuntu.com/questions/418532/whats-ubuntu-package-for-virtualgl-libs

https://forums.developer.nvidia.com/t/error-couldnt-get-an-rgb-double-buffered-visual/108823

`vglrun glxgears` <=== How do I get `vglrun`.

http://www.cgl.ucsf.edu/chimera/graphics/updatelinux.html


https://www.wikihow.com/Install-Mesa-(OpenGL)-on-Linux-Mint

-----

## Technical details

[Original source repo](https://github.com/yuvipanda/jupyter-desktop-server) allows running Run XFCE (or other desktop environments) on a JupyterHub. Source based on https://github.com/ryanlovett/nbnovnc and a fork of https://github.com/manics/jupyter-omeroanalysis-desktop .



----

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/Jupyter-desktop_with_chimera/master?urlpath=desktop)
