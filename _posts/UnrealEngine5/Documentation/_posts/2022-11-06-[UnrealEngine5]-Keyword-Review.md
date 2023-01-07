---
title: "[UnrealEngine5]-Keyword-Review"
date: 2022-11-06 17:42:00+0900
categories: [UnrealEngine5, Documentation]
tags: [Notes]
math: true
---

Based on official documentation of Unreal Engine 5, these are some keywords that will help you understand basics of the engine.
 
<span style="color:yellow">짧게 대충 뭐하는 놈들인지 정리</span>.

# Project
> *Basically holds all content*

- Saved as `.uproject` 

# BluePrint
> Visual Scripting using node-based interface

- Represents Object-Oriented classes or objects (BUT 기본적으로 코드보다 느림)

# Object
> Basic class in UE5. Almost everything inherits `Object`

- C++ 한정으로 `UObject` == BaseClass 
    * Features such as 
        + `Grabage Collection`
        + `metadata(UProperty) support for Editor`
        + `Serialization for load/save`

# Class 
> Defines behaviors & properties of arbitrary `Actor` or `Object`

- The Class you use in C++(No big difference in its meaning)
- Prefix for gamePlay classes...
    
    | Prefix      | Meaning                            |
    |:------------|:-----------------------------------|
    | `A`         | Actor -> Spawnable gameplay object.|
    | `U`         | Components -> Belongs to an Actor.|

# Actor
> Everything you can put inside a level

- Everything that can be spawned / destroyed through gameplay code. <br>
    *ex)* <br>
    + Camera
    + Static Mesh
    + Player Start Position

# Casting
> Treat class $\alpha$ as class $\beta$

- 주로 해당 클래스의 특정 기능을 쓸 때 사용

# Component
> Functionality that can be added to Actor

- 액터 클래스에 특정 기능 추가할 때 그 `기능`을 `Component`라고 함<br>
    *ex)* <br>
    + `SpotLight` to `ACandle` -> 캔들 액터가 Spotlight처럼 빛을 냄

# Pawn
> SubClass of Actor. Can be `Possessed` by Player OR  game's AI

- 컨트롤을 플레이어 혹은 AI가 갖고 있으면 `Possessed`, 아니면 `Unpossessed`. 

# Character
> SubClass of Pawn. Intended to be used for player character 

- Includes...
    + Input binding for 이족보행
    + Collision setup
    + +@ code for player-controlled movement

# Player Controller
> Title explains itself. Controller for Player

- Input -> Output as interaction ingame. 
- Every game has at least 1 Player Controller
    
    For Multiplayer games...<br> Server has 1:1 instance of player controller for every client. Of course client only has its own controller

# AI Controller
> Possess pawn as NPC

- By default, Pawns & Character will end up with base AI Controller

# Player State
> Status of game participant

- 말그대로 플레이어 상태

    For Multiplayer...<br>Every client replicates others PlayerState through server.

# Game Mode
> Set of rules for the game

- 참여 / 승리 / 일시정지 종료 조건과 같이 게임 안에서 이루어지는 행위들을 위한 규칙
- 각 레벨별로 1개의 `Game Mode`를 갖을 수 있음

# Game State
> Status of the game

- 전반적인 현재 게임 상태 정보

    For Multiplayer...<br>There is one local instance of the Game State on each player's machine. Local Game State instances get their updated information from the server's instance of the Game State.

# Brush
> Actor describing 3D shapes

- Used for defining level geometry ( AKA Binary Space Partition Brush)

# Volume
> Bounded 3D space for various effects

- 특정 기능, 혹은 이팩트가 발생하는 한정된 구간(영역)

# Level
> Arbitrary gameplay area that you define

- 각각의 level을 `.umap`으로 저장(The reason why `level`'s are also called `Maps`)

# World
> Container for levels

- 게임세계


각 항목의 구체적인 내용은 문서를 읽다보면 나오기 때문에 그때 다시 상세히 정리하는 걸로...


UE5 Documentation [UE5 Doc - Terminology](https://docs.unrealengine.com/5.0/en-US/unreal-engine-terminology/).