TARGET_SYM := /usr/share/X11/xkb/symbols/us
SOURCE_SYM := usr-share-X11-xkb-symbols-us
TARGET_RULE := /usr/share/X11/xkb/rules/evdev.xml
SOURCE_RULE := usr-share-X11-xkb-rules-evdev

all: reinstall

install: $(SOURCE_SYM) $(TARGET_SYM) $(SOURCE_RULE) $(TARGET_RULE)
	echo '//EVI//BEGIN' >> $(TARGET_SYM)
	cat $(SOURCE_SYM) >> $(TARGET_SYM)
	echo '//EVI//END' >> $(TARGET_SYM)
	sed -i "$$(awk '/variantList/ {print NR; exit}' $(TARGET_RULE)) r $(SOURCE_RULE)" $(TARGET_RULE)

uninstall: $(TARGET_SYM) $(TARGET_RULE)
	sed -i '/^\/\/EVI\/\/BEGIN$$/,/^\/\/EVI\/\/END$$/d' $(TARGET_SYM)
	sed -i '/EVI BEGIN/,/EVI END/d' $(TARGET_RULE)

reinstall:
	$(MAKE) uninstall
	$(MAKE) install

.PHONY: all install uninstall reinstall
