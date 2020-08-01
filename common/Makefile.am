if ENABLE_GTK2
GTK2_SUBDIR = gtk-2.0
endif

if ENABLE_GTK3
GTK3_SUBDIR = gtk-3.0
endif

SUBDIRS = $(GTK2_SUBDIR) $(GTK3_SUBDIR) 

if ENABLE_LIGHT
theme_DATA = $(srcdir)/index/light/index.theme
endif

if ENABLE_DARKER
themedarker_DATA = $(srcdir)/index/darker/index.theme
endif

if ENABLE_DARK
themedark_DATA = $(srcdir)/index/dark/index.theme
endif

if ENABLE_LIGHTER
themelighter_DATA = $(srcdir)/index/lighter/index.theme
endif


ithemedir        = $(DESTDIR)$(themedir)
ithemedarkerdir  = $(DESTDIR)$(themedarkerdir)
ithemedarkdir    = $(DESTDIR)$(themedarkdir)
ithemelighterdir = $(DESTDIR)$(themelighterdir)

install-exec-hook:

install-data-local:

if ENABLE_GNOME_SHELL
	$(MKDIR_P) $(ithemedir)/gnome-shell

if ENABLE_TRANSPARENCY

	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell.css;

else !ENABLE_TRANSPARENCY

	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell-solid.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell.css;

endif

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -RL \
		common-assets \
		light-assets \
		gnome-shell.css \
		$(ithemedir)/gnome-shell

if ENABLE_DARK
	$(MKDIR_P) $(ithemedarkdir)/gnome-shell

if ENABLE_TRANSPARENCY

	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell-dark.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell-dark.css;

else !ENABLE_TRANSPARENCY

	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell-solid-dark.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell-dark.css;

endif

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -RL \
		common-assets \
		dark-assets \
		$(ithemedarkdir)/gnome-shell

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -R \
		gnome-shell-dark.css \
		$(ithemedarkdir)/gnome-shell/gnome-shell.css
endif # ENABLE_DARK

if GNOME_SHELL_3_32_OR_NEWER
if ENABLE_LIGHTER
	$(MKDIR_P) $(ithemelighterdir)/gnome-shell

if ENABLE_TRANSPARENCY

	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell-lighter.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell-lighter.css;

else !ENABLE_TRANSPARENCY

	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell-solid-lighter.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell-lighter.css;

endif

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -RL \
		common-assets \
		lighter-assets \
		$(ithemelighterdir)/gnome-shell

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -R \
		gnome-shell-lighter.css \
		$(ithemelighterdir)/gnome-shell/gnome-shell.css
endif # ENABLE_LIGHTER
endif # GNOME_SHELL_3_32_OR_NEWER

endif # ENABLE_GNOME_SHELL


uninstall-local:
	rm -rf $(ithemedir)

if ENABLE_DARKER
	rm -rf $(ithemedarkerdir)
endif # ENABLE_DARKER

if ENABLE_DARK
	rm -rf $(ithemedarkdir)
endif # ENABLE_DARK

if ENABLE_LIGHTER
	rm -rf $(ithemelighterdir)
endif # ENABLE_LIGHTER


EXTRA_DIST = \
	gnome-shell \
	index 
