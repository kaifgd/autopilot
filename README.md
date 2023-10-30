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
