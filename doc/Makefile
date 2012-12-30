.PHONY:    default clean tarball

core =	amount animation antiban autocolor bank bitmaps chat \
		color flag gametab globals globalstats inventory \
		login mapwalk math mouse object players timing symbol \
		text worldswitcher

skill =	 magic

misc =  paintsmart SmartParams online

all:
	@python docgen.py `echo $(core) | sed -r \
		's/(\w+)/..\/SRL\/core\/\1.simba/g'` > /dev/null
	@python docgen.py `echo $(skill) | sed -r \
		's/(\w+)/..\/SRL\/skill\/\1.simba/g'` > /dev/null
	@python docgen.py `echo $(misc) | sed -r \
		's/(\w+)/..\/SRL\/misc\/\1.simba/g'` > /dev/null
	@make -C sphinx/ html

clean:
	@rm -f `echo $(core) | sed -r 's/(\w+)/sphinx\/\1.rst/g'`
	@make -C sphinx/ clean

tarball:
	@$(MAKE) all
	@tar cjf doc.tar.bz2 -C sphinx/_build/ html
