DIR := $(shell pwd)
VENV := .venv


install:
	@poetry config virtualenvs.in-project true
	@poetry install
	@echo "[ \033[00;32mPoetry setup completed. You are good to go!\033[0m ]"

fastapi:
	@echo "[ \033[00;32mStarting service\033[0m ]"
	@. $(DIR)/$(VENV)/bin/activate && uvicorn --host 0.0.0.0 --port $(PORT) "server.main:create_app"

server-kill:
	@docker-compose kill
	@docker-compose rm

server-start: server-kill
	@echo ""
	@echo "[ \033[00;32mRunning in docker-compose\033[0m ]"
	@docker-compose build --pull base
	@docker-compose up --build --force-recreate --remove-orphans -d redis triton api
