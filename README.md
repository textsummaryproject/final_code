
# 세 줄 톡 (Three Line Talk)

## 팀 소개

**Team:** 뚜벅이들  
**팀원:**
- 2022042019 조찬미
- 2022042024 위다인

## 프로젝트 개요

세 줄 톡은 사용자가 입력한 텍스트, 이미지, 또는 문서 파일을 요약하고 이를 음성으로 변환하는 프로그램입니다. 본 프로젝트는 다양한 입력 방식을 지원하여 사용자 편의성을 높이고자 하였으며, 초기 GUI 구현을 시도하였으나 어려움으로 인해 콘솔 기반 프로그램으로 변경하였습니다.

## 기능 설명

1. **이미지 입력**
    - 사용자가 제공한 이미지에서 텍스트를 추출 (OCR)
    - 추출된 텍스트를 요약
    - 요약된 텍스트를 음성으로 변환 및 출력

2. **텍스트 입력**
    - 사용자가 입력한 텍스트를 요약
    - 요약된 텍스트를 음성으로 변환 및 출력

3. **문서 입력**
    - 사용자가 제공한 문서 파일에서 텍스트를 추출
    - 추출된 텍스트를 요약
    - 요약된 텍스트를 음성으로 변환 및 출력

## 개발 환경 및 기술 스택

- **언어:** C++
- **라이브러리:** OpenCV, Tesseract-OCR, gTTS (Google Text-to-Speech)
- **기타 도구:** Visual Studio, Python

## 설치 및 실행 방법

1. **사전 준비**
    - OpenCV 설치
    - Tesseract-OCR 설치
    - Python 및 gTTS 라이브러리 설치 (`pip install gtts`)


2. **빌드 및 실행**
    - Visual Studio에서 프로젝트 파일을 열고 빌드
    - 빌드된 실행 파일을 통해 프로그램 실행

## 주요 코드 설명

### 초기 화면 및 메뉴 선택

```cpp
void printinitview() {
    cout << "\n\n\n\n";
    cout << "\t\t\t\t\t==========================================" << endl;
    cout << "\t\t\t\t\t                                          " << endl;
    cout << "\t\t\t\t\t                  세 줄 톡                " << endl;
    cout << "\t\t\t\t\t                                          " << endl;
    cout << "\t\t\t\t\t==========================================" << endl;
    cout << "\n\n";
    cout << "\t\t\t\t\t          오픈소스전문프로젝트\n";
    cout << "\t\t\t\t\t            제작자: 뚜벅이들\n\n\n";
    cout << "\t\t\t\t\t        엔터를 누르면 계속합니다...";
    cin.get();
}
```

### 텍스트 요약 및 음성 변환

```cpp
void summarizeText(const std::string& text) {
    std::istringstream iss(text);
    std::string line;
    std::vector<std::string> sentences;
    while (std::getline(iss, line, '.')) {
        if (!line.empty()) {
            sentences.push_back(line + '.');
        }
    }

    // TF-IDF 계산 및 요약
    std::vector<std::vector<std::string>> corpus;
    for (const std::string& sentence : sentences) {
        corpus.push_back(split(toLowerCase(sentence)));
    }

    // 요약 결과 출력
    std::cout << "요약 결과:\n";
    std::vector<std::string> summary;
    for (size_t i = 0; i < std::min<size_t>(sentenceScores.size(), size_t(3)); ++i) {
        std::cout << sentenceScores[i].first << "\n";
        summary.push_back(sentenceScores[i].first);
    }

    // 요약된 내용을 하나의 문자열로 결합
    std::string fullSummary = "";
    for (const auto& sentence : summary) {
        fullSummary += sentence + " ";
    }

    textToSpeech(fullSummary);
}
```

## 문제 해결 및 개선 사항

- **GUI 환경 설정 어려움**: GUI 환경 구성이 어려워 콘솔 기반 프로그램으로 변경
- **OCR 성능 저하**: 이미지의 화질로 인한 OCR 성능 저하 문제를 발견하여 이미지 전처리 과정 개선

## 기여 방법

1. 이 레포지토리를 포크합니다.
2. 기능을 추가하거나 버그를 수정합니다.
3. 변경 사항을 커밋합니다.
4. 자신의 레포지토리에 푸시합니다.
5. Pull Request를 생성합니다.

## 라이선스

이 프로젝트는 MIT 라이선스를 따릅니다. 자세한 내용은 `LICENSE` 파일을 참고하세요.

