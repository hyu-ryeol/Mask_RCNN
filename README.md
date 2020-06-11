# Mask_RCNN
Ubuntu 18.04LTS, Geforce RTX2060 super 기준

**1.그래픽드라이버가 깔려있는 경우 제거**

터미털창에 다음과 같이 친다
```bash
sudo apt-get remove nvidia* && sudo apt autoremove
sudo apt-get install dkms build-essential linux-headers-generic
sudo gedit /etc/modprobe.d/blacklist.conf
```

실행된 blacklist.conf 파일 맨 밑에 추가한다
```bash
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```

---다시 터미널창에 다음과 같이 친다---
```bash
echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
sudo update-initramfs -u
sudo reboot
```

**2.CUDA 설치**

    https://www.nvidia.co.kr/Download/index.aspx?lang=kr    
에서 자신의 그래픽카드에 맞는 nvidia 그래픽 드라이버 버전을 확인
나의 경우 20년6월11기준 440.82가 최신
 
  
    https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal 
에서 CUDA 설치
참고로 CUDA Toolkit을 설치하면 자동으로 그래픽드라이버도 설치하는데 과정은 아래와 같음.


**설치순서 내 그래픽 드라이버 기준**
위의 링크에 들어가서 Linux-x86_64-Ubuntu-18.04-runfile(Local) 순서로 클릭하면
```bash
    wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run 
        (런파일 다운로드. 내경우 home/baek 경로)
```
  !본인의 그래픽 드라이버 버전에 맞는 CUDA를 설치해야함! 
  run파일 이름을보면 cuda_10.2.89_440.33.01_linux.run 라고 되있는데 내 그래픽카드 버전은 440.** 이므로 일치하는 것을 확인할 수 있음.

  run파일을 인스톨 하기 전 충돌 가능성 때문에 gui를 사용하지 않는 모드로 들어가야함
   ctrl+alt+f1 
   를 눌러 root로 로그인
   
 
   sudo service lightdm stop
   cd /home/baek
   ./cuda_cuda_10.2.89_440.33.01_linux.run      (아까받은 런파일 실행)
 
 
 
 까지 입력하면 약관에 동의하냐고 물어보는데  accept 입력
 그리고 전부 x로 체크 되있을 텐데 바로 install 누르면 됨
 
 그리고 bashrc에 path를 입력하기 위해
 
 
 gedit ~/.bashrc  
 
 맨밑에 다음과같이 입력
 export PATH=$PATH:/usr/local/cuda-10.2/bin
 export CUDADIR=/usr/local/cuda-10.2
 export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.2/lib64
 저장하고 종료
 
 source ~/.bashrc 
 
 

 
 
