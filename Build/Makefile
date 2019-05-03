# Farben/ Textformatierung
BACKGR=`tput setaf 0`
GREEN=`tput setaf 10`
GREENB=`tput setab 10`
BOLD=`tput bold`
RESET=`tput sgr0`

all: Vortrag.pdf

build:
	@mkdir -p build

clean:
		@rm -rf build
		@echo ${GREEN}${BOLD}Removing build folder${RESET}



.DELETE_ON_ERROR:
Vortrag.pdf: Vortrag.tex lit.bib |build
	@TEXINPUTS="$(call translate,build:)" lualatex \
	  --output-directory=build \
	  --interaction=nonstopmode \
	  --halt-on-error \
	Vortrag.tex|grep -B 12 -e'no output PDF file produced' -e'LuaTeX' --color=auto
	@echo
	@lualatex \
	  --output-directory=build \
	  --interaction=nonstopmode \
	  --halt-on-error \
	Vortrag.tex>/dev/null
	@echo
	@BIBINPUTS=build: biber build/Vortrag.bcf|grep -i -e'biber' -e'error' -e'errors' -e'warn' -e'warnings' --color=auto
	@echo
	@lualatex \
	  --output-directory=build \
	  --interaction=nonstopmode \
	  --halt-on-error \
	Vortrag.tex|grep  -e'reference' -e'LuaTeX' --color=auto
	@mv build/Vortrag.pdf Vortrag.pdf
	@make clean
	@echo ${GREENB}${BACKGR}Success!${RESET}
