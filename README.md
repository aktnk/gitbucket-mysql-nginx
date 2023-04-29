# GitBucket + MySQL + Nginx Reverse Proxy

Here I use docker compose to set up the GitBucket server.
And use MySQL sever for GitBucket's DB, and also use a Nginx reverse proxy and publish to the /gitbucket path.

# How to use

* clone this repository
* create two files
    * ./.env  
        Specify the user name and password for the DB for GitBucket to be created in MySQL and the user name and password for MySQL in the .env file.
    * mysql/.secret  
        Specify the root password for MySQL in the .secret file.
* build containers
    ```
    $ docker compose build
    [+] Building 2.9s (8/8) FINISHED                                                                   
    => [internal] load .dockerignore                                                             0.3s
    => => transferring context: 2B                                                               0.0s
    => [internal] load build definition from Dockerfile                                          0.2s
    => => transferring dockerfile: 332B                                                          0.0s
    => [internal] load metadata for docker.io/library/openjdk:11-jre                             1.8s
    => https://github.com/gitbucket/gitbucket/releases/download/4.38.4/gitbucket.war             0.8s
    => [1/3] FROM docker.io/library/openjdk:11-jre@sha256:356949c3125c4fa8104745e7ea92bd995da45  0.0s
    => CACHED [2/3] ADD https://github.com/gitbucket/gitbucket/releases/download/4.38.4/gitbuck  0.0s
    => CACHED [3/3] RUN ln -s /gitbucket /root/.gitbucket                                        0.0s
    => exporting to image                                                                        0.0s
    => => exporting layers                                                                       0.0s
    => => writing image sha256:0fe171da329a142549cc2b5513f5be33d4c1ee6291e7e99f33b3f09ac19ca10b  0.0s
    => => naming to docker.io/library/gitbucket-gitbucket                                        0.0s
    [+] Building 0.2s (6/6) FINISHED                                                                   
    => [internal] load build definition from Dockerfile                                          0.1s
    => => transferring dockerfile: 158B                                                          0.0s
    => [internal] load .dockerignore                                                             0.2s
    => => transferring context: 2B                                                               0.0s
    => [internal] load metadata for docker.io/library/nginx:1.23.4                               0.0s
    => [1/2] FROM docker.io/library/nginx:1.23.4                                                 0.0s
    => CACHED [2/2] RUN echo "Asia/Tokyo" > /etc/timezone     && dpkg-reconfigure -f noninterac  0.0s
    => exporting to image                                                                        0.0s
    => => exporting layers                                                                       0.0s
    => => writing image sha256:ce56eabecb3cd3b7d6a4d4b75fc7e8f61e2d5957d0c811c8bd9f340fd35b807a  0.0s
    => => naming to docker.io/library/gitbucket-nginx  
* run containers
    ```
    $ docker compose up -d
    [+] Running 3/3
    ⠿ Container gb-mysql   Started                                                              20.1s
    ⠿ Container gitbucket  Started                                                              15.2s
    ⠿ Container gb-nginx   Started                                                               4.8s
    ```
* add plugins  
    To add a plugin, obtain the plugin jar file from the provider and place it in gitbucket/data/plugins.
    ```
    $ sudo cp (plugin filename).jar gitbucket/data/plugins/
    ```

# Reference

* [yoshinorin
/
docker-gitbucket-orchestration](https://github.com/yoshinorin/docker-gitbucket-orchestration)
