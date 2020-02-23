---
title: About Me
layout: tag
permalink: /about_kor/
taxonomy: markup
---

# Introduce

![profile](https://avatars1.githubusercontent.com/u/18162344?s=460&v=4)

* 서인석 (InSeock Suh)
* Email :   <yoyus5@naver.com>
* Github :  [github.com/ISSuh](https://github.com/ISSuh)
* Resume : [KOR](/about_kor/) / [ENG](/about_en/)

> 더 나은 소프트웨어를 위해

# Experience

* [스프링클라우드](http://www.tasio.io)
    - 솔루션 개발팀 / 매니저
    - 시스템개발
    - 2018.01 ~

# Projects

## **_자율주행 AI 컴퓨팅모듈 검증 및 차량실증기술 개발_**
### 자율주행 컴퓨팅 모듈을 탑재하여 자율주행 기능 실증 및 실험

`시스템 분석 및 개발 2019.05 ~ 2019.12`

### 분석 및 개발

* 상용 자율주행 셔틀차량 분석 및 연동
    * 자율주행 차량 운행 데이터 분석
    * 사내 프로젝트인 차량 운행데이터 관제 연동 단말기 연동
* 특허 2건 출원
    * 자율주행 시스템
    * 센싱데이터 전송장치 및 방법

## **_자율주행 부품 성능검증을 위한 자율셔틀 실증 기반기술 개발_**
### 자율주행 셔틀 차량의 운영자 모니터링 시스템 개발

`시스템 개발 2019.03 ~ 2019.12`

### 개발

* 자율주행 셔틀차량의 운영자 모니터링 시스템의 일부 기능 개발
    * 차량 데이터 관제 연동을 위한 데이터 전송 규격 설계 및 기능 개발
    * 차량의 영상 전송을 위한 영상 스트리밍 서버(RTSP, RTP) 개발
    * 네트웨크 모니터링(네트워크 인터페이스, 대역폭 등) 기능 개발

## **_차량 운행데이터 관제 연동 단말기 개발_**
### 관제 연동을 위한 차량정보 및 센서정보 연동 솔루션

`시스템 개발 2019.02 ~ 2019.11`

### 개발

* 자율주행 차량 센서데이터 획득 및 차량정보 연동 소프트웨어 개발
    * Camera, GNSS, LiDAR, Radar, IMU, CAN 데이터 연동 소프트웨어 개발
* 획득한 센서데이터 및 차량정보 관제 서버로 전송 소프트웨어 개발
    * JSON 및 Google Protobuf를 통한 데이터 전송 구조 및 규격 설계
    * TCP, MQTT, Websocket, Kafka등 관제 시스템 버전에 맞춰 다양한 통신 인터페이스 사용
* 획득한 Camera 영상 전송을 위한 RTSP 서버 개발
    * Multi Camera기반 RTSP 서버 개발
    * 최적화를 위한 Multi Camera 영상 합성 및 이미지 프로세싱
* 정보 연동 소프트웨어 및 정보 전송 소프트웨어 Dockernize
    * Docker를 통한 센서별 연동 드라이버 소프트웨어및 관리
    * Docker-compos를 통한 시스템 orchestration

## **_대규모 실시간 비디오 분석에 의한 전역적 다중 관심객체 추적 및 상황 예측 기술 개발_**
### 이동체에서(차량, 사람등)의 센서 연동 및 데이터 획득, 전송 시스템 개발

`시스템 개발 2018.03 ~ 2018.12`

### 개발

* DrivePX2 보드 기반 Camera, GNSS 센서 연동 및 데이터 획득
* QT5를 이용한 데이터 획득 및 전송 GUI 어플리케이션 개발
    * Camera, GNSS 데이터 저장기능 개발
    * RTSP 서버를 통한 Camera 영상 스트리밍 기능 개발
    * TCP 서버를 통한 GNSS 데이터 전송 기능 개발
* 개발된 소프트웨어 저작권 등록

# Personal Projects

## **_Image2RTSP_**
### ROS Image 스트림을 위한 멀티 세션 RTSP 서버 노드

`개인 프로젝트` - <https://github.com/ISSuh/image2rtsp>

### 개발

* ROS Image(sensor_msgs/Image)를 x264로 압축하여 h264로 인코딩
* 인코딩된 이미지를 live555기반 RTSP 서버에서 송출
* Proxy를 내장하여 외부 접속 가능

## **_CUDA Image Process_**
### CUDA 기반 이미지 변환 ROS 노드

`개인 프로젝트` - <https://github.com/ISSuh/CudaImageProcessing>

### 개발

* ROS Image(sensor_msgs/Image)를 CUDA 라이브러리를 이용하여 GPU기반 이미지 변환
    - 이미지 크기 변환
    - Gray scale 변환
    - JPEG 압축 (sensor_msgs/Image -> sensor_msgs/CompressedImage)

# Technical Experience

## Development

* 차량에서의 센서연동 및 차량정보 연동 경험
    * Camera
    * GNSS (Swift, Novaltel, uBlox, Gamin)
    * LiDAR (Velodyne, Robosence)
    * Radar (Delphi)
    * CAN
* 다양한 데이터 통신 프로토콜 경험
    * TCP/UDP, HTTP, Kafka, MQTT 등
* FrameWork 사용경험
    * ROS
    * Apollo
    * Flask
* Tools
    * Docker / Docker-compose
    * Git
    
## Language

* C / C++ 11
* Python

# Education

* 고려대학교 세종캠퍼스 컴퓨터정보학과 졸업 (2011.03 ~ 2018.02)
