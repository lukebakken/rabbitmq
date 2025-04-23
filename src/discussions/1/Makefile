.PHONY: start stop start-release remove-release

RABBITMQ_VERSION ?= 4.1.0
RABBITMQ_ARCHIVE ?= rabbitmq-server-generic-unix-latest-toolchain-$(RABBITMQ_VERSION).tar.xz

start:
	docker run --rm --name rabbitmq --mount "type=bind,src=$(CURDIR)/conf.d,dst=/etc/rabbitmq/conf.d,ro" rabbitmq:4-management

stop:
	docker stop rabbitmq

$(CURDIR)/rabbitmq_server-$(RABBITMQ_VERSION)/sbin/rabbitmq-server:
	curl -LO https://github.com/rabbitmq/rabbitmq-server/releases/download/v$(RABBITMQ_VERSION)/$(RABBITMQ_ARCHIVE) && \
	tar xf $(CURDIR)/$(RABBITMQ_ARCHIVE)
rabbitmq-server-4: $(CURDIR)/rabbitmq_server-$(RABBITMQ_VERSION)/sbin/rabbitmq-server
start-release: rabbitmq-server-4
	cd $(CURDIR)/rabbitmq_server-$(RABBITMQ_VERSION) && \
	RABBITMQ_CONFIG_FILES="$(CURDIR)/conf.d" ./sbin/rabbitmq-server

remove-release:
	rm -rf $(RABBITMQ_ARCHIVE) rabbitmq_server-$(RABBITMQ_VERSION)
