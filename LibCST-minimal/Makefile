LIBCST_DIR?="${HOME}/kode/LibCST"

build:
	docker build -t libcst-minimal:latest .

run:
	docker run -it -v ${LIBCST_DIR}:/root/LibCST libcst-minimal:latest bash

.DEFAULT_GOAL := build
