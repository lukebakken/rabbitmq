.PHONY: start stop
start:
	docker run --rm --name rabbitmq --mount "type=bind,src=$(CURDIR)/conf.d,dst=/etc/rabbitmq/conf.d,ro" rabbitmq:4-management

stop:
	docker stop rabbitmq
