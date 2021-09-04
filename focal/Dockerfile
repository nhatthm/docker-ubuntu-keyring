FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive

RUN set -ex \
    # Configure APT to not install the docs
    && echo '\
path-exclude /usr/share/doc/*\n\
path-include=/usr/share/doc/*/copyright\n\
path-exclude /usr/share/man/*\n\
path-exclude /usr/share/groff/*\n\
path-exclude /usr/share/info/*\n\
path-exclude /usr/share/lintian/*\n\
path-exclude /usr/share/linda/*\n\
' > /etc/dpkg/dpkg.cfg.d/01_nodoc \
    && echo '\
APT::Install-Recommends "false";\n\
    ' > /etc/apt/apt.conf.d/99synaptic \
    && apt-get update \
    && apt-get install -y gnome-keyring build-essential ca-certificates tzdata git curl wget \
    # Cleanup
    && apt-get clean \
    && apt-get autoremove \
    && rm -rf \
        /var/lib/apt/lists/* \
        /tmp/* \
        /var/tmp/* \
        /var/cache/apt/archives \
        /usr/share/doc/ \
        /usr/share/man/ \
        /usr/share/info/ \
        /usr/share/groff/ \
        /usr/share/locale/

ENTRYPOINT [ "dbus-run-session", "--", "bash" ]
