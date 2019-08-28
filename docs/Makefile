# Minimal makefile for Sphinx documentation
#
# Put it first so that "make" without argument is like "make help".
help:
	@python3 -msphinx -M help "workbook" "workbook/_build"

.PHONY: help Makefile

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
%: Makefile
	@echo "\n--- Building Workbook ---"
	@python3 -msphinx -M $@ "workbook" "workbook/_build"
