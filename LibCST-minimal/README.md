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
pip install -e .
```


Note: currently the final pip install seems to be hanging for me,
so I'm not yet convinced this setup works.
