ALL: docker-build


# get image tag from git submodule under ./sigmoni 
DOCKER_IMAGE=haliliceylanua/sigmoni:$(shell git -C sigmoni describe --tags --always)

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t $(DOCKER_IMAGE) .

docker-push:
	docker tag $(DOCKER_IMAGE) haliliceylanua/sigmoni:latest
	docker push $(DOCKER_IMAGE)
	docker push haliliceylanua/sigmoni:latest