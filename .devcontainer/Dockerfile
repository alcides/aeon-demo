FROM mcr.microsoft.com/devcontainers/base:jammy

USER vscode
WORKDIR /home/vscode

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

RUN sudo apt update && sudo apt install -y python3-dev

RUN uv venv
RUN uv pip install aeonlang



