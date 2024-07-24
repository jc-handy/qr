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
qr This is a test!
```

This will use Unicode block characters to output the QR code directly to standard output. It should look like this:


```
