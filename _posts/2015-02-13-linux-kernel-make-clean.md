---
layout: post
category : linux
tags : [kernel, make, driver]
---

## Difference of make clean/mrproper/distclean

Run make help in linux kernel direcroty, can get

	# make help
	Cleaning targets:
	clean       - Remove most generated files but keep the config and enough build support to build external modules
	mrproper    - Remove all generated files + config + various backup files
	distclean   - mrproper + remove editor backup and patch files

So,
- for removed files, clean < mrproper < distclean
- if want to build external modules, then run make clean, and remove all the source (*.S, *.c) files.

See kernel's Makefile for more details.

	clean: archclean $(clean-dirs)
		$(call cmd,rmdirs)
		$(call cmd,rmfiles)
		@find . $(RCS_FIND_IGNORE) \
		[Math Processing Error] \
		-type f -print | xargs rm -f

	mrproper: clean archmrproper $(mrproper-dirs)
		$(call cmd,rmdirs)
		$(call cmd,rmfiles)

	distclean: mrproper
		@find $(srctree) $(RCS_FIND_IGNORE) \
		[Math Processing Error] \
		-type f -print | xargs rm -f
