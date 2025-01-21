ALL: docker-build


# The Docker image tag combines the submodule's commit SHA and the latest commit SHA 
# relevant to the folder containing the Dockerfile. This ensures:
# 1. Changes in the parent repository only rebuild the image if they affect the Dockerfile's folder.
# 2. Submodule changes are always reflected in the tag.
# 3. Image tags are precise and avoid unnecessary rebuilds due to unrelated changes in the parent repository.

DOCKER_IMAGE=haliliceylanua/rawalign:$(shell git -C RawAlign describe --tags --always)-$(shell git log -1 --format=%h .)

git-submodule-init-recursive:
	git submodule update --init --recursive

docker-build: git-submodule-init-recursive
	docker build -t $(DOCKER_IMAGE) .

docker-push:
	docker tag $(DOCKER_IMAGE) haliliceylanua/rawalign:latest
	docker push $(DOCKER_IMAGE)
	docker push haliliceylanua/rawalign:latest