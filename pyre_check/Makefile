PYRE_CHECK_DIR?="${HOME}/kode/pyre_check"

build:
	rm -rf pyre_check
	find ${PYRE_CHECK_DIR} \! \( \
		-name . -or -name ".git" \
		-or -path "*/.git/*" \
		-or -path "*/_build/*" \
		-or -path "*/__pycache__/*" \
		-or -path "*/documentation/*" \
		-or -path "*/build/*" \
        	\) -print \
		| cpio -padv copied
	mv copied/${PYRE_CHECK_DIR} pyre_check
	rm -rf copied
	docker build -t pyre_check:latest .

run:
	docker run -it -v ${PYRE_CHECK_DIR}:/root/pyre_check pyre_check:latest bash -l

.DEFAULT_GOAL := build
