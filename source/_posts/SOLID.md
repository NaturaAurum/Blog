---
title: SOLID
date: 2016-07-12 21:14:18
tags:
    - 객체지향
---

[출처 : HG's Note](http://hg-note.tistory.com/entry/SOLID-%EC%9B%90%EC%B9%99)

## SOLID

객체지향의 5대원칙을 정하는 단어.

5대원칙이란
- SRP : 단일 책임 원칙
- OCP : 개방 - 폐쇠 원칙
- LSP : 리스코프 치환 법칙
- DIP : 의존 역전 법칙
- ISP : 인터페이스 분리 법칙

을 말하며 앞 글자들을 따서 SOLID 원칙이라고 불린다. 프로그래머가 시간이 지나도 유지 보수와 확장이 쉬운 소프트웨어를 만드는데 이 원칙들을 적용할 수 있다.

### Single Responsiblity Principle ( 단일 책임 원칙 )

#### - 소프트웨어의 설계 부품 ( 클래스, 함수 등 )은 단 하나의 책임만을 가져야 한다.

여기서 책임이란, '기능' 정도의 의미로 해석하면 된다.

설계를 잘한 프로그램은 기본적으로 새로운 요구사항과 프로그램 변경에 영향을 받는 부분이 적다. 다시말해, 응집도는 높고 결합도는 낮은 프로그램을 뜻한다. 만약 한 클래스가 수행할 수 있는 기능, 즉 책임이 많아진다. 책임이 많아지면 클래스 내부의 함수끼리 강한 결합을 발생할 가능성이 높아진다. 이는 유지보수에 비용이 증가하게 되므로 따라서 책임을 분리시킬 필요가 있다.

### Open-Closed Principle ( 개방-패쇄 원칙 )

####  - 기존의 코드를 변경하지 않고( Closed ) 기능을 수정하거나 추가할 수 있도록( Open ) 설계해야 한다.

OCP에 만족하는 설계를 할 때 변경되는 것이 무엇인지에 초점을 맞춘다. 자주 변경되는 내용은 수정하기 쉽게 설계 하고, 변경되지 않아야 하는 것은 수정되는 내용에 영향을 받지 않게 하는 것이 포인트다. 이를 위해 자주 사용되는 문법이 인터페이스( Interface )이다. 다음 예제를 함께 보자.

``` cs
public class SoundPlayer
{
    public void Play()
    {
        Console.WriteLine( "WavPlay" ); // Wav 재생
    }
}

public class Client
{
    static void main( string[] args )
    {
        SoundPlayer sp = new SoundPlayer();
        sp.Play();
    }
}

```
SoundPlayer 클래스는 음악을 재생해주는 클래스이다. 이 클래스는 기본적으로 wav파일을 재생할 수 있다. 그러나 SoundPlayer가 다른 포맷의 파일, 예를 들어 Mp3 파일을 재생하도록 요구사항이 변경 되었다고 하자. 요구사항을 만족 시키기 위해서는 SoundPlayer의 play() 메소드를 수정하여야 한다. 그러나 이러한 소스코드 변경은 OCP 원칙에 위배된다. 

그렇다면 어떻게 해야 OCP 원칙을 만족시킬 수 있을까? 다양한 방법이 있지만 여기선 앞에서 언급한 인터페이스를 이용하여 OCP를 만족시켜 보자. 먼저 변해야 하는것은 무엇인지 정의한다. 위 클래스에서는 play() 메소드가 변해야 하는 것이다. 따라서 play() 메소드를 인터페이스로 분리한다.

``` cs
public interface ISound
{
    void Play();
}

public class Wav : ISound
{
    public void Play()
    {
        Console.WriteLine( "Play Wav" ); // Wav 재생
    }
}

public class Mp3 : ISound
{
    public void Play()
    {
        Console.WriteLine( "Play Mp3" ); // Wav 재생
    }
}

```

일단 재생하고자 하는 파일 클래스( Wav, Mp3 )를 만들어 Sound 인터페이스의 play() 메소드를 재정의하도록 설계한다. 
