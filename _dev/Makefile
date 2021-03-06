GO ?= go
GOROOTINFO := $(shell $(GO) version | cut -d' ' -f 3)_$(shell $(GO) env GOOS)_$(shell $(GO) env GOARCH)

.PHONY: GOROOT
GOROOT: GOROOT/.ok_$(GOROOTINFO)
	@rm -f GOROOT/pkg/*/crypto/tls.a

GOROOT/.ok_$(GOROOTINFO):
	rm -rf GOROOT
	mkdir -p GOROOT/pkg
	cp -r "$(shell $(GO) env GOROOT)/src" GOROOT/src
	cp -r "$(shell $(GO) env GOROOT)/pkg/include" GOROOT/pkg/include
	cp -r "$(shell $(GO) env GOROOT)/pkg/tool" GOROOT/pkg/tool
	rm -r GOROOT/src/crypto/tls
	ln -s ../../../.. GOROOT/src/crypto/tls
	GOROOT="$(CURDIR)/GOROOT" $(GO) install -v std
ifeq ($(shell go env CGO_ENABLED),1)
	GOROOT="$(CURDIR)/GOROOT" $(GO) install -race -v std
endif
	@touch "$@"

GO_COMMIT := 7f0d4506a23398116934a6b2b31bc9cda63402b1

.PHONY: go/bin/go
go/bin/go: .ok_go_$(GO_COMMIT)_$(shell $(GO) env GOOS)_$(shell $(GO) env GOARCH)

.ok_go_$(GO_COMMIT)_$(shell $(GO) env GOOS)_$(shell $(GO) env GOARCH):
	rm -rf go .ok_go_*
	git clone --branch 1.7 --single-branch --depth 25 https://github.com/cloudflare/go
	cd go && git checkout $(GO_COMMIT)
	cd go/src && GOROOT_BOOTSTRAP="$(shell $(GO) env GOROOT)" ./make.bash
	@touch "$@"

.PHONY: clean
clean:
	rm -rf GOROOT go .ok_go_*
