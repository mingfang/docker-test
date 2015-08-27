# docker-test
Test Docker 1.8 build problem with Boot2Docker when building in a directory that is NOT under "home", e.g. in /tmp.

My setup

```
>uname -a
Darwin mfang-lv.local 15.0.0 Darwin Kernel Version 15.0.0: Mon Aug 10 17:09:09 PDT 2015; root:xnu-3247.1.99~3/RELEASE_X86_64 x86_64

>boot2docker version
Boot2Docker-cli version: v1.8.0
Git commit: 9a26066

>docker version
Client:
 Version:      1.8.1
 API version:  1.20
 Go version:   go1.4.2
 Git commit:   d12ea79
 Built:        Thu Aug 13 02:49:29 UTC 2015
 OS/Arch:      darwin/amd64

Server:
 Version:      1.8.1
 API version:  1.20
 Go version:   go1.4.2
 Git commit:   d12ea79
 Built:        Thu Aug 13 02:49:29 UTC 2015
 OS/Arch:      linux/amd64
```

To see the problem;

1-clone this repo from ```/tmp``` or anywhere NOT under "home".

2-cd into ```docker-test```

3-run ```docker build -f docker/Dockerfile -t test .```

I get this error 
```
unable to prepare context: The Dockerfile (/tmp/docker/Dockerfile) must be within the build context (.)
```

4-Now cd into ```docker``` sub directory and run ```docker build -t test .```, it works.

5-Note, inside the docker directory, ```docker build -f ./Dockerfile -t test .``` also fails.

6-Finally, full path fails for me also.

```
>docker build -f `pwd`/Dockerfile -t test `pwd`
unable to prepare context: The Dockerfile (/tmp/Dockerfile) must be within the build context (/tmp)
```

