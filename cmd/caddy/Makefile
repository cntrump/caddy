NAME=caddy
BINDIR=bin
VERSION=$(shell git describe --tags || echo "unknown version")
BUILDTIME=$(shell date -u)
GOBUILD=CGO_ENABLED=1 go build -trimpath -ldflags '-X "github.com/caddyserver/caddy/constant.Version=$(VERSION)" \
		-X "github.com/caddyserver/caddy/constant.BuildTime=$(BUILDTIME)" \
		-linkmode external -w -s -buildid='

all: apple linux

apple: darwin-amd64 darwin-arm64 ios-arm64

linux: linux-amd64 linux-arm64

darwin-amd64:
	GOARCH=amd64 GOOS=darwin \
	CGO_CFLAGS="-mmacosx-version-min=10.12 -arch x86_64 -isysroot `xcrun --sdk macosx --show-sdk-path`" \
	CGO_LDFLAGS="-mmacosx-version-min=10.12 -arch x86_64 -isysroot `xcrun --sdk macosx --show-sdk-path`" \
	$(GOBUILD) -o $(BINDIR)/$(NAME)-$@

darwin-arm64:
	GOARCH=arm64 GOOS=darwin \
	CGO_CFLAGS="-mmacosx-version-min=10.12 -arch arm64 -isysroot `xcrun --sdk macosx --show-sdk-path`" \
	CGO_LDFLAGS="-mmacosx-version-min=10.12 -arch arm64 -isysroot `xcrun --sdk macosx --show-sdk-path`" \
	$(GOBUILD) -o $(BINDIR)/$(NAME)-$@

ios-arm64:
	GOARCH=arm64 GOOS=ios \
	CGO_CFLAGS="-miphoneos-version-min=10.0 -arch arm64 -isysroot `xcrun --sdk iphoneos --show-sdk-path`" \
	CGO_LDFLAGS="-miphoneos-version-min=10.0 -arch arm64 -isysroot `xcrun --sdk iphoneos --show-sdk-path`" \
	$(GOBUILD) -o $(BINDIR)/$(NAME)-$@

linux-amd64:
	GOARCH=amd64 GOOS=linux $(GOBUILD) -o $(BINDIR)/$(NAME)-$@

linux-arm64:
	GOARCH=arm64 GOOS=linux $(GOBUILD) -o $(BINDIR)/$(NAME)-$@