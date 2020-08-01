VPATH =

targets := $(shell cat $(srcdir)/assets.txt)
dark := $(patsubst %,dark/assets/%.png,$(targets))

mbt_entry := $(filter entry-%toolbar,$(targets))
mbt_menubar := $(filter menubar%,$(targets))
mbt_button := $(filter button%,$(targets))

mbt_dark := \
	$(srcdir)/menubar-toolbar/menubar-toolbar-dark.rc \
	$(patsubst %,menubar-toolbar/%-dark.png,$(mbt_entry) $(mbt_menubar)) \
	$(patsubst %,menubar-toolbar/%.png,$(mbt_button))

rc := apps main panel xfce-notify
srcrc := $(patsubst %,$(srcdir)/%.rc,$(rc))

dark: $(dark)
mbt_dark: $(mbt_dark)

dark/assets menubar-toolbar:
	$(MKDIR_P) "$@"/

clean:
	rm -rf dark/assets/ menubar-toolbar/*.png

$(dark): $(srcdir)/dark/assets.svg | dark/assets

$(dark):
if INKSCAPE_1_0_OR_NEWER
	$(INKSCAPE) --export-id-only --export-filename="$@" --export-id="$(basename $(notdir $@))" --export-dpi=96 "$<" >/dev/null
else !INKSCAPE_1_0_OR_NEWER
	$(INKSCAPE) --export-id-only --export-png="$@" --export-id="$(basename $(notdir $@))" --export-dpi=96 "$<" >/dev/null
endif
if OPTIPNG
	$(OPTIPNG) -o7 --quiet "$@"
endif

menubar-toolbar/%-dark.png: dark/assets/%.png | menubar-toolbar
	cp "$<" "$@"

.PHONY: dark mbt_dark clean

if ENABLE_DARK
gtk2themedarkdir = $(themedarkdir)/gtk-2.0
gtk2themedarkassetsdir = $(gtk2themedarkdir)/assets
gtk2themedark_DATA = $(srcrc) $(srcdir)/dark/gtkrc
gtk2themedarkassets_DATA = $(dark)
nobase_gtk2themedark_DATA = $(mbt_dark)
endif

EXTRA_DIST = \
	assets.txt \
	$(srcrc) \
	$(patsubst %,%/assets.svg,light dark) \
	$(patsubst %,%/gtkrc,light darker dark lighter) \
	$(patsubst %,menubar-toolbar/menubar-toolbar%,.rc -dark.rc)

