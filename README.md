# How Singularity Container works on Kepler server?

Here's an illustration of Singularity containers for multiple students, each with their preferred OS, software, and packages, on Kepler:\
'''
    +----------------------------------+
    |               Kepler             |
    |    High Performance GPU Server   |
    |          OS:Ubuntu Server        |
    +----------------------------------+
               |                   |
               |                   |
+--------------|-------------------|--------------+
|              |                   |              |
|   Student_1  |     Student_2     |   Student_3  |
|    eyy001    |      eyy002       |    eyy003    |
|              |                   |              |
+--------------|-------------------|--------------+
               |                   |
               |                   |
               v                   v

    +----------------------------------+
    |       Singularity Runtime        |
    |                                  |
    | +--------------------------+     |
    | |                          |     |
    | | Singularity Container    |     |
    | | for eyy001               |     |
    | | - prefferd OS (Ubunutu)  |     |
    | | - prefferd languages(..) |     |
    | | - prefferd packages(..)  |     |
    | | - preffered software     |     |
    | +--------------------------+     |
    |                                  |
    | +--------------------------+     |
    | |                          |     |
    | | Singularity Container    |     |
    | | for eyy002               |     |
    | | eg: {                    |     |
    | | - OS: CentOS             |     |
    | | - languages:R            |     |
    | | - GCC, Make              |     |
    | | - Data Analysis Tools  } |     |
    | +--------------------------+     |
    |                                  |
    | +--------------------------+     |
    | |                          |     |
    | | Singularity Container    |     |
    | | for eyy003               |     |
    | | eg: {                    |     |
    | | - OS: Fedora             |     |
    | | - languages: Java        |     |
    | | - Apache Spark           |     |
    | | - Hadoop                 |     |
    | +--------------------------+     |
    |                                  |
    +----------------------------------+    '''




# Why Use Singularity?
    - 




# Singularity Quick-Start for New User

1. Login to the kepler GPU server with your username and password.(The same credentials as for aiken or tesla).

    ```$ ssh eyyxxx@kepler.ce.pdn.ac.lk ```
   server public documentation: https://faq.ce.pdn.ac.lk/network-n-servers/kepler/

3. A sample singularity container definition file(Already comes with python3, pip3 and pytorch) is available at /srv/singularity/base.def  

4. Copy it to your preferred (home) directory.\
    ```$ cp /srv/singularity/base.def path/to/your/dir/base.def```

5. Build a Sandbox version to test and install necessary packages/dependencies.\
    ```$ cd path/to/your/dir```\
    ```$ singularity build --sandbox --fakeroot base base.def ```

6. To enter the singularity container\
    ```$ singularity shell --writable --fakeroot base```

7. Check whether new packages can be installed with apt package manager to the new container.For example:\
    ```$ apt-get install neofetch```

8. Add the commands from step 6 to the def file under the %post blob so that the final build will have the packages you tested above.

9. Build the container\
    ```$ singularity build --fakeroot base.sif base.def```

10. Run commands using the container\
    ```$ singularity exec base.sif <your-command>```


<b>Singularity Official Documentation<b> https://apptainer.org/user-docs/master/


