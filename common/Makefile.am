if ENABLE_GTK2
GTK2_SUBDIR = gtk-2.0
endif

if ENABLE_GTK3
GTK3_SUBDIR = gtk-3.0
endif

SUBDIRS = $(GTK2_SUBDIR) $(GTK3_SUBDIR) 

if ENABLE_DARK
themedark_DATA = $(srcdir)/index/dark/index.theme
endif

ithemedir        = $(DESTDIR)$(themedir)
ithemedarkdir    = $(DESTDIR)$(themedarkdir)

install-exec-hook:

install-data-local:

if ENABLE_GNOME_SHELL
	$(MKDIR_P) $(ithemedir)/gnome-shell

if ENABLE_TRANSPARENCY
	$(SASSC) $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/sass/gnome-shell.scss $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION)/gnome-shell.css;
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

endif

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -RL \
		common-assets \
		dark-assets \
		$(ithemedarkdir)/gnome-shell

	cd $(srcdir)/gnome-shell/$(GNOME_SHELL_VERSION) && cp -R \
		gnome-shell-dark.css \
		$(ithemedarkdir)/gnome-shell/gnome-shell.css
endif # ENABLE_DARK

endif # ENABLE_GNOME_SHELL

uninstall-local:
	rm -rf $(ithemedir)

if ENABLE_DARK
	rm -rf $(ithemedarkdir)
endif # ENABLE_DARK

EXTRA_DIST = \
	gnome-shell \
	index 
