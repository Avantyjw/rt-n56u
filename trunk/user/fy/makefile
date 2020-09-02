THISDIR = $(shell pwd)
export GO111MODULE=on
export GOPROXY=https://goproxy.io
fy_URL := https://github.com/dextercai/feeyo-adsb-golang/archive/v1.2.tar.gz

all:download_fy build_extract build

build_extract:
	mkdir -p $(THISDIR)/fy
	mkdir -p $(THISDIR)/bin
	( if [ ! -d $(THISDIR)icG/fy/feeyo-adsb-golang-v1.2 ]; then \
	tar zxfv $(THISDIR)/feeyo-adsb-golang-v1.2).tar.gz -C $(THISDIR)/fy ; \
	fi )

build:
	( cd $(THISDIR)/fy/feeyo-adsb-golang-v1.2; \
	GOOS=linux GOARCH=mipsle go build -ldflags "-w -s" -o $(THISDIR)/bin/fy; \
	) 

download_fy:
	( if [ ! -f $(THISDIR)/feeyo-adsb-golang-v1.2.tar.gz ]; then \
	curl --create-dirs -L $(fy_URL) -o $(THISDIR)/feeyo-adsb-golang-v1.2.tar.gz ; \
	fi )

clean:
	rm -rf $(THISDIR)/fy
	rm -rf $(THISDIR)/bin

romfs:
	$(ROMFSINST) $(THISDIR)/bin/ /usr/bin/
	$(ROMFSINST) -p +x $(THISDIR)/bin/fy /usr/bin/fy
