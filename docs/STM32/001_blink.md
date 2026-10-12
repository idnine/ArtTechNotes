# Blink LED

1. ST-LINK 연결
1. CubeMX 세팅
1. CubeIDE 확인
1. 코드 작성
1. 빌드와 업로드

## 1. ST-LINK 연결

* STLINK:GND - STM32:GND
* STLINK:SCL - STM32:SCL
* STLINK:SDA - STM32:SDA
* STM32 보드에 USB 전원 넣기

## 2. CubeMX 세팅

* CPU 선택에서 STM32F411CEU6 선택하기
* GPIO-C13 핀 클릭해서 GPIO-OUTPUT 선택
* GPIO-C13 핀 우클릭해서 사용자 이름 지정, "LED_BUILTIN" 이라고 설정
* Project에서 폴더 위치, 프로젝트 이름 정하기
* Project 타입을 CubeIDE 선택
* 오른쪽 위에 있는 Generate Code 버튼 눌러 프로젝트 생성

## 3. CubeIDE 확인

* Workspace 선택하기 - 만들어진 프로젝트 위치 선택
* Import STM32 Project 해서 MX에서 만든 프로젝트 열기

## 4. 코드 작성

* Core/Src 폴더에 있는 main.c 수정
* while 구역에 있는 UserCode 영역에 다음 코드 추가

```

HAL_GPIO_TogglePin(LED_BUILIN_GPIO_Port, LED_BUILTIN_Pin)
HAL_Delay(300);

```

## 5. 빌드와 업로드

* 왼쪽 위 상단 메뉴 버튼 중 망치(Build) 선택, 첫 빌드는 망치!
* 화면 중간이나 조금 오른쪽 위 메뉴 버튼 중 녹색 플레이 버틑 누르면 Build와 Upload 진행됨

