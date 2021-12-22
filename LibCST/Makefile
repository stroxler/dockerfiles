LIBCST_DIR?="${HOME}/kode/LibCST"

build:
	mkdir -p libcst-deps
	cp ${LIBCST_DIR}/requirements.txt libcst-deps
	cp ${LIBCST_DIR}/requirements-dev.txt libcst-deps
	cp -R ${LIBCST_DIR}/native/ libcst-deps/native
	docker build -t libcst:latest . --build-arg PYTHON_VERSION=3.10.1

run:
	docker run -it -v ${LIBCST_DIR}:/root/LibCST libcst:latest bash

.DEFAULT_GOAL := build
