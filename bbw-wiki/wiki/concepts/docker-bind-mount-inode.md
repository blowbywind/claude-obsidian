---
title: Docker Bind Mount Inode 문제
aliases: [도커 바인드 마운트 아이노드]
tags: [docker, infra, debugging]
summary: Docker 컨테이너 바인드 마운트 시 호스트 파일 inode 변경(예: git checkout)으로 마운트가 끊기는 현상
---

# Docker Bind Mount Inode 문제

## 현상

`git checkout` 또는 파일 교체 시 호스트 파일의 inode가 변경되면 컨테이너 내부의 마운트 경로가 구 inode를 참조한 채 남아 있어 변경사항이 반영되지 않는다.

## 해결

- 볼륨 대신 bind mount를 사용할 때 교체가 아닌 **in-place 수정** 방식 사용
- 또는 컨테이너 재시작으로 마운트 재연결

## 관련 노트

- [[caddy]]
