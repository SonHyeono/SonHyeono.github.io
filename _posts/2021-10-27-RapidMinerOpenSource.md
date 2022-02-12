---
title: "RapidMinerOpenSource-Run"
categories:
  - Intern
feature_text: |
  The History of the 산학 R&D 프로젝트 인턴
---

#### RapidMiner 상용 버전 말고 Github에서 다운받아서 오픈소스로 Run하기

##### 1. [rapidminer-studio](https://github.com/rapidminer/rapidminer-studio) 오픈소스 다운 받기

![opensource_error](https://user-images.githubusercontent.com/26592315/138993527-3b58cd1c-16eb-4c21-b5a1-ff7c4e87fdaf.png){: width="100%" height="100%"}{: .center}

> - 굉장히 많은 Error들이......

---

##### 2. Error 해결법

> - Error들의 이유는 버전과 관련된 환경 설정이 문제이기에

- [Eclipse 19-12](https://www.eclipse.org/downloads/packages/release/2019-12)의 R Packages 를 다운 (여기서 R은 안정화된 버전, RC1은 안정화가 될 후보 버전, M1~M3는 개발 중인 버전)
- jdk의 경우는 정말 다양한 버전들을 깔고 지우고 open jdk 1.8을 깔아보아도 안되고 고생을 하다가 Engine팀에서 찾아낸 [jdk](<https://www.manageengine.com/products////////desktop-central/patch-management/AdoptOpenJDK-JDK-with-Hotspot-8-(x64)-patches/OpenJDK8U-jdk_x64_windows_hotspot_8u302b08-patch.html>)인 OpenJDK8U-jdk_x64_windows_hotspot_8u302b08 를 사용

- jdk 환경변수 설정 (위의 파일깔면 java 아래에 생기는게 아니라 programFiles아래 Eclipse Foundation 파일 안에 생김)

---

![opensource_error2](https://user-images.githubusercontent.com/26592315/138994793-d1e847f0-1f04-40fc-8106-e02fac535c43.png){: width="100%" height="100%"}{: .center}

- 위의 사진처럼 System library를 default로 설정

---

![opensource_error3](https://user-images.githubusercontent.com/26592315/138995306-342532bb-89af-4c91-923a-05e5ff9a378c.jpg){: width="100%" height="100%"}{: .center}

- 프로젝트 우클릭 -> Import -> Gradle Project에서 해당 폴더로 설정하기

---

##### 3. Run

![opensource](https://user-images.githubusercontent.com/26592315/138995588-75f92b48-e2b6-4d26-b3d1-1f355f21df7f.png){: width="100%" height="100%"}{: .center}

- GUILauncher 클래스 생성

```java
import java.nio.file.Paths;

import com.rapidminer.gui.RapidMinerGUI;
import com.rapidminer.gui.ToolbarGUIStartupListener;
import com.rapidminer.tools.PlatformUtilities;

class GUILauncher {
   public static void main(String args[]) throws Exception {
      System.setProperty(PlatformUtilities.PROPERTY_RAPIDMINER_HOME, Paths.get("").toAbsolutePath().toString());
      RapidMinerGUI.registerStartupListener(new ToolbarGUIStartupListener());
      RapidMinerGUI.main(args);
   }
}
```

##### 4. 공개SW 버전 빌드

![opensource2](https://user-images.githubusercontent.com/26592315/138995750-1b147ebd-532e-4802-8d2c-8c58f8a79ef9.png){: width="100%" height="100%"}{: .center}

- 다음과 같이 실행이 되고 특징으로는
  > - Read CSV, 기본적으로 제공되는 Data Mining tool 등을 모두 사용 가능
  > - Extensions 탭이 비활성화 되어 상용 버전에서 사용할 수 있었던 Market Place 기능을 사용할 수 없다는 것을 확인했고, 이로 인해서 다양한 확장 기능을 사용할 수 없기 때문에 필요한 operator들을 직접 만들어줘야 하는 것을 확인
  > - 상용 버전과 다르게 Result가 visualize되지 않은 상태로 출력되는 것을 확인
