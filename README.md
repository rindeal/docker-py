# Docker SDK for Python

[![Build Status](https://travis-ci.org/docker/docker-py.svg?branch=master)](https://travis-ci.org/docker/docker-py)

**Warning:** This readme is for the development version of docker-py, which is significantly different to the stable version. [Documentation for the stable version is here.](https://docker-py.readthedocs.io/)

A Python library for the Docker API. It lets you do anything the `docker` command does, but from within Python apps – run containers, manage containers, manage Swarms, etc.

## Installation

The latest stable version [is available on PyPi](https://pypi.python.org/pypi/docker/). Either add `docker` to your `requirements.txt` file or install with pip:

    pip install docker-py

## Usage

Connect to Docker using the default socket or the configuration in your environment:

```python
import docker
client = docker.from_env()
```

You can run containers:

```python
>>> client.containers.run("ubuntu", "echo hello world")
'hello world\n'
```

You can run containers in the background:

```python
>>> client.containers.run("bfirsh/reticulate-splines", detach=True)
<Container '45e6d2de7c54'>
```

You can manage containers:

```python
>>> client.containers.list()
[<Container '45e6d2de7c54'>, <Container 'db18e4f20eaa'>, ...]

>>> container = client.containers.get('45e6d2de7c54')

>>> container.attrs['Config']['Image']
"bfirsh/reticulate-splines"

>>> container.logs()
"Reticulating spline 1...\n"

>>> container.stop()
```

You can stream logs:

```python
>>> for line in container.logs(stream=True):
...   print line.strip()
Reticulating spline 2...
Reticulating spline 3...
...
```

You can manage images:

```python
>>> client.images.pull('nginx')
<Image 'nginx'>

>>> client.images.list()
[<Image 'ubuntu'>, <Image 'nginx'>, ...]
```

[Read the full documentation](https://docker-py.readthedocs.io) to see everything you can do.
