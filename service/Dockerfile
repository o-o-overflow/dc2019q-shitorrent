from ubuntu:18.04
run echo "travis_fold:start:Dapt\033[33;1mservice Dockerfile apt\033[0m" && \
    apt-get -y update && apt-get -y install clang python3 xinetd && \
    echo "\ntravis_fold:end:Dapt\r"
# python3-pip, etc.

copy src/config.py /
copy shitorrent /shitorrent
# Currently anything that goes in public files must be pre-built and checked in git
# Can still build other things locally though
#run clang -std=gnu99 -o /service /service.c \
#    && rm /service.c \
#    && apt-get -y purge clang \
#    && apt-get -y autoremove

# Or, include the flag file in the repository
run touch /flag && chmod 644 /flag && echo "OOO{i did not read the fd_set manpage}" > /flag

copy service.conf /service.conf
copy wrapper /wrapper
copy banner_fail /

expose 5000
cmd ["/usr/sbin/xinetd", "-filelog", "-", "-dontfork", "-f", "/service.conf"]
