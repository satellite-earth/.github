setup: clone switch-branch install build

clone:
	if [ ! -d "core" ]; then git clone git@github.com:satellite-earth/core.git; fi
	if [ ! -d "web-ui" ]; then git clone git@github.com:satellite-earth/web-ui.git; fi
	if [ ! -d "personal-node" ]; then git clone git@github.com:satellite-earth/personal-node.git; fi

switch-branch:
	cd core && git checkout dev
	cd web-ui && git checkout dev
	cd personal-node && git checkout dev

setup-workspace:
	echo '{ "name": "satellite", "private": true, "workspaces": [ "core", "web-ui", "personal-node" ] }' > package.json

install: setup-workspace
	yarn install

update-make:
	wget https://raw.githubusercontent.com/satellite-earth/.github/master/tools/dev/personal-node/Makefile -O Makefile

update: switch-branch
	cd core && git pull
	cd personal-node && git pull
	cd web-ui && git pull

build:
	cd core && build
	cd web-ui && build
	cd personal-node && build
