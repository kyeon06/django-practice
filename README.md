# TIL
- [poetry를 이용한 가상환경 생성](#poetry를-이용한-가상환경-생성)
- [django-environ를 이용한 환경변수 관리](#django-environ를-이용한-환경변수-관리)
- [django project & app 생성](#django-project--app-생성)
- [migration 명령어](#migration-기능)
- [DB data 다루기:dumpdata & loaddata](#dumpdata--loaddata)

## poetry를 이용한 가상환경 생성
[기록](https://hapsunny.tistory.com/94)
```bash
$ poetry init
$ poetry add django djangorestframework
```
## django project & app 생성
- project 생성
```bash
# 현재 위치한 폴더에서 프로젝트 폴더를 만든 후 그 안에 프로젝트 생성
$ django-admin startproject <프로젝트이름>

# 현재 위치한 폴더에서 프로젝트 생성
$ django-admin startproject <프로젝트이름> . 
```
- app 생성
```bash
$ python manage.py startapp <앱이름>
```

## Migration 기능
- models.py에 정의된 모델의 생성/변경 히스토리를 관리하고 DB에 적용할때 사용하는 명령어
```bash
# migration 파일 생성
$ python manage.py makemigrations <앱이름>

# migration 파일 적용
$ python manage.py migrate <앱이름>

# 적용 현황
$ python manage.py showmigrations <앱이름>

# 지정 migration SQL 내역
$ python manage.py sqlmigrate <앱이름> <마이그레이션이름>
```

## django-environ를 이용한 환경변수 관리
- 환경변수를 관리할 수 있도록 도와주는 라이브러리
- settings.py나 프로젝트를 진행할 때 노출되지 말아야하는 환경변수들을 `.env` 파일로 분리한다.
    - 이때 `.env` 파일에 변수를 넣을 경우 변수와 값 사이에는 공백이 없게 넣어야 함
- settings.py에 적용
```py
# 1. import
import os
import environ

# 2. 환경변수를 불러올 수 있도록 세팅
env = environ.Env(DEBUG=(bool, True))

# 3. 파일 경로 설정
environ.Env.read_env(env_file=os.path.join(BASE_DIR, '.env'))

# 4. 불러온 값 설정
SECRET_KEY = env("SECRET_KEY")
```

## dumpdata & loaddata
- 프로젝트를 진행하다 보면 데이터를 임시로 저장해야할 경우나 팀원들 간의 공유를 해야할 상황이 발생할 수 있다.
- 그럴 경우에 아래와 같이 명령어를 사용하면 현재 DB에 있는 데이터들을 json 형태로 꺼내고 다시 DB에 저장할 수 있다.
```bash
python -Xutf8 manage.py dumpdata [앱이름] > [파일이름.json] # 데이터 json형태로 저장하는 명령
python manage.py loaddata [파일이름.json] # DB에 data load 하는 명령
```
