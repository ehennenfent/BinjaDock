
# binja_toolbar

binja_toolbar is a fork of BinjaDock that adds a toolbar to Binary Ninja and allows you to easily add buttons to it. You probably won't have a reason to use this as it is, but other plugin developers may find it makes it easy for them to effectively incorporate their code into the UI.

## Installation
Inside your [Binary Ninja plugins folder](https://github.com/Vector35/binaryninja-api/tree/master/python/examples#loading-plugins), just run `git clone https://github.com/ehennenfent/binja_toolbar.git`

## Sample Usage
The following script adds some demo buttons to the toolbar. This can be placed in the `__init__.py` file of its own plugin.
```
~/
  .binaryninja/
    plugins/
      toolbar_tester/
        __init__.py
        fidget_spinner.png
      binja_toolbar/
```

```python
from binja_toolbar import add_image_button, add_text_button
from binaryninja import log

def show_demo_message(_view):
    try:
        log.log(3, "Current bv is associated with: " + _view.file.filename)
    except:
        print("No view yet!")

add_text_button("Test", show_demo_message)

def show_toolbar_message(_view):
    log.log(3, "This is an image button!")

add_image_button('.binaryninja/plugins/toolbar_tester/fidget_spinner.png', (24,24), show_toolbar_message, tooltip="Just a demo button")
```

Note that plugins are initialized inside of `~`, so it is necessary to specify the entire file path for images.

## Current Limitations
There's currently (to my knowledge) no good way to track when the user switches between open binary views, so this plugin works best when used with only a single binary open. One can make it work by reinitializing the toolbar every time one switches between binaries, but that's less than ideal. This may not be fixed until the upcoming UI API features in version 1.2.

## Requirements
* PyQt5
* Binary Ninja

binja_toolbar has only been tested on Ubuntu 16.04. You are encouraged to file a pull request or open an issue for any incompatibilities.
