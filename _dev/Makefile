all: bin/tris-publicserver bin/tris-localserver

GOROOT/.ok:
	rm -rf GOROOT
	mkdir -p GOROOT/pkg
	cp -r "$(shell go env GOROOT)/src" GOROOT/src
	cp -r "$(shell go env GOROOT)/pkg/include" GOROOT/pkg/include
	cp -r "$(shell go env GOROOT)/pkg/tool" GOROOT/pkg/tool
	rm -r GOROOT/src/crypto/tls
	ln -s ../../../.. GOROOT/src/crypto/tls
	@echo 'GOROOT="$(CURDIR)/GOROOT"'
	@touch "$@"

bin:
	mkdir -p "$@"

bin/tris-publicserver: bin tris-publicserver/* ../*.go GOROOT/.ok
	GOROOT="$(CURDIR)/GOROOT" go build -i -v -o "$@" ./tris-publicserver
bin/tris-localserver: bin tris-localserver/* ../*.go GOROOT/.ok
	GOROOT="$(CURDIR)/GOROOT" go build -i -v -o "$@" ./tris-localserver