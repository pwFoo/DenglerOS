ARG	BASE_IMAGE=$BASE_IMAGE
FROM	$BASE_IMAGE AS rootfs

RUN	apk --update --no-cache upgrade 

RUN	apk --update --no-cache add \
	busybox-static

WORKDIR	/rootfs

RUN	mkdir -p \
	run/resolvconf \
	etc/unitfiles \
	lib/firmware \
	lib/modules \
	var/log \
	var/lib \
	proc \
#	root \
	etc \
#	mnt \
	dev \
	sys \
	run \
	tmp \
	bin

RUN	ln -s ../tmp var/tmp
RUN	ln -s ../run var/run
RUN	ln -s bin sbin	

RUN	 cp -a /bin/busybox.static bin/busybox

RUN	chroot /rootfs /bin/busybox --install -s /bin

RUN	chroot /rootfs ln -s /bin/busybox /init

RUN	echo "nameserver 8.8.8.8" > run/resolvconf/resolv.conf

COPY	files/ /rootfs/



FROM	scratch

COPY	--from=rootfs /rootfs/ /
