### Description:
Complete internal telephony project

### Powered by:
By Israel Glixinski

### To build the image manually:
* "docker build -t phonehubimage ."

### To create the container manually:
* "docker run -d --name phonehubcont -p 5038:5038 -p 5060:5060/udp -p 10000-10100:10000-10100/udp phonehubimage"

### To pull the built container:
* "docker pull registry.gitlab.com/docker8554241/phonehub:latest"
