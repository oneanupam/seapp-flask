# Example App
This repository contains Example App written in python programming language using flask framework of web development.

## Prerequisites
Below prerequisites must be fulfilled for successful execution of code.

### Software Requirements

Install the required tools before contributing to this project:

- [Python 3](https://www.python.org/downloads/) >= 3.14.6
- [pip](https://pypi.org/project/pip/) >= 26.1.2
- [pre-commit](https://pre-commit.com/) >= 4.2.0

```bash
python -m pip install --upgrade pip
```

> [!NOTE]
> To confirm your environment, run `python3 --version` or `python --version`, and `pip3 --version` or `pip --version`. See the [Python download page](https://www.python.org/downloads/) for installation instructions.

### Set Up a Virtual Environment

It is recommended to create an isolated virtual environment for this project to avoid dependency conflicts with other Python projects.

```bash
# Linux / macOS
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Windows
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

> [!NOTE]
> Activating the virtual environment updates your shell PATH so `python` and `pip` point to the environment for the current session. To leave the environment, run `deactivate`.

## Run and Test the App on Local Machine
Flask has the built-in Werkzeug server. To start the default dev web server of the app, execute the below command -

```bash
# To start the default dev web server of the app
python python/run.py
```

To start the production grade wsgi gunicorn server, execute the below command -

```bash
gunicorn main:app
gunicorn --bind :9090 --workers 1 --threads 8 main:app

# Where:
# gunicorn -> Runs the Gunicorn WSGI server
# --bind :9090 -> Bind to all network interfaces (0.0.0.0) on port 9090
# --workers -> 1	Start 1 worker process
# --threads -> 8	Each worker can run 8 threads concurrently
# main:app -> main is the Python file name (i.e., main.py), and app is the Flask app object inside it
```

To check the webapp, open a browser and hit the below URL -

``` bash
http://<IP>:Port
http://127.0.0.1:4999/
```

## Run and Test the App on Docker
1. Clone the repository and switch inside the directory.
2. Build the docker image using one of below command:

```bash
docker build -t eapp:latest .
docker build -t eapp:latest -f Dockerfile.dev .
```

3. To run the docker container from built image in the background with port mapping, use one of below command:

```bash
# To explicitly specify the what port to map in the form, <host_port>:<container_port>
    # with --rm flag, Docker will automatically remove the container after the container exits.
docker run -d -p 5000:4999 --name eapp-container eapp:latest

# To map the exposed port (via EXPOSE) to random ports on the host machine
docker run -d -P --name eapp-container eapp:latest
```

4. To test the app on host machine, open the browser or use curl command:
```bash
    curl http://localhost:5000
```

> [!NOTE]
> ( . ) tells about the build context. The build context is the current directory (.), which should contain your application code and the Dockerfile. Pass the Dockerfile, if its name is not exactly Dockerfile.
>
> Port mapping is used to access the services running inside a Docker container. In the above case, we can now access the application using port 5000 on the host machine.

## Run pre-commit
This repository already includes a `.pre-commit-config.yaml`. Run the following commands to install the hooks locally:

```bash
python -m pip install pre-commit
pre-commit install
pre-commit validate-config
```

This installs the hook into `.git/hooks/pre-commit`. Once installed, pre-commit runs automatically when you commit changes. By default, it checks only the files included in the commit.

To run all hooks manually, use:

```bash
pre-commit run --all-files
pre-commit run <hook_id>
```

## Contributing

Contributions and suggestions are welcome. Before opening an issue or pull request:

1. Review the [contribution guidelines](CONTRIBUTING.md).
2. Install the pre-commit hooks and run them against your changes.
3. Open an issue for bugs or ideas, or submit a pull request with a clear description of the change.

## License

This project is licensed under the [MIT License](LICENSE).

## References
- https://www.warp.dev/terminus/docker-logs-tail
- https://www.warp.dev/terminus/docker-expose-port
- https://www.warp.dev/terminus/docker-exec-container
- https://www.warp.dev/terminus/docker-start-container
