---
Created: Invalid date
Updated: Invalid date
URL: http://msdn.microsoft.com/ko-kr/library/vstudio/bb558976(v=vs.110).aspx
---
- [**로그인**](https://login.live.com/login.srf?wa=wsignin1.0&rpsnv=12&ct=1415089611&rver=6.0.5276.0&wp=MCLBI&wlcxt=msdn%24msdn%24msdn&wreply=http%3a%2f%2fmsdn.microsoft.com%2fko-kr%2flibrary%2fvstudio%2fbb558976%2528v%3dvs.110%2529.aspx&lc=1042&id=254354&mkt=ko-KR)
- [**홈**](http://msdn.microsoft.com/vstudio/aa718325.aspx)
- [**샘플**](http://code.msdn.microsoft.com/vstudio)
- [**언어**](http://msdn.microsoft.com/vstudio/jj672990.aspx)
- [**확장 기능**](http://visualstudiogallery.msdn.microsoft.com/)
- [**설명서**](http://msdn.microsoft.com/library/vstudio)
- [**포럼**](http://social.msdn.microsoft.com/forums/vstudio/ko-kr/home)

[무료로 시작해 보십시오](http://go.microsoft.com/fwlink/?LinkId=309297&clcid=0x409&slcid=0x409)

[개발 도구 및 언어](http://msdn.microsoft.com/ko-kr/library/vstudio/jj159353.aspx)

[Visual Studio 2013](http://msdn.microsoft.com/ko-kr/library/vstudio/dd831853.aspx)

[Visual Studio 2012](http://msdn.microsoft.com/ko-kr/library/vstudio/dd831853\(v=vs.110\).aspx)

[Visual Studio 2010](http://msdn.microsoft.com/ko-kr/library/vstudio/dd831853\(v=vs.100\).aspx)

[.NET Framework 4.5](http://msdn.microsoft.com/ko-kr/library/vstudio/w0x726c2\(v=vs.110\).aspx)

[.NET Framework 4](http://msdn.microsoft.com/ko-kr/library/vstudio/w0x726c2\(v=vs.100\).aspx)

[.NET Framework 3.5](http://msdn.microsoft.com/ko-kr/library/vstudio/w0x726c2\(v=vs.90\).aspx)

![[ImageSprite.png]]

[라이브러리 전환](http://msdn.microsoft.com/ko-kr/library/vstudio/bb558976\(v=vs.110\).aspx#)

![[ImageSprite.png]]

요청한 주제가 아래에 표시됩니다. 그러나 이 주제는 이 라이브러리에 포함되지 않습니다.

# SQL Server Reporting Services 역할

**Visual Studio 2012**

다른 버전

![[ImageSprite.png]]

이 항목은 아직 평가되지 않았습니다.- [이 항목 평가](http://msdn.microsoft.com/ko-kr/library/vstudio/bb558976\(v=vs.110\).aspx\#feedback)  
  

SQL Server Reporting Services에 있는 역할을 사용하여 Visual Studio Team Foundation Server 사용자에게 특정 사용 권한을 할당할 수 있습니다. Team Foundation Server의 모든 사용자와 그룹은 Reporting Services에서 적절한 권한을 할당 받아야 합니다. Reporting Services는 역할 할당을 통해 기본적인 보안 기능을 제공합니다. Management Studio와 보고서 관리자 같은 SQL Server 관리 도구를 사용하여 사용자와 그룹에게 미리 정의된 역할을 할당할 수 있습니다.

Team Foundation Server 그룹 멤버 자격을 사용하면 Reporting Services의 미리 정의된 역할 중 하나에서 적절한 멤버 자격을 결정할 수 있습니다. 대부분의 경우 추가 역할 구성은 필요 없지만, 비즈니스 요구 사항에 맞게 미리 정의된 역할을 수정하고 사용자 지정 역할을 추가할 수는 있습니다. 사용자 지정 역할을 추가하거나 미리 정의된 역할을 수정하려는 경우 그러한 역할에 보고서와 보고 기능에 액세스하는 데 필요한 적절한 수준의 권한이 있는지 확인해야 합니다. 자세한 내용은 Microsoft 웹 사이트의 [Granting Permissions on a Native Mode Report Server](http://go.microsoft.com/fwlink/?LinkId=117112) 항목을 참조하십시오.

Team Foundation Server에서는 다음과 같은 미리 정의된 역할이 기본으로 제공됩니다.

- 시스템 관리자
- Team Foundation Content Manager
- 브라우저

Reporting Services의 미리 정의된 역할에 대한 자세한 내용은 Microsoft 웹 사이트의 [미리 정의된 역할 사용](http://go.microsoft.com/fwlink/?LinkId=117113) 항목을 참조하십시오.

|중요|
|---|
|[[Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting Reporting...]]|

  
  

## 시스템 관리자

시스템 관리자 역할에는 보고서 서버를 전체적으로 책임지고 있지만 그 내용에 대해서는 알 필요가 없는 보고서 서버 관리자에게 유용한 권한이 포함되어 있습니다. 시스템 관리자 역할에는 로컬 관리자가 컴퓨터에 대해 갖고 있는 모든 권한이 제공되지 않으므로 Team Foundation 관리자를 시스템 관리자 역할과 내용 관리자 역할 모두에 추가해야 합니다. 이 두 가지 역할을 함께 정의하면 Team Foundation Administrators 그룹의 멤버에게 필요한 모든 권한이 제공됩니다.

## Team Foundation Content Manager

이 항목에서 설명하는 다른 역할과 달리 Team Foundation Content Manager 역할은 SQL Server에서 기본 역할이 아닙니다. Team Foundation Server가 설치된 경우 이 역할은 특히 Team Foundation Server와 SQL Server Reporting Services 간의 통합을 위해 만들어집니다. 이 역할은 구조 및 사용 권한 면에서 SQL Server의 기본 역할인 내용 관리자 역할과 유사합니다. Team Foundation Content Manager 역할에는 보고서와 웹 콘텐츠를 관리하지만 보고서를 작성하거나 웹 서버 또는 SQL Server 인스턴스를 관리할 필요가 없는 사용자에게 유용한 권한이 포함됩니다. 내용 관리자는 보고서를 배포하고 보고서 모델과 데이터 소스 연결을 관리하며 보고서 사용 방법을 결정합니다. Team Foundation Content Manager 역할은 팀 프로젝트에서 Project Administrators 그룹에 속한 사용자뿐 아니라 Project Collection Administrators 그룹에 속한 사용자에게 필요한 일반적인 범위의 권한을 제공합니다. Team Foundation Administrators 그룹의 멤버도 이 역할에 추가해야 합니다.

## 브라우저

브라우저 역할에는 보고서를 볼 수 있지만 보고서를 작성하거나 관리할 필요가 없는 사용자에게 유용한 권한이 포함됩니다. 이 역할은 팀 프로젝트에서 Contributor 또는 Reader 그룹에 속한 사용자에게 유용한 기본적인 기능을 제공합니다.

## 참고 항목

### 개념

[SQL Server 및 SQL Server Reporting Services 이해](http://msdn.microsoft.com/ko-kr/library/vstudio/bb552243\(v=vs.110\).aspx)

이 정보가 도움이 되었습니까?

예

아니요

## 커뮤니티 추가 항목

- **개발자 센터**
- [Windows](http://dev.windows.com/)
- [Office](http://msdn.microsoft.com/office)
- [Nokia](http://developer.nokia.com/)
- [더 보기...](http://msdn.microsoft.com/aa937802)
- **관련 사이트**
- [시작하기](http://www.visualstudio.com/)
- [Visual Studio Integrate](http://www.visualstudio.com/integrate/)
- [VSIP Program](http://www.vsipprogram.com/)
- [Microsoft .NET](http://www.microsoft.com/net)
- [Microsoft Azure](http://azure.microsoft.com/)
- **연결**
- [포럼](http://social.msdn.microsoft.com/forums/vstudio/ko-kr/home?category=visualstudio%2cvslanguages%2cvstfs%2cnetdevelopment%2cvsarch)
- [블로그](http://blogs.msdn.com/b/developer-tools/)
- [Facebook](https://www.facebook.com/visualstudio.us?brand_redir=1)
- [LinkedIn](https://www.linkedin.com/company/microsoft-visual-studio)
- [스택 오버플로](http://stackoverflow.com/questions/tagged/visual-studio)
- [Twitter](https://twitter.com/visualstudio)
- [Visual Studio이벤트](http://events.visualstudio.com/)
- [YouTube](http://www.youtube.com/user/visualstudio)
- **개발자 리소스**
- [코드 샘플](http://msdn.microsoft.com/library/se881ay9\(v=vs.120\).aspx)
- [설명서](http://msdn.microsoft.com/ko-kr/library/vstudio)
- [다운로드](http://www.visualstudio.com/downloads/download-visual-studio-vs)
- [Visual Studio용 제품 및 확장 프로그램](http://visualstudiogallery.msdn.microsoft.com/)
- [REST APIs](http://www.visualstudio.com/integrate/get-started/get-started-rest-basics-vsi)
- [웹 개발자를 위한 테스팅 도구](http://www.modern.ie/)
- [비디오 및 자습서](http://msdn.microsoft.com/ko-kr/vstudio/ff459609)
- [Virtual Labs](http://msdn.microsoft.com/vstudio/ff640662)

[한국(한국어)](http://msdn.microsoft.com/ko-kr/vstudio/SelectLocale?fromPage=%2flibrary%2fvstudio%2fbb558976)

- © 2014 Microsoft
- [서비스 계약](http://msdn.microsoft.com/cc300389.aspx)
- [상표](http://www.microsoft.com/library/toolbar/3.0/trademarks/ko-kr.mspx)
- [개인 정보 및 쿠키](http://go.microsoft.com/fwlink/?linkid=248681)