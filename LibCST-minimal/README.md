# Minimal LibCST starter

I made this image to have a documented flow for what it takes
to set up a minimal LibCST development environment.

To verify that the approach works, do the following:

```bash
export LIBCST_DIR=<set_me>
make
make run
```
and then inside the docker shell run
```
pip install -r requirements.txt -r requirements-dev.txt

# It seems like the cargo build might be necessary?
# - if you try to pip install off the bat, it seems to hang.
# - I may be wrong about that though
#   - the very first cargo build takes a long time because of
#     pyo3
#   - cargo prints progress, pip doesn't, so maybe me thinking
#     it's hanging is just because it takes too long with no
$     feedback
cd native && cargo build && cd /root/LibCST

pip install -e .
```

Now you can test it out:
```bash
LIBCST_PARSER=native python3 -c '

import libcst

module = libcst.parse_module("""
with (f,
      g): pass
""")

print(module)
'
```
