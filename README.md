[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/craftignite/mc-server-runner)](https://github.com/craftignite/mc-server-runner/releases/latest)
[![CircleCI](https://img.shields.io/circleci/build/github/craftignite/mc-server-runner)](https://app.circleci.com/pipelines/github/craftignite/mc-server-runner/)

This is a modified version of the Minecraft server process wrapper used by 
[the itzg/minecraft-server Docker image](https://hub.docker.com/r/itzg/minecraft-server/). It is modified to work with [the craftignite auto-start-stop Minecraft server](https://github.com/craftignite/).
It is designed to handle some startup tasks as well as ensure the Minecraft server is stopped gracefully when the container is sent the `TERM` signal.

## Usage

> Available at any time using `-h`

```
  -bootstrap string
    	Specifies a file with commands to initially send to the server
  -cf-instance-file string
    	Path to a Twitch/Curse minecraftinstance.json file for server setup
  -debug
    	Enable debug logging
  -detach-stdin
    	Don't forward stdin and allow process to be put in background
  -shell string
    	When set, pass the arguments to this shell
  -stop-duration duration
    	Amount of time in Golang duration to wait after sending the 'stop' command.
```

## Development Testing

Start a golang container for building and execution:

```bash
docker run -it --rm \
  -v ${PWD}:/build \
  -w /build \
  circleci/golang:1.12
```

Within that container, build/test by running:

```bash
go run main.go test/dump.sh
go run main.go test/bash-only.sh
# The following should fail
go run main.go --shell sh test/bash-only.sh
```