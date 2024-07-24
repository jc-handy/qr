# QR
The `qr` command I'm offering here is a small wrapper around [mnooner256](https://pypi.org/user/mnooner256/)'s very nice [`pyqrcode`](https://pypi.org/project/PyQRCode/) package and makes generating QR codes simple and easy from the command line.

# QUICK START
## Clone the QR project and Put it in its own Python Virtual Environment
You can `pip install pyqrcode` into your current version of Python's `site-packages` directory, and then simply copy the `qr` command directly into your `~/bin` directory (or wherever you keep local scripts under your home directory). But that's sloppy and will lead to trouble. I strongly recommend using the simple procedure below to create a small Python virtual environment where `qr` will run and find `pyqrcode` installed.

```shell
mkdir ~/venvs # (if necessary). This is where I keep my local Python virtual environments.
cd ~/venvs
get clone https://github.com/jc-handy/qr.git
cd qr
python3 -m venv .
source bin/activate
pip3 install -r requirements.txt
```

If there are any errors during `pip3 install ...`, you'll have to deal with whatever error messages it offers. But the `pyqrcode` appears to have no dependencies, so I wouldn't expect problems.

At this point, you can test the venv by running `./qr --help`. If you get only the usage message, all is well.

Run `deactivate` to deactivate the venv we created and activated above.

## Greatly Simplify running `qr` in It's Venv
If you find yourself using `qr` often, or if you just don't want to mess with activating and deactivating the venv it's in, it's simple to set up a `qr` simlink from somewhere on your PATH.

```shell
cd ~/venvs/qr
ln -s "$PWD/runner" ~/bin/qr # (assuming ~/bin is where you keep local commands on your PATH)
```

That's it. You can now (possibly after running `rehash` from your current shell) run `qr` from any directory, and you don't have to manually activate and deactivate the venv! Life is good.

# USAGE

Create a test QR code.
```shell
qr 'This is a test!'
```

This will use Unicode block characters to output the QR code directly to standard output. The aspect ratio will depend on the font your terminal is using, but it ought to be close enough to square that QR readers will have no trouble with it. It should look something like this:

![textual QR code for "This is a test!"](docs/assets/text-output.png)

Create a test QR code as a PNG file. 'The text generally needn't be quoted as below, but the `!` character can be problematic in some shell configurations if it's not single-quoted.)
```shell
qr --format png --file testing.png --scale 4 'This is a test!'
```

That will create a small file called testing.png scaled by a factor of 4 (smaller that the default scaling factor of 16). This image will be perfectly square and suitable for display in the corner of a web page, for instance.

![PNG image of our test QR code](docs/assets/png-output.png)

One last handly little step-saver is to generate the PNG file and show it in your default image viewer. This is often convenient if all you want is to copy the image to your clipboard.

```shell
qr --format show --scale 4 Any number of command line arguments can be accepted as the input to be QR-encoded.
```

The `show` format
1. creates the QR code in a temporary PNG file,
2. opens it with your system's default application for that file type,
3. deletes the PNG file,
4. and terminates.

The presumption is you can copy the image from the default PNG-opener on your system and paste it into some other document.
