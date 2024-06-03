ALL: docker-build

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t haliliceylanua/rawalign .