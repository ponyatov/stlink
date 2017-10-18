Some hot fixes for:
[![GitHub release](https://img.shields.io/github/release/texane/stlink.svg)](https://github.com/texane/stlink/releases/1.4.0)

- [x] [issue 645](https://github.com/texane/stlink/issues/645): add CMAKE_ABSOLUTE_PREFIX
- [ ] [issue 646](https://github.com/texane/stlink/issues/646): build and run without root access

Use this Makefile snippet:
```
CWD = $(CURDIR)
TMP = $(CWD)/tmp
TOOL = $(CWD)/tools

STLINK_TAG = 1.4.0
STLINK_GITHUB = git@github.com:ponyatov/stlink.git
STLINK_BRANCH = ponyatov_140

.PHONY: stlink
stlink: $(TOOL)/bin/st-util
$(TOOL)/bin/st-util: stlink/README_ponyatov.md
	cd stlink ; $(MAKE) clean ; $(MAKE) \
		DESTDIR=$(TMP) CMAKEFLAGS="-DCMAKE_INSTALL_PREFIX=/stlink" \
		install &&\
	cp -r $(TMP)/stlink/* $(TOOL)/
stlink/README_ponyatov.md: stlink/README.md
	cd stlink ; git checkout $(STLINK_BRANCH)
stlink/README.md:
	git clone -o gh $(STLINK_GITHUB)

``` 
