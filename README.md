# dockerfiles

Docker config for various projects I work on.

Because I'm trying to dockerize things that live outside my control, it's
harder to use a normal docker setup which relies on the code living under
the repo with a Dockerfile.

As a result, these dev containers are built using makefiles that allow me
to work around such limitations. Generally you can run `make` or
`make build` to build a docker container, and `make run` to run it with
a mount. You'll likely need to set an environment variable pointing at
where the project code lives.


## Notes, project by project

### LibCST

I make a base rust+python image first, which really could be extracted into
its own image.

Then, I install python (with the python version to use as a docker build
arguments).

Then, I copy in some files as needed to pre-fetch both pip and cargo
dependencies. Unfortunately at this time the way cargo does it means that
re-running `make` after *any* edit to the rust files will rerun the cargo
fetch, but the pip fetches are smart and only depend on requirements files.

One thing that worried me was whether stopping and starting the container
would trigger a full cargo rebuild, which is a bit time consuming, but it
turns out that because the mounted-in LibCST directory persists this isn't
an issue.
