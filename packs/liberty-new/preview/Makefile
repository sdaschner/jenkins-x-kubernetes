OS := $(shell uname)
DB_VERSION := $(shell cat ../../DB_VERSION)

preview: 
ifeq ($(OS),Linux)
	sed -i -e "s/version:.*/version: $(PREVIEW_VERSION)/" Chart.yaml
	sed -i -e "s/version:.*/version: $(PREVIEW_VERSION)/" ../*/Chart.yaml
	sed -i -e "s|repository:.*|repository: $(DOCKER_REGISTRY)\/REPLACE_ME_DOCKER_REGISTRY_ORG\/REPLACE_ME_APP_NAME|" values.yaml
	sed -i -e "s/tag:.*/tag: $(PREVIEW_VERSION)/" values.yaml
	sed -i -e "s|dbRepository:.*|dbRepository: $(DOCKER_REGISTRY)\/REPLACE_ME_DOCKER_REGISTRY_ORG\/REPLACE_ME_APP_NAME-db-migration|" values.yaml
	sed -i -e "s/dbTag:.*/dbTag: $(DB_VERSION)/" values.yaml
else
	echo "platfrom $(OS) not supported to release from"
	exit -1
endif
	echo "  version: $(PREVIEW_VERSION)" >> requirements.yaml
	jx step helm build
