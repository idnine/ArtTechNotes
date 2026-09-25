# 리눅스에 OpenCV 설치

- Ubuntu 24.04에 OpenCV 라이브러리 설치하기
- 여기서는 Ubuntu 24.04.1, OpenCV 4.10.0 버전으로 설명
- OpenCV 5 버전으로 테스트 한 것은 보충 설명으로 추가되었음

## 0. 확인

설치하는 과정은

1. 소스코드 받기
1. 빌드
1. 설치

순으로 진행된다.

- 우분투 리눅스 기본 설치에 c++, git, cmake는 설치되어 있지 않았다.
- 혹시 이미 설치되어 있다면 이미 설치되어 있다고 알려준다.
- 확인 차원에서 다음과 같이 실행한다.

```
sudo apt install build-essential git cmake pkg-config
```


## 1. OpenCV 다운로드

다운로드 폴더에서 OpenCV 소스 받기

```
cd ~/Downloads
git clone https://github.com/opencv/opencv.git
```

## 2. OpenCV 빌드

opencv 폴더에 들어가 CMakeLists.txt 수정

```
cd opencv
vi CMakeLists.txt
```

CMakeLists.txt에서 다음 항목을 수정한다. (기본값 OFF 를 ON 으로 수정)

```
OCV_OPTION(OPENCV_GENERATE_PKGCONFIG "Gererate .pc ...... " ON)
OCV_OPTION(WITH_OPENGL "Include OpenGL support" ON)
```

다운로드된 opencv 폴더에 build 폴더 만들고, build 폴더에 들어간다.

```
mkdir build
cd build
```

cmake, make 순서로 build 한다.

OpenCV 4에서는 그냥 cmake 만 하면 된다
```
cmake ..
```

OpenCV 5에서는 그래픽 관련 옵션을 켜 줘야 GUI 연결이 된다

```
cmake -D WITH_GTK=ON \
      -D WITH_OPENGL=ON \
      -D OPENCV_GENERATE_PKGCONFIG=ON \
      ..
```

이제 make 단계, 여기서 오래 걸린다. (다행히 진행상태가 %로 표시된다)

```
make -j$(nproc)
```



## 3. OpenCV 설치
완성된 build 를 시스템에 설치한다.

```
sudo make install
```

여기까지 하면 시스템에 OpenCV 라이브러리가 설치된 것이다.

## 4. 확인
opencv4.pc 파일이 있는지 확인한다.

```
ls -l /usr/local/lib/pkgconfig
```
목록이 나타나면 제대로 설치된 것이다.

pkg-config 를 통해 opencv 라이브러리 설치가 되었는지 확인한다.

```
pkg-config --modversion opencv4
```

opencv5를 설치되었다면 이렇게 5 버전으로 해야한다

```
pkg-config --modversion opencv5
```

여기서 OpenCV 버전이 표시되면 정상이다.

## 5. 종료
- 여기까지 하면 OpenCV 라이브러리가 설치된 것이다.
- 하지만, 작성하는 코드에 따라 새로운 에러들이 나타나는데...
- 대체로 apt install 로 해결 가능한 것들이다.
- 뭔가 필요하다는 모듈이 나타나면 apt instll 해서 그것들을 설치하면 잘 동작한다.


