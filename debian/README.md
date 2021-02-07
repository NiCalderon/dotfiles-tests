Build:
docker build --build-arg FORCE_REBUILD=`date +%s` -t dotfiles-tests .

Run:
docker run -it dotfiles-tests
