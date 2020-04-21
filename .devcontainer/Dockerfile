FROM opensuse/leap:15

LABEL maintainer "Gregor Dschung <gregor@chkpnt.de>"
LABEL description "Build-Environment for rspamd"

RUN zypper addrepo --refresh obs://server:mail/openSUSE_Leap_15.1 server:mail
RUN zypper -n --gpg-auto-import-keys refresh --force

# Install the build requirements based on this spec file:
# https://build.opensuse.org/package/view_file/server:mail/rspamd/rspamd.spec
RUN zypper -n source-install --build-deps-only rspamd

# Additional dependencies:
# - for -DENABLE_LIBUNWIND=ON
RUN zypper -n install libunwind-devel
# - for lua
RUN zypper -n install lua51-devel lua51-luarocks
RUN luarocks install luacheck

# Needed for the installation of VS Code Server and the Devcontainer
RUN zypper -n install tar gzip git

# Debugger
RUN zypper -n install gdb