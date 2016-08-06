# Overview

1. Source (don't run) `start-docker-osx.sh` - this will create a VM (if
needed) named `mlcaffe`, and set it up.
2. `cd docker`
3. `docker build -t caffe:cpu standalone/cpu`

Or, if you want to push to DockerHub,

    docker build -t <username>/caffe:cpu standalone/cpu

Then, create a repository on DockerHub and 

    docker push <username>/caffe:cpu

Check `docker images` to see if everything built. Check the Caffe install with:

    docker run -ti caffe:cpu caffe --version

Also, these work to run Python scripts or get an interpreter

    docker run -ti caffe:cpu python
    docker run -ti caffe:cpu ipython

Note that `pwd` in interactive Python will resolve to `/workspace`, in the 
container. To run a script on the host machine, use commands like:

    $ more test.py
    import caffe
    print 'mellow, whirled'
    $ docker run -ti --volume=$(pwd):/workspace caffe:cpu python test.py
    libdc1394 error: Failed to initialize libdc1394
    /usr/local/lib/python2.7/dist-packages/matplotlib/font_manager.py:273: UserWarning: Matplotlib is building the font cache using fc-list. This may take a moment.
      warnings.warn('Matplotlib is building the font cache using fc-list. This may take a moment.')
    mellow, whirled

Other usage flags are available at:

    https://github.com/BVLC/caffe/tree/master/docker

## More

To stop Docker, use `docker-machine stop mlcaffe`.
