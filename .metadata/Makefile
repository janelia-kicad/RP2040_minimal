# This file is generated automatically from .metadata.org
# File edits may be overwritten!

MAKEFILE_PATH := $(abspath $(lastword $(MAKEFILE_LIST)))
MAKEFILE_DIR := $(notdir $(patsubst %/,%,$(dir $(MAKEFILE_PATH))))
MAKEFILE_DIR_ABS := $(dir $(MAKEFILE_PATH))
KICAD_CONFIG_HOME := $(MAKEFILE_DIR_ABS).config/kicad/
GUIX-TIME-MACHINE = guix time-machine -C $(MAKEFILE_DIR)/guix/channels.scm
GUIX-SHELL = $(GUIX-TIME-MACHINE) -- shell -m $(MAKEFILE_DIR)/guix/manifest.scm
CONTAINER = --container -F -E "^DISPLAY$$" -E "^XAUTHORITY$$" --expose="$$XAUTHORITY" --expose=/tmp/.X11-unix/ --expose=$$HOME/.Xauthority --expose=/etc/machine-id
GUIX-CONTAINER = $(GUIX-SHELL) $(CONTAINER)

.PHONY: metadata-edits
metadata-edits:
	$(GUIX-CONTAINER) -- sh -c "emacs -q --no-site-file --no-site-lisp --no-splash -l $(MAKEFILE_DIR)/emacs/init.el --file $(MAKEFILE_DIR)/metadata.org"

.PHONY: metadata
metadata:
	$(GUIX-CONTAINER) -- sh -c "emacs --batch -Q  -l $(MAKEFILE_DIR)/emacs/init.el --eval '(process-org \"$(MAKEFILE_DIR)/metadata.org\")'"

.PHONY: guix-shell
guix-shell:
	$(GUIX-SHELL)

.PHONY: guix-container
guix-container:
	$(GUIX-CONTAINER)

.PHONY: ipython-shell
ipython-shell:
	$(GUIX-CONTAINER) -- ipython

.PHONY: kicad-edits
kicad-edits:
	# $(GUIX-CONTAINER) -S /home/$(USER)/.config/kicad/7.0=$(MAKEFILE_DIR)/.config/kicad/7.0 -- kicad
	# $(GUIX-SHELL) -- kicad
	KICAD_CONFIG_HOME=$(KICAD_CONFIG_HOME) $(GUIX-SHELL) -E "^KICAD_CONFIG_HOME" -- kicad

.PHONY: freecad-edits
freecad-edits:
	$(GUIX-SHELL) -- FreeCAD

.PHONY: filter-edits
filter-edits:
	$(GUIX-SHELL) -- sh -c "dosbox documentation/filter/FILTER42.exe"

.PHONY: skip-worktree-config
skip-worktree-config:
	git ls-files -z .metadata/.config/ | xargs -0 git update-index --skip-worktree

.PHONY: no-skip-worktree-config
no-skip-worktree-config:
	git ls-files -z .metadata/.config/ | xargs -0 git update-index --no-skip-worktree

.PHONY: ls-files-config
ls-files-config:
	git ls-files .metadata/.config/ -v

.PHONY: cropped
cropped:
	# $(GUIX-SHELL) -- inkscape -D --export-overwrite --export-plain-svg documentation/pcb/*.svg
	inkscape -D --export-overwrite --export-plain-svg documentation/pcb/*.svg

.PHONY: trimmed-images
trimmed-images:
	mogrify -trim documentation/pcb/*.png

.PHONY: zipped-gerbers
zipped-gerbers:
	$(GUIX-SHELL) -- sh -c "rm -f documentation/gerbers/*.zip && zip -j -r documentation/gerbers/RP2040_minimal-1.0.zip documentation/gerbers"
