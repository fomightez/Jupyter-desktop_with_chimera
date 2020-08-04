# Jupyter Desktop Server with PyMOL installed
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/Jupyter-desktop_with_pymol/master?urlpath=desktop)

## How to use

To get started, click on `launch binder` badge at the top of bottom of this page.

After launch, when the linux desktop comes up, choose 'Use default config' button on the left.

In the upper left of the desktop screen, click on `Applications` > select `Run Program...` from the top of the list, and enter `pymol` (all lowercase). Click the `Launch` button below where you entered `pymol`
That will Launch PyMOL on a remote, temporary computer streaming in your browser.

Choose `Skip Activation` at the bottom the dialog box that comes up as PyMOL starts.

Adjust the width of the PyMOL window, if you like, by dragging on the bottom right corner.

Next to any `PyMOL>` prompt you see on the screen, type `fetch` followed by a PDB id and you'll be viewing your choice of molecule.

If you end up making anything useful, such as a session file (ending in `.pse`) or image file, you'll want to download it to your local machine. You'll need to do that from a different interface with the remote machine. Look at the URL of your PyMOL session screen and copy it. It will look similar to the following but be unique in some ways, such as the part in front of `mybinder` may be different depending on where in the global network the remote machine is:

```
https://hub.gke.mybinder.org/user/fomightez-jupyt-ktop_with_pymol-r7gbgfa3/desktop/?token=zdDDLXhXTzSw7Xcg0g1zfg
```

You want to look for `desktop` in front of `/?token..` and copy everything in front of `desktop` to **ANOTHER browser window** and add on `lab` at the end. This will result in something like this example below that's built on the example above:

```
https://hub.gke.mybinder.org/user/fomightez-jupyt-ktop_with_pymol-r7gbgfa3/lab
```

Hit return to load the page. Your generated PyMOL session file (ending in `.pse`) or image file should appear in the list of files in the file navigation panel in the upper. Right-click on the file in the list, and select `Download` from the middle of the list of possible actions.

----

If you want to use PyMOL reproducibly using scripts and the API, see [here for PyMOL use via commandline on Jupyter using MyBinder](https://github.com/fomightez/pymol-binder).

-----


This repo was originally meant to be able to run `pymol_preview_generator.py` from [here](https://github.com/mmagnus/rna-tools/tree/master/rna_tools/tools/pymol_preview_generator); however, the XFCE desktop doesn't seem to allow the icons to be changed (even using `gio set`), and so that was **a dead-end effort for now**. However, since PyMOL did at leat work in the desktop GUI, I left it in this state and a use case arose later where I could use it for training.




-----

## Technical details

[Original source repo](https://github.com/yuvipanda/jupyter-desktop-server) allows running Run XFCE (or other desktop environments) on a JupyterHub. Source based on https://github.com/ryanlovett/nbnovnc and a fork of https://github.com/manics/jupyter-omeroanalysis-desktop .

Details on some of the underlying tech is found under 'Details' [here](https://www.ovirt.org/develop/release-management/features/virt/novnc-console.html). `pymol_preivew` added from [here](https://github.com/mmagnus/rna-tools/tree/master/rna_tools/tools/pymol_preview_generator). PyMOL added as described [here](https://github.com/fomightez/pymol-binder).

Originally, dimensions of the desktop geometry were set to '1680x1050' due to [original source repo](https://github.com/yuvipanda/jupyter-desktop-server), but PyMOL interface was overly pixelated; copied '1024x768' geometry from [here](https://github.com/manics/jupyter-omeroanalysis-desktop/blob/napari-binder/jupyter_desktop/jupyter_desktop.py).


----

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/Jupyter-desktop_with_pymol/master?urlpath=desktop)
