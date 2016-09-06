---
title: 언리얼 엔진 Cone Tutorial
date: 2016-09-07 01:56:22
tags:
    - UnrealEngine
    - Tutorial
---

## Unreal Engine 4 Tutorial 1

제대로 시작해보자고 해서 다시 진행해본 c++ 튜토리얼이다.

먼저 언리얼 에디터에서 새로운 C++ Class를 만들어준다.

![C++ 클래스 생성](/uploads/UnrealStudy/1/1.png)

그럼 부모 클래스 선택 메누가 열리는데,

여기서 Actor를 선택해준다. 
( 액터가 언리얼 엔진 레벨에서 존재할 수  있는 가장 기본 클래스 Unity = Monobehaviour ?? )

![클래스 선택](/uploads/UnrealStudy/1/2.png)

액터 이름을 지어야 하는데, 원하는 클래스 이름으로 짓는다.

그 다음 클래스 생성을 클릭.

![액터 이름 짓기](/uploads/UnrealStudy/1/3.png)

그럼 지은 클래스 이름으로 .h파일과 .cpp 파일이 생성되면서 VS에서 자동으로 열린다.

다음은 소스 작성.

.h 파일에서 추가

```cpp
float runningTime;
```

.cpp 파일에서 추가

```cpp
FVector newPos = GetActorLocation();
float deltaHeight = (FMath::Sin(rinningTime + DeltaTime) - FMath::Sin(runningTime));
newPos.Z += deltaHeight * 20.0f;
runningTime += DeltaTime;
SetActorLocation(newPos);
```

![.h](/uploads/UnrealStudy/1/4.png)
![.cpp](/uploads/UnrealStudy/1/5.png)

소스 작성이 끝났으니 컴파일인데 VS에서도 가능하고, 에디터에서도 가능하다.

![컴파일 VS](/uploads/UnrealStudy/1/6.png)
![컴파일 에디터](/uploads/UnrealStudy/1/7.png)

이제 레벨에다가 세팅을 해야한다.

에디터에서 콘텐츠 브라우저에서 C++ Classes 라는 폴더를 찾아 펼친다.

그럼 프로젝트 생성시 정해준 이름으로 되어있는 폴더가 있다.

안쪽에 보면 직접 만든 액터가 있다.

![Actor](/uploads/UnrealStudy/1/8.png)

그 액터를 레벨 에디터 창에 드래그 하면 인스턴스가 생성된다.

![Actor Instance](/uploads/UnrealStudy/1/9.png)

이제 기본 지오메트리인 Cone을 추가해서 플레이를 눌러보면 위 아래로 왔다갔다 할 것이다.

![Add Component](/uploads/UnrealStudy/1/10.png)

액터 소스

.h

```cpp
#pragma once

#include "GameFramework/Actor.h"
#include "FloatingActor.generated.h"

UCLASS()
class MYUNREALGAME_API AFloatingActor : public AActor
{
	GENERATED_BODY()
	
public:	
	// Sets default values for this actor's properties
	AFloatingActor();

	// Called when the game starts or when spawned
	virtual void BeginPlay() override;
	
	// Called every frame
	virtual void Tick( float DeltaSeconds ) override;

	float runningTime;
	
};

```

.cpp

```cpp
// Fill out your copyright notice in the Description page of Project Settings.

#include "MyUnrealGame.h"
#include "FloatingActor.h"


// Sets default values
AFloatingActor::AFloatingActor()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

}

// Called when the game starts or when spawned
void AFloatingActor::BeginPlay()
{
	Super::BeginPlay();
	
}

// Called every frame
void AFloatingActor::Tick( float DeltaTime )
{
	Super::Tick( DeltaTime );

	FVector newPos = GetActorLocation();
	float deltaHeight = ( FMath::Sin( runningTime + DeltaTime ) - FMath::Sin( runningTime ) );
	newPos.Z += deltaHeight * 20.0f;
	runningTime += DeltaTime;
	SetActorLocation( newPos );
}

```
