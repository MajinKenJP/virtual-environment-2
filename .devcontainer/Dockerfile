FROM python:3.11

ENV PYTHONUNBUFFERED=1

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

WORKDIR /workspace

RUN apt-get update \
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    && apt-get -y install git iproute2 procps lsb-release \
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME

RUN apt-get -y install curl git
RUN pip install --upgrade pip
RUN pip install --upgrade setuptools
RUN pip install flake8 autopep8

COPY .devcontainer/requirements.txt .
RUN pip install -r requirements.txt

# 本番環境ではCMD ["python", "main.py"] とする
CMD ["python"]