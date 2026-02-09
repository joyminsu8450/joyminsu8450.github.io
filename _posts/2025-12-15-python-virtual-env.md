---
layout: post
title: "Python 가상환경 제대로 이해하기"
date: 2025-12-15
categories: [개발]
---

Python 프로젝트를 시작할 때 가장 먼저 해야 할 일은 가상환경을 만드는 것입니다. 왜 가상환경이 필요하고, 어떻게 사용하는지 정리해보겠습니다.

## 가상환경이란?

가상환경은 프로젝트별로 독립적인 Python 패키지 공간을 만들어주는 도구입니다. 프로젝트 A에서는 Django 4.0을, 프로젝트 B에서는 Django 5.0을 사용해야 하는 상황을 생각해보세요.

## venv 사용법

Python 3.3부터 기본 내장된 `venv` 모듈을 사용하는 것이 가장 간단합니다.

```bash
# 가상환경 생성
python -m venv myenv

# 활성화 (macOS/Linux)
source myenv/bin/activate

# 활성화 (Windows)
myenv\Scripts\activate

# 패키지 설치
pip install django

# 설치된 패키지 확인
pip list

# 비활성화
deactivate
```

## requirements.txt 관리

프로젝트의 패키지 의존성을 관리하려면 `requirements.txt`를 활용합니다.

```bash
# 현재 설치된 패키지를 파일로 저장
pip freeze > requirements.txt

# 파일로부터 패키지 일괄 설치
pip install -r requirements.txt
```

## pyenv와 함께 사용하기

여러 Python 버전을 관리해야 한다면 `pyenv`를 함께 사용하는 것을 추천합니다.

```bash
# Python 3.12 설치
pyenv install 3.12.0

# 프로젝트 디렉토리에서 Python 버전 설정
pyenv local 3.12.0

# 가상환경 생성
python -m venv .venv
```

가상환경을 습관적으로 사용하면 패키지 충돌 문제를 미리 방지할 수 있습니다. 특히 팀 프로젝트에서는 필수입니다!
