PWD := $(shell pwd)

.PHONY: all deps test

all: test

deps:
	@docker run --rm -t -v "$(PWD)":/app -w /app \
			golang:1.16.5-alpine3.13 go mod vendor

test:
	@docker run --rm -t -v "$(PWD)":/app -w /app \
			golangci/golangci-lint:v1.40.1-alpine \
			golangci-lint run --config .golangci.yml
	@docker run --rm -t -v "$(PWD)":/app -w /app \
			--entrypoint go golang:1.16.5-alpine3.13 \
			test -vet off $(go list ./...)
