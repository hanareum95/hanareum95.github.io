---
layout: post
title:  "[Windows] Process info API"
subtitle:   "CreateToolhelp32Snapshot"
categories: Programming
tags: C++, Windows
comments: true
---

### API : CreateToolhelp32Snapshot 

---

> 프로세스 정보를 가져오는 API.

<br/>

- 플래그와 프로세스 id를 받아서 핸들을 넘겨준다.
- 핸들을 이용하여 루프를 돌면서 Process32First와 Process32Next를 사용하여 프로세스의 정보를 얻어올 수 있다.
- 프로세스의 정보는 PROCESSENTRY32라는 구조체에 담아진다.

<br/>

#### * 구조체 - PROCESSENTRY32

```c++
typedef struct tagPROCESSENTRY32  
{  
    DWORD   dwSize;  
    DWORD   cntUsage;  
    DWORD   th32ProcessID;          // this process  
    ULONG_PTR th32DefaultHeapID;  
    DWORD   th32ModuleID;           // associated exe  
    DWORD   cntThreads;  
    DWORD   th32ParentProcessID;    // this process's parent process  
    LONG    pcPriClassBase;         // Base priority of process's threads  
    DWORD   dwFlags;  
    CHAR    szExeFile[MAX_PATH];    // Path  
} PROCESSENTRY32;
```

<br/>

#### * 프로세스 이름 출력

```c++
#include <stdio.h>  
#include <windows.h>  
#include <iostream>
#include <tlhelp32.h>  
using namespace std;


int main(int argc, char* argv[])  
{  
    BOOL bGet = FALSE;  
    char buf[260] = "";  
    HANDLE hSnapshot;  
    PROCESSENTRY32 ppe;     //구성된 자료구조를 저장하기 위한 엔트리.  
  
    hSnapshot = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS, 0);//system 프로세서(pid=0)의 상태를 읽어 온다   
    ppe.dwSize = sizeof(PROCESSENTRY32);                        //엔트리 구조체 사이즈를 정해준다.  
    
	if(Process32First(hSnapshot, &ppe))
	{
		do
		{
			cout << ppe.szExeFile << "\n" ;
		}while(Process32Next(hSnapshot, &ppe));
	}
  
    return 0;  
}    
```



