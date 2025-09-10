# Variables
COMPOSE = docker compose

# Build app image
build:
	$(COMPOSE) build app

# Start services with build
up:
	$(COMPOSE) up --build

# Stop services and remove volumes
down:
	$(COMPOSE) down -v

# Clean output directory and stop services
clean: down
	rm -rf out && mkdir -p out

# Complete workflow: clean and start
all: clean up

# Phony targets
.PHONY: build up down clean all