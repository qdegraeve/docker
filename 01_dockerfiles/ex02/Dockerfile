FROM gogs/gogs

RUN apk update \
	&& apk --no-cache --no-progress add postgres postgresql-9.3 postgresql-client-9.3 git \
	&& rm -rf /var/cache/apk/*

