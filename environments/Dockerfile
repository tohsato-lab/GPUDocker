ARG BASE_IMAGE=ubuntu:20.04
FROM ${BASE_IMAGE}

ARG PROJECT_NAME=ProjectCompbio
ARG USER_NAME=user
ARG GROUP_NAME=compbio
ARG UID=1000
ARG GID=1000
ARG PYTHON_VERSION=3.9
ARG APPLICATION_DIRECTORY=/home/${USER_NAME}/${PROJECT_NAME}
ARG RUN_POETRY_INSTALL_AT_BUILD_TIME="false"

ENV DEBIAN_FRONTEND="noninteractive" \
    LC_ALL="C.UTF-8" \
    LANG="C.UTF-8" \
    PYTHONPATH=${APPLICATION_DIRECTORY}

# Following is needed to install python 3.7
RUN apt update && apt install --no-install-recommends -y software-properties-common 
RUN add-apt-repository ppa:deadsnakes/ppa

RUN apt update && apt install --no-install-recommends -y \
    git curl make ssh openssh-client \
    python${PYTHON_VERSION} python3-pip python-is-python3
    
# Following is needed to swtich default python3 version
# For detail, please check following link https://unix.stackexchange.com/questions/410579/change-the-python3-default-version-in-ubuntu
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python${PYTHON_VERSION} 1 
RUN update-alternatives --set python3 /usr/bin/python${PYTHON_VERSION}
    # `requests` needs to be upgraded to avoid RequestsDependencyWarning
    # ref: https://stackoverflow.com/questions/56155627/requestsdependencywarning-urllib3-1-25-2-or-chardet-3-0-4-doesnt-match-a-s
# if python version ">=3.10", package "distutils" is not deprecated.
# RUN python3 -m pip install setuptools
# RUN python3 -m pip install requests
# RUN python3 -m pip install distutils
# RUN python3 -m pip install --upgrade pip setuptools requests
# RUN python3 -m pip install --user pipx
# RUN python3 -m pipx install poetry

# RUN curl -sSL https://install.python-poetry.org | python3 -

RUN apt update && apt install bash -y

# Add user. Without this, following process is executed as admin. 
RUN groupadd -g ${GID} ${GROUP_NAME} \
    && useradd -ms /bin/sh -u ${UID} -g ${GID} ${USER_NAME}

USER ${USER_NAME}
WORKDIR ${APPLICATION_DIRECTORY}
RUN curl -sSL https://install.python-poetry.org | python3 -
RUN export PATH="/home/${USER_NAME}/.local/bin:$PATH" && poetry completions bash >> ~/.bashrc \
    && poetry config virtualenvs.in-project true \
    && poetry config virtualenvs.path .

RUN echo 'export PATH="/home/'${USER_NAME}'/.local/bin:$PATH"' >> ~/.bashrc
RUN bash -c "source ~/.bashrc"
# RUN poetry config virtualenvs.create false --local
# RUN bash -c "poetry config virtualenvs.in-project true"



