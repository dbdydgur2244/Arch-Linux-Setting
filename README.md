# Arch Linux(Manjaro) Setting
## Install 과정
https://www.youtube.com/watch?v=KAPRs_yWiek

참고
## Local 설정

언어랑 시간 설정

## Pacman  aliasing

```bash
alias pacman='sudo pacman'
```

## pacman 설정

```bash
sudo pacman-optimize
sudo pacman -Syu
```

## vim 설치

```bash
pacman -Sy vim
pacman -R vi
ln -s /usr/bin/vim /usr/bin/vi
# yonghyuk vimrc install
cd ~/
git clone https://github.com/dbdydgur2244/vim-setting .vim
ln -s ~/.vim/vimrc ~/.vimrc
vim -c ":PlugInstall" -c ":q" -c ":q"
```

## yaourt 설치

Pacman configuration file 수정

```bash
$ sudo vi /etc/pacman.conf
```

가장 아래에 해당 내용 추가

```bash
[archlinuxfr]
SigLevel = Never
Server = http://repo.archlinux.fr/$arch
```

그리고 pacman으로 설치

```bash
pacman -Sy yaourt
```



## 한글 설정

> nabi 사용
>
> 2018.03.08 테스트해본 결과 configure이 없어서 설치 못함.
>
> ibus로 세팅하였음.

### nabi

```bash
git clone https://github.com/choehwanjin/nabi.git
cd nabi
./configure --prefix=$PREFIX
make
sudo make install
```

다음 내용을 `.xinitrc`, `.xprofile`, 혹은 `.xsession`에 추가.

```bash
export XIM=nabi
export XIM_ARGS=
export XIM_PROGRAM="nabi"
export XMODIFIERS="@im=nabi"
export GTK_IM_MODULE=xim
export QT_IM_MODULE=xim
```

#### 한영키 사용하기

```bash
vi .xprofile
```

```bash
xmodmap -e 'remove mod1 = Alt_R'
xmodmap -e 'keycode 108 = Hangul'
xmodmap -e 'remove control = Control_R'
xmodmap -e 'keycode 105 = Hangul_Hanja'
```

### IBus

```bash
pacman -S ibus-hangul ibus-qt
```

`.xprofile`의 마지막에 이 부분 추가

```bash
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
export OOO_FORCE_DESKTOP="gnome"
```



## Mouse 설정

### 키 관련 설정

`.imwheelrc`을 홈 디렉토리에 만들고 다음과 같은 내용 추가

```bash
"^chromium$"
None,      Up,   Button4, 4
None,      Down, Button5, 4
```

### 마우스 가속도 설정

설정에서 마우스 `flat`으로 바꾸고

https://unix.stackexchange.com/questions/90572/how-can-i-set-mouse-sensitivity-not-just-mouse-acceleration

참고



## 32비트 앱을 설치할 때 필요한 것

```bash
# 32bit 앱이나 라이브러리 설치할 때 충돌 안나기 위해서 /etc/pacman.conf에 추가
[multilib]
Include = /etc/pacman.d/mirrorlist
```



## 필요한 것들 설치

> $(pkg-list.txt)가 현재 안되는 거 같음

```bash
yaourt -S $(pkg-list.txt)
```



## DISCORD 설치 에러

설치하면 에러가 날것이다.

키 머시기 머시기 있으므로 그거로 다음 명령어에 `key...` 대신 넣으면 설치 가능.

```bash
gpg --recv keys `key...`
```
