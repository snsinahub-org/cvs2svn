# cvs2svn has some dependencies that are no longer widely available
# (e.g., Python 2.x and an oldish version of the Subversion library).
# This Dockerfile builds images that can be used to run or test
# cvs2svn. Note that it is based on debian:jessie, which is pretty
# old. But this is the most recent version of Debian where the
# required dependencies are easily available. One way to use this is
# to run
#
#     make docker-image
#
# to make an image for running cvs2svn, or
#
#     make docker-test
#
# to make an image for testing cvs2svn and to run those tests using
# the image.

FROM python:2.7 AS run

RUN cat /etc/apt/sources.list
RUN apt-get update && \
    apt-get install -y \
        python \
        python-bsddb3 \
        subversion \
        rcs \
        cvs \
        vim

RUN mkdir /src
WORKDIR /src
RUN cd ..
COPY . .
RUN ls -l
RUN ${PYTHON} ./setup.py install
# RUN python ./run_tests.py



# The CVS repository can be mounted here:
VOLUME ["/cvs"]

# A volume for storing temporary files can be mounted here:
VOLUME ["/tmp"]
RUN ln -s /tmp cvs2svn-tmp
RUN ${PYTHON} ./run-tests.py
# CMD ["python", "./run_tests.py"]
# ENTRYPOINT ["./run-tests.py"]





