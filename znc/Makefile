build:
	docker build --rm --no-cache -t zenithar/znc .

debug:
	docker run -p :6697:6697 -v /srv/znc:/opt/znc/state -i -t zenithar/znc bash

start:
	docker run -p :6697:6697 -v /srv/znc:/opt/znc/state -t zenithar/znc
