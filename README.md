# Jetpack & ROS install
https://drive.google.com/file/d/1HU5F1cwiw2wzuNBdLL9R3Wvpg5AXLzw5/view
sudo nmcli device wifi list
sudo nmcli device wifi connect <ssid_name> password <password>
ifconfig
# password가 없는 경우
zeta@jp461:~$ sudo nmcli device wifi connect STARTUP_LOUNGE_love
zeta@jp461:~$ ifconfig
# password가 있는 경우
jetson@jp4512G:~$ sudo nmcli device wifi connect U+NetD681 password xxxxxxx
jetson@jp4512G:~$ ifconfig wlan0
# 연결을 해제할 때
sudo nmcli device disconnect wlan0
#명령 실행 로그
jetson@jp4512G:~/catkin_ws$ sudo nmcli device disconnect wlan0
# Cooling Fan
cd Downloads
git clone https://github.com/jetsonworld/jetson-fan-ctl.git
cd jetson-fan-ctl
sudo sh install.sh
# ROS Melodic 설치
cd ~/Downloads/
sudo apt update
git clone https://github.com/zeta0707/installROS.git
cd installROS
./install-ros.sh
# .bashrc 수정
gedit ~/.bashrc 
# 파일 제일 아래에 다음과 같은 내용 입력
alias cma='catkin_make -DCATKIN_WHITELIST_PACKAGES=""'
alias cop='catkin_make --only-pkg-with-deps'
alias coc='catkin clean'
alias cca='catkin clean -y'
# 용어 설명
cmake /home/jetson/catkin_ws/src -DCATKIN_WHITELIST_PACKAGES= -

cmake: 이것은 소프트웨어 프로젝트의 빌드 프로세스를 관리하기 위한 널리 사용되는 빌드 시스템인 CMake 명령입니다.

/home/jetson/catkin_ws/src: 이것은 ROS 패키지가 위치한 소스 코드 디렉토리의 경로입니다.

-DCATKIN_WHITELIST_PACKAGES=: 이 부분은 CMake 변수를 지정하는데, 이 경우에는 아무 패키지도 화이트리스트에 포함되지 않았음을 나타냅니다.

# mirco USB 케이블 연결을 사용할 경우, jetson master
export ROS_MASTER_URI=http://192.168.55.1:11311
export ROS_IP=192.168.55.100

source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bas
# 종료 후 터미널 업데이트
$ source ~/.bashrc
아래 명령어를 사용하여 clean을 한 번 하면 cma가 문제없이 실행됩니다.
jetson@jp4512G:~/catkin_ws$ cca
jetson@jp4512G:~/catkin_ws$ cma
# ROS 동작 확인
세 개의 창에 하나씩 아래 명령어를 실행
# 터미널 #1
jetson@jp4512G:~/catkin_ws$ roscore
# 터미널 #2
jetson@jp4512G:~/catkin_ws$ rosrun turtlesim turtlesim_node
# 터미널 #3
jetson@jp4512G:~/catkin_ws$ rosrun turtlesim turtle_teleop_key

# jessicar install on Jetson
cd ~/catkin_ws/src
git clone https://github.com/zeta0707/jessicar.git
cd ~/catkin_ws
cd ~/Downloads/opencvDownTo34
sudo patch -p1 /opt/ros/melodic/share/cv_bridge/cmake/cv_bridgeConfig.cmake -p1 < cv_brige.patch
cd ~/catkin_ws
# Teleop by joystick
Jetson USB port에 USB dongle을 연결하고, gamepad 뒷면 ON/OFF 버튼을 ON으로 이동시켜주세요. 그 후 HOME 버튼을 한 번 눌러 붉은 LED 하나가 켜지는지 확인해주세요. 
# joystick 패키지 설치
sudo apt-get install joystick
cd /dev/input
ls js*
# js0 확인
jetson@jp4612GCv346Py37:/dev/input$ ls js*
js0
# joystick 동작 확인
왼쪽 패드를 좌우로 움직이면 Axe X가 -32767 ~32767 까지 변한다. 패드를 아래 위로 움직이면 Axe Y가 역시 -32767 ~32767까지 변합니다.
# Teleop by keyboard
# terminal #1
$ roslaunch jessicar_control keyboard_control.launch
# terminal #2
$ roslaunch jessicar_teleop jessicar_teleop_key.launch
# Bash
zeta@changwhan-asus:~/catkin_ws$ rostopic list
/cmd_vel
/rosout
/rosout_agg
