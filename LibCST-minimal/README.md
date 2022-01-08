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

# install dependencies and build libcst
#
pip install -r requirements.txt -r requirements-dev.txt
pip install -e .


# Test it out, using the native parser
#
LIBCST_PARSER_TYPE=native python3 -c '

import libcst

module = libcst.parse_module("""
# this code wouldn't parse without the native parser
try:
    pass
except* OSError as e:
    pass
""")

print(module)
'

```
