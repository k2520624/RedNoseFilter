# RedNoseFilter

웹캠 및 이미지/영상 파일에서 얼굴을 인식해 루돌프 코를 그려주는 WPF 애플리케이션입니다.  
이미지는 Dlib, 영상과 실시간 웹캠은 MediaPipe 를 사용해서 구현했습니다.  

---

## ✅ 사전 준비 사항

- **Visual Studio 2022** 이상
- **.NET 6.0 SDK**
- **Python 3.8 ~ 3.10 권장** (설치 경로에 한글 또는 공백이 없어야 함)
- `pip`가 정상적으로 등록된 환경

---

## 📦 초기 세팅 방법

1. **Python 라이브러리 설치**

   `cmd`를 열고 프로젝트 폴더 내 `requirements.txt` 파일이 있는 경로로 이동한 후 아래 명령어를 실행합니다:

   ```cmd
   pip install -r requirements.txt
   ```
   *오류 발생시 mediapipe,opencv-python,numpy,flask 수동 설치*

2. **Python 실행 경로 설정**

   Visual Studio에서 프로젝트를 열고 `MainWindowViewModel.cs` 파일을 엽니다.  
   다음 두 줄의 `FileName` 값을 자신의 Python 실행 파일 경로로 수정합니다:

   - **57번 줄**
   - **166번 줄**

   예시:
   ```csharp
   FileName = @"C:\Python\Python310\python.exe";
   ```

---

## ▶️ 프로그램 사용 방법

1. **Visual Studio에서 `Debug` 모드로 실행**합니다.

2. 상단에 위치한 버튼 중 하나를 클릭합니다:

   - **이미지 / 영상 버튼**  
     → 파일 탐색기가 열립니다. 컴퓨터 내 이미지(.jpg/.png 등) 또는 영상(.mp4/.avi/.mov 등) 파일을 선택하고 **열기**를 클릭하면,  
     선택한 파일이 얼굴 인식 및 루돌프 코 추가 처리를 거쳐 화면에 표시됩니다.  
     영상의 경우, 속도 문제로 사전 처리한 후 결과 영상을 재생하는 방식으로 되어 있어 약간의 **딜레이**가 발생할 수 있습니다.
     *파일 경로에 한글이 포함되면 오류 발생*

   - **웹캠 버튼**  
     → 연결된 웹캠을 통해 얼굴을 인식하고 루돌프 코를 실시간으로 화면에 표시합니다.  
     웹캠 영상의 해상도를 조절하려면 다음 경로에 있는 `rudolph_webcam.py` 파일의 22, 23번째 줄을 수정하면 됩니다:

     ```
     RedNoseFilter\bin\Debug\net6.0-windows\rudolph_webcam.py
     ```

   - 동영상이나 웹캠이 실행 중일 때 다른 버튼을 누르면 자동으로 현재 작업을 중단하고 다음 UI 업데이트를 준비합니다.

---

## 📁 파일 구성

| 파일명 | 설명 |
|--------|------|
| `MainWindow.xaml` | 메인 UI 레이아웃 |
| `MainWindowViewModel.cs` | UI 로직 및 명령 처리 |
| `RedNoseFilter\bin\Debug\net6.0-windows\rudolph_webcam.py` | 웹캠 실시간 처리용 파이썬 스크립트 |
| `RedNoseFilter\bin\Debug\net6.0-windows\rudolph_video.py` | 영상 파일 처리용 파이썬 스크립트 |
| `ImageProcessor.cs` | Dlib을 이용한 이미지 처리 |
| `requirements.txt` | 필요한 Python 라이브러리 목록 |

---

## 📌 참고 사항

- 웹캠 실행 시 처음 몇 초간 딜레이가 있을 수 있으며, 영상 파일 처리 시에도 시간 소요가 있습니다.

- **Dlib vs MediaPipe**  
  `dlib`은 `mediapipe`보다 **정확도는 더 우수**하지만 **처리 속도가 느린 단점**이 있습니다.  
  따라서 이미지에 대해서는 **`dlib` 기반 처리**를 사용하고,  
  영상 및 웹캠처럼 **속도가 중요한 경우에는 `mediapipe`**를 활용해 구현했습니다.

---
