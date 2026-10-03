# gitpod doesn't support multiple FROM statements, (or rather, you can't copy from one to another)
# so we just install everything in one go
FROM ubuntu:jammy

USER root

RUN apt-get update && apt-get install sudo git curl git bash-completion -y && apt-get clean

RUN useradd -l -u 33333 -G sudo -md /home/gitpod -s /bin/bash -p gitpod gitpod \
    # passwordless sudo for users in the 'sudo' group
    && sed -i.bkp -e 's/%sudo\s\+ALL=(ALL\(:ALL\)\?)\s\+ALL/%sudo ALL=NOPASSWD:ALL/g' /etc/sudoers
USER gitpod
WORKDIR /home/gitpod

SHELL ["/bin/bash", "-c"]

# gitpod bash prompt
RUN { echo && echo "PS1='\[\033[01;32m\]\u\[\033[00m\] \[\033[01;34m\]\w\[\033[00m\]\$(__git_ps1 \" (%s)\") $ '" ; } >> .bashrc

# install uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

ENV PATH="/home/gitpod/.local/bin:${PATH}"

# Keep the project command available in every Gitpod terminal.
ENV VIRTUAL_ENV="/home/gitpod/.venv"
ENV PATH="/home/gitpod/.venv/bin:${PATH}"
RUN uv venv /home/gitpod/.venv && uv pip install --python /home/gitpod/.venv/bin/python aeonlang

# ssh to github once to bypass the unknown fingerprint warning
RUN ssh -o StrictHostKeyChecking=no github.com || true

# run sudo once to suppress usage info
RUN sudo echo finished
