---
layout: post
title: 플러터
image: /assets/img/blog/flutter.png
accent_image: 
  background: url('/assets/img/me/wave3.jpg') center/cover
  overlay: false
accent_color: '#fff'
theme_color: '#fff'
description: >
  Flutter start!
invert_sidebar: true
categories :
 - devlog	
 - flutter

---

# Flutter pub 명령어 모음

일반적으로 새로운 플러그인을 추가할 때

`pubspec.yaml` 파일을 직접 수정한 다음 `flutter pub get` 명령을 실행해줘야 한다.



`get` 말고도 **add,** **remove, outdated, upgrade** 같은 명령을 이용하면 `pubspec.yaml` 파일을 직접 수정할 수 있다.

```
  add         pubspec.yaml에 의존성을 추가한다.
  cache       Work with the Pub system cache.
  deps        패키지 의존성들을 출력한다.
  downgrade   플러터 프로젝트의 패키지들을 다운그레이드한다.
  get         플러터 프로젝트로 패키지들을 가져온다.
  global      Work with Pub global packages.
  login       Log into pub.dev..
  logout      Log out of pub.dev..
  outdated    업그레이드 가능한 패키지를 찾아준다.
  pub         Pass the remaining arguments to Dart's "pub" tool.
  publish     Publish the current package to pub.dartlang.org.
  remove      Removes a dependency from the current package..
  run         Run an executable from a package.
  test        Run the "test" package.
  upgrade     Upgrade the current package's dependencies to latest versions..
  uploader    Manage uploaders for a package on pub.dev.
  version     Pub의 버전을 출력한다.
```



주로 사용하는 명령어를 정리해보았다.

```
# 버전 확인
flutter pub version

# 의존성 출력 (트리 형태로 출력한다.)
flutter pub deps

# 의존성 추가 (자동으로 yaml 파일이 수정된다.)
flutter pub add [패키지 이름]

# 의존성 제거 (자동으로 yaml 파일이 수정된다.)
flutter pub remove [패키지 이름]

# 업그레이드가 필요한 플러그인을 찾아준다.
flutter pub outdated

# 업그레이드가 가능한 플러그인을 업그레이드 한다.
flutter pub upgrade

# 플러그인들을 사용할 수 있게 프로젝트로 가져온다.
flutter pub get
```