# Example Python Cryptographic Machine Files

This is an example of how to verify and decrypt [cryptographic machine files](https://licensegen.focusapps.app/docs/api/cryptography/#cryptographic-lic)
in Python, using Ed25519 signing and AES-256-GCM encryption. This example
verifies the `aes-256-gcm+ed25519` algorithm.

## Running the example

First up, add an environment variable containing your Ed25519 public key:
```bash
export LICENSEGEN_PUBLIC_KEY='002e17159b4321fd8705ffeb52e5c25c19d8999e29310c49e35f7769844bd587'
```

You can either run each line above within your terminal session before
starting the app, or you can add the above contents to your `~/.bashrc`
file and then run `source ~/.bashrc` after saving the file.

Next, install dependencies with [`pip`](https://packaging.python.org/):

```
python3 -m pip install -r requirements.txt
```

Then run the script, passing in a `path` to a machine file, and a `license`
key as arguments:

```bash
python3 main.py --license 'A_LICENSE_KEY' \
  --path examples/machine.lic
```

Or run one of the pre-defined examples:

```bash
LICENSEGEN_PUBLIC_KEY='002e17159b4321fd8705ffeb52e5c25c19d8999e29310c49e35f7769844bd587' python3 main.py \
  --fingerprint '198e9fe586114844f6a4eaca5069b41a7ed43fb5a2df84892b69826d64573e39' \
  --license '80246B-1DE0D3-B22291-00B387-B9C4DD-V3' \
  --path examples/machine.lic
```

The following will happen:

1. The current device will be fingerprinted, using a SHA256-HMAC digest of the
   device's [machineid](https://github.com/focusapps/licensegen-py-machineid). You may
   want to look into alternative fingerprinting, depending on your expected
   run environment.
1. The machine file's authenticity will be verified using Ed25519, by verifing
   its signature using the public key.
1. The machine file will be decrypted using the license key and fingerprint
   as the decryption key.

If everything checks out, the script will print the decrypted contents of
the machine file — the machine object, with any included data. If it
fails, check your inputs.

## Questions?

Reach out at [licensegen@focusapps.app](mailto:licensegen@focusapps.app) if you have any
questions or concerns!
