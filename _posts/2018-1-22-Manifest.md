---
layout: post
title:  "[C++] Manifest"
subtitle:   "Manifest"
categories: Programming
tags: C++
comments: true
---



### Manifest

------



참고 : [MSDN 매니페스트 설명](https://msdn.microsoft.com/ko-kr/library/ws1c2fch(v=vs.85).aspx)

<br/>

| 요소                   | 설명                                       | 특성                                       |
| -------------------- | ---------------------------------------- | ---------------------------------------- |
| `<assembly>`         | 최상위 요소                                   | manifestVersion                          |
| `<assemblyIdentity>` | 응용프로그램의 주 어셈블리를 식별                       | name<br/>version<br/>publicKeyToken<br/>processorArchitecture<br/>language |
| `<trustInfo>`        | 응용프로그램 보안 요구 사항을 식별                      | -                                        |
| `<dependency>`       | 실행을 위한 응용 프로그램 코드 진입점을 식별                | -                                        |
| `<file>`             | 응용프로그램에 사용되는 어셈블리 이외의 각 파일을 식별. 파일과 관련된 COM 격리 데이터가 포함될 수 있다. | name<br/>size                            |



#### assembly

------

- assembly - **manifestVersion**

  - 1.0으로 설정해야한다.
  - ​

- ```xml
  <asmv1:assembly 
                    xmlns="urn:schemas-microsoft-com:asm.v2" 
                    manifestVersion="1.0" 
                    xmlns:asmv1="urn:schemas-microsoft-com:asm.v1" 
                    xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" 
                    xmlns:dsig="http://www.w3.org/2000/09/xmldsig#" 
                    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                    xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd">
  ```

  <br/>

#### assemblyIdentity

------

- assemblyIdentity - **Name**
  - 응용프로그램의 이름을 식별
  - ', " 같은 특수문자가 들어 있으면 응용프로그램이 활성화 되지 않을 수 있음

<br/>

- assemblyIdentity - **Version**
  - 응용프로그램의 버전 번호를 지정

<br/>

- assemblyIdentity - **publicKeyToken**
  - (선택) 어셈플리에 서명하는데 사용되는 공개키의 SHA-1 해시 값에서 마지막 8바이트를 나타내는 16개의 16진수 문자를 지정

<br/>

- assemblyIdentity - **processArchitecture**
  - 프로세서를 지정
  - 유효한 값은 32비트 windows의 경우 x86, 64비트 windows의 경우 IA64

<br/>

- assemblyIdentity - **language**
  - en-US같이 두 부분으로 구성된 어셈블리의 언어 코드를 식별
  - 기본값 : neutral

<br/>

- ```xml
  <!-- Identify the application. -->
  <assemblyIdentity 
                    name="DatumCorpApp.exe" 
                    version="1.0.0.0" 
                    publicKeyToken="0123456789abcdef" 
                    processorArchitecture="x86" 
                    language="neutral"/>
  ```

<br/>

#### trustInfo

------



- trustInfo - **security**
  - `applicationRequestMinimum` 요소가 포함

<br/>

- trustInfo - **applicationRequestMinimum **
  - 이 요소는 `security` 요소의 자식
  - `PermissionSet`, `assemblyRequest` 및 `defaultAssemblyRequest` 요소를 포함
  - `PermissionSet` 
    - ID : `assemblyRequest` 및 `defaultAssemblyRequest` 특성에서 참조
    - version : 권한의 버전을 식별. 일반적으로 1
    - `IPermission` : .NET Framework에서 권한 클래스를 완전히 식별
  - `assemblyRequest` 
    - name : 어셈블리 이름을 식별
    - permissionSetReference : 어셈블리에 필요한 권한 집합의 ID를 식별, 권한 집합은 PermissionSet요소에 선언
  - `defaultAssemblyRequest` 
    - permissionSetReference : 기본 권한인 권한 집합의 ID를 식별

<br/>

#### dependency

------

- dependency - **dependentOS**

  - supportUrl : (선택) 종속 플랫폼의 지원 URL을 지정
  - description : (선택) dependentOS 요소에서 설명하는 운영 체제를 사람이 읽을 수 있는 형식으로 설명
  - `osVersionInfo` 
    - `os` - majorVersion, minorVersion, buildNumber, servicePackMajor, servicePackMinor, productType, suiteType

- dependency - **dependentAssembly**

  - size : 종속 어셈블리의 바이트 단위 크기
  - codebase : 어셈블리의 경로. 유효한 경로여야 매니페스트가 유효
  - `assemblyIdentity`
    - name : 응용프로그램의 이름 식별
    - version : major.minor.build.revision같은 형식으로 응용 프로그램의 버전 번호 지정
    - publicKeyToken : (선택) 
    - processorArchitecture : (선택) 
    - language : (선택) 

- ```xml
  <!-- This XML identifies a SpellingChecker assembly. -->
  <dependency>
    <dependentAssembly codebase="SpellingChecker.dll" size="29696">
      <assemblyIdentity name="SpellingChecker" version="2.0.0.0" publicKeyToken="e8ed396099c4b4e9" processorArchitecture="msil" language="es-PE" />
      <hash>
        <dsig:Transforms>
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
        </dsig:Transforms>
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
        <dsig:DigestValue>2+33lqQoPphgov907Kfp1v4TZMw=</dsig:DigestValue>
      </hash>
    </dependentAssembly>
  </dependency>

  <!-- This XML describes an operating system dependency for the application. -->
  <!--Microsoft Windows Operating System Platform Dependency-->
  <dependency>
    <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">
      <osVersionInfo>
        <os majorVersion="4" minorVersion="10" />
      </osVersionInfo>
    </dependentOS>
  </dependency>
  ```

<br/>

#### file

------

- file - **name**

- file - **size**

- file - **group**

- file - **optional**

- file - **writeableType**

- ```xml
  <file name="Icon.ico" size="9216">
      <hash>
        <dsig:Transforms>
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />
        </dsig:Transforms>
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
        <dsig:DigestValue>lVoj+Rh6RQ/HPNLOdayQah5McrI=</dsig:DigestValue>
      </hash>
  </file>
  ```

  ​

