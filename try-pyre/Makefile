PYRE_VERSION?="0.9.11"

build:
	docker build --build-arg PYRE_VERSION=${PYRE_VERSION} -t pyrepycon2022/try-pyre:${PYRE_VERSION} .

run:
	docker run -it pyrepycon2022/try-pyre:${PYRE_VERSION} bash -l

.DEFAULT_GOAL := build
