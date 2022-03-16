FROM golang:1.17

# Configure to avoid redundant error "debconf: delaying package configuration, since apt-utils is not installed".
# See https://code.visualstudio.com/docs/remote/containers-advanced#_debconf-delaying-package-configuration-since-aptutils-is-not-installed.
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get -y install --no-install-recommends apt-utils

# Verify git, process tools, lsb-release (common in install instructions for CLIs) installed.
RUN apt-get -y install git iproute2 procps lsb-release

# Install essential tools for Go development.
RUN go get \
	github.com/ramya-rao-a/go-outline@latest \
	github.com/cweill/gotests/gotests@latest \
 	github.com/fatih/gomodifytags@latest \
 	github.com/josharian/impl@latest \
 	github.com/haya14busa/goplay/cmd/goplay@latest \
 	github.com/go-delve/delve/cmd/dlv@latest \
	honnef.co/go/tools/cmd/staticcheck@latest\
	golang.org/x/tools/gopls@latest

# Clean up.
RUN apt-get autoremove -y && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Revert workaround of avoiding redundant error "debconf: delaying package configuration, since apt-utils is not installed".
# See https://code.visualstudio.com/docs/remote/containers-advanced#_debconf-delaying-package-configuration-since-aptutils-is-not-installed.
ENV DEBIAN_FRONTEND=dialog

# Expose service ports.
EXPOSE 8000