Some specific builds:

The `cpu_grl_0.1` tag is for the `grad_rev_layer_gnp2017april` branch, commit
hash ed18030

    docker build -t gnperdue/caffe:cpu_grl_0.1 standalone/cpu_grl
    docker push gnperdue/caffe:cpu_grl_0.1

Test:

    docker$ docker run -ti --volume=$(pwd):/workspace gnperdue/caffe:cpu_grl_0.1 python test.py
    libdc1394 error: Failed to initialize libdc1394
    mellow, whirled

The `gpu_grl_0.1` tag is for the `grad_rev_layer_gnp2017april` branch, commit
hash ed18030

    docker build -t gnperdue/caffe:gpu_grl_0.1 standalone/gpu_grl
    docker push gnperdue/caffe:gpu_grl_0.1

The `cpu_grl` tag is for Sohini's `patch-2` version of Caffe (gradient reversal
layer is implemented, etc.)

The `gpu_grl` tag is for Sohini's `patch-2` version of Caffe (gradient reversal
layer is implemented, etc.) with the `gpu` support turned on.

    docker$ docker build -t gnperdue/caffe:gpu_grl standalone/gpu_grl
    docker$ docker push gnperdue/caffe:gpu_grl


