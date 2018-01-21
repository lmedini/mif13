#HELP:
#HELP: make xxx.html
#HELP:    produit la présentation au format HTML
#HELP:
#HELP: make [all]
#HELP:    convertit tous les fichiers
#HELP:
#HELP: requiert markdown-to-slides: https://www.npmjs.com/package/markdown-to-slides
#HELP: npm install markdown-to-slides -g
#HELP:


SOURCES=$(shell ls *.md)
PRESENTATIONS=$(patsubst %.md,%.html,$(SOURCES))

all: $(PRESENTATIONS)

help:
	sed -n -e 's/^\#HELP:\(.*\)$$/\1/p' < Makefile


.PHONY: all help

%.html: %.md
	markdown-to-slides $*.md -o $*.html -i 
