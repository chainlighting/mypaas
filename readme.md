MyPaas
======
This project will make it easy to build your private PAAS environment.

## ToolsBox
1. Virtual Box 5.0.20 r106931

  * use virtualbox as our IAAS' machine.

2. ubuntu-16.04-server-amd64.iso

  * use ubuntu-16.04-tls as our IAAS' machine OS. OS Intall-Setting should chosen language-->*English*, language-->*chinese* maybe meet some install error.
  
  * change the network device name to *ethx*
  
    ```
    vi /etc/default/grub
    ```
    change *grub* settting
    ```
    GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"
    ```
    save *grub* setting
    ```
    update-grub
    ```
    modify network device name to *ethx* by edit */etc/network/interface*
    then reboot system
    ```
    reboot
    ```

3. docker engine

  * install latest docker-engine to host
  
    3.1 install from china daocloud site,**higher speed in china**
    ```
    curl -sSL https://get.daocloud.io/docker | sh
    ```

    3.2 install from china aliyun,**higher speed in china**
    ```
    curl -sSL http://acs-public-mirror.oss-cn-hangzhou.aliyuncs.com/docker-engine/internet | sh
    ```

    3.3 install from docker official site,**lower speed in china**
    ```
    wget -qO- https://get.docker.com | sh
    ```

    3.4 check the intalled docker-engine version and docker's infomation. if the installation is OK, we should get some useful info.
    ```
    docker version
    docker info
    ```

## Deployment

         Registry[https://index.docker.io/v1/)-----------Registry-mirror(https://*your-id*.mirror.aliyuncs.com)
            |                                                    |
            |________________________external____________________|
                                        |
                                        |
                                 MyPaas Manager(paas enabler)
                                        |
            ----------------------------|-------------------------------------------------
            |                           |                        |                       |
     MyPaas Registry              MyPaas Composer            MyPaas Monitor        MyPaas Iaas Driver
            |                           |                        |                       |
            |                     (K8S/Swarm...)                 |            (RawMachine/OpenStack/VMWare....)
            |                           |                        |                       |     
            V                           V                        V                       V
     [Supply Images]              [Supply Container]       [Monitor&Schedule]       [Supply Host&Store]
            |                           |                        |                       |
            |-----------attach--------->|------------------------|-------------attach--->|
                                        |                        |                       |
                                        |                        |-----monitor&schedule->|
                                        |<---monitor&schedule----|                       |
                                                                 |                       |
                                                                 |                       V 
                                                                 |-----M&S------->[Supply Service]
                                                                 |
                                                                 |
                                                                 V
                                                          [Export Service]
            





1. set the docker-engine's mirro registry

    *registry* supply the image-meta, *registry mirror* supply the image.

    *when registry down, docker-image can be downloaded?*
    
    * use aliyun docker mirror site

        register your account on https://dev.aliyun.com.

        on page: https://dev.aliyun.com/search.html, you will get how to set mirror in *special linux distribution*.

2. create a private registry

## management

* use **rancher** to manage our cluster infrastructure. 
* use **swarm** to shecdule all our docker supply.

#### start rancher

#### start swarm

    
    