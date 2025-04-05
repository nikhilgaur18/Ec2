sudo apt update
    2  apt-get install openjdk-17-jdk
    3  sudo apt-get install openjdk-17-jdk
    4  sudo apt install jenkins
    5  sudo wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    6  sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    7      /etc/apt/sources.list.d/jenkins.list'
    8  sudo apt-get update
    9  sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys  5BA31D57EF5975CA
   10  sudo apt-get install jenkins
